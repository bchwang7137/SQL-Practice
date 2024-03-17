# 진료과별 총 예약 횟수 출력하기 lv2
https://school.programmers.co.kr/learn/courses/30/lessons/132202

`APPOINTMENT` 테이블에서 2022년 5월에 예약한 환자 수를 진료과코드 별로 조회하는 SQL문을 작성해주세요. 이때, 컬럼명은 '진료과 코드', '5월예약건수'로 지정해주시고 결과는 진료과별 예약한 환자 수를 기준으로 오름차순 정렬하고, 예약한 환자 수가 같다면 진료과 코드를 기준으로 오름차순 정렬해주세요.

```sql
SELECT mcdp_cd AS '진료과 코드'
     , COUNT(DISTINCT pt_no) AS '5월예약건수'
FROM appointment
WHERE apnt_ymd BETWEEN '2022-05-01 00:00:00' AND '2022-05-31 23:59:59'
GROUP BY mcdp_cd
ORDER BY COUNT(DISTINCT pt_no), mcdp_cd
;
```
