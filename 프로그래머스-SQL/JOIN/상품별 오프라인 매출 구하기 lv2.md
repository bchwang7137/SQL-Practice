# 상품별 오프라인 매출 구하기 lv2
https://school.programmers.co.kr/learn/courses/30/lessons/131533

`PRODUCT` 테이블과 `OFFLINE_SALE` 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성해주세요. 결과는 매출액을 기준으로 내림차순 정렬해주시고 매출액이 같다면 상품코드를 기준으로 오름차순 정렬해주세요.

```sql
SELECT product_code
     , (p.price * s.vol) AS sales
FROM product AS p
    JOIN (
        SELECT product_id
             , SUM(sales_amount) AS vol
        FROM offline_sale
        GROUP BY product_id) AS s ON p.product_id = s.product_id
ORDER BY sales DESC, product_code
;
```
