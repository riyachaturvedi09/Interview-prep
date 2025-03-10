#Advance DAX Queries

### CONCATENATEX - 
#### To find out best selling products, their names, % of their contribution for each much

##### Step1- To find the top Selling product from each month
```sql
-- // fetchs top 3 product from the product table
Best Selling products = TOPN (1, Products)
```

##### Step2- To find the top Selling product from each month - calculating total sales
```sql
--  // fetchs top 3 product from the product table & calculate the totalSales
Best Selling products = SUMX(TOPN (3, Products,[total Sales]),[TotalSales])
```

##### Step3- To find the 3 top Selling product from each month - calculating total sales with Names & Sales Value
```sql

Best Selling products = CONCATENATEX( 
    SUMX(
        -- // checks whether the total sales value is NULL or not
        TOPN (3, Filter( Products,[total Sales] <> Null) 
        ),
        [Total Sales]
    ),
    -- // Expression for Concat
    product([ProdcutName]) & format([Total Sales]," | $0.0")  
    -- // parameter for Enter ( NextLine)
    UNICHAR(10), 
    -- // Parameter to sort the sales value 
    [Total Sales],

    DESC
)

```
##### Step4- To find the 3 top Selling product from each month - calculating total sales with Names & Sales Value & also want to see the contribution in the current month's sales

Best Selling products = 
<!-- variable to hold the totalsale- reference to calculate the %contribution -->
VAR totSale = [Total_sales] 
RETURN

CONCATENATEX(
    SUMX( 
        TOPN (1,
            FILTER(
                PRODCUCTS,
                [total_sales] <> Null
                )
              ),
        [total_sales]
        )
<!-- //to get the %contribution we have divided the [TOTAL_SALES] of the product with the Overall Sales - held in 'totsale' variable -->
        product[product_name] & FORMAT([total_sales], "| $0.0") & FORMAT(DIVIDE([total_sales],TotSale),"| 0%")
 <!-- -- // parameter for Enter ( NextLine) -->
        UNICHAR(10),
        [total_Sales],
        DESC
    )





