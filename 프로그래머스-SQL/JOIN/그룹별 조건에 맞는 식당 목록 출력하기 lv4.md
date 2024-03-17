# 그룹별 조건에 맞는 식당 목록 출력하기 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/131124

`MEMBER_PROFILE`와 `REST_REVIEW` 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요. 회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.

`REVIEW_DATE`의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.

```sql
-- avoided using LIMIT because there may be multiple users with the same highest review count
WITH cnt AS (
    SELECT member_id
         , COUNT(DISTINCT review_id) AS review_count
    FROM rest_review
    GROUP BY member_id)

SELECT mp.member_name
     , rr.review_text
     , DATE_FORMAT(rr.review_date, '%Y-%m-%d') AS review_date
FROM rest_review AS rr
    JOIN member_profile AS mp ON rr.member_id = mp.member_id
    JOIN cnt ON mp.member_id = cnt.member_id
WHERE cnt.review_count = (SELECT MAX(review_count) FROM cnt)
ORDER BY review_date, review_text
;

-- using DENSE_RANK(), another way to be robust against multiple users with same review count
WITH members_ranked AS (
    SELECT member_id
         , DENSE_RANK() OVER (ORDER BY cnt_review DESC) AS rnk_rev
    FROM (
        SELECT member_id
             , COUNT(DISTINCT review_id) AS cnt_review
        FROM rest_review
        GROUP BY member_id) AS counts
)

SELECT mp.member_name
     , rr.review_text
     , DATE_FORMAT(rr.review_date, '%Y-%m-%d') AS review_date
FROM member_profile AS mp
    JOIN members_ranked AS mr ON mp.member_id = mr.member_id
    JOIN rest_review AS rr ON mp.member_id = rr.member_id
WHERE mr.rnk_rev = 1
ORDER BY review_date, review_text
;
```
