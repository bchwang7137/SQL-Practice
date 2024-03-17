# Symmetric Pairs - Medium
[https://www.hackerrank.com/challenges/symmetric-pairs/problem](https://www.hackerrank.com/challenges/symmetric-pairs/problem)

You are given a table, Functions, containing two columns: X and Y. Two pairs (X1, Y1) and (X2, Y2) are said to be symmetric pairs if X1 = Y2 and X2 = Y1. Write a query to output all such symmetric pairs in ascending order by the value of X. List the rows such that X1 ≤ Y1.

```sql
-- using a JOIN and HAVING
SELECT f1.x, f1.y
FROM functions AS f1
	JOIN functions AS f2 ON f1.x = f2.y AND f1.y = f2.x
GROUP BY f1.x, f1.y
HAVING COUNT(*) > 1 OR f1.x < f1.y
ORDER BY f1.x
;

-- using a UNION and JOIN
SELECT x, y
FROM functions
WHERE x = y
GROUP BY x, y
HAVING COUNT(*) >= 2

UNION

SELECT f1.x, f1.y
FROM functions AS f1 INNER JOIN functions AS f2 ON f1.x = f2.y AND f1.y = f2.x
WHERE f1.x < f1.y

ORDER BY x ASC
;
```
