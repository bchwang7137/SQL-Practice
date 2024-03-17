# SqlWorldCup
Link: https://app.codility.com/programmers/trainings/6/sql_world_cup/

Each record in the table teams represents a single soccer team. Each record in the table matches represents a finished match between two teams. Teams (host_team, guest_team) are represented by their IDs in the teams table (team_id). No team plays a match against itself. You know the result of each match (that is, the number of goals scored by each team).

You would like to compute the total number of points each team has scored after all the matches described in the table. The scoring rules are as follows:

- If a team wins a match (scores strictly more goals than the other team), it receives three points.
- If a team draws a match (scores exactly the same number of goals as the opponent), it receives one point.
- If a team loses a match (scores fewer goals than the opponent), it receives no points.

Write an SQL query that returns a ranking of all teams (team_id) described in the table teams. For each team you should provide its name and the number of points it received after all described matches (num_points). The table should be ordered by num_points (in decreasing order). In case of a tie, order the rows by team_id (in increasing order).

```sql
SELECT t.team_id
     , t.team_name
     , COALESCE(SUM(CASE 
        WHEN t.team_id = m.host_team THEN 
        (
            CASE WHEN host_goals > guest_goals THEN 3
                 WHEN host_goals = guest_goals THEN 1
                 WHEN host_goals < guest_goals THEN 0
            END
        )
        WHEN t.team_id = m.guest_team THEN
        (
            CASE WHEN guest_goals > host_goals THEN 3
                 WHEN guest_goals = host_goals THEN 1
                 WHEN guest_goals < host_goals THEN 0
            END
        )
        END), 0) AS num_points
FROM teams AS t
    LEFT JOIN matches AS m ON t.team_id = m.host_team 
                           OR t.team_id = m.guest_team
GROUP BY t.team_id, t.team_name
ORDER BY num_points DESC, team_id
;
```