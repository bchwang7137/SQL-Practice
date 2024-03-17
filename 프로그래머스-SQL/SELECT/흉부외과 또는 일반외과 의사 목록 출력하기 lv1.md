# 흉부외과 또는 일반외과 의사 목록 출력하기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/132203

`DOCTOR` 테이블에서 진료과가 흉부외과(CS)이거나 일반외과(GS)인 의사의 이름, 의사ID, 진료과, 고용일자를 조회하는 SQL문을 작성해주세요. 이때 결과는 고용일자를 기준으로 내림차순 정렬하고, 고용일자가 같다면 이름을 기준으로 오름차순 정렬해주세요.

```sql
SELECT dr_name
     , dr_id
     , mcdp_cd
     , DATE(hire_ymd)
FROM doctor
WHERE mcdp_cd IN ('CS', 'GS')
ORDER BY hire_ymd DESC, dr_name
;
```
