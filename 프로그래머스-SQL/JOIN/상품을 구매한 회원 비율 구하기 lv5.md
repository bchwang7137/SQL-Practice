# 상품을 구매한 회원 비율 구하기 lv5
https://school.programmers.co.kr/learn/courses/30/lessons/131534

`USER_INFO` 테이블과 `ONLINE_SALE` 테이블에서 2021년에 가입한 전체 회원들 중 상품을 구매한 회원수와 상품을 구매한 회원의 비율(=2021년에 가입한 회원 중 상품을 구매한 회원수 / 2021년에 가입한 전체 회원 수)을 년, 월 별로 출력하는 SQL문을 작성해주세요. 상품을 구매한 회원의 비율은 소수점 두번째자리에서 반올림하고, 전체 결과는 년을 기준으로 오름차순 정렬해주시고 년이 같다면 월을 기준으로 오름차순 정렬해주세요.

```sql
-- first approach
WITH total AS (
    SELECT COUNT(DISTINCT user_id) AS tot
    FROM user_info
    WHERE joined BETWEEN '2021-01-01 00:00:00' AND '2021-12-31 23:59:59')

SELECT DATE_FORMAT(os.sales_date, '%Y') AS yr
     , DATE_FORMAT(os.sales_date, '%m') AS mn
     , COUNT(DISTINCT os.user_id) AS pu
     , ROUND(COUNT(DISTINCT os.user_id)/t.tot, 1) AS pr
FROM (
    SELECT user_id
    FROM user_info
    WHERE joined BETWEEN '2021-01-01 00:00:00' AND '2021-12-31 23:59:59') AS ui
    LEFT JOIN online_sale AS os ON ui.user_id = os.user_id
    CROSS JOIN total AS t
WHERE os.online_sale_id IS NOT NULL 
GROUP BY DATE_FORMAT(os.sales_date, '%Y'), DATE_FORMAT(os.sales_date, '%m')
ORDER BY yr, mn
;

-- slightly more compact
SELECT DATE_FORMAT(os.sales_date, '%Y') AS yr
		 , DATE_FORMAT(os.sales_date, '%m') AS mn
		 , COUNT(DISTINCT os.user_id) AS pu
		 , ROUND(COUNT(DISTINCT os.user_id) 
					/ (SELECT COUNT(DISTINCT user_id)
						 FROM user_info
						 WHERE joined BETWEEN '2021-01-01 00:00:00' 
													AND '2021-12-31 23:59:59'), 1) AS pr
FROM user_info AS ui
		JOIN online_sale AS os ON ui.user_id = os.user_id
WHERE ui.joined BETWEEN '2021-01-01 00:00:00' AND '2021-12-31 23:59:59'
GROUP BY DATE_FORMAT(os.sales_date, '%Y'), DATE_FORMAT(os.sales_date, '%m')
ORDER BY yr, mn
;
```
