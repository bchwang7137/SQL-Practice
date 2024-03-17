# 180 Consecutive Numbers - Medium
[https://leetcode.com/problems/consecutive-numbers/](https://leetcode.com/problems/consecutive-numbers/)

Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in **any order**.

```sql
-- using multiple self-joins
SELECT l1.num AS ConsecutiveNums
FROM logs AS l1
    JOIN logs AS l2 ON l1.id + 1 = l2.id
    JOIN logs AS l3 ON l1.id + 2 = l3.id
WHERE l1.num = l2.num AND l2.num = l3.num
GROUP BY l1.num
;

-- using LAG() (the CTE could also be a FROM subquery)
WITH lags AS (
    SELECT id
         , num
         , LAG(num) OVER (ORDER BY id) AS n1
         , LAG(num, 2) OVER (ORDER BY id) AS n2
    FROM logs)

SELECT num AS 'ConsecutiveNums'
FROM lags
WHERE num = n1 AND num = n2
;
```
