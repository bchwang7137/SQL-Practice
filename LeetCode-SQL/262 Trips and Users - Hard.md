# 262 Trips and Users - Hard
[https://leetcode.com/problems/trips-and-users/](https://leetcode.com/problems/trips-and-users/)

The **cancellation rate** is computed by dividing the number of canceled (by client or driver) requests with unbanned users by the total number of requests with unbanned users on that day.

Write a SQL query to find the **cancellation rate** of requests with unbanned users (**both client and driver must not be banned**) each day between `"2013-10-01"` and `"2013-10-03"`. Round `Cancellation Rate` to **two decimal** points.

Return the result table in **any order**.

```sql
SELECT t.request_at AS 'Day'
     , ROUND(COUNT(DISTINCT CASE WHEN t.status IN ('cancelled_by_driver', 'cancelled_by_client') THEN t.id END)
                / COUNT(DISTINCT t.id), 2) AS 'Cancellation Rate'
FROM trips AS t
    JOIN users AS c ON t.client_id = c.users_id
    JOIN users AS d ON t.driver_id = d.users_id
WHERE c.banned = 'No'
    AND d.banned = 'No'
    AND t.request_at BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY t.request_at
ORDER BY t.request_at
;
```
