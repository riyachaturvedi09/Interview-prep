# RUNNING TOTAL FOR DATES

#### Monthly Running total - Works with Date-Number

```sql
Monthly_Running_total= 
Calculate(
    [TotalSales],
    Filter(
        ALL(Calender[Date]), calender[Date] <= MAX(calender[Date])
    )
)

```


#### Product Running total - Works with Date-Number
##### step1
```sql
Pro_running_total = 
-- Defining the rank of products
RANX(
    ALL(Products[Product_Name]),
    [TotalSales],,
    DESC,
    DENSE
)
,
```
##### step2
```sql
-- Calculate the running total for the current Rank where takes sum of the totalsales where rank is < current rank
Var Prod_rank = RANX(
    ALL(Products[Product_Name]),
    [TotalSales],,
    DESC,
    DENSE
)

VAR Runningtotal = Calculate(
    [TotalSales],
    filter (All(product[product_Name],
    Prod_Rank >= RANX(
        ALL(Product[productName]),
        [TotalSales],,
        DESC,
        DENSE 
            )
    ))
)
-- IF condition to ensure the running total calculates only for the sold products

RETURN RunningTotal;
    IF(
        [TotalSales] <> Blank(),
        RunningTotal
    )
```
