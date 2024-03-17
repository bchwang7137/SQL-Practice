# 유입 채널 별 실전반 전환율 (Funnel 4) - 어려움
`ga` 테이블에 있는 전체 기간 동안, 실전반 페이지를 본 이후에 스크롤을 내려본 세션은 얼마나 되는지, 또 스크롤을 내려 실전반 신청하기 버튼까지 클릭한 세션은 얼마나 되는지를 유입 채널별로 나누어 조회하는 쿼리를 작성해주세요. 퍼널 분석이므로 동일 세션 내에서도 이벤트들 간의 선후 관계가 집계 시에 고려되어야 합니다. 동시에 발생한 이벤트의 경우 다음 퍼널로 전환된 것으로 간주해주세요. 쿼리 결과에는 아래 컬럼이 포함되어야 하고, `**pv` 컬럼을 기준으로 내림차순 정렬되어 있어야 합니다.**

- `source` - 트래픽 획득 소스
- `medium` - 트래픽 획득 매체
- `pv` - 실전반 페이지를 본 세션 수
- `scroll_after_pv` - 실전반 페이지를 본 후 스크롤를 내린 세션 수
- `click_after_scroll` - 실전반 페이지를 본 후 스크롤을 내려 실전반 신청하기 버튼을 클릭한 세션 수
- `pv_scroll_rate` - 실전반 페이지를 본 세션 중 스크롤을 내린 세션의 비율 (= `scroll_after_pv` / `pv`)
- `pv_click_rate` - 실전반 페이지를 본 세션 중 스크롤을 내리고 신청하기 버튼까지 클릭한 세션의 비율 (=`click_after_scroll` / `pv`
- `scroll_click_rate` - 실전반 페이지에서 스크롤을 내린 세션 중 신청하기 버튼까지 클릭한 세션의 비율 (= `click_after_scroll` / `scroll_after_pv`)

세션의 비율을 나타내는 `pv_scroll_rate`, `pv_click_rate`, `scroll_click_rate` 컬럼은 소수점 아래 **넷째 자리에서 반올림 해 셋째자리까지 표현해주세요**.

```sql
WITH pv AS (
  SELECT user_pseudo_id
       , ga_session_id
       , event_timestamp_kst AS pv_ts
       , source
       , medium
  FROM ga 
  WHERE page_title = '백문이불여일타 SQL 캠프 실전반'
    AND event_name = 'page_view'
), sc AS (
  SELECT user_pseudo_id
       , ga_session_id
       , event_timestamp_kst AS sc_ts
       , source
       , medium
  FROM ga 
  WHERE page_title = '백문이불여일타 SQL 캠프 실전반'
    AND event_name = 'scroll'
), cl AS (
  SELECT user_pseudo_id
       , ga_session_id
       , event_timestamp_kst AS cl_ts
       , source
       , medium
  FROM ga 
  WHERE page_title = '백문이불여일타 SQL 캠프 실전반'
    AND event_name = 'SQL_advanced_form_click'
)

SELECT pv.source
     , pv.medium
     , COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id) AS pv 
     , COUNT(DISTINCT sc.user_pseudo_id, sc.ga_session_id) AS scroll_after_pv
     , COUNT(DISTINCT cl.user_pseudo_id, cl.ga_session_id) AS click_after_scroll
     , ROUND(COUNT(DISTINCT sc.user_pseudo_id, sc.ga_session_id)
              /COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id), 3) AS pv_scroll_rate
     , ROUND(COUNT(DISTINCT cl.user_pseudo_id, cl.ga_session_id)
              /COUNT(DISTINCT pv.user_pseudo_id, pv.ga_session_id), 3) AS pv_click_rate
     , ROUND(COUNT(DISTINCT cl.user_pseudo_id, cl.ga_session_id)
              /COUNT(DISTINCT sc.user_pseudo_id, sc.ga_session_id), 3) AS scroll_click_rate
FROM pv
  LEFT JOIN sc ON pv.user_pseudo_id = sc.user_pseudo_id
               AND pv.ga_session_id = sc.ga_session_id
               AND pv.pv_ts <= sc.sc_ts
  LEFT JOIN cl ON sc.user_pseudo_id = cl.user_pseudo_id
               AND sc.ga_session_id = cl.ga_session_id
               AND sc.sc_ts <= cl.cl_ts
GROUP BY pv.source, pv.medium
ORDER BY pv DESC
;
```
