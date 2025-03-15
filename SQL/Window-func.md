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
SELECT EMP_ID,
DENSE_RANK() OVER(PARTITION BY DEPART_ID ORDER BY EMP_ID DESC) AS rnk
FROM EMPLOYEE;

```

#### ROW_NUMBER() Function
##### assigns unique row_number to each of the row to the total of the row, it can be partitoned by groups

```sql
SELCT EMP_ID,salary
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
SELECT OPEN, CLOSE
--  THIS WILL EXTRACT THE NEXT CLOSING VALUE 
LEAD(CLOSE) OVER (ORDER BY DATE) AS NEXT_MONTH_CLOSE
-- THIS WILL EXTRACT THE NEXT CLOSING VALUE & SUBTRCATING IT WITH THE CLOSE GIVES THE DIFFERENCE
LEAD(CLOSE) OVER (ORDER BY DATE) - CLOSE AS DIFFERENCE 
FROM STOCKS
WHERE EXTRACT(YEAR FROM DATE) = 2023 AND TICKER = 'GOOG'
```
