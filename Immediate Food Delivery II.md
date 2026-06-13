```sql
WITH first_order AS 
( 
    SELECT customer_id, 
    CASE WHEN MIN(order_date) = MIN(customer_pref_delivery_date) THEN 1 
    ELSE 0 END AS col
    FROM delivery
    GROUP BY customer_id
)
SELECT ROUND(SUM(col) * 100.0 / COUNT(*),2) AS immediate_percentage
FROM first_order
```
