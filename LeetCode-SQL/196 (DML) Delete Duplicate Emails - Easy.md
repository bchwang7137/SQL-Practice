# 196 **(DML)** Delete Duplicate Emails - Easy
[https://leetcode.com/problems/delete-duplicate-emails/](https://leetcode.com/problems/delete-duplicate-emails/)

Write an SQL query to **delete** all the duplicate emails, keeping only one unique email with the smallest `id`. Note that you are supposed to write a `DELETE` statement and not a `SELECT` one.

After running your script, the answer shown is the `Person` table. The driver will first compile and run your piece of code and then show the `Person` table. The final order of the `Person` table **does not matter**.

```sql
-- using subquery
DELETE 
FROM person 
WHERE id NOT IN (SELECT mid 
								 FROM (
										SELECT email
												 , MIN(id) AS mid 
										FROM person 
										GROUP BY email) AS tmp)
;

-- using inner join
DELETE p1
FROM person p1
	JOIN person p2 ON p1.email = p2.email
WHERE p1.id > p2.id
;
```
