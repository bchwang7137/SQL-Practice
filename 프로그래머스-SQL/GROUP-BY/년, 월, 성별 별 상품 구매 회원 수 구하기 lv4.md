# 년, 월, 성별 별 상품 구매 회원 수 구하기 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/131532

`USER_INFO` 테이블과 `ONLINE_SALE` 테이블에서 년, 월, 성별 별로 상품을 구매한 회원수를 집계하는 SQL문을 작성해주세요. 결과는 년, 월, 성별을 기준으로 오름차순 정렬해주세요. 이때, 성별 정보가 없는 경우 결과에서 제외해주세요.

```sql
SELECT YEAR(os.sales_date) AS year
     , MONTH(os.sales_date) AS month
     , ui.gender
     , COUNT(DISTINCT os.user_id) AS users
FROM online_sale AS os
    JOIN user_info AS ui ON os.user_id = ui.user_id
WHERE ui.gender IS NOT NULL
GROUP BY YEAR(os.sales_date), MONTH(os.sales_date), ui.gender
ORDER BY year, month, gender
;
```
