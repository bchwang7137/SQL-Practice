# Challenges - Medium
[https://www.hackerrank.com/challenges/challenges/problem](https://www.hackerrank.com/challenges/challenges/problem)

Julia asked her students to create some coding challenges. Write a query to print the _hacker_id_, _name_, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by _hacker_id_. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

```sql
-- consider two cases:
-- 1. challenge count = max(challenge count)
--     in this case, we include every student with the same challenge count
-- 2. challenge count != max(challenge count)
--     in this case, we exclude every student with the same challenge count
--     in other words, we only include students with unique challenge counts

-- with nested subqueries 
SELECT hck.hacker_id
		 , hck.name
		 , COUNT(*) AS cnt_chal
FROM hackers AS hck
	JOIN challenges AS chl ON hck.hacker_id = chl.hacker_id
GROUP BY hck.hacker_id, hck.name
HAVING cnt_chal = (SELECT MAX(cnt_chal) 
									 FROM (
												SELECT hacker_id
														 , COUNT(*) AS cnt_chal
												FROM challenges
												GROUP BY hacker_id) AS tmp)
	OR cnt_chal IN (SELECT cnt_chal
									FROM (
											SELECT hacker_id
													 , COUNT(*) AS cnt_chal
											FROM challenges
											GROUP BY hacker_id) AS tmp
									GROUP BY cnt_chal
									HAVING COUNT(*) = 1)
ORDER BY cnt_chal DESC, hacker_id
;

-- with CTE and OR
WITH counts AS (
	SELECT hck.hacker_id
			 , hck.name
			 , COUNT(*) AS cnt_chal
	FROM hackers AS hck
		JOIN challenges AS chl ON hck.hacker_id = chl.hacker_id
	GROUP BY hck.hacker_id, hck.name)

SELECT counts.hacker_id
		 , counts.name
		 , counts.cnt_chal
FROM counts
WHERE cnt_chal = (SELECT MAX(cnt_chal) FROM counts)
	OR cnt_chal IN (SELECT cnt_chal
									FROM counts
									GROUP BY cnt_chal
									HAVING COUNT(*) = 1)
ORDER BY counts.cnt_chal DESC, counts.hacker_id
;

-- with CTEs and UNION / UNION ALL
WITH counts AS (
	SELECT hck.hacker_id
			 , hck.name
			 , COUNT(*) AS cnt_chal
	FROM hackers AS hck
		JOIN challenges AS chl ON hck.hacker_id = chl.hacker_id
	GROUP BY hck.hacker_id, hck.name)

SELECT hacker_id
		 , name
		 , cnt_chal
FROM counts
WHERE cnt_chal = (SELECT MAX(cnt_chal) FROM counts)

UNION ALL

SELECT hacker_id
		 , name
		 , cnt_chal
FROM counts
WHERE cnt_chal IN (SELECT cnt_chal
									 FROM counts
									 GROUP BY cnt_chal
									 HAVING COUNT(*) = 1)

ORDER BY counts.cnt_chal DESC, counts.hacker_id
;
```
