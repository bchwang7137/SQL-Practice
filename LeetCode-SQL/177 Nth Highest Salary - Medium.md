# 177 Nth Highest Salary - Medium
[https://leetcode.com/problems/nth-highest-salary/](https://leetcode.com/problems/nth-highest-salary/)

Write an SQL query to report the `nth` highest salary from the `Employee` table. If there is no `nth` highest salary, the query should report `null`.

```sql
-- using CASE
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
    SELECT CASE WHEN COUNT(tmp.Salary) < N THEN NULL
                ELSE MIN(tmp.Salary)
            END
    FROM (
        SELECT DISTINCT Salary
        FROM Employee
        ORDER BY Salary DESC
        LIMIT N
        ) AS tmp
  );
END

-- using IF(condition, return when true, return when false)
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
    SELECT IF(COUNT(tmp.Salary) < N, NULL, MIN(tmp.Salary))
    FROM (
        SELECT DISTINCT Salary
        FROM Employee
        ORDER BY Salary DESC
        LIMIT N
        ) AS tmp
  );
END

-- using LIMIT OFFSET
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N = N - 1;
  RETURN (
    SELECT DISTINCT salary
    FROM employee
    ORDER BY salary DESC
    LIMIT 1 OFFSET N
  );
END

-- or... LIMIT N, 1
```
