# Finding Updated Records - Easy
[https://platform.stratascratch.com/coding/10299-finding-updated-records](https://platform.stratascratch.com/coding/10299-finding-updated-records)

We have a table with employees and their salaries, however, some of the records are old and contain outdated salary information. Find the current salary of each employee assuming that salaries increase each year. Output their id, first name, last name, department ID, and current salary. Order your list by employee ID in ascending order.

```sql
SELECT id
     , first_name
     , last_name
     , department_id
     , MAX(salary) AS current_salary
FROM ms_employee_salary
GROUP BY id, first_name, last_name, department_id
;

-- robust solution
SELECT id
     , first_name
     , last_name
     , department_id
     , salary AS max_salary
FROM (
    SELECT *
         , DENSE_RANK() OVER (PARTITION BY id ORDER BY salary DESC) AS rnk
    FROM ms_employee_salary) AS sal
WHERE sal.rnk = 1
ORDER BY id
;
```
