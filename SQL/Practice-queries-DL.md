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
  -- STEP1: --  to find the number of tweets posted by each user in 2022 by grouping 
  -- the tweet records by user ID and counting the tweets.
  SELECT 
    user_id, 
    COUNT(tweet_id) AS tweet_count_per_user
  FROM tweets 
  WHERE tweet_date BETWEEN '2022-01-01' 
    AND '2022-12-31' 
  GROUP BY user_id
) 
-- Step2: we use the above CTE as temp table, then we use the tweet_count_per_user field 
-- as the tweet bucket and retrieve the number of users.
  
SELECT 
  tweet_count_per_user AS tweet_bucket, 
  COUNT(user_id) AS users_num 
FROM total_tweets 
GROUP BY tweet_count_per_user;
```
#### Query to get the hacker Id, hacker name - 
##### 1.respective hacker_id and name of hackers who achieved full scores for more than one challenge. ##### 2.Order your output in descending order by the total number of challenges in which the hacker earned a full score 
##### 3.If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

```sql
SELECT 
    hacker_id,
    hacker_name
FROM (
  -- Checking If the Hacker Achieved the Full Score
    SELECT 
        S.hacker_id AS hacker_id, 
        H.name AS hacker_name,
        CASE
            WHEN S.score = D.score THEN 1
            ELSE 0
        END AS Full_score
    FROM 
        Submissions S
    JOIN Challenges C ON S.challenge_id = C.challenge_id
    JOIN Difficulty D ON C.difficulty_level = D.difficulty_level
    JOIN Hackers H ON S.hacker_id = H.hacker_id
) T
-- Grouping by hacker_id and hacker_name ensures we count the full scores per hacker.
-- HAVING SUM(Full_score) > 1 filters out hackers who got a full score only once or never.
-- Only hackers who scored full marks in at least two different challenges remain.

GROUP BY hacker_id, hacker_name
HAVING SUM(Full_score) > 1

-- sort by the total number of full scores in descending order (most full scores first).
ORDER BY SUM(Full_score) DESC, hacker_id ASC;
``` 
#### challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

```sql

WITH ChallengeCount AS (
    SELECT C.hacker_id, H.name, COUNT(C.challenge_id) AS total_challenges
    FROM Challenges C
    JOIN Hackers H ON C.hacker_id = H.hacker_id
    GROUP BY C.hacker_id, H.name
)
SELECT hacker_id, name, total_challenges
FROM ChallengeCount
WHERE total_challenges = (SELECT MAX(total_challenges) FROM ChallengeCount)
   OR total_challenges IN (
       SELECT total_challenges FROM ChallengeCount 
       GROUP BY total_challenges 
       HAVING COUNT(hacker_id) = 1
   )
ORDER BY total_challenges DESC, hacker_id ASC;

```
