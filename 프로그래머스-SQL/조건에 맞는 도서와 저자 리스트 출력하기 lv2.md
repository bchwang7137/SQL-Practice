# 조건에 맞는 도서와 저자 리스트 출력하기 lv2
[https://school.programmers.co.kr/learn/courses/30/lessons/144854](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

`'경제'` 카테고리에 속하는 도서들의 도서 ID(`BOOK_ID`), 저자명(`AUTHOR_NAME`), 출판일(`PUBLISHED_DATE`) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 출판일을 기준으로 오름차순 정렬해주세요.

`PUBLISHED_DATE`의 데이트 포맷이 예시와 동일해야 정답처리 됩니다.

```sql
SELECT b.book_id
     , a.author_name
     , DATE_FORMAT(b.published_date, '%Y-%m-%d') AS pd
FROM book AS b
    JOIN author AS a ON b.author_id = a.author_id
WHERE b.category = '경제'
ORDER BY pd
;
```
