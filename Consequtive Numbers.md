```sql
SELECT DISTINCT(num) AS ConsecutiveNums
FROM ( 
    SELECT num,
    LAG(num) OVER() AS lag1,
    LAG(num,2) OVER() AS lag2
    FROM logs ) AS lag
WHERE num = lag1 AND lag1 = lag2
```
