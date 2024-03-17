# 가격대 별 상품 개수 구하기 lv2
https://school.programmers.co.kr/learn/courses/30/lessons/131530

`PRODUCT` 테이블에서 만원 단위의 가격대 별로 상품 개수를 출력하는 SQL 문을 작성해주세요. 이때 컬럼명은 각각 컬럼명은 PRICE_GROUP, PRODUCTS로 지정해주시고 가격대 정보는 각 구간의 최소금액(10,000원 이상 ~ 20,000 미만인 구간인 경우 10,000)으로 표시해주세요. 결과는 가격대를 기준으로 오름차순 정렬해주세요.

```sql
SELECT tmp.rng AS price_group
     , COUNT(tmp.product_id) AS products
FROM (
    SELECT CASE WHEN price BETWEEN 0 AND 9999 THEN 0
                WHEN price BETWEEN 10000 AND 19999 THEN 10000
                WHEN price BETWEEN 20000 AND 29999 THEN 20000
                WHEN price BETWEEN 30000 AND 39999 THEN 30000
                WHEN price BETWEEN 40000 AND 49999 THEN 40000
                WHEN price BETWEEN 50000 AND 59999 THEN 50000
                WHEN price BETWEEN 60000 AND 69999 THEN 60000
                WHEN price BETWEEN 70000 AND 79999 THEN 70000
                WHEN price BETWEEN 80000 AND 89999 THEN 80000
                WHEN price BETWEEN 90000 AND 99999 THEN 90000
                ELSE '100000+'
            END AS rng
          , product_id
          , product_code
    FROM product) AS tmp
GROUP BY tmp.rng
ORDER BY price_group
;
```
