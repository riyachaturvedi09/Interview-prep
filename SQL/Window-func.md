### Window Functions - RANK,DENSE_RANK(),LEAD,LAG,ROW_NUMBER()

#### Ranking Window Functions -

##### The RANK() function assigns ranks to rows within a partition,
##### with the same rank given to rows with identical values. If two rows share the same rank, the next rank is skipped

```sql
SELECT EMP_ID,
RANK() OVER(PARTITION BY DEPART_ID ORDER BY EMP_ID DESC) AS rnk
FROM EMPLOYEE;
```
#### DENSE_RANK() Window Functions 
##### DENSE_RANK() functin assign ranks to the rows within a partition
##### with the same rank given to rows with identical values, If two rows share the same rank, this function does not skips the next rank like RANK()

```sql
SELECT EMP_ID,SALARY,
DENSE_RANK() OVER(PARTITION BY DEPART_ID ORDER BY EMP_ID DESC) AS rnk
FROM EMPLOYEE;

```

#### ROW_NUMBER() Function
##### assigns unique row_number to each of the row to the total of the row, it can be partitoned by groups

```sql
SELCT EMP_ID,salary,
ROW_NUMBER() OVER(partition by depart_if order by EMP_ID) as rn
from employee;
```


#### LAG() & LEAD() Function
##### lag & Lead both are time-series window function- used for access the data coming before or after the current row


#### LEAD() Function
#####
```sh 
date	          ticker    open	 high	low	    close
01/01/2023 00:00:00	GOOG	89.83	101.58	85.57	99.87
02/01/2023 00:00:00	GOOG	99.74	108.82	88.86	90.30
03/01/2023 00:00:00	GOOG	90.16	107.51	89.77	104.00
04/01/2023 00:00:00	GOOG	102.67	109.63	102.38	108.22
05/01/2023 00:00:00	GOOG	107.72	127.05	104.50	123.37
```
<!-- from the above table calculate the difference in closing prices between consecutive months of the year 2023 for the stock with ticker 'GOOG'. -->
```sql
SELECT OPEN, CLOSE,
--  THIS WILL EXTRACT THE NEXT CLOSING VALUE 
LEAD(CLOSE) OVER (ORDER BY DATE) AS NEXT_MONTH_CLOSE,
-- THIS WILL EXTRACT THE NEXT CLOSING VALUE & SUBTRCATING IT WITH THE CLOSE GIVES THE DIFFERENCE
LEAD(CLOSE) OVER (ORDER BY DATE) - CLOSE AS DIFFERENCE 
FROM STOCKS
WHERE EXTRACT(YEAR FROM DATE) = 2023 AND TICKER = 'GOOG'
```

#### Analyzing Stocks Data with Row Gaps - 
<!-- calculate the difference between the current month's closing price and the closing price from 3 months ago -->

```sql
SELECT OPEN, CLOSE,
-- EXTRACT THE CLOSING PRICE 3 MONTH AGO
LAG(CLOSE,3) OVER(ORDER BY DATE) AS CLOSE_THREE_MONTH_AGO, 
CLOSE - LAG(CLOSE,3) OVER(ORDER BY DATE) AS DIFFERENCE
FROM STOCKS
WHERE EXTRACT(YEAR FROM DATE)= 2023 AND TICKER = 'GOOG';
```

## Real-Life Scenarios with LEAD() and LAG()

### Retail Management: Forecasting Sales
Scenario: Forecast inventory requirements by analyzing upcoming sales trends in order to adjust stock levels accordingly.
```sh
sales_date	product_id	sales_quantity	next_day_sales
2023-08-01	A001	        100	                 75
2023-08-02	A001	        75	                 50
2023-08-03	A001	        50	                 60
2023-08-04	A001	        60	                 80
2023-08-05	A001	        80	                 70
```

##### Write a query to calculate the year-on-year growth rate for the total spend of each product, grouping the results by product ID.

<!-- The output should include the year in ascending order, product ID, current year's spend, previous year's spend and year-on-year growth percentage, rounded to 2 decimal places. -->

```sql
With CTE_YOY AS(
    -- extracts year from trascation date
Select Extract(Year from transaction_date) AS year, product_id, 
spend as current_year_spend,
-- find the previous transaction spend using LAG() by grouping it by the product_id
LAG(spend) OVER(partition by product_id order by transaction_date) AS Previous_year_spend
FROM user_transactions 
)
-- calculate YOY Rate- [(current-previous)/previous ]*100
SELECT year,product_id, current_Year_spend, previous_year_spend,
Round(((current_year_spend - previous_year_spend) / previous_year_spend)*100,2) AS YOY_Rate
From CTE_YOY

```

##### Write a query to find the maximum number of prime and non-prime batches that can be stored in the 500,000 square feet warehouse based on the following criteria:
##### Prioritize stocking prime batches
##### After accommodating prime items, allocate any remaining space to non-prime batches
<!-- 1.
products must be stocked in batches, so we want to find the largest available quantity of prime batches, 
2.  then the largest available quantity of non-prime batches
3. Non-prime items must always be available in stock to meet customer demand, so the non-prime item count should never be zero.
4.Item count should be whole numbers (integers). 
-->

```sql
--  This CTE (stats) retrieves aggregated data from the inventory table.
-- It groups data by item_type and calculates:
-- sqft: Total square footage occupied by each item_type.
-- items: The total count of items for each item_type.
-- The order by item_type desc sorts item_type in descending order.

with stats as (
  select
    item_type,
    sum(square_footage) as sqft,
    count(*) as items
  from inventory
  group by item_type
  order by item_type desc
)

It calculates the number of items that can fit within a 500,000 square-foot constraint.
prime_eligible items are allocated space first.
not_prime items get the remaining space based on the MOD() function

select
  item_type,
  case item_type
--   if prime_eligible then simply calculate the space
    when 'prime_eligible' then items * floor(500000 / sqft) 
    --  if not-prime then calculate the space using MOD(), MOD gives the remaining space 
    when 'not_prime' then items * floor(mod(500000, lag(sqft) over ()) / sqft)
  end as item_count
from stats

```

####  you're tasked with finding the candidates best suited for an open Data Science job. You want to find candidates who are proficient in Python, Tableau, and PostgreSQL.Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.

```sql
SELECT DISTINCT(candidate_id) FROM candidates where skill = 'Python'
INTERSECT
SELECT DISTINCT(candidate_id) FROM candidates where skill = 'Tableau'
INTERSECT
SELECT DISTINCT(candidate_id) FROM candidates where skill = 'PostgreSQL'

```