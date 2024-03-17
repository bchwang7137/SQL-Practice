# Weather Observation Station 11 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-11/problem](https://www.hackerrank.com/challenges/weather-observation-station-11/problem)

Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT city
FROM station
WHERE city NOT LIKE 'a%'
	AND city NOT LIKE 'e%'
	AND city NOT LIKE 'i%'
	AND city NOT LIKE 'o%'
	AND city NOT LIKE 'u%'
OR city NOT LIKE '%a'
	AND city NOT LIKE '%e'
	AND city NOT LIKE '%i'
	AND city NOT LIKE '%o'
	AND city NOT LIKE '%u'
;
```
