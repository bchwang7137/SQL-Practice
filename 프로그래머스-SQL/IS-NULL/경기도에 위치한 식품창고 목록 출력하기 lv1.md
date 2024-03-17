# 경기도에 위치한 식품창고 목록 출력하기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/131114

`FOOD_WAREHOUSE` 테이블에서 경기도에 위치한 창고의 ID, 이름, 주소, 냉동시설 여부를 조회하는 SQL문을 작성해주세요. 이때 냉동시설 여부가 NULL인 경우, 'N'으로 출력시켜 주시고 결과는 창고 ID를 기준으로 오름차순 정렬해주세요.

```sql
SELECT warehouse_id
     , warehouse_name
     , address
     , CASE WHEN freezer_yn IS NOT NULL THEN freezer_yn ELSE 'N' END AS freezer_yn
FROM food_warehouse
WHERE address LIKE '경기도%'
ORDER BY warehouse_id
;
```
