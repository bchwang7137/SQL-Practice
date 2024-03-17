# Population Census - Easy
[https://www.hackerrank.com/challenges/asian-population/problem](https://www.hackerrank.com/challenges/asian-population/problem)

Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

```sql
SELECT SUM(city.population)
FROM city 
	JOIN country ON city.countrycode = country.code
WHERE country.continent = 'Asia'
;
```
