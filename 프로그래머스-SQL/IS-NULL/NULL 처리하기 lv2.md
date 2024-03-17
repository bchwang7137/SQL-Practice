# NULL 처리하기 - lv2
https://school.programmers.co.kr/learn/courses/30/lessons/59410

입양 게시판에 동물 정보를 게시하려 합니다. 동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 "No name"으로 표시해 주세요.

```sql
SELECT animal_type
     , CASE WHEN name IS NOT NULL THEN name ELSE 'No name' END AS name
     , sex_upon_intake
FROM animal_ins
ORDER BY animal_id
;
```
