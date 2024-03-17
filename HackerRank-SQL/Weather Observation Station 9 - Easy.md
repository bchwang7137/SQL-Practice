# Weather Observation Station 9 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-9/problem](https://www.hackerrank.com/challenges/weather-observation-station-9/problem)

Query the list of _CITY_ names from **STATION** that _do not start_ with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT city
FROM station
WHERE city NOT REGEXP '^[aeiou].*'
;
```
