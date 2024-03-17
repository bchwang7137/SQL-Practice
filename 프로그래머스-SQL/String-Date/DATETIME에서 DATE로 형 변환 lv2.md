# DATETIME에서 DATE로 형 변환 lv2
https://school.programmers.co.kr/learn/courses/30/lessons/59414

`ANIMAL_INS` 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜를 조회하는 SQL문을 작성해주세요. 이때 결과는 아이디 순으로 조회해야 합니다.

- 시각(시-분-초)을 제외한 날짜(년-월-일)만 보여주세요.

```sql
SELECT animal_id
     , name
     , DATE_FORMAT(datetime, '%Y-%m-%d') AS '날짜'
FROM animal_ins
ORDER BY animal_id
;
```
