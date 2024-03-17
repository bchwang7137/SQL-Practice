# Weather Observation Station 6 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-6/problem](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

```sql
-- using LIKE
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
	OR CITY LIKE 'e%'
	OR CITY LIKE 'i%'
	OR CITY LIKE 'o%'
	OR CITY LIKE 'u%'
;

-- using REGEXP
SELECT DISTINCT city
FROM station
WHERE city REGEXP '^[AEIOUaeiou].*'
;
```
