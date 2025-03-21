# HCL Interview QnA
---

### 1. **RLS & How did you implement it?**
   - RLS (Row-Level Security) restricts data access based on user roles.
   - Implement using:
     - **Static RLS:** Define roles in Power BI Desktop.
     - **Dynamic RLS:** Use `USERNAME()` or `USERPRINCIPALNAME()` with a mapping table.
   - Apply security in **Manage Roles** and test with View As.

---

### 2. **Cross Filtering**
   - Enables filtering between related tables.
   - **Single Direction:** Filters only one way.
   - **Both Direction:** Allows bidirectional filtering between tables.

---

### 3. **Types of Data Importing Mode**
   - **Import Mode:** Data stored in Power BI memory.
   - **Direct Query:** Real-time queries to data source.
   - **Composite Mode:** Combination of Import and Direct Query.

---

### 4. **DAX Functions: ALL, ALLSELECTED, REMOVEFILTERS, ALLEXCEPT**
   - **ALL:** Removes filters from a table or column.
   - **ALLSELECTED:** Removes filters but respects user-applied filters.
   - **REMOVEFILTERS:** Similar to ALL, but only for specified columns.
   - **ALLEXCEPT:** Removes filters except for specified columns.
```sql
TotalSalesAll = 
CALCULATE(SUM(Sales[Amount]), ALL(Sales))
```

```sql
TotalSalesSelected = 
CALCULATE(SUM(Sales[Amount]), ALLSELECTED(Sales))
Effect: Removes filters set by visuals but respects user-applied slicers.
```

```sql
SalesWithoutFilter = 
CALCULATE(SUM(Sales[Amount]), REMOVEFILTERS(Sales[Region]))
Effect: Removes filters only on Region but retains others.
```
```sql
SalesByRegion = 
CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Sales, Sales[Region]))
Effect: Removes all filters except Region.
```


---

### 5. **Filters in a Report**
   - **Page Level:** Affects a single page.
   - **Visual Level:** Affects individual visuals.
   - **Report Level:** Applies to the entire report.

---

### 6. **Joins - Outputs from Each Type of Join**
   - **Inner Join:** Matching rows from both tables.
   - **Left Join:** All rows from the left table and matching rows from the right.
   - **Right Join:** All rows from the right table and matching rows from the left.
   - **Full Outer Join:** All rows from both tables.

---

### 7. **What is Join?**
   - Combines rows from two or more tables based on a related column.
   - **Inner Join** returns only matching rows.

---

### 8. **Query for Join**
```sql
SELECT A.*, B.*
FROM TableA A
INNER JOIN TableB B
ON A.ID = B.ID
```

---

### 9. **Type of Schema - Star & Snowflake**
   - **Star Schema:** Single fact table with dimension tables.
   - **Snowflake Schema:** Dimensions normalized into multiple related tables.

---

### 10. **DAX Query - Last Month’s Sale/Revenue, Top N Employees**
```DAX
LastMonthSales = 
CALCULATE(SUM(Sales[Amount]), PREVIOUSMONTH(Sales[Date]))

TopNEmployees = 
TOPN(5, SUMMARIZE(Sales, Employee[Name], "TotalSales", SUM(Sales[Amount])), [TotalSales], DESC)
```

---

### 11. **Primary Key, Candidate Key & Foreign Key**
   - **Primary Key:** Unique identifier for a table.
   - **Candidate Key:** Can qualify as a primary key.
   - **Foreign Key:** Links to primary key in another table.

---

### 12. **Process of the Project & How Did You Load Data into Power BI**
   - **Process:** Requirement gathering → Data extraction → Transformation → Report development → Testing → Deployment.
   - **Data Load:** Power Query, SQL connectors, APIs, or Excel files.

---

### 13. **How to Remove Duplicates in BI & SQL**
- **Power BI:** Remove duplicates using Power Query.
- **SQL:**
```sql
DELETE FROM TableName
WHERE ID NOT IN (
    SELECT MIN(ID) FROM TableName
    GROUP BY Column1, Column2
)
```

---

### 14. **Types of Triggers in Power Automate**
   - **Manual Trigger:** On button click.
   - **Automated Trigger:** Based on an event (e.g., email arrival).
   - **Scheduled Trigger:** Runs at specified intervals.

---

### 15. **Which Functions You Used in Power Apps**
   - **Patch:** Updates records.
```sh
   Patch(Employee, First(Employee), {Name: "John", Salary: 60000})
```

   - **Filter:** Filters records.
```sh
   Filter(Orders, Status = "Shipped")
```


   - **Collect:** Creates a collection.

```sh
   Collect(OrderList, {OrderID: 101, Item: "Laptop", Price: 50000})

```
   - **Navigate:** Moves between screens.
```sh
Navigate(Screen2, ScreenTransition.Fade)
```


   - **LookUp:** Finds records.
```sh
LookUp(Products, ProductID = 10, Price)
```

---

### 16. **Brief of Project**
   - Mention: Industry, Problem Statement, Solution, Tools Used, Outcome.

---

### 17. **UAT?**
   - Purpose: Validate whether the developed solution meets business requirements.
   Process:
   Identify test scenarios.
   Execute test cases.
   Validate output with stakeholders.
   Report defects and retest.
---

### 18. **SQL Query to Label Salary Range Using CASE**
```sql
SELECT EmpName, 
       CASE 
           WHEN Salary < 50000 THEN 'Low'
           WHEN Salary BETWEEN 50000 AND 260000 THEN 'Medium'
           ELSE 'High'
       END AS SalaryRange
FROM Employee
```

---

### 19. **How Do You Optimize Performance in Power BI?**
   - **Reduce Data Model Size:** Use necessary columns and tables.
   - **Aggregations:** Pre-aggregate large data.
   - **Use DAX Optimally:** Avoid complex calculated columns.
   - **Reduce Cardinality:** Optimize relationships.

---

### 20. **What is ETL Process & How Did You Do It?**
   - **ETL:** Extract, Transform, Load.
   - **Steps:** 
     - **Extract:** Get data from sources.
     - **Transform:** Clean, enrich, and structure data.
     - **Load:** Import into Power BI.

---

### 21. **Max Line Items You Have Worked Upon?**
   - Mention handling large datasets in millions with optimized models.

---

### 22. **Difference Between Calculated Column & Measure**
   - **Calculated Column:** Pre-calculated at row-level, stored in the model.
   - **Measure:** Calculated at runtime, efficient for aggregations.

---

### 23. **Import Mode vs Direct Query**
   - **Import Mode:** Data loaded into Power BI for fast performance.
   - **Direct Query:** Real-time data queries but slower.

---

### 24. **Used Azure Cloud?**
   - Mention if you used **Azure SQL, Azure Data Lake, Synapse, or Azure Blob Storage** in Power BI.

Let me know if you want detailed explanations or examples for any specific question! 🚀