# Salaries Differences - Easy
[https://platform.stratascratch.com/coding/10308-salaries-differences](https://platform.stratascratch.com/coding/10308-salaries-differences)

Write a query that calculates the difference between the highest salaries found in the marketing and engineering departments. Output just the absolute difference in salaries.

```sql
-- first approach
WITH mkt AS (
    SELECT MAX(salary) AS maxsal
    FROM db_employee AS e
        JOIN db_dept AS d ON e.department_id = d.id
    WHERE d.department = 'marketing'),
engi AS (
SELECT MAX(salary) AS maxsal
    FROM db_employee AS e
        JOIN db_dept AS d ON e.department_id = d.id
    WHERE d.department = 'engineering')

SELECT ABS(m.maxsal - e.maxsal) AS saldiff
FROM mkt m, engi e
;

-- neater approach
SELECT ABS(MAX(CASE WHEN d.department = 'marketing' THEN salary END) 
            - MAX(CASE WHEN d.department = 'engineering' THEN salary END)) AS saldiff
FROM db_employee AS e
    JOIN db_dept AS d ON e.department_id = d.id
;
```
