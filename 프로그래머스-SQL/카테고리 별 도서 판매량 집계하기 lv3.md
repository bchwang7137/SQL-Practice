# 카테고리 별 도서 판매량 집계하기 lv3
[https://school.programmers.co.kr/learn/courses/30/lessons/144855](https://school.programmers.co.kr/learn/courses/30/lessons/144855)

`2022년 1월`의 카테고리 별 도서 판매량을 합산하고, 카테고리(`CATEGORY`), 총 판매량(`TOTAL_SALES`) 리스트를 출력하는 SQL문을 작성해주세요.

결과는 카테고리명을 기준으로 오름차순 정렬해주세요.

```sql
SELECT bk.category
     , SUM(bs.sales) AS total_sales
FROM book AS bk
    JOIN book_sales AS bs ON bk.book_id = bs.book_id
WHERE bs.sales_date BETWEEN '2022-01-01 00:00:00' AND '2022-01-31 23:59:59'
GROUP BY bk.category
ORDER BY bk.category
;
```
