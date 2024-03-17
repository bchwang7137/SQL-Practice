# 어린 동물 찾기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/59037

동물 보호소에 들어온 동물 중 젊은 동물의 아이디와 이름을 조회하는 SQL 문을 작성해주세요. 이때 결과는 아이디 순으로 조회해주세요.

```sql
SELECT animal_id
     , name
FROM animal_ins
WHERE intake_condition != 'Aged'
ORDER BY animal_id
;
```
