# sql Practice Questions

## Basic Power sql Queries

### Sum of the sales Amount
```sql
TotalSales = SUM(Sales[Amount])
```

### Average of the Sales Amount
```sql
TotalSales = AVG(Sales[Amount])
```

### MAX of the Sales Amount.
```sql
TotalSales = MAX(Sales[Amount])
```

### MIN of the Sales Amount
```sql
TotalSales = MIN(Sales[Amount])
```

## DATETIME Functions
### Date and time functions are used to manipulate dates and time

#### Date Returns Datetime format
```sql
DateValue = Date(20,10,1)
```

#### Today Returns Datetime format
```sql
CurrentDate = Today()
```
#### DATEDIFF Returns Datetime format
```sql
DateDiff_Value = DATEDIFF(Sales[orderdate],Sales[Salesdate],DAY)
```

## FILTER Functions
### Returns a table as subset of the Table on which filter is applied

#### ALL - Removes all the filters from the table
```sql
 AllSales = Calculate(Sum(Sales[Amount]),ALL(Sales)) 
```

#### RELATED - Returns a table related to the 1:M side of the relationsqlip, always applied on 1 side of the relationsqlip
```sql
 AllSales = RELATED(Product[Product_Category]) 
```

## INFORMATION Functions
### Information functions return information about the data type, value, or reference

#### ISBLANK - checks the value is blank or not

```sql
 ISBlankCheck = ISBLANK(Sales[Aount])
```

#### ISERROR- checks if error returned or not

```sql
 ISErrorCheck = ISERROR(Sales[Amount]/ Sales[Quantity])
```

#### ISNUMBER- checks if value is number or not

```sql
 ISNumberCheck = ISNUMBER(Sales[Amount])
```


## RELATIONsqlIP Functions
### These functions work with relationsqlips between tables.

#### RELATEDTABLE- Returns 
```sql
 ISNumberCheck = RELATEDTABLE(Sales)
```

#### RELATEDVALUE- Returns 
```sql
 ISNumberCheck = RELATEDVALUE(Sales[Product])
```

## Time-Intelligence Functions
### Time intelligence functions work with time periods to create calculations over those periods

#### TOTALYTD/TOTALMTD/TOTALQMTD- Returns year-to-date/Month-to-date/Quarter-to-date calculations
```sql
    TotalSales_YeartoDate = TOTALYTD(SUM(Sales[Amount],Sales[Orderdate])
    )   
```

#### SAMEPERIODLASTYEAR: Returns a table that contains a column of dates sqlifted one year back.
```sql
   LastYearSales = Calculate(SUM(Sales[Amount]),SAMEPERIODLASTYEAR(Sales[OrderDate]))
```

