# 식품분류별 가장 비싼 식품의 정보 조회하기 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/131116

`FOOD_PRODUCT` 테이블에서 식품분류별로 가격이 제일 비싼 식품의 분류, 가격, 이름을 조회하는 SQL문을 작성해주세요. 이때 식품분류가 '과자', '국', '김치', '식용유'인 경우만 출력시켜 주시고 결과는 식품 가격을 기준으로 내림차순 정렬해주세요.

```sql
-- using INNER JOIN by finding maximum price per category
SELECT tmp.category
     , tmp.mp AS max_price
     , fp.product_name
FROM food_product AS fp 
    JOIN (
        SELECT category
             , MAX(price) AS mp
        FROM food_product
        WHERE category IN ('과자', '국', '김치', '식용유')
        GROUP BY category) AS tmp
    ON fp.category = tmp.category AND fp.price = tmp.mp
ORDER BY max_price DESC
;

-- using DENSE_RANK()
SELECT category
     , price AS max_price
     , product_name
FROM (
    SELECT category
         , price
         , product_name
         , DENSE_RANK() OVER (PARTITION BY category ORDER BY price DESC) AS rnk_price
    FROM food_product
    WHERE category IN ('과자', '국', '김치', '식용유')
) AS tmp
WHERE rnk_price = 1
ORDER BY max_price DESC
;
```
