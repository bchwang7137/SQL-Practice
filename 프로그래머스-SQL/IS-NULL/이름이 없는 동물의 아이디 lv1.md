# 이름이 없는 동물의 아이디 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/59039

동물 보호소에 들어온 동물 중, 이름이 없는 채로 들어온 동물의 ID를 조회하는 SQL 문을 작성해주세요. 단, ID는 오름차순 정렬되어야 합니다.

```sql
SELECT animal_id
FROM animal_ins
WHERE name IS NULL
ORDER BY animal_id
;
```
