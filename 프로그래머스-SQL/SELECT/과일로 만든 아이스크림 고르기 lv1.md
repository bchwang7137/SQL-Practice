# 과일로 만든 아이스크림 고르기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/133025

상반기 아이스크림 총주문량이 3,000보다 높으면서 아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이 큰 순서대로 조회하는 SQL 문을 작성해주세요.

```sql
SELECT fh.flavor
FROM first_half fh join icecream_info ii on fh.flavor = ii.flavor
WHERE ii.ingredient_type = 'fruit_based'
GROUP BY fh.flavor
HAVING SUM(total_order) > 3000
ORDER BY SUM(total_order) DESC
;
```
