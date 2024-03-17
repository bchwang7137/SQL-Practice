# 우유와 요거트가 담긴 장바구니 lv4
[https://school.programmers.co.kr/learn/courses/30/lessons/62284](https://school.programmers.co.kr/learn/courses/30/lessons/62284)

데이터 분석 팀에서는 우유(Milk)와 요거트(Yogurt)를 동시에 구입한 장바구니가 있는지 알아보려 합니다. 우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요. 이때 결과는 장바구니의 아이디 순으로 나와야 합니다.

should be wary that a cart might have multiple types/brands of milk/yogurt in it - this may lead to multiple occurrences of `cart_id` in result set if not careful

```sql
-- using two subqueries and a join
SELECT m.cart_id
FROM (SELECT DISTINCT cart_id
      FROM cart_products
      WHERE name = 'milk') AS m
JOIN (SELECT DISTINCT cart_id
      FROM cart_products
      WHERE name = 'yogurt') AS y ON m.cart_id = y.cart_id
ORDER BY m.cart_id
;

-- using subquery, case, having (could easily utilize CTE)
-- would likely execute faster than above due to only 1 pass at original table
SELECT cart_id
FROM (
    SELECT cart_id
         , CASE WHEN name = 'milk' THEN 1 ELSE 0 END AS has_milk
         , CASE WHEN name = 'yogurt' THEN 1 ELSE 0 END AS has_yogurt
    FROM cart_products) AS tmp
GROUP BY cart_id
HAVING SUM(has_milk) > 0 AND SUM(has_yogurt) > 0
ORDER BY cart_id
;
```
