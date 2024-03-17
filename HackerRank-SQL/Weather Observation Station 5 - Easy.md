# Weather Observation Station 5 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-5/problem](https://www.hackerrank.com/challenges/weather-observation-station-5/problem)

Query the two cities in **STATION** with the shortest and longest _CITY_ names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```sql
-- using parenthesized query and multiple LIMITs with UNION ALL
(SELECT city
      , LENGTH(city) AS len
 FROM station
 ORDER BY LENGTH(city) ASC, city
 LIMIT 1)

UNION ALL

(SELECT city
      , LENGTH(city) AS len
 FROM station
 ORDER BY LENGTH(city) DESC, city
 LIMIT 1)
;

-- using ROW_NUMBER() and UNION ALL
SELECT city
     , len
FROM (
    SELECT city
         , length(city) AS len
         , ROW_NUMBER() OVER (ORDER BY LENGTH(city) DESC, city) AS rn
    FROM station) AS longs
WHERE rn = 1

UNION ALL

SELECT city
     , len
FROM (
    SELECT city
         , length(city) AS len
         , ROW_NUMBER() OVER (ORDER BY LENGTH(city), city) AS rn
    FROM station) AS shorts
WHERE rn = 1

ORDER BY city
;
```
