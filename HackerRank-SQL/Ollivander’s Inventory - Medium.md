# Ollivander’s Inventory - Medium
[https://www.hackerrank.com/challenges/harry-potter-and-wands/problem](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem)

Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each _non-evil_ wand of high power and age. Write a query to print the _id_, _age_, _coins_needed_, and _power_ of the wands that Ron's interested in, sorted in order of descending _power_. If more than one wand has same power, sort the result in order of descending _age_.

```sql
-- using subqueries
SELECT w.id
     , wp.age
     , w.coins_needed
     , w.power
FROM (
    SELECT code
         , MIN(coins_needed) AS min_price
         , power
    FROM wands
    GROUP BY code, power) AS m
    JOIN wands AS w ON m.code = w.code 
                    AND m.power = w.power 
                    AND m.min_price = w.coins_needed
    JOIN wands_property AS wp ON w.code = wp.code
WHERE wp.is_evil = 0
ORDER BY power DESC, age DESC
;

-- using CTE and ROW_NUMBER(), does not seem to work with HackerRank MySQL
WITH interest AS (
    SELECT w.id
         , wp.age
         , w.coins_needed
         , w.power
         , ROW_NUMBER() OVER(PARTITION BY wp.age, w.power ORDER BY w.coins_needed) AS rn
    FROM Wands AS w
        JOIN Wands_Property AS wp ON w.code = wp.code
    WHERE wp.is_evil = 0
)

SELECT id
     , age
     , coins_needed
     , power
FROM interest
WHERE rn = 1
ORDER BY power DESC, age DESC
;
```
