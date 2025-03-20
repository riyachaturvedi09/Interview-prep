
---

### 1. What is the difference between ALL, ALLEXCEPT, and REMOVEFILTERS in DAX?

**Answer:**  
- **ALL:** Removes all filters from a table or specific columns.  
   ```DAX
   TotalSalesAll = CALCULATE(SUM(Sales[Amount]), ALL(Sales))
   ```

- **ALLEXCEPT:** Removes all filters except the specified columns.  
   ```DAX
   TotalSalesByRegion = CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Sales, Sales[Region]))
   ```

- **REMOVEFILTERS:** Similar to `ALL` but designed for improved readability and can be used in more scenarios.  
   ```DAX
   TotalSalesNoFilter = CALCULATE(SUM(Sales[Amount]), REMOVEFILTERS(Sales))
   ```

---

### 2. What is the difference between SUMX and SUM in DAX?

**Answer:**  
- **SUM:** Adds all values in a column.  
   ```DAX
   TotalSales = SUM(Sales[Amount])
   ```

- **SUMX:** Iterates over a table and evaluates the expression for each row, then sums the results.  
   ```DAX
   TotalProfit = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice])
   ```

**Key Difference:**  
- `SUM` works on a single column.  
- `SUMX` is an iterator that evaluates a row-by-row expression.

---

### 3. What is the difference between RELATED and LOOKUPVALUE in DAX?

**Answer:**  
- **RELATED:** Retrieves values from a related table through an established relationship.  
   ```DAX
   ProductCategory = RELATED(Product[Category])
   ```

- **LOOKUPVALUE:** Searches for a value in a table and returns a corresponding value based on specific conditions.  
   ```DAX
   ProductCategory = LOOKUPVALUE(Product[Category], Product[ProductID], Sales[ProductID])
   ```

**When to Use:**  
- Use `RELATED` when there is a defined relationship.  
- Use `LOOKUPVALUE` when no relationship exists.

---

### 4. Explain the concept of Context Transition in DAX.

**Answer:**  
**Context Transition** occurs when a row context is converted into a filter context during the evaluation of a measure or a calculated column inside `CALCULATE()`.  

**Example:**  
```DAX
TotalSales = SUM(Sales[Amount])
```
If used inside `CALCULATE`:  
```DAX
FilteredSales = CALCULATE(TotalSales, Sales[Region] = "North")
```
- Row context becomes filter context, modifying the data being evaluated.  

---

### 5. How do you implement dynamic Row-Level Security (RLS) using DAX?

**Answer:**  
**Dynamic RLS** dynamically filters data based on the user’s login credentials.  

**Steps:**
1. Create a user table with email and region columns.  
2. Define a relationship between the fact table and the user table.  
3. Apply a DAX filter in **Manage Roles**:  
```DAX
[Email] = USERNAME()
```
4. Publish to Power BI Service and assign roles to users.  

---

### 6. What is the difference between DISTINCT, VALUES, and SELECTCOLUMNS in DAX?

**Answer:**  
- **DISTINCT:** Returns unique values from a column.  
   ```DAX
   DistinctRegions = DISTINCT(Sales[Region])
   ```

- **VALUES:** Returns a one-column table of distinct values but can include BLANK().  
   ```DAX
   RegionValues = VALUES(Sales[Region])
   ```

- **SELECTCOLUMNS:** Creates a new table with specific columns.  
   ```DAX
   SalesSummary = SELECTCOLUMNS(Sales, "Region", Sales[Region], "Total", SUM(Sales[Amount]))
   ```

---

### 7. How do you optimize DAX expressions for performance?

**Answer:**  
1. **Use Variables:** Store intermediate results to reduce redundant calculations.  
   ```DAX
   VAR TotalSales = SUM(Sales[Amount])
   RETURN TotalSales
   ```

2. **Avoid Iterators:** Minimize use of `SUMX`, `FILTER`, and `ALL`.  
3. **Reduce Filter Context Changes:** Avoid excessive use of `CALCULATE` inside nested functions.  
4. **Use Aggregated Columns:** Pre-aggregate data in SQL or Power Query when possible.  
5. **Disable Auto Date/Time:** Improves performance by preventing unnecessary date hierarchies.

---

### 8. What is the difference between USERNAME() and USERPRINCIPALNAME()?

