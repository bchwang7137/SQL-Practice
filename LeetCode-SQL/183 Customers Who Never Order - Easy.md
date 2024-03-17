# 183 Customers Who Never Order - Easy
[https://leetcode.com/problems/customers-who-never-order/](https://leetcode.com/problems/customers-who-never-order/)

Write an SQL query to report all customers who never order anything.

Return the result table in **any order**.

```sql
SELECT c.name AS 'Customers'
FROM customers AS c 
    LEFT JOIN orders AS o ON c.id = o.customerId
WHERE o.id IS NULL
;
```
