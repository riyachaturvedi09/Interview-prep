# DAX Practice Questions

## Basic Power DAX Queries

### Sum of the Sales Amount
'''dax
TotalSales = SUM(Sales[Amount])
'''

### Average of the Sales Amount
'''dax
TotalSales = AVG(Sales[Amount])
'''

### MAX of the Sales Amount
'''dax
TotalSales = MAX(Sales[Amount])
'''

### MIN of the Sales Amount
'''dax
TotalSales = MIN(Sales[Amount])
'''

## DATETIME Functions
### Date and time functions are used to manipulate dates and time

#### Date Returns Datetime format
'''dax
DateValue = Date(20,10,1)
'''

#### Today Returns Datetime format
'''dax
CurrentDate = Today()
'''
#### DATEDIFF Returns Datetime format
'''dax
DateDiff_Value = DATEDIFF(Sales[orderdate],Sales[Salesdate],DAY)
'''

## FILTER Functions
### Returns a table as subset of the Table on which filter is applied

#### ALL - Removes all the filters from the table
'''dax
 AllSales = Calculate(Sum(Sales[Amount]),ALL(Sales)) 
'''

#### RELATED - Returns a table related to the 1:M side of the relationship, always applied on 1 side of the relationship
'''dax
 AllSales = RELATED(Product[Product_Category]) 
'''

## INFORMATION Functions
### Information functions return information about the data type, value, or reference

#### ISBLANK - checks the value is blank or not

'''dax
 ISBlankCheck = ISBLANK(Sales[Aount])
'''

#### ISERROR- checks if error returned or not

'''dax
 ISErrorCheck = ISERROR(Sales[Amount]/ Sales[Quantity])
'''

#### ISNUMBER- checks if value is number or not

'''dax
 ISNumberCheck = ISNUMBER(Sales[Amount])
'''


## RELATIONSHIP Functions
### These functions work with relationships between tables.

#### RELATEDTABLE- Returns 
'''dax
 ISNumberCheck = RELATEDTABLE(Sales)
'''

#### RELATEDVALUE- Returns 
'''dax
 ISNumberCheck = RELATEDVALUE(Sales[Product])
'''

## Time-Intelligence Functions
### Time intelligence functions work with time periods to create calculations over those periods

#### TOTALYTD/TOTALMTD/TOTALQMTD- Returns year-to-date/Month-to-date/Quarter-to-date calculations
'''dax
    TotalSales_YeartoDate = TOTALYTD(SUM(Sales[Amount],Sales[Orderdate])
    )   
'''

#### SAMEPERIODLASTYEAR: Returns a table that contains a column of dates shifted one year back.
'''dax
   LastYearSales = Calculate(SUM(Sales[Amount]),SAMEPERIODLASTYEAR(Sales[OrderDate]))
'''