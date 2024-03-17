# 184 Department Highest Salary - Medium
[https://leetcode.com/problems/department-highest-salary/](https://leetcode.com/problems/department-highest-salary/)

Write an SQL query to find employees who have the highest salary in each of the departments.

Return the result table in **any order**.

```sql
-- subquery in WHERE
SELECT dpt.name AS 'Department'
     , emp.name AS 'Employee'
     , emp.salary AS 'Salary'
FROM employee AS emp
    JOIN department AS dpt ON emp.departmentid = dpt.id
WHERE (departmentid, salary) IN (SELECT departmentid
                                      , MAX(salary)
                                 FROM employee
                                 GROUP BY departmentid)
;

-- subquery in FROM
SELECT dpt.name AS 'Department'
     , emp.name AS 'Employee'
     , emp.salary AS 'Salary'
FROM employee AS emp
    JOIN (SELECT departmentid
               , MAX(salary) AS max_salary
          FROM employee
          GROUP BY departmentid) AS ms ON emp.departmentid = ms.departmentid
                                       AND emp.salary = ms.max_salary
    JOIN department AS dpt ON emp.departmentid = dpt.id
;

-- using RANK()
SELECT sr.Department
     , sr.Employee
     , sr.Salary
FROM (
    SELECT dep.name AS 'Department'
         , emp.name AS 'Employee'
         , emp.salary AS 'Salary'
         , RANK() OVER (PARTITION BY dep.id ORDER BY emp.salary DESC) AS salary_rank
    FROM employee AS emp
        JOIN department AS dep ON emp.departmentid = dep.id) AS sr
WHERE sr.salary_rank = 1
;

-- using MAX()
SELECT ms.Department
     , ms.Employee
     , ms.Salary
FROM (
    SELECT dep.name AS 'Department'
         , emp.name AS 'Employee'
         , emp.salary AS 'Salary'
         , MAX(salary) OVER (PARTITION BY dep.id) AS maxsal
    FROM employee AS emp
        JOIN department AS dep ON emp.departmentid = dep.id) AS ms
WHERE ms.salary = ms.maxsal
;

```
