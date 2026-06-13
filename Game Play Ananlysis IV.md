WITH first_login AS (
    SELECT
        player_id,
        MIN(event_date) AS first_date
    FROM Activity
    GROUP BY player_id
)
SELECT ROUND(
    AVG(
        CASE WHEN EXISTS (
            SELECT 1
            FROM Activity a
            WHERE a.player_id = f.player_id
              AND a.event_date = f.first_date + 1
        )
        THEN 1 ELSE 0 END
    )::numeric,
    2
) AS fraction
FROM first_login f;
