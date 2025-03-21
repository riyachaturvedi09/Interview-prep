# Set-4 - NAB
---

###    **Basic to Intermediate Level**

1. **Find Duplicate Records in a Table**
```sql
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

2. **Retrieve the Second Highest Salary**
```sql
SELECT MAX(salary) AS second_highest_salary
FROM employee
WHERE salary < (SELECT MAX(salary) FROM employee);
```

3. **Identify Orphan Records**
```sql
SELECT c.customer_id
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

4. **Calculate Total Sales by Region**
```sql
SELECT region, SUM(sales) AS total_sales
FROM sales_data
GROUP BY region;
```

5. **Identify Consecutive Absences for Employees**
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

###    **Intermediate to Advanced Level**

6. **Find the Moving Average of Sales**
```sql
SELECT order_date, 
       AVG(sales) OVER (ORDER BY order_date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AS moving_avg
FROM sales;
```

7. **Identify Customers Who Placed Multiple Orders in a Day**
```sql
SELECT customer_id, order_date, COUNT(order_id) AS order_count
FROM orders
GROUP BY customer_id, order_date
HAVING COUNT(order_id) > 1;
```

8. **Get the Top N Records from Each Category**
```sql
SELECT product_category, product_name, revenue
FROM (
    SELECT product_category, product_name, revenue,
           RANK() OVER (PARTITION BY product_category ORDER BY revenue DESC) AS rank_num
    FROM products
) ranked
WHERE rank_num <= 3;
```

9. **Find Consecutive Login Streaks**
```sql
SELECT user_id, login_date
FROM (
    SELECT user_id, login_date,
           DATEDIFF(login_date, LAG(login_date) OVER (PARTITION BY user_id ORDER BY login_date)) AS diff
    FROM logins
) login_streak
WHERE diff = 1;
```

10. **Calculate Running Total**
```sql
SELECT order_date, 
       SUM(sales_amount) OVER (ORDER BY order_date) AS running_total
FROM orders;
```

---

###    **Complex Queries**

11. **Identify Customers Who Made Purchases in Consecutive Months**
```sql
WITH purchase_data AS (
    SELECT customer_id, EXTRACT(YEAR FROM purchase_date) AS purchase_year, EXTRACT(MONTH FROM purchase_date) AS purchase_month
    FROM orders
)
SELECT customer_id
FROM (
    SELECT customer_id, purchase_year, purchase_month,
           LAG(purchase_month) OVER (PARTITION BY customer_id ORDER BY purchase_year, purchase_month) AS prev_month
    FROM purchase_data
) consecutive_purchases
WHERE purchase_month = prev_month + 1;
```

12. **Delete Duplicate Rows Without Using ROWID**
```sql
DELETE FROM employees
WHERE employee_id IN (
    SELECT employee_id
    FROM (
        SELECT employee_id,
               ROW_NUMBER() OVER (PARTITION BY name, department ORDER BY employee_id) AS rn
        FROM employees
    ) duplicates
    WHERE rn > 1
);
```

13. **Pivot Sales Data by Month**
```sql
SELECT *
FROM (
    SELECT product_name, sales_amount, EXTRACT(MONTH FROM sales_date) AS sales_month
    FROM sales
) source_table
PIVOT (
    SUM(sales_amount)
    FOR sales_month IN (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12)
) AS pivot_table;
```

14. **Find Consecutive Duplicate Values in a Column**
```sql
SELECT user_id, event_date, event_type
FROM (
    SELECT user_id, event_date, event_type,
           LAG(event_type) OVER (PARTITION BY user_id ORDER BY event_date) AS prev_event
    FROM user_activity
) consecutive_events
WHERE event_type = prev_event;
```

15. **Calculate Year-over-Year Growth**
```sql
SELECT year, 
       revenue,
       LAG(revenue) OVER (ORDER BY year) AS prev_year_revenue,
       (revenue - LAG(revenue) OVER (ORDER BY year)) / LAG(revenue) OVER (ORDER BY year) * 100 AS yoy_growth
FROM sales;
```

---

###    **Window Functions & Aggregations**

16. **Rank Products Based on Revenue**
```sql
SELECT product_name, revenue,
       RANK() OVER (ORDER BY revenue DESC) AS rank_num
FROM sales;
```

17. **Calculate Percentage of Total Sales by Region**
```sql
SELECT region, SUM(sales) AS total_sales,
       SUM(sales) * 100.0 / SUM(SUM(sales)) OVER () AS pct_total_sales
FROM sales_data
GROUP BY region;
```

18. **Find Employees with No Direct Reports**
```sql
SELECT e.employee_id, e.employee_name
FROM employees e
LEFT JOIN employees m ON e.employee_id = m.manager_id
WHERE m.employee_id IS NULL;
```

19. **Identify First and Last Purchase Date for Each Customer**
```sql
SELECT customer_id,
       MIN(order_date) AS first_purchase,
       MAX(order_date) AS last_purchase
FROM orders
GROUP BY customer_id;
```

20. **Retrieve Order Count Using CTE**
```sql
WITH order_cte AS (
    SELECT customer_id, COUNT(order_id) AS order_count
    FROM orders
    GROUP BY customer_id
)
SELECT customer_id, order_count
FROM order_cte
WHERE order_count > 5;
```

---

###    **Advanced Joins & Subqueries**

21. **Self Join to Get Manager-Employee Relationships**
```sql
SELECT e1.employee_name AS employee, e2.employee_name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

22. **Find the Latest Order for Each Customer**
```sql
SELECT customer_id, order_date, order_id
FROM (
    SELECT customer_id, order_date, order_id,
           ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) AS rn
    FROM orders
) latest_orders
WHERE rn = 1;
```

23. **Join Three Tables with Common Column**
```sql
SELECT c.customer_name, o.order_id, s.status
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN shippings s ON o.order_id = s.order_id;
```

24. **Find Uncommon Records Between Two Tables**
```sql
SELECT name FROM table1
EXCEPT
SELECT name FROM table2;
```

25. **Retrieve Employees Whose Names Start with 'A'**
```sql
SELECT employee_name
FROM employees
WHERE employee_name LIKE 'A%';
```

---

###    **Bonus: Optimization & Performance**

26. **Identify Slow Running Queries Using Indexes**
- Analyze `EXPLAIN` plan and optimize queries by:
  - Adding indexes on `JOIN` and `WHERE` clauses.
  - Avoiding unnecessary `ORDER BY` and `DISTINCT`.
  - Using `LIMIT` to restrict data.

27. **Delete Duplicate Records Using CTE**
```sql
WITH duplicates AS (
    SELECT row_number() OVER (PARTITION BY column_name ORDER BY id) AS rn
    FROM table_name
)
DELETE FROM duplicates WHERE rn > 1;
```

---