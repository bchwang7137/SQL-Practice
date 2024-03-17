# 181 Employees Earning More Than Their Managers - Easy
[https://leetcode.com/problems/employees-earning-more-than-their-managers/](https://leetcode.com/problems/employees-earning-more-than-their-managers/)

Write an SQL query to find the employees who earn more than their managers.

Return the result table in **any order**.

```sql
SELECT e1.name AS 'Employee'
FROM employee AS e1 
    JOIN employee AS e2 ON e1.managerId = e2.id
WHERE e1.salary > e2.salary
;
```
