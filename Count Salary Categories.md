# Without Join
```sql
-- Write your PostgreSQL query statement below
SELECT category, COUNT(*)
FROM ( SELECT *,
CASE WHEN income < 20000 THEN 'Low Salary'
     WHEN income > 50000 THEN 'High Salary'
     ELSE 'Average Salary'
END AS category
FROM accounts) AS sub
GROUP BY category
```
The problem with above query is that if one of the categories is not there, instead of show 0, will not show the categories
# With Join
```sql
WITH CTE AS
(
    SELECT 'Low Salary' AS Category
    UNION ALL
    SELECT 'Average Salary'
    UNION ALL  
    SELECT 'High Salary'
)
SELECT 
    C.Category,
    COUNT(A.income) AS accounts_count
FROM CTE AS C
LEFT JOIN Accounts AS A
    ON C.Category = (CASE 
                        WHEN A.income < 20000 THEN 'Low Salary'
                        WHEN A.income >= 20000 AND A.income <= 50000 THEN 'Average Salary'
                        ELSE 'High Salary' 
                     END)
GROUP BY C.Category;
```
