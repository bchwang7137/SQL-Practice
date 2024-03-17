# 보호소에서 중성화한 동물 lv4
https://school.programmers.co.kr/learn/courses/30/lessons/59045

보호소에서 중성화 수술을 거친 동물 정보를 알아보려 합니다. 보호소에 들어올 당시에는 중성화되지 않았지만, 보호소를 나갈 당시에는 중성화된 동물의 아이디와 생물 종, 이름을 조회하는 아이디 순으로 조회하는 SQL 문을 작성해주세요.

```sql
SELECT ai.animal_id
     , ai.animal_type
     , ai.name
FROM animal_ins AS ai
    JOIN animal_outs AS ao ON ai.animal_id = ao.animal_id AND ai.sex_upon_intake != ao.sex_upon_outcome
WHERE SUBSTRING(ai.sex_upon_intake,1,6) = 'Intact'
ORDER BY ai.animal_id
;
```
