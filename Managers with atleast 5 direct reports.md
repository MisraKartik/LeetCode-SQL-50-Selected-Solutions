## Original Inefficient Query
```sql
-- Write your PostgreSQL query statement below
WITH manage AS
(
    SELECT *,
    COUNT(id) OVER(PARTITION BY managerId) AS direct
    FROM employee
),
manage_id AS
(
    SELECT DISTINCT managerId
    FROM manage
    WHERE direct > 4
)
SELECT name
FROM employee
WHERE id IN (SELECT * FROM manage_id)
```
## Final optimised query
Beats 98.7%
```sql
SELECT e.name
FROM Employee e
JOIN (
    SELECT managerId
    FROM Employee
    GROUP BY managerId
    HAVING COUNT(*) >= 5
) m ON e.id = m.managerId;
```
