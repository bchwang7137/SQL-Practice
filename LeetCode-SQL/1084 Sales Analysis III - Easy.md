# 1084 Sales Analysis III - Easy
[https://leetcode.com/problems/sales-analysis-iii/](https://leetcode.com/problems/sales-analysis-iii/)

Write an SQL query that reports the **products** that were **only** sold in the first quarter of `2019`. That is, between `2019-01-01` and `2019-03-31` inclusive.

Return the result table in **any order**.

```sql
WITH items AS (
    SELECT p.product_id
         , p.product_name
         , s.sale_date
    FROM product AS p
        JOIN sales AS s ON p.product_id = s.product_id
)

SELECT DISTINCT product_id
     , product_name
FROM items
WHERE sale_date BETWEEN '2019-01-01' AND '2019-03-31'
    AND product_id NOT IN (SELECT DISTINCT product_id
                           FROM items
                           WHERE sale_date < '2019-01-01'
                                OR sale_date > '2019-03-31')
;
```
