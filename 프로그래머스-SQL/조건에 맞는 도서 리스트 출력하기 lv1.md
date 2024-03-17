# 조건에 맞는 도서 리스트 출력하기 lv1
[https://school.programmers.co.kr/learn/courses/30/lessons/144853](https://school.programmers.co.kr/learn/courses/30/lessons/144853)

`BOOK` 테이블에서 `2021년`에 출판된 `'인문'` 카테고리에 속하는 도서 리스트를 찾아서 도서 ID(`BOOK_ID`), 출판일 (`PUBLISHED_DATE`)을 출력하는 SQL문을 작성해주세요. 결과는 출판일을 기준으로 오름차순 정렬해주세요.

`PUBLISHED_DATE`의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.

```sql
SELECT book_id
     , DATE_FORMAT(published_date, '%Y-%m-%d') AS pd
FROM book
WHERE category = '인문'
    AND published_date BETWEEN '2021-01-01 00:00:00' AND '2021-12-31 23:59:59'
ORDER BY pd
;
```
