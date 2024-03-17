# 저자 별 카테고리 별 매출액 집계하기 lv4
[https://school.programmers.co.kr/learn/courses/30/lessons/144856](https://school.programmers.co.kr/learn/courses/30/lessons/144856)

`2022년 1월`의 도서 판매 데이터를 기준으로 저자 별, 카테고리 별 매출액(`TOTAL_SALES = 판매량 * 판매가`) 을 구하여, 저자 ID(`AUTHOR_ID`), 저자명(`AUTHOR_NAME`), 카테고리(`CATEGORY`), 매출액(`SALES`) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 저자 ID를 오름차순으로, 저자 ID가 같다면 카테고리를 내림차순 정렬해주세요.

```sql
SELECT au.author_id
     , au.author_name
     , bk.category
     , SUM(bk.price * bs.sales) AS total_sales
FROM book AS bk
    JOIN author AS au ON bk.author_id = au.author_id
    JOIN book_sales AS bs ON bk.book_id = bs.book_id
WHERE bs.sales_date BETWEEN '2022-01-01 00:00:00' AND '2022-01-31 23:59:59'
GROUP BY au.author_id, bk.category
ORDER BY au.author_id, bk.category DESC
;
```
