Here’s a list of **25-30 most frequently asked SQL questions** for the **NAB (National Australia Bank) coding round for Data Analyst roles**, along with solutions.

---

###      **1. Retrieve Duplicate Records from a Table**

```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

---

###      **2. Find Consecutive Absences in Employee Attendance**

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

---

###      **3. Identify Orphan Records (No Matching Data in Another Table)**

```sql
SELECT a.*
FROM table_a a
LEFT JOIN table_b b
ON a.id = b.id
WHERE b.id IS NULL;
```

---

###      **4. Calculate Moving Average Using Window Functions**

```sql
SELECT order_id, order_date, 
       AVG(amount) OVER (PARTITION BY customer_id ORDER BY order_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg
FROM orders;
```

---

###      **5. Find Second Highest Salary**

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

---

###      **6. Identify Anomalies or Outliers**

```sql
SELECT order_id, amount
FROM orders
WHERE amount > (SELECT AVG(amount) + 2 * STDDEV(amount) FROM orders);
```

---

###      **7. Handle NULL Values Using COALESCE or ISNULL**

```sql
SELECT employee_id, COALESCE(department, 'Not Assigned') AS department_name
FROM employees;
```

---

###      **8. Get Employees with Highest Salary in Each Department**

```sql
SELECT department_id, employee_name, salary
FROM (
    SELECT department_id, employee_name, salary,
           RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = 1;
```

---

###      **9. Find Customers Who Have Placed More Than 5 Orders**

```sql
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) > 5;
```

---

###      **10. Pivot Query to Transform Rows into Columns**

```sql
SELECT customer_id, 
       SUM(CASE WHEN product_category = 'Electronics' THEN amount ELSE 0 END) AS electronics,
       SUM(CASE WHEN product_category = 'Clothing' THEN amount ELSE 0 END) AS clothing
FROM orders
GROUP BY customer_id;
```

---

###      **11. Get the First and Last Order Date per Customer**

```sql
SELECT customer_id,
       MIN(order_date) AS first_order_date,
       MAX(order_date) AS last_order_date
FROM orders
GROUP BY customer_id;
```

---

###      **12. Calculate Year-over-Year Sales Growth**

```sql
SELECT YEAR(order_date) AS year, 
       SUM(amount) AS total_sales,
       LAG(SUM(amount)) OVER (ORDER BY YEAR(order_date)) AS prev_year_sales,
       (SUM(amount) - LAG(SUM(amount)) OVER (ORDER BY YEAR(order_date))) / LAG(SUM(amount)) OVER (ORDER BY YEAR(order_date)) * 100 AS YoY_growth
FROM orders
GROUP BY YEAR(order_date);
```

---

###      **13. Identify Orders with Above Average Sales**

```sql
SELECT order_id, amount
FROM orders
WHERE amount > (SELECT AVG(amount) FROM orders);
```

---

###      **14. Delete Duplicates Without Using ROWID**

```sql
DELETE FROM employees
WHERE id NOT IN (
    SELECT MIN(id)
    FROM employees
    GROUP BY employee_name, department_id
);
```

---

###      **15. Get Percentage Contribution of Sales by Each Product**

```sql
SELECT product_id, 
       (SUM(amount) * 100.0 / (SELECT SUM(amount) FROM orders)) AS percentage_contribution
FROM orders
GROUP BY product_id;
```

---

###      **16. Identify Employees Who Have No Department Assigned**

```sql
SELECT employee_name
FROM employees
WHERE department_id IS NULL;
```

---

###      **17. Write a Query to Find Nth Highest Salary**

```sql
SELECT DISTINCT salary
FROM employees e1
WHERE N-1 = (SELECT COUNT(DISTINCT salary) FROM employees e2 WHERE e2.salary > e1.salary);
```

---

###      **18. Join 3 Tables Using INNER JOIN**

```sql
SELECT a.id, a.name, b.department_name, c.project_name
FROM employees a
INNER JOIN departments b ON a.department_id = b.department_id
INNER JOIN projects c ON a.project_id = c.project_id;
```

---

###      **19. Create a View to Store Employee Details with Salary > 50000**

```sql
CREATE VIEW high_salary_employees AS
SELECT employee_id, employee_name, salary
FROM employees
WHERE salary > 50000;
```

---

###      **20. Find Median Salary Using PERCENTILE_CONT**

```sql
SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY salary) AS median_salary
FROM employees;
```

---

###      **21. Get Records with Non-Numeric Values in a Column**

```sql
SELECT *
FROM orders
WHERE column_name NOT LIKE '%[0-9]%';
```

---

###      **22. Get List of Employees Whose Name Starts with ‘A’**

```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'A%';
```

---

###      **23. Identify Duplicate Records with All Column Matches**

```sql
SELECT employee_id, COUNT(*)
FROM employees
GROUP BY employee_id, employee_name, department_id
HAVING COUNT(*) > 1;
```

---

###      **24. SQL Query to Find Gaps in a Sequence**

```sql
SELECT id + 1 AS missing_id
FROM table_name t1
WHERE NOT EXISTS (
    SELECT 1 FROM table_name t2 WHERE t2.id = t1.id + 1
);
```

---

###      **25. Find Records Updated in the Last 7 Days**

```sql
SELECT *
FROM orders
WHERE DATEDIFF(CURDATE(), updated_date) <= 7;
```

---

###      **26. Query to Calculate Running Total in a Table**

```sql
SELECT order_id, order_date, 
       SUM(amount) OVER (PARTITION BY customer_id ORDER BY order_date) AS running_total
FROM orders;
```

---

###      **27. Find Employees Who Joined in the Last 3 Months**

```sql
SELECT employee_name, joining_date
FROM employees
WHERE joining_date >= DATEADD(MONTH, -3, GETDATE());
```

---

###      **28. Find Customers Who Have Not Placed Any Orders**

```sql
SELECT c.customer_id, c.customer_name
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

---

###      **29. Query to Check for Duplicate Emails**

```sql
SELECT email, COUNT(*) AS email_count
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

---

###      **30. Delete All Records from a Table Except the Latest Record for Each User**

```sql
DELETE FROM orders
WHERE order_id NOT IN (
    SELECT MAX(order_id)
    FROM orders
    GROUP BY customer_id
);
```

---
