# 즐겨찾기가 가장 많은 식당 정보 출력하기 lv3
https://school.programmers.co.kr/learn/courses/30/lessons/131123

`REST_INFO` 테이블에서 음식종류별로 즐겨찾기수가 가장 많은 식당의 음식 종류, ID, 식당 이름, 즐겨찾기수를 조회하는 SQL문을 작성해주세요. 이때 결과는 음식 종류를 기준으로 내림차순 정렬해주세요.

```sql
SELECT ri.food_type
     , ri.rest_id
     , ri.rest_name
     , ri.favorites
FROM rest_info AS ri 
    JOIN (
        SELECT food_type
             , MAX(favorites) AS fav
        FROM rest_info
        GROUP BY food_type) AS tmp
    ON ri.food_type = tmp.food_type AND ri.favorites = tmp.fav
ORDER BY ri.food_type DESC
;
```
