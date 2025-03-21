## Set-1

## Basic Level Queries**

1. **Select Specific Columns**
```sql
SELECT column1, column2 FROM table_name;
```
*Common Task:* Extracting required columns from a dataset.

---

2. **Filtering with WHERE Clause**
```sql
SELECT * FROM employees
WHERE department = 'Finance';
```
*Common Task:* Extract data based on conditions.

---

3. **Sorting Results (ORDER BY)**
```sql
SELECT name, salary 
FROM employees
ORDER BY salary DESC;
```
*Common Task:* Sorting data in ascending/descending order.

---

4. **LIMIT and OFFSET**
```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 5 OFFSET 10;
```
*Common Task:* Extracting top N rows or paginating results.

---

5. **Counting Rows**
```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```
*Common Task:* Finding the total number of rows.

---

6. **DISTINCT Values**
```sql
SELECT DISTINCT department
FROM employees;
```
*Common Task:* Getting unique values from a column.

---

##  Intermediate Level Queries**

7. **GROUP BY with Aggregates**
```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```
*Common Task:* Grouping data and applying aggregate functions.

---

8. **HAVING Clause Usage**
```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING employee_count > 10;
```
*Common Task:* Filtering grouped data.

---

9. **INNER JOIN to Combine Tables**
```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
```
*Common Task:* Joining multiple tables for consolidated data.

---

10. **LEFT JOIN with NULL Handling**
```sql
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id;
```
*Common Task:* Ensuring all records from one table are preserved.

---

11. **Self JOIN for Hierarchies**
```sql
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
JOIN employees e2
ON e1.manager_id = e2.employee_id;
```
*Common Task:* Handling hierarchical data.

---

12. **Subquery in SELECT**
```sql
SELECT name, 
       (SELECT AVG(salary) 
        FROM employees) AS avg_salary
FROM employees;
```
*Common Task:* Using subqueries for derived columns.

---

13. **Subquery in WHERE Clause**
```sql
SELECT name
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
*Common Task:* Filter rows based on subquery results.

---

14. **Find Duplicates**
```sql
SELECT name, COUNT(*)
FROM employees
GROUP BY name
HAVING COUNT(*) > 1;
```
*Common Task:* Identifying duplicate records.

---

15. **Updating Rows**
```sql
UPDATE employees
SET salary = salary * 1.1
WHERE department = 'Finance';
```
*Common Task:* Modifying specific rows.

---

16. **Delete Duplicate Rows Without ROWID**
```sql
DELETE FROM employees
WHERE employee_id NOT IN (
    SELECT MIN(employee_id)
    FROM employees
    GROUP BY name, department, salary
);
```
*Common Task:* Deleting duplicates while retaining one record.

---

## Advanced Level Queries**

17. **Window Functions (ROW_NUMBER, RANK, DENSE_RANK)**
```sql
SELECT name, department, salary,
       ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```
*Common Task:* Ranking and analyzing data by partitions.

---

18. **Finding Consecutive Absences**
```sql
SELECT employee_id, attendance_date
FROM (
    SELECT employee_id, attendance_date,
           LAG(attendance_date, 1) OVER (PARTITION BY employee_id ORDER BY attendance_date) AS prev_day,
           LAG(attendance_date, 2) OVER (PARTITION BY employee_id ORDER BY attendance_date) AS prev_two_days
    FROM attendance
    WHERE status = 'Absent'
) consecutive_absences
WHERE attendance_date = prev_day + INTERVAL 1 DAY
AND prev_day = prev_two_days + INTERVAL 1 DAY;
```
*#* Option-2

```sql
SELECT 
    employee_id, 
    attendance_date
FROM (
    SELECT 
        employee_id,
        attendance_date,
        DATEDIFF(attendance_date, LAG(attendance_date) OVER (PARTITION BY employee_id ORDER BY attendance_date)) AS diff
    FROM 
        attendance
    WHERE 
        status = 'Absent'
) consecutive_absences
WHERE 
    diff = 1;

```
*Common Task:* Identifying streaks or patterns.

---

19. **PIVOT in SQL**
```sql
SELECT department,
       SUM(CASE WHEN gender = 'Male' THEN salary ELSE 0 END) AS male_salary,
       SUM(CASE WHEN gender = 'Female' THEN salary ELSE 0 END) AS female_salary
FROM employees
GROUP BY department;
```
*Common Task:* Transforming rows into columns for reporting.

---

20. **Recursive CTE for Hierarchical Data**
```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT employee_id, name, manager_id
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.name, e.manager_id
    FROM employees e
    JOIN EmployeeHierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM EmployeeHierarchy;
```
*Common Task:* Handling organizational hierarchies.

---

21. **Top N Per Group Using RANK**
```sql
WITH RankedEmployees AS (
    SELECT name, department, salary,
           RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rnk
    FROM employees
)
SELECT name, department, salary
FROM RankedEmployees
WHERE rnk <= 3;
```
*Common Task:* Finding top N results per group.

---

22. **Deleting Duplicate Rows with CTE**
```sql
WITH CTE AS (
    SELECT name, 
           ROW_NUMBER() OVER(PARTITION BY name ORDER BY employee_id) AS rn
    FROM employees
)
DELETE FROM employees
WHERE employee_id IN (
    SELECT employee_id FROM CTE WHERE rn > 1
);
```

---

23. **Finding Gaps in Date Ranges**
```sql
SELECT a.end_date + INTERVAL 1 DAY AS gap_start,
       b.start_date - INTERVAL 1 DAY AS gap_end
FROM reservations a
JOIN reservations b
ON a.end_date < b.start_date
WHERE a.end_date + INTERVAL 1 DAY != b.start_date;

---

24. **JSON Data Extraction (PostgreSQL & MySQL)**
```sql
SELECT info->>'age' AS age,
       info->>'city' AS city
FROM users
WHERE info->>'age'::int > 30;
```

---

25. **Longest Consecutive Streak in Data**
```sql
SELECT employee_id, MIN(attendance_date) AS start_date, MAX(attendance_date) AS end_date
FROM (
    SELECT employee_id, attendance_date,
           attendance_date - INTERVAL ROW_NUMBER() OVER(PARTITION BY employee_id ORDER BY attendance_date) DAY AS grp
    FROM attendance
    WHERE status = 'Present'
) streaks
GROUP BY employee_id, grp;
```

---
