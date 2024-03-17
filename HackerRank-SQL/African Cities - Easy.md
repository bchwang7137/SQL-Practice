# African Cities - Easy
https://www.hackerrank.com/challenges/african-cities/problem](https://www.hackerrank.com/challenges/african-cities/problem)

Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

```sql
SELECT c1.name
FROM city AS c1 
	JOIN country AS c2 ON c1.countrycode = c2.code
WHERE c2.continent = 'Africa'
;
```
