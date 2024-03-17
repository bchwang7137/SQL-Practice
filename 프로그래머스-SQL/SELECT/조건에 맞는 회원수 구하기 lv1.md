# 조건에 맞는 회원수 구하기 lv1
https://school.programmers.co.kr/learn/courses/30/lessons/131535

`USER_INFO` 테이블에서 2021년에 가입한 회원 중 나이가 20세 이상 29세 이하인 회원이 몇 명인지 출력하는 SQL문을 작성해주세요.

```sql
SELECT COUNT(DISTINCT user_id) AS users
FROM user_info
WHERE (age BETWEEN 20 AND 29) 
	AND (joined BETWEEN '2021-01-01' AND '2021-12-31')
;
```
