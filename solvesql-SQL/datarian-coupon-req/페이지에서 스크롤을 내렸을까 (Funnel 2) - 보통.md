# 페이지에서 스크롤을 내렸을까? (Funnel 2) - 보통
`ga` 테이블에 있는 전체 기간 동안, 입문반 페이지를 봤는지 여부와 스크롤 했는지 여부를 고려한 세션 수를 집계하는 쿼리를 작성해주세요. 쿼리 결과에는 아래 컬럼이 포함되어야 합니다.

- `total` - 전체 세션 수
- `pv_no` - 입문반 페이지를 안 본 세션 수
- `pv_yes_scroll_no` - 입문반 페이지를 봤지만 입문반 페이지 스크롤은 하지 않은 세션 수
- `pv_yes_scroll_yes` - 입문반 페이지를 봤고 입문반 페이지 스크롤도 한 세션 수

```sql
WITH pv AS (
  SELECT user_pseudo_id
       , ga_session_id
       , event_timestamp_kst AS pv_ts
  FROM ga
  WHERE page_title = '백문이불여일타 SQL 캠프 입문반'
    AND event_name = 'page_view'
), sc AS (
SELECT user_pseudo_id
     , ga_session_id
     , event_timestamp_kst AS sc_ts
FROM ga 
WHERE page_title = '백문이불여일타 SQL 캠프 입문반'
  AND event_name = 'scroll'
)

SELECT COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id) AS total
     , COUNT(DISTINCT ga.user_pseudo_id, ga.ga_session_id)
        - COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv_no
     , COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id)
        - COUNT(DISTINCT sc.user_pseudo_id, sc.ga_session_id) AS pv_yes_scroll_no 
     , COUNT(DISTINCT sc.user_pseudo_id, sc.ga_session_id) AS pv_yes_scroll_yes
FROM ga
  LEFT JOIN pv ON ga.user_pseudo_id = pv.user_pseudo_id
               AND ga.ga_session_id = pv.ga_session_id
  LEFT JOIN sc ON pv.user_pseudo_id = sc.user_pseudo_id
               AND pv.ga_session_id = sc.ga_session_id
               AND pv.pv_ts <= sc.sc_ts
;
```
