# Weather Observation Station 4 - Easy
[https://www.hackerrank.com/challenges/weather-observation-station-4/problem](https://www.hackerrank.com/challenges/weather-observation-station-4/problem)

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

```sql
SELECT
    COUNT(city) - COUNT(DISTINCT city) AS diff
FROM
    station
;
```
