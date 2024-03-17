# Average Population of Each Continent - Easy
[https://www.hackerrank.com/challenges/average-population-of-each-continent/problem](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem)

Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

```sql
SELECT country.continent
		 , FLOOR(AVG(city.population))
FROM city 
	JOIN country on city.countrycode = country.code
GROUP BY country.continent
;
```
