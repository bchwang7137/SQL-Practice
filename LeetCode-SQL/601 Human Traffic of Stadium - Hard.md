# 601 Human Traffic of Stadium - Hard
[https://leetcode.com/problems/human-traffic-of-stadium/](https://leetcode.com/problems/human-traffic-of-stadium/)

Write an SQL query to display the records with three or more rows with **consecutive** `id`'s, and the number of people is greater than or equal to 100 for each.

Return the result table ordered by `visit_date` in **ascending order**.

```sql
-- using CTEs and ROW_NUMBER() 
WITH cte1 AS (
    SELECT *
         , CASE WHEN people >= 100 THEN 1 ELSE 0 END AS high_traffic
         , ROW_NUMBER() OVER (ORDER BY visit_date) AS rn1
         , ROW_NUMBER() OVER (PARTITION BY CASE WHEN people >= 100 THEN 1 ELSE 0 END ORDER BY visit_date) AS rn2
    FROM stadium
), cte2 AS (
    SELECT *
         , rn1 - rn2 AS diff
         , COUNT(*) OVER (PARTITION BY high_traffic, rn1 - rn2) AS consec
    FROM cte1
)

SELECT id
	 , visit_date
	 , people
FROM cte2
WHERE consec >= 3
ORDER BY visit_date
;
```
