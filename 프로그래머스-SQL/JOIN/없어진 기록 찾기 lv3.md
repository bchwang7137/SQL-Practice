# 없어진 기록 찾기 lv3
https://school.programmers.co.kr/learn/courses/30/lessons/59042

천재지변으로 인해 일부 데이터가 유실되었습니다. 입양을 간 기록은 있는데, 보호소에 들어온 기록이 없는 동물의 ID와 이름을 ID 순으로 조회하는 SQL문을 작성해주세요.

```sql
SELECT ao.animal_id
     , ao.name
FROM animal_outs AS ao
    LEFT JOIN animal_ins AS ai ON ao.animal_id = ai.animal_id
WHERE ai.animal_id IS NULL
ORDER BY animal_id
;
```
