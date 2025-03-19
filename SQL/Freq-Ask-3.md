## Frequently Asked Question but Alternative Approach
---

## 1. Identify Orphan Records (Without Matching Data)     
   Scenario:    Find records in `orders` table that do not have a matching `customer_id` in the `customers` table.

```sql
SELECT o.order_id, o.customer_id, o.order_date
FROM orders o
LEFT JOIN customers c
ON o.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

     Explanation:   
- `LEFT JOIN` returns all records from the `orders` table.
- `WHERE c.customer_id IS NULL` filters out records that do not have a match in the `customers` table, identifying orphan records.

---

##  2. Calculate Moving Averages Using Window Functions     
   Scenario:    Calculate a 3-day moving average of `sales_amount` from the `sales` table.

```sql
SELECT sale_date, 
       product_id,
       sales_amount,
       ROUND(AVG(sales_amount) OVER(PARTITION BY product_id ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW), 2) AS moving_avg
FROM sales;
```

     Explanation:   
- `PARTITION BY product_id` ensures the moving average is calculated per product.
- `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` defines the window size (last 3 days including the current row).
- `AVG(sales_amount)` calculates the average within that window.

---

## 3. Identify Anomalies or Outliers
   Scenario:    Identify records in `sales` where `sales_amount` is more than 1.5 times the standard deviation above the average for each product.

```sql
WITH SalesStats AS (
    SELECT product_id,
           AVG(sales_amount) AS avg_sales,
           STDDEV(sales_amount) AS std_dev
    FROM sales
    GROUP BY product_id
)
SELECT s.sale_date, s.product_id, s.sales_amount
FROM sales s
JOIN SalesStats ss
ON s.product_id = ss.product_id
WHERE s.sales_amount > (ss.avg_sales + 1.5 * ss.std_dev);
```

     Explanation:   
- `WITH SalesStats` calculates the average and standard deviation for each `product_id`.
- `WHERE s.sales_amount > (ss.avg_sales + 1.5 * ss.std_dev)` filters out potential outliers.

---

##  4. Handle NULL Values Using COALESCE or ISNULL     
### (a) Using `COALESCE`     
   Scenario:    Replace `NULL` in the `address` column of `customers` with 'Not Provided'.

```sql
SELECT customer_id,
       COALESCE(address, 'Not Provided') AS address
FROM customers;
```

     Explanation:   
- `COALESCE(address, 'Not Provided')` returns the first non-null value, replacing `NULL` with 'Not Provided'.

---

###  (b) Using `ISNULL` (SQL Server Only)
```sql
SELECT customer_id,
       ISNULL(address, 'Not Provided') AS address
FROM customers;
```

     Explanation:   
- `ISNULL` works similarly to `COALESCE` but only takes two arguments.

---

###  Handle Multiple NULL Columns with COALESCE   
```sql
SELECT customer_id,
       COALESCE(email, phone_number, 'Contact Not Available') AS contact_info
FROM customers;
```
     Explanation:   
- Returns the first non-null value from `email` or `phone_number`, defaulting to 'Contact Not Available'.

---
