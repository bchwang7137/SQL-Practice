# 서울에 위치한 식당 목록 출력하기 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/131118

`REST_INFO`와 `REST_REVIEW` 테이블에서 서울에 위치한 식당들의 식당 ID, 식당 이름, 음식 종류, 즐겨찾기수, 주소, 리뷰 평균 점수를 조회하는 SQL문을 작성해주세요. 이때 리뷰 평균점수는 소수점 세 번째 자리에서 반올림 해주시고 결과는 평균점수를 기준으로 내림차순 정렬해주시고, 평균점수가 같다면 즐겨찾기수를 기준으로 내림차순 정렬해주세요.

```sql
SELECT ri.rest_id
     , ri.rest_name
     , ri.food_type
     , ri.favorites
     , ri.address
     , ROUND(AVG(rr.review_score), 2) AS score
FROM rest_info AS ri 
    JOIN rest_review AS rr ON ri.rest_id = rr.rest_id
WHERE ri.address LIKE '서울%'
GROUP BY ri.rest_id
ORDER BY score DESC, favorites DESC
;
```