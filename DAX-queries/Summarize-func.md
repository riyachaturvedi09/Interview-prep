# SUMMARIZE FUNCTION IN DAX

##### Summarize function is used to create a summary Table based on the specified columns & aggregartions.

##### allows you to grp data by one or more columns and perform calculations on the other columns.


##### Syntax
```sh 
SUMMARIZE(
    table,
    [groupBy_columnName1],
    [groupBy_columnName2],
    ...,
    [name1], expression1,
    [name2], expression2,
    ...
)
```sh

#### Sales Value of the best Selling Month
<!-- sales table is not at the granuality level at which we want calculation, it has duplicate dates in the sales table -->

```sh
Best_Selling_daY_Sales = MAXX(Calender,[TotalSales])
```