**Answer:**  
- **USERNAME():** Returns the domain name and user name of the currently logged-in user.  
   - Example: `DOMAIN\username`  
   ```DAX
   RLS_Filter = USERNAME()
   ```

- **USERPRINCIPALNAME():** Returns the user’s email address or UPN (User Principal Name).  
   - Example: `user@domain.com`  
   ```DAX
   RLS_Filter = USERPRINCIPALNAME()
   ```

**Use Case:**  
- `USERPRINCIPALNAME()` is preferred for dynamic RLS scenarios in Power BI Service.  

---

### 9. What are Aggregation Tables and how do they improve Power BI performance?

**Answer:**  
**Aggregation Tables** store pre-aggregated data, reducing query complexity and improving performance.  

**Steps to Implement:**
1. Create an aggregated version of your fact table with fewer rows.  
2. Define relationships between the aggregate and detail tables.  
3. Use `SUMMARIZE` or `GROUP BY` in DAX for pre-aggregations.  

**Example:**  
```DAX
AggregatedSales = SUMMARIZE(Sales, Sales[Region], "TotalSales", SUM(Sales[Amount]))
```

---

### 10. What is Composite Model in Power BI and how do you use it?

**Answer:**  
**Composite Model** allows you to use a combination of Import and DirectQuery in a single dataset.  

**Use Case:**
- Import frequently used tables and keep large fact tables in DirectQuery mode for real-time access.  

**Steps:**
1. Set Import/DirectQuery mode at the data source level.  
2. Define relationships and manage storage modes in Model View.  
3. Optimize the DirectQuery queries to reduce load times.  

---

### 11. What is Time Intelligence in DAX? Provide examples.

**Answer:**  
**Time Intelligence** functions perform calculations over date and time periods.  

**Common Functions:**
- **TOTALYTD:** Calculates year-to-date totals.  
   ```DAX
   YTDSales = TOTALYTD(SUM(Sales[Amount]), Sales[Date])
   ```

- **SAMEPERIODLASTYEAR:** Compares values from the same period in the previous year.  
   ```DAX
   LastYearSales = CALCULATE(SUM(Sales[Amount]), SAMEPERIODLASTYEAR(Sales[Date]))
   ```

- **DATESINPERIOD:** Returns a table of dates within a specified range.  
   ```DAX
   DateRange = DATESINPERIOD(Sales[Date], TODAY(), -1, MONTH)
   ```

---

### 12. How do you handle many-to-many relationships in Power BI?

**Answer:**  
1. Create a **bridge table** to resolve many-to-many relationships.  
2. Define relationships between fact and dimension tables.  
3. Apply `USERELATIONSHIP` or `CROSSFILTER` in DAX to control relationship behavior.  

**Example:**
```DAX
SalesAmount = CALCULATE(SUM(Sales[Amount]), USERELATIONSHIP(Sales[CustomerID], Customers[CustomerID]))
```
**Example:**
. Using Bidirectional Relationships (Direct Approach)
In Power BI, many-to-many relationships can be created directly with bidirectional cross-filtering.
Steps:
Define a many-to-many relationship between the two tables.
Set the cross-filter direction to Both to allow filtering between the tables.
Considerations:
This approach can lead to performance issues with large datasets.
Avoid using bidirectional relationships with complex models

---

### 13. How do you configure Incremental Data Refresh in Power BI?

**Answer:**  
**Incremental Refresh** improves performance by refreshing only new or changed data.  

**Steps:**
1. Define date/time parameters in Power Query.  
2. Configure incremental refresh settings in **Manage Parameters**.  
3. Publish the report to Power BI Service.  

**Benefits:**  
- Reduces data load and processing time.  
- Allows historical data to remain intact.

---

### 14. What is CrossFilter in DAX and how is it used?

**Answer:**  
`CROSSFILTER` modifies the relationship direction between tables.  

**Example:**  
```DAX
SalesByRegion = CALCULATE(SUM(Sales[Amount]), CROSSFILTER(Sales[RegionID], Regions[RegionID], BOTH))
```
**Modes:**  
- `BOTH`: Applies filters in both directions.  
- `NONE`: Removes filters.  

---

### 15. How do you manage version control in Power BI reports?

**Answer:**  
1. Use **Power BI Template (.PBIT)** to save the structure and configurations.  
2. Store .PBIX files in **SharePoint** or **GitHub** for version control.  
3. Use **Power BI Service** to maintain report versions and manage deployment pipelines.  

---
