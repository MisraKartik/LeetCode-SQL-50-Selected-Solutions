```sql
WITH LatestDates AS (
    SELECT 
        product_id,
        MAX(change_date) AS max_date
    FROM products
    WHERE change_date <= '2019-08-16'
    GROUP BY product_id
),
AllProducts AS (
    SELECT DISTINCT product_id FROM products
)
SELECT 
    ap.product_id,
    COALESCE(pr.new_price, 10) AS price
FROM AllProducts ap
LEFT JOIN LatestDates ld ON ap.product_id = ld.product_id
LEFT JOIN products pr ON ld.product_id = pr.product_id AND ld.max_date = pr.change_date;
```
