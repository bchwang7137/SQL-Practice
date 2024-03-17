# 197 Rising Temperature - Easy
[https://leetcode.com/problems/rising-temperature/](https://leetcode.com/problems/rising-temperature/)

Write an SQL query to find all dates' `Id` with higher temperatures compared to its previous dates (yesterday).

Return the result table in **any order**.

```sql
SELECT w1.id
FROM weather w1 
    JOIN WEATHER w2 on w1.recordDate = DATE_ADD(w2.recordDate, INTERVAL 1 DAY)
WHERE w1.temperature > w2.temperature
;
```
