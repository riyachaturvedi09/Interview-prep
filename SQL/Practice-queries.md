### DataLemur Practice question

##### Find duplicate jobids

```sql
With cte_job_count AS
(SELECT company_id,Count(company_id) AS job_count
FROM job_listings
GROUP BY company_id
)

SELECT Count(DISTINCT(company_id)) AS duplicate_company
FROM cte_job_count
where job_count >1
```

##### Write a query to retrieve the top three cities that have the highest number of completed trade orders listed in descending order. Output the city name and the corresponding number of completed trade orders.

```sql
-- get the user city & order_id from trade table & users table where the trade status is "Completed"
SELECT 
  users.city, 
  COUNT(trades.order_id) AS total_orders 
FROM trades 
INNER JOIN users 
  ON trades.user_id = users.user_id 
WHERE trades.status = 'Completed' 
-- grouped by cities & sort total order in Descending order & pull top 3 orders
GROUP BY users.city 
ORDER BY total_orders DESC
LIMIT 3;
```