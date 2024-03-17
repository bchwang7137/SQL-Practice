# Weather Observation Station 12 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-12/problem](https://www.hackerrank.com/challenges/weather-observation-station-12/problem)

Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'a%'
	AND CITY NOT LIKE '%a'
	AND CITY NOT LIKE 'e%'
	AND CITY NOT LIKE '%e'
	AND CITY NOT LIKE 'i%'
	AND CITY NOT LIKE '%i'
	AND CITY NOT LIKE 'o%'
	AND CITY NOT LIKE '%o'
	AND CITY NOT LIKE 'u%'
	AND CITY NOT LIKE '%u'
;
```
