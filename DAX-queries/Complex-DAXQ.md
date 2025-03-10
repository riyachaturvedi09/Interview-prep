#Advance DAX Queries

### CONCATENATEX - 
#### To find out best selling products, their names, % of their contribution for each much

##### Step1- To find the top Selling product from each month
```sql
Best Selling products = TOPN (1, Products,[total Sales])
```

##### Step2- To find the top Selling product from each month - calculating total sales
```sql
Best Selling products = SUMX(TOPN (1, Products,[total Sales]),[TotalSales])
```

##### Step3- To find the 3 top Selling product from each month - calculating total sales with Names & Sales Value
```sql

Best Selling products = CONCATENATE( 
    SUMX(
        -- // checks whether the total sales value is NULL or not
        TOPN (3, Filter( Products,[total Sales] <> Null) 
        ),
        [Total Sales]
    ),
    -- // Expression for Concat
    product([ProdcutName]) & format([Total Sales]," | $0.0")  
    -- // parameter for space
    UNICHAR(10), 
    -- // Parameter to sort the sales value 
    [Total Sales],
    
    DESC
)

```
