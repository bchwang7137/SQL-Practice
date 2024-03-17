# New Companies - Medium
[https://www.hackerrank.com/challenges/the-company/problem](https://www.hackerrank.com/challenges/the-company/problem)

Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:

![https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the _company_code_, _founder_ name, total number of _lead_ managers, total number of _senior_ managers, total number of _managers_, and total number of _employees_. Order your output by ascending _company_code_.

**Note:**

- The tables may contain duplicate records.
- The _company_code_ is string, so the sorting should not be **numeric**. For example, if the _company_codes_ are _C_1_, _C_2_, and _C_10_, then the ascending _company_codes_ will be _C_1_, _C_10_, and _C_2_.

```sql
-- first approach (CTE didn't work with HackerRank MySQL)
SELECT c.company_code
     , c.founder
     , cnts.lm
     , cnts.sm
     , cnts.mc
     , cnts.e
FROM company AS c
    JOIN (
        SELECT company_code
             , COUNT(DISTINCT lead_manager_code) AS lm
             , COUNT(DISTINCT senior_manager_code) AS sm
             , COUNT(DISTINCT manager_code) AS mc
             , COUNT(DISTINCT employee_code) AS e
        FROM employee
        GROUP BY company_code) AS cnts 
    ON c.company_code = cnts.company_code
ORDER BY c.company_code ASC
;

-- cleaner
SELECT c.company_code
     , c.founder
     , COUNT(DISTINCT e.lead_manager_code) AS lm
     , COUNT(DISTINCT e.senior_manager_code) AS sm
     , COUNT(DISTINCT manager_code) AS mc
     , COUNT(DISTINCT employee_code) AS e
FROM company AS c
    JOIN employee AS e
GROUP BY c.company_code, c.founder
ORDER BY c.company_code
;
```
