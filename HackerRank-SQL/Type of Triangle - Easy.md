# Type of Triangle - Easy
[https://www.hackerrank.com/challenges/what-type-of-triangle/problem](https://www.hackerrank.com/challenges/what-type-of-triangle/problem)

Write a query identifying the _type_ of each record in the **TRIANGLES** table using its three side lengths. Output one of the following statements for each record in the table:

- **Equilateral**: It's a triangle with sides of equal length.
- **Isosceles**: It's a triangle with sides of equal length.
- **Scalene**: It's a triangle with sides of differing lengths.
- **Not A Triangle**: The given values of _A_, _B_, and _C_ don't form a triangle.

```sql
-- first, naive, approach
SELECT
    CASE 
        WHEN 
            NOT (A + B <= C OR B + C <= A OR C + A <= B)
            AND A = B
            AND B = C 
            AND C = A 
            THEN 'Equilateral'
        WHEN 
            NOT (A + B <= C OR B + C <= A OR C + A <= B)
            AND (A = B AND B != C AND A != C) 
            OR (B = C AND B != A AND C != A) 
            OR (C = A AND C != B AND A != B) 
            THEN 'Isosceles'
        WHEN
            NOT (A + B <= C OR B + C <= A OR C + A <= B)
            AND A != B
            AND B != C
            AND C != A
            THEN 'Scalene'
        ELSE
            'Not A Triangle'
    END AS triangleType
FROM
    triangles
;

-- cleaner
SELECT
    CASE
        WHEN A = B AND B = C THEN 'Equilateral'
        WHEN A + B <= C OR B + C <= A OR C + A <= B THEN 'Not A Triangle'
        WHEN A = B OR B = C OR C = A THEN 'Isosceles'
        ELSE 'Scalene'
    END
FROM
    triangles
;
```
