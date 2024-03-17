# SQL Project Planning - Medium
[https://www.hackerrank.com/challenges/sql-projects/problem](https://www.hackerrank.com/challenges/sql-projects/problem)

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

**w/ reference to:** [https://www.red-gate.com/simple-talk/databases/sql-server/t-sql-programming-sql-server/gaps-islands-sql-server-data/](https://www.red-gate.com/simple-talk/databases/sql-server/t-sql-programming-sql-server/gaps-islands-sql-server-data/)

```sql
-- if DATE_SUB(start_date, INTERVAL 1 DAY) DNE, then start_date marks the start of a project
    -- use ROW_NUMBER() to assign this a project number, order chronologically
-- if DATE_ADD(end_date, INTERVAL 1 DAY) DNE, then end_date marks the end of a project
    -- use ROW_NUMBER() to assign this a project number, order chronologically
-- match project start and end dates using assigned project numbers
    -- perhaps INNER JOIN with CTEs
-- calculate difference between end_date and start_date for ordering
    -- DATEDIFF()

WITH starts AS (
    SELECT p1.task_id
         , p1.start_date
         , ROW_NUMBER() OVER (ORDER BY p1.start_date) AS project_num
    FROM projects AS p1
    WHERE NOT EXISTS (SELECT *
                      FROM projects AS p2
                      WHERE p2.start_date = DATE_SUB(p1.start_date, INTERVAL 1 DAY))
), ends AS (
    SELECT p1.task_id
         , p1.end_date
         , ROW_NUMBER() OVER (ORDER BY p1.end_date) AS project_num
    FROM projects AS p1
    WHERE NOT EXISTS (SELECT *
                      FROM projects AS p2
                      WHERE p2.end_date = DATE_ADD(p1.end_date, INTERVAL 1 DAY))
)

SELECT s.start_date
     , e.end_date
FROM starts AS s
    JOIN ends AS e ON s.project_num = e.project_num
ORDER BY DATEDIFF(e.end_date, s.start_date), s.start_date
;
```
