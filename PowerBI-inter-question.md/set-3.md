# HCL Tech Interview notes:

⸻

Power BI Questions
	1.	RLS & How did you implement it?
	•	Row-Level Security (RLS) is used in Power BI to restrict data access for users.
	•	Implemented using Static RLS (by defining roles in Power BI Desktop) or Dynamic RLS (using user-based filters in DAX with USERNAME() or USERPRINCIPALNAME() functions).
	•	Publish to Power BI Service and assign roles in security settings.
	2.	Cross Filtering
	•	Cross-filtering allows filters from one visual to affect another in a report.
	•	It works in two modes: Single-directional (default) or Bi-directional (filters propagate both ways).
	3.	Types of Data Importing Mode & Which You Used
	•	Import Mode – Data is loaded into Power BI for better performance.
	•	DirectQuery Mode – Fetches live data directly from the database.
	•	Composite Mode – Mix of Import & DirectQuery.
	•	Commonly, Import Mode is preferred for performance.
	4.	DAX Functions - ALL, ALLSELECTED, REMOVEFILTERS, ALLEXCEPT
	•	ALL() – Ignores all filters on a table.
	•	ALLSELECTED() – Ignores filters but keeps user-applied selections.
	•	REMOVEFILTERS() – Removes filters from a column/table.
	•	ALLEXCEPT() – Ignores filters except for specified columns.
	5.	Filters in Reports
	•	Page-level filter – Applies to a single page.
	•	Visual-level filter – Applies to one visual.
	•	Report-level filter – Applies to all pages.

⸻

SQL & Data Modeling Questions
	6.	Joins - Outputs from Each Type of Join
	•	Inner Join – Returns matching records from both tables.
	•	Left Join – Returns all records from the left table + matching records from the right.
	•	Right Join – Returns all records from the right table + matching records from the left.
	•	Full Join – Returns all records from both tables.
	7.	What is a Join? Explain Inner Join.
	•	A Join combines records from two tables based on a related column.
	•	Inner Join: Returns only the rows where there is a match in both tables.
	8.	Query for Join

SELECT A.EmployeeID, A.Name, B.Department  
FROM Employees A  
INNER JOIN Departments B ON A.DepartmentID = B.DepartmentID;


	9.	Type of Schema - Star & Snowflake
	•	Star Schema: One central fact table connected to dimension tables.
	•	Snowflake Schema: Dimension tables are further normalized into sub-tables.
	10.	DAX Query for Last Month’s Sales/Revenue & Top N Employees

Last Month Sales:  
CALCULATE(SUM(Sales[Amount]), PREVIOUSMONTH(Sales[Date]))  

Top 5 Employees by Revenue:  
TOPN(5, SUMMARIZE(Sales, Employees[Name], "Total Sales", SUM(Sales[Amount])), [Total Sales], DESC)


	11.	Primary Key, Candidate Key & Foreign Key

	•	Primary Key: Unique identifier for a table (e.g., EmployeeID).
	•	Candidate Key: A column(s) that could be a primary key.
	•	Foreign Key: A column linking to a Primary Key in another table.

	12.	Process of the Project & How Did You Load Data into Power BI?

	•	Steps: Data Extraction → Data Transformation (ETL) → Data Modeling → Report Development → Publishing.
	•	Loading Data: Connected via SQL Server, SharePoint, or Excel → Applied transformations in Power Query → Loaded into Power BI Model.

	13.	How to Remove Duplicates in Power BI & SQL

	•	Power BI: Use “Remove Duplicates” in Power Query.
	•	SQL:

DELETE FROM Employees  
WHERE EmployeeID NOT IN (SELECT MIN(EmployeeID) FROM Employees GROUP BY Name, Department);



	14.	Types of Triggers in Power Automate

	•	Manual Trigger (Button click)
	•	Automated Trigger (Event-based, like new email)
	•	Scheduled Trigger (Runs at set intervals)

	15.	Which Functions You Used in PowerApps?

	•	Patch(), If(), Filter(), Lookup(), Navigate(), Collect().

	16.	Brief of Project

	•	Prepare a 2-3 minute summary of your project, focusing on the problem, solution, tools used, and impact.

⸻

Advanced Power BI & ETL Questions
	17.	VAT?

	•	Value Added Tax – A consumption tax levied on goods & services at each production stage.

	18.	SQL Query to Label Salary Brackets

SELECT EmployeeID, Name, Salary,  
CASE  
    WHEN Salary < 50000 THEN 'Low'  
    WHEN Salary BETWEEN 50000 AND 260000 THEN 'Medium'  
    ELSE 'High'  
END AS SalaryBracket  
FROM Employees;

	19.	How Do You Optimize Performance in Power BI?

	•	Use Aggregations & Summarized Data
	•	Limit Data Loading (Use Import Mode when possible)
	•	Optimize DAX Queries (Avoid iterators like SUMX)
	•	Use Star Schema
	•	Disable Unnecessary Visual Interactions

	20.	What is the ETL Process & How Did You Do It?

	•	ETL: Extract, Transform, Load.
	•	Used Power Query to clean and transform data before loading it into Power BI.

	21.	Max Line Items You Have Worked Upon?

	•	Mention the highest volume dataset you’ve handled (e.g., “Worked with 10 million+ records in Power BI”).

	22.	Difference Between Calculated Column & Measures with Example

	•	Calculated Column: Computed at the row level and stored in the model.
	•	Measure: Computed dynamically based on user filters.
	•	Example:

-- Calculated Column  
'Sales'[Total Price] = 'Sales'[Quantity] * 'Sales'[Unit Price]  
-- Measure  
Total Sales = SUM('Sales'[Total Price])



	23.	Import Mode vs. DirectQuery

	•	Import Mode: Stores data in Power BI; faster performance.
	•	DirectQuery: Fetches live data from a source, good for real-time updates.

	24.	Used Azure Cloud?

	•	If you have, mention Azure SQL Database, Azure Data Factory, or Azure Synapse Analytics.

⸻

Let me know if you need explanations on any specific topic!