# 온라인 쇼핑몰의 Stickiness - 보통
`records` 테이블을 이용하여 2020년 11월 한 달 동안의 일별 DAU, WAU, Stickiness를 계산하는 쿼리를 작성해주세요. 쿼리 결과는 아래 네 개의 컬럼을 포함해야 합니다. `stickiness` 는 반올림하여 소수점 둘째자리까지만 출력해주세요. 고객들이 한번도 주문을 하지 않은 날은 집계에서 제외하며, `dt` 컬럼을 기준으로 오름차순 정렬해주세요.

- `dt` - 기준 날짜
- `dau` - 기준 날짜에 주문한 고객 수
- `wau` - 기준 날짜 6일 전부터 해당 날짜까지 상품을 주문한 고객 수
- `stickiness` - 기준 날짜의 고객 고착도

```sql
-- with multiple CTEs 
WITH days AS (
  SELECT DATE_FORMAT(order_date, '%Y-%m-%d') AS dt
  FROM records
  GROUP BY dt
),
usrs AS (
  SELECT DATE_FORMAT(order_date, '%Y-%m-%d') AS dt
      , customer_id
  FROM records
  GROUP BY dt, customer_id
)

SELECT d.dt
    , COUNT(DISTINCT IF(u.dt = d.dt, u.customer_id, NULL)) as dau
    , COUNT(DISTINCT u.customer_id) AS wau
    , ROUND(COUNT(DISTINCT IF(u.dt = d.dt, u.customer_id, NULL))
              /COUNT(DISTINCT u.customer_id) , 2) AS stickiness
FROM usrs AS u
  JOIN days AS d ON u.dt <= d.dt
                AND u.dt > DATE_SUB(d.dt, INTERVAL 7 DAY)
GROUP BY d.dt
HAVING d.dt BETWEEN '2020-11-01' AND '2020-11-30'
ORDER BY d.dt 
;

-- with a self LEFT JOIN (instructor soln)
SELECT d.order_date AS dt
     , COUNT(DISTINCT d.customer_id) AS dau 
     , COUNT(DISTINCT w.customer_id) AS wau 
     , ROUND(COUNT(DISTINCT d.customer_id) / COUNT(DISTINCT w.customer_id), 2) AS stickiness
FROM records AS d
  LEFT JOIN records AS w 
  ON w.order_date BETWEEN DATE_SUB(d.order_date, INTERVAL 6 DAY) AND d.order_date
WHERE d.order_date BETWEEN '2020-11-01' AND '2020-11-30'
GROUP BY d.order_date
;
```
