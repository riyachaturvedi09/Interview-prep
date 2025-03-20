Set 1:
---

### 1. What are the differences between Calculated Columns and Measures in Power BI?

**Answer:**  
- **Calculated Columns:**  
   - Evaluated at the row level during data load or data refresh.  
   - Stored in the model and consume storage space.  
   - Used when you need to add a new column to the table.  
   - Example:  
   ```DAX
   SalesWithTax = Sales[Amount] * 1.18
   ```

- **Measures:**  
   - Calculated at the time of query and not stored in the model.  
   - Dynamic and recalculated when filters change.  
   - Used for aggregations and calculations across the entire dataset.  
   - Example:  
   ```DAX
   TotalSales = SUM(Sales[Amount])
   ```

---

### 2. What is Row-Level Security (RLS) and how do you implement it in Power BI?

**Answer:**  
**Row-Level Security (RLS)** restricts data access for specific users by applying filters at the row level.  

**Steps to implement RLS:**
1. Open Power BI Desktop.
2. Go to **Model View** and select **Manage Roles**.
3. Define a role and add DAX filters for the required tables.
4. Publish the report to the Power BI service.
5. Assign the role to users or groups in the Power BI Service.

**Example:**  
```DAX
[Region] = "North"
```
This restricts data visibility to only records where the region is “North.”  

---

### 3. What is the difference between Import Mode and Direct Query in Power BI?

**Answer:**  
- **Import Mode:**  
   - Data is imported and stored in the Power BI model.  
   - Faster performance due to in-memory storage.  
   - Suitable for small to medium datasets.  
   - Requires data refresh to update.  

- **Direct Query:**  
   - Queries data directly from the source in real time.  
   - No data is stored in Power BI.  
   - Slower performance for complex queries or large datasets.  
   - Ideal for large datasets that need real-time updates.  

**When to Use:**  
- **Import Mode:** When performance is critical and the dataset size is manageable.  
- **Direct Query:** When real-time updates are required or data size is too large to import.

---

### 4. What are the different types of visualizations in Power BI and when do you use them?

**Answer:**  
1. **Bar/Column Chart:** For comparing data across categories.  
2. **Line Chart:** To show trends over time.  
3. **Pie/Donut Chart:** To show proportions or percentage breakdown.  
4. **Matrix/Table:** For detailed data visualization with drill-downs.  
5. **Card:** To display single values (KPIs).  
6. **Map/Geographic Chart:** To visualize location-based data.  

**Example Usage:**  
- **Bar Chart:** Monthly sales comparison.  
- **Line Chart:** Revenue growth over time.  
- **Card:** Showing total revenue or average order value.  

---

### 5. How do you optimize a slow Power BI report?

**Answer:**  
To optimize a slow Power BI report:  

1. **Limit Data Volume:** Import only necessary columns and rows.  
2. **Reduce Calculated Columns:** Use measures instead for aggregations.  
3. **Optimize DAX Queries:** Avoid using `FILTER` inside `CALCULATE`, use variables to store intermediate results.  
4. **Disable Auto Date/Time:** Turn off auto date/time for faster model processing.  
5. **Aggregate Data at Source:** Pre-aggregate data to reduce query load.  
6. **Use Star Schema:** Prefer star schema over snowflake schema for better performance.  

---

### 6. How do you create a KPI in Power BI and display it?

**Answer:**  
1. Open Power BI Desktop.  
2. Create a **measure** that calculates the KPI value.  
   ```DAX
   TotalSales = SUM(Sales[Amount])
   ```

3. Add a **KPI visual** to the report.  
4. Drag the measure to the **Indicator field** and define the target value.  
5. Set thresholds to show the status as good, neutral, or bad.  

**Example:**
- KPI shows **Total Sales** with a target of $500K.  

---

### 7. What is a Star Schema, and why is it preferred in Power BI?

**Answer:**  
**Star Schema** is a data modeling technique where:  
- **Fact Table:** Contains numerical data (e.g., Sales Amount, Quantity).  
- **Dimension Tables:** Contain descriptive attributes (e.g., Date, Product, Region).  

**Advantages:**  
- Faster query performance.  
- Easier to manage relationships.  
- Reduces complexity in DAX calculations.  

**Example:**  
- **Fact Table:** Sales  
- **Dimensions:** Date, Product, Customer, Region  

---

### 8. What are common DAX functions used in Power BI?

**Answer:**  
1. **SUM:** Adds all values in a column.  
   ```DAX
   TotalSales = SUM(Sales[Amount])
   ```
2. **AVERAGE:** Returns the average value.  
   ```DAX
   AvgSales = AVERAGE(Sales[Amount])
   ```
3. **COUNT:** Counts the number of rows.  
   ```DAX
   OrderCount = COUNT(Sales[OrderID])
   ```
4. **CALCULATE:** Modifies context of a calculation.  
   ```DAX
   SalesFiltered = CALCULATE(SUM(Sales[Amount]), Sales[Region] = "North")
   ```
5. **IF:** Returns a value based on a condition.  
   ```DAX
   Status = IF(Sales[Amount] > 1000, "High", "Low")
   ```

---

### 9. How do you create relationships between tables in Power BI?

**Answer:**  
1. Go to **Model View** in Power BI.  
2. Drag and drop the field from one table to the matching field in another table.  
3. Define the relationship type:  
   - **One-to-Many (1:*):** Common for dimension and fact tables.  
   - **Many-to-Many (M:N):** Used when both tables contain unique records.  
4. Ensure the cross-filter direction is set appropriately (single or both directions).  

---

### 10. How do you use Parameters in Power BI?

**Answer:**  
1. Go to **Home > Manage Parameters > New Parameter**.  
2. Define the parameter name, data type, and range.  
3. Use the parameter in your DAX calculations or queries.  
4. Allow users to select values dynamically to change visuals based on the parameter.  

**Example:**
- Parameter: `DateRange` to filter data between start and end dates.

---

### Bonus Tips:
- Be prepared to explain real-life projects where you used Power BI to improve decision-making.  
- Be ready for scenario-based questions where you need to troubleshoot report performance issues.  

---

This version keeps it formal and to the point. Let me know if you need help with sample DAX queries or scenario-based answers!