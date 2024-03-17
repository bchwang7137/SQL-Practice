# Days At Number One - Hard
[https://platform.stratascratch.com/coding/10173-days-at-number-one?code_type=3](https://platform.stratascratch.com/coding/10173-days-at-number-one?code_type=3)

Find the number of days a US track has stayed in the 1st position for both the US and worldwide rankings. Output the track name and the number of days in the 1st position. Order your output alphabetically by track name.

If the region 'US' appears in dataset, it should be included in the worldwide ranking.

```sql
-- 'official' solution on StrataScratch Youtube seems a bit overkill
-- this simpler approach seems to provide the same expected output

-- note that the us rankings table appears to only contain tracks that were at position 1
-- still specified a u.position filter to make the query robust against possible test cases

SELECT u.trackname
     , COUNT(*) AS cnt_days_at_1st
FROM spotify_daily_rankings_2017_us AS u
    JOIN spotify_worldwide_daily_song_ranking AS w ON u.url = w.url AND u.date = w.date
WHERE u.position = 1 AND w.position = 1
GROUP BY u.trackname
ORDER BY u.trackname
;
```
