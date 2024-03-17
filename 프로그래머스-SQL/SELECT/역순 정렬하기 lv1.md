# 역순 정렬하기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/59035

동물 보호소에 들어온 모든 동물의 이름과 보호 시작일을 조회하는 SQL문을 작성해주세요. 이때 결과는 ANIMAL_ID 역순으로 보여주세요. SQL을 실행하면 다음과 같이 출력되어야 합니다.

```sql
SELECT tmp.name
     , tmp.datetime
FROM (
    SELECT animal_id
         , name
         , datetime
    FROM animal_ins
    ORDER BY animal_id DESC) AS tmp
;
```
