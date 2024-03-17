# 입문반 페이지를 본 세션 찾기 (Funnel 1) - 보통
`ga` 테이블에 있는 전체 기간 동안, 입문반 페이지를 본 세션과 그렇지 않은 세션의 수를 집계하는 쿼리를 작성해주세요. 쿼리 결과에는 아래 컬럼이 포함되어야 합니다.

- `total` - 전체 세션 수
- `pv_no` - 입문반 페이지를 안 본 세션 수 (= `total` - `pv_yes`)
- `pv_yes` - 입문반 페이지를 본 세션 수

```sql
WITH pv AS (
  SELECT user_pseudo_id
       , ga_session_id
  FROM ga
  WHERE page_title = '백문이불여일타 SQL 캠프 입문반'
    AND event_name = 'page_view'
)

SELECT COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id) AS total
     , COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id)
        - COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv_no
     , COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv_yes
FROM ga
  LEFT JOIN pv ON ga.user_pseudo_id = pv.user_pseudo_id
               AND ga.ga_session_id = pv.ga_session_id
;
```
