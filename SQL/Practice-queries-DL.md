### DataLemur Practice question

#### Find duplicate jobids

```sql
-- Step1: Job Count
With cte_job_count AS
(SELECT company_id,Count(company_id) AS job_count
FROM job_listings
GROUP BY company_id
)
-- Step2: to check where the Job_count>1
SELECT Count(DISTINCT(company_id)) AS duplicate_company
FROM cte_job_count
where job_count >1
```

#### Write a query to retrieve the top three cities that have the highest number of completed trade orders listed in descending order. Output the city name and the corresponding number of completed trade orders.

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

#### Assume you're given a table Twitter tweet data, write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket.

#### In other words, group the users by the number of tweets they posted in 2022 and count the number of users in each group.
```sql

WITH total_tweets AS 
(
  -- STEP1: --  to find the number of tweets posted by each user in 2022 by grouping the tweet records by user ID and counting the tweets.
  SELECT 
    user_id, 
    COUNT(tweet_id) AS tweet_count_per_user
  FROM tweets 
  WHERE tweet_date BETWEEN '2022-01-01' 
    AND '2022-12-31' 
  GROUP BY user_id
) 
-- Step2: we use the above CTE as temp table, then we use the tweet_count_per_user field as the tweet bucket and retrieve the number of users.
  
SELECT 
  tweet_count_per_user AS tweet_bucket, 
  COUNT(user_id) AS users_num 
FROM total_tweets 
GROUP BY tweet_count_per_user;

GROUP BY tweet_count_per_user;
```
