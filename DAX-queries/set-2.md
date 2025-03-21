# Freq-asked Set2 - NAB Codility/CodeLive assessments
---

###   **11. Calculate Moving Average for Last 7 Days**
**Question:**  
Write a DAX query to calculate the 7-day moving average of sales.

**Solution:**
```DAX
Moving Avg 7 Days = 
AVERAGEX(
    DATESINPERIOD(Sales[Date], MAX(Sales[Date]), -7, DAY),
    CALCULATE(SUM(Sales[SalesAmount]))
)
```
- **Explanation:** Uses `DATESINPERIOD` to define a rolling 7-day period and calculates the average.

---

###   **12. Count Number of Transactions Per Customer**
**Question:**  
Count the number of transactions made by each customer.

**Solution:**
```DAX
Transactions Per Customer = 
COUNTROWS(
    FILTER(Sales, Sales[CustomerID] = EARLIER(Sales[CustomerID]))
)
```
- **Explanation:** `EARLIER` returns the current row’s value to iterate over all rows and count matching records.

---

###   **13. Calculate Sales Growth Percentage for Current vs. Previous Month**
**Question:**  
Calculate percentage growth of sales between the current and previous month.

**Solution:**
```DAX
Sales Growth % = 
VAR CurrentMonthSales = 
    CALCULATE(SUM(Sales[SalesAmount]), DATESMTD(Sales[Date]))
VAR PreviousMonthSales = 
    CALCULATE(SUM(Sales[SalesAmount]), DATEADD(Sales[Date], -1, MONTH))
RETURN
    DIVIDE(CurrentMonthSales - PreviousMonthSales, PreviousMonthSales, 0)
```
- **Explanation:** Uses `DATESMTD` and `DATEADD` to calculate percentage growth.

---

###   **14. Identify Top 3 Products by Region**
**Question:**  
Return the top 3 products by region based on sales.

**Solution:**
```DAX
Top 3 Products by Region = 
TOPN(
    3,
    SUMMARIZE(
        Sales, 
        Sales[Region], 
        Sales[ProductName], 
        "TotalSales", SUM(Sales[SalesAmount])
    ),
    [TotalSales], DESC
)
```
- **Explanation:** `TOPN` returns the top 3 products for each region.

---

###   **15. Calculate Year-to-Date (YTD) Sales**
**Question:**  
Get the total sales for the year-to-date period.

**Solution:**
```DAX
YTD Sales = 
TOTALYTD(SUM(Sales[SalesAmount]), Sales[Date])
```
- **Explanation:** `TOTALYTD` aggregates sales from the start of the year to the current date.

---

###   **16. Calculate Retention Rate of Customers**
**Question:**  
Calculate the percentage of returning customers.

**Solution:**
```DAX
Retention Rate = 
DIVIDE(
    COUNTROWS(
        FILTER(Sales, Sales[IsReturningCustomer] = TRUE)
    ),
    COUNTROWS(Sales),
    0
)
```
- **Explanation:** Counts returning customers and divides by total customers.

---

###   **17. Calculate Sales for Current and Previous Quarter**
**Question:**  
Compare sales between current and previous quarters.

**Solution:**
```DAX
Sales Previous Quarter = 
CALCULATE(SUM(Sales[SalesAmount]), PREVIOUSQUARTER(Sales[Date]))

Sales Current Quarter = 
CALCULATE(SUM(Sales[SalesAmount]), DATESQTD(Sales[Date]))
```
- **Explanation:** `PREVIOUSQUARTER` and `DATESQTD` help compare quarterly sales.

---

###   **18. Calculate Sales Variance Between Two Products**
**Question:**  
Calculate the difference in sales between two products.

**Solution:**
```DAX
Product Sales Variance = 
VAR ProductA = 
    CALCULATE(SUM(Sales[SalesAmount]), Sales[ProductName] = "Product A")
VAR ProductB = 
    CALCULATE(SUM(Sales[SalesAmount]), Sales[ProductName] = "Product B")
RETURN
    ProductA - ProductB
```
- **Explanation:** Subtracts sales between two products.

---

###   **19. Calculate Count of New Customers Each Month**
**Question:**  
Get the number of new customers acquired each month.

**Solution:**
```DAX
New Customers Count = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(Sales, Sales[FirstPurchaseDate] = Sales[Date])
)
```
- **Explanation:** Counts unique customers who made their first purchase.

---

###   **20. Identify Highest Revenue-Generating Month**
**Question:**  
Return the month with the highest revenue.

**Solution:**
```DAX
Highest Revenue Month = 
TOPN(
    1,
    SUMMARIZE(
        Sales, 
        Sales[Month], 
        "TotalRevenue", SUM(Sales[SalesAmount])
    ),
    [TotalRevenue], DESC
)
```
- **Explanation:** Uses `TOPN` to get the month with the highest revenue.

---

###   **21. Count Customers Who Purchased Multiple Products**
**Question:**  
Count the customers who bought more than one product.

**Solution:**
```DAX
Multiple Product Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        VALUES(Sales[CustomerID]),
        CALCULATE(DISTINCTCOUNT(Sales[ProductID])) > 1
    )
)
```
- **Explanation:** Counts distinct customers who purchased more than one product.

---

###   **22. Calculate Time Difference Between Two Events**
**Question:**  
Calculate the time difference in hours between two datetime fields.

**Solution:**
```DAX
Time Difference in Hours = 
DATEDIFF(Sales[StartTime], Sales[EndTime], HOUR)
```
- **Explanation:** `DATEDIFF` calculates the difference between two datetime fields.

---

###   **23. Calculate Conversion Rate of Leads to Customers**
**Question:**  
Calculate the conversion rate between leads and customers.

**Solution:**
```DAX
Conversion Rate = 
DIVIDE(
    DISTINCTCOUNT(Sales[CustomerID]),
    DISTINCTCOUNT(Leads[LeadID]),
    0
)
```
- **Explanation:** Divides distinct customer count by lead count.

---

###   **24. Identify Inactive Customers for Last 90 Days**
**Question:**  
Identify customers who have not made a purchase in the last 90 days.

**Solution:**
```DAX
Inactive Customers = 
FILTER(
    Customers, 
    NOT(ISBLANK(
        CALCULATE(
            MAX(Sales[Date]), 
            DATESINPERIOD(Sales[Date], TODAY(), -90, DAY)
        )
    ))
)
```
- **Explanation:** Filters customers with no activity in the last 90 days.

---

###   **25. Calculate Sales Contribution for Each Region**
**Question:**  
Get the percentage of sales from each region.

**Solution:**
```DAX
Sales Contribution by Region = 
DIVIDE(
    SUM(Sales[SalesAmount]),
    CALCULATE(SUM(Sales[SalesAmount]), ALL(Sales[Region])),
    0
)
```
- **Explanation:** Calculates the contribution of each region to total sales.

---
