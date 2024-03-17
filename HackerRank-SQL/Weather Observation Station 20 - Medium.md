# Weather Observation Station 20 - Medium
[https://www.hackerrank.com/challenges/weather-observation-station-20/problem](https://www.hackerrank.com/challenges/weather-observation-station-20/problem)

A _[median](https://en.wikipedia.org/wiki/Median)_ is defined as a number separating the higher half of a data set from the lower half. Query the _median_ of the _Northern Latitudes_ (_LAT_N_) from **STATION** and round your answer to 4 decimal places.

```sql
-- need to know if row count is even or odd
-- if odd, then the middlemost value will be the median
-- if even, then the average of the two middlemost values will be the median

-- we will calculate the row count + 1
	-- if row count is odd, then (row count + 1) / 2 will be a whole number
		-- ceil and floor will produce the same number
		-- avg(1 number) will produce the median
	-- if row count is even, then (row count + 1) / 2 will be a decimal
		-- ceil and floor will produce two different numbers
		-- avg(2 numbers) will produce the median

-- using nested subqueries
SELECT ROUND(AVG(lat_n), 4) AS median
FROM (
    SELECT lat_n
    FROM (
        SELECT lat_n
             , ROW_NUMBER() OVER (ORDER BY lat_n) AS rn
             , COUNT(*) OVER () AS cnt
        FROM station
    ) AS ordered
    WHERE rn IN (CEIL((cnt + 1)/2), FLOOR((cnt + 1)/2))
) AS middles
;

-- using CTEs
WITH ordered AS (
    SELECT lat_n
         , ROW_NUMBER() OVER (ORDER BY lat_n) AS rn
         , COUNT(*) OVER () AS cnt
    FROM station
), middles AS (
    SELECT lat_n
    FROM ordered
    WHERE rn IN (CEIL((cnt + 1)/2), FLOOR((cnt + 1)/2))
)

SELECT ROUND(AVG(lat_n), 4) AS median
FROM middles
;
```
