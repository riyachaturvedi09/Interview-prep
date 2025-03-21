# Freq-asked Set1 - NAB Codility/CodeLive assessments

---

###   **1. Calculate Year-over-Year (YoY) Growth**
**Question:**  
Write a DAX formula to calculate YoY growth in sales.

**Solution:**
```DAX
YoY Growth = 
VAR CurrentYearSales = 
    CALCULATE(SUM(Sales[SalesAmount]), SAMEPERIODLASTYEAR(Sales[Date]))
VAR PreviousYearSales = 
    CALCULATE(SUM(Sales[SalesAmount]), SAMEPERIODLASTYEAR(Sales[Date]))
RETURN
    IF(
        ISBLANK(PreviousYearSales), 
        BLANK(),
        DIVIDE(CurrentYearSales - PreviousYearSales, PreviousYearSales)
    )
```
- **Explanation:** Compares sales of the current year with the previous year to calculate growth.

---

###   **2. Calculate Cumulative Sales (Running Total)**
**Question:**  
Create a running total of sales amount by date.

**Solution:**
```DAX
Cumulative Sales = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    FILTER(
        ALL(Sales[Date]),
        Sales[Date] <= MAX(Sales[Date])
    )
)
```
- **Explanation:** Accumulates sales over time using `FILTER` and `ALL` to ensure all rows are considered.

---

###   **3. Calculate Percentage of Total Sales**
**Question:**  
Write a DAX query to calculate the percentage contribution of each product to total sales.

**Solution:**
```DAX
Percentage of Total = 
DIVIDE(
    SUM(Sales[SalesAmount]), 
    CALCULATE(SUM(Sales[SalesAmount]), ALL(Sales)),
    0
)
```
- **Explanation:** Divides individual product sales by total sales to get percentage contribution.

---

###   **4. Calculate Sales for Last 3 Months**
**Question:**  
Get the total sales for the last 3 months dynamically.

**Solution:**
```DAX
Sales Last 3 Months = 
CALCULATE(
    SUM(Sales[SalesAmount]),
    DATESINPERIOD(Sales[Date], MAX(Sales[Date]), -3, MONTH)
)
```
- **Explanation:** `DATESINPERIOD` helps calculate sales within the last 3 months.

---

###   **5. Identify Top N Customers by Sales**
**Question:**  
Get the top 5 customers based on sales amount.

**Solution:**
```DAX
Top 5 Customers = 
TOPN(
    5,
    SUMMARIZE(
        Sales, 
        Customer[CustomerName],
        "TotalSales", SUM(Sales[SalesAmount])
    ),
    [TotalSales], DESC
)
```
- **Explanation:** `TOPN` returns the top 5 customers sorted by total sales.

---

###   **6. Calculate Average Sales per Customer**
**Question:**  
Calculate the average sales per customer.

**Solution:**
```DAX
Avg Sales Per Customer = 
DIVIDE(
    SUM(Sales[SalesAmount]),
    DISTINCTCOUNT(Sales[CustomerID]),
    0
)
```
- **Explanation:** Divides total sales by distinct customer count to get the average.

---

###   **7. Count Distinct Products Sold**
**Question:**  
Count the number of unique products sold.

**Solution:**
```DAX
Distinct Products Sold = 
DISTINCTCOUNT(Sales[ProductID])
```
- **Explanation:** Counts unique `ProductID` in the sales table.

---

###   **8. Calculate Sales Variance Between Two Periods**
**Question:**  
Write a DAX query to calculate the variance in sales between the current and previous months.

**Solution:**
```DAX
Sales Variance = 
VAR CurrentMonthSales = 
    CALCULATE(SUM(Sales[SalesAmount]), DATESMTD(Sales[Date]))
VAR PreviousMonthSales = 
    CALCULATE(SUM(Sales[SalesAmount]), DATEADD(Sales[Date], -1, MONTH))
RETURN
    CurrentMonthSales - PreviousMonthSales
```
- **Explanation:** Uses `DATESMTD` and `DATEADD` to calculate monthly variance.

---

###   **9. Filter Data Based on Condition**
**Question:**  
Filter sales where the amount is greater than 50,000.

**Solution:**
```DAX
High Sales = 
FILTER(Sales, Sales[SalesAmount] > 50000)
```
- **Explanation:** `FILTER` returns records with sales above 50,000.

---

###   **10. Dynamic Ranking of Products by Sales**
**Question:**  
Rank products by their sales amount dynamically.

**Solution:**
```DAX
Product Ranking = RANKX(
    ALL(Sales[ProductName]),
    SUM(Sales[SalesAmount]),
    ,
    DESC,
    DENSE
)
```
- **Explanation:** `RANKX` ranks products by sales in descending order.

---