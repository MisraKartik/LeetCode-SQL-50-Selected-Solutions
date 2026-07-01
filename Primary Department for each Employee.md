```sql
SELECT employee_id, department_id
FROM (
    SELECT employee_id, department_id, primary_flag,
           COUNT(*) OVER(PARTITION BY employee_id) AS departs
    FROM employee
) sub
WHERE primary_flag = 'Y' OR departs = 1;
```
