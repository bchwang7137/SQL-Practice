# 오프라인/온라인 판매 데이터 통합하기 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/131537

`ONLINE_SALE` 테이블과 `OFFLINE_SALE` 테이블에서 2022년 3월의 오프라인/온라인 상품 판매 데이터의 판매 날짜, 상품ID, 유저ID, 판매량을 출력하는 SQL문을 작성해주세요. `OFFLINE_SALE` 테이블의 판매 데이터의 `USER_ID` 값은 NULL 로 표시해주세요. 결과는 판매일을 기준으로 오름차순 정렬해주시고 판매일이 같다면 상품 ID를 기준으로 오름차순, 상품ID까지 같다면 유저 ID를 기준으로 오름차순 정렬해주세요.

```sql
SELECT DATE_FORMAT(sales_date, '%Y-%m-%d') AS sales_date
     , product_id
     , user_id
     , sales_amount
FROM online_sale
HAVING sales_date BETWEEN '2022-03-01' AND '2022-03-31'

UNION ALL

SELECT DATE_FORMAT(sales_date, '%Y-%m-%d') AS sales_date
     , product_id
     , CASE WHEN offline_sale_id IS NOT NULL THEN NULL END AS user_id
     , sales_amount
FROM offline_sale
HAVING sales_date BETWEEN '2022-03-01' AND '2022-03-31'

ORDER BY sales_date, product_id, user_id
;
```
