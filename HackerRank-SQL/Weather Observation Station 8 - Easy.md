# Weather Observation Station 8 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-8/problem](https://www.hackerrank.com/challenges/weather-observation-station-8/problem)

Query the list of _CITY_ names from **STATION** which have vowels (i.e., _a_, _e_, _i_, _o_, and _u_) as both their first _and_ last characters. Your result cannot contain duplicates.

```sql
-- using LIKE
SELECT DISTINCT city
FROM station
WHERE (city LIKE 'a%' OR city LIKE 'e%' OR city LIKE 'i%' OR city LIKE 'o%' OR city LIKE 'u%')
    AND (city LIKE '%a' OR city LIKE '%e' OR city LIKE '%i' OR city LIKE '%o' OR city LIKE '%u')
;

-- using REGEXP
SELECT DISTINCT city
FROM station
WHERE city REGEXP '^[aeiou].*[aeiou]$'
;
```
