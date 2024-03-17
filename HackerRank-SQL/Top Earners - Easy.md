# Top Earners - Easy
[https://www.hackerrank.com/challenges/earnings-of-employees/problem?isFullScreen=true](https://www.hackerrank.com/challenges/earnings-of-employees/problem?isFullScreen=true)

We define an employee's _total earnings_ to be their monthly salary * months worked, and the _maximum total earnings_ to be the maximum total earnings for any employee in the **Employee** table. Write a query to find the _maximum total earnings_ for all employees as well as the total number of employees who have maximum total earnings. Then print these values as space-separated integers.

```sql
-- using ORDER BY and LIMIT
SELECT (months * salary) AS earnings
     , COUNT(DISTINCT employee_id) AS cnt
FROM employee
GROUP BY earnings
ORDER BY earnings DESC
LIMIT 1
;

-- using a subquery
SELECT (months * salary) AS earnings
     , COUNT(DISTINCT employee_id) AS cnt
FROM employee
WHERE (months * salary) = (SELECT MAX(months * salary) FROM employee)
GROUP BY earnings
;
```
