# 185 Department Top Three Salaries - Hard
[https://leetcode.com/problems/department-top-three-salaries/](https://leetcode.com/problems/department-top-three-salaries/)

A company's executives are interested in seeing who earns the most money in each of the company's departments. A **high earner** in a department is an employee who has a salary in the **top three unique** salaries for that department.

Write an SQL query to find the employees who are **high earners** in each of the departments.

Return the result table **in any order**.

```sql
-- using DENSE_RANK()
SELECT sr.Department
     , sr.Employee
     , sr.Salary
FROM (
    SELECT emp.name AS 'Employee'
         , emp.salary AS 'Salary'
         , dep.name AS 'Department'
         , DENSE_RANK() OVER (PARTITION BY dep.id ORDER BY emp.salary DESC) AS salary_rank
    FROM employee AS emp
        JOIN department AS dep ON emp.departmentid = dep.id) AS sr
WHERE sr.salary_rank BETWEEN 1 AND 3
;
```
