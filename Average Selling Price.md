# Wrong approach
```sql
SELECT product_id, 
COALESCE( ROUND( SUM(price * units)*1.0/SUM(units),2 ),0 ) AS average_price
FROM prices LEFT JOIN unitssold USING(product_id)
WHERE purchase_date BETWEEN start_date AND end_date
GROUP BY product_id
```
 <img width="870" height="209" alt="Screenshot 2026-06-09 at 2 16 12 PM" src="https://github.com/user-attachments/assets/f611c8c0-8e84-4cde-8a23-5ef813924ddb" />

# Correct Approach
```sql
SELECT
    p.product_id,
    COALESCE(
        ROUND(SUM(p.price * u.units) * 1.0 / SUM(u.units), 2),
        0
    ) AS average_price
FROM Prices p
LEFT JOIN Unitssold u
    ON p.product_id = u.product_id
   AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```
<img width="577" height="160" alt="Screenshot 2026-06-09 at 2 17 46 PM" src="https://github.com/user-attachments/assets/0f4e4a4b-64b5-4c1c-9365-08953d60c0eb" />
