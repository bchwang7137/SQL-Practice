# The Report - Medium
[https://www.hackerrank.com/challenges/the-report/problem](https://www.hackerrank.com/challenges/the-report/problem)

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order. Write a query to help Eve.

```sql
-- first approach
WITH mks AS (
     SELECT id
          , name AS fname
          , marks
          , CASE
                 WHEN marks BETWEEN 0 AND 9 THEN 1
                 WHEN marks BETWEEN 10 AND 19 THEN 2
                 WHEN marks BETWEEN 20 AND 29 THEN 3
                 WHEN marks BETWEEN 30 AND 39 THEN 4
                 WHEN marks BETWEEN 40 AND 49 THEN 5
                 WHEN marks BETWEEN 50 AND 59 THEN 6
                 WHEN marks BETWEEN 60 AND 69 THEN 7
                 WHEN marks BETWEEN 70 AND 79 THEN 8
                 WHEN marks BETWEEN 80 AND 89 THEN 9
                 WHEN marks BETWEEN 90 AND 100 THEN 10
             END AS 'grade'
     FROM students
 )

SELECT CASE
            WHEN grade >= 8 THEN fname
            ELSE 'NULL'
       END AS name
     , grade
     , marks
FROM mks
ORDER BY grade DESC, name ASC, marks ASC
;

-- cleaner
SELECT CASE
        WHEN gr.grade >= 8 THEN st.name
        ELSE 'NULL'
       END
     , gr.grade
     , st.marks
FROM students AS st
    JOIN grades AS gr ON st.marks >= gr.min_mark AND st.marks <= gr.max_mark
ORDER BY gr.grade DESC, st.name ASC
;

-- using BETWEEN
SELECT CASE WHEN g.grade >= 8 THEN s.name ELSE 'NULL' END AS name
     , g.grade
     , s.marks
FROM students AS s
    JOIN grades AS g ON s.marks BETWEEN g.min_mark AND g.max_mark
ORDER BY grade DESC, name, marks
;
```
