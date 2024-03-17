# 있었는데요 없었습니다 lv3
https://school.programmers.co.kr/learn/courses/30/lessons/59043

관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일이 빠른 순으로 조회해야합니다.

```sql
WITH ordered AS (
    SELECT ai.animal_id
         , ai.name
         , ai.datetime
    FROM animal_ins AS ai
        JOIN animal_outs AS ao ON (ai.animal_id = ao.animal_id) AND (ao.datetime < ai.datetime)
    ORDER BY ai.datetime)
    
SELECT animal_id
     , name
FROM ordered
;
```
