## Set-2

##### 1. Write a SQL query to retrieve the second-highest salary from an "employees" table.

```sql
SELECT DISTINCT SALARY 
FROM EMPLOYEE 
ORDER BY SALARY DESC 
LIMIT 1 OFFSET 1;
```
##### 1.1 SQL query to retrieve the highest salary using DENSE_Rank() window function

```sql
WITH SalaryRank AS (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk 
    FROM employees
)
SELECT salary FROM SalaryRank WHERE rnk = 3;
```

##### 2. Write a SQL query to find employees who have the same salary as another employee in the "employees" table.

```sql
SELECT EMPLOYEE_NAME  FROM EMPLOYEE WHERE SALARY  IN (SELECT SALARY
FROM EMPLOYEE
GROUP BY SALARY 
HAVING COUNT(SALARY) >1 )
```
##### 3. Write a SQL query to find the department(s) with the highest total salary expenditure in the "employees" table.

```sql
-- Groups by department_id and calculates SUM(salary) for each department.

WITH depart_cte AS (
   select department_id, sum(salary) as total_salary from employee
   group by department_id
)

-- Selects only the department(s) with the highest total salary expenditure.
select d.department_id, d.total_salary
from employee e
JOIN depart_cte d
where total_salary < (select max(total_salary) from depart_cte);
```

##### 4. Employees Who Earn More Than Their Manager

```sql
select e1.employee_name, e1.employee_id from employee e1
JOIN employee e2 on e1.manager_id = e1.manager_id
where e1.salary > e2.salary
```

##### 5. Find Duplicate Records in a Table

```sql
select orderId from orders
group by orderId
having count(order_id)>1
```
##### 6. Get Cumulative Salary Using Window Functions

```sql
Select empID,empName
from employee 
Over(partition by DepartmentId order by salary) AS Cum_salary
from employee

```

##### 7. Retrieve Employees Who Joined in the Last 6 Months
 <!-- practice -->
```sql
SELECT EmployeeID, Name, JoinDate
FROM Employee
WHERE JoinDate >= DATEADD(MONTH, -6, GETDATE());
```

##### 8.Delete Duplicate Records and Keep One Record
```sql
WITH CTE AS (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY Name, Age, City ORDER BY ID) AS RowNum
    FROM Customer
)
DELETE FROM Customer WHERE ID IN (SELECT ID FROM CTE WHERE RowNum > 1);

```
##### 9. IMP Fetch Top N record
```sql
WITH ranked_cte AS (
    SELECT * ,
    DENSE RANK() OVER (PARTITION BY salary ORDER BY DESC ) AS rn
    FROM employee
)

SELECT * FROM ranked_cte where rn <=3
```

##### 10. How can you create calculated columns in SQL for Power BI?

```sql
SELECT order_id, 
       order_date, 
       customer_id, 
       order_total, 
       order_total * 0.1 AS DiscountAmount 
FROM orders;
```

##### 11. Employees Who Have the Highest Salary in Each Department
```sql
with rank_salary AS (
    SELECT EMP_ID, DEPART_ID, SALARY
    RANK() OVER(PARTITION BY DEPART_ID ORDER BY DESC) AS RN
    FROM EMPLOYEE
)
SELECT EMP_ID,DEPART_ID,SALARY
FROM RANK_SALARY 
WHERE RN = 1;
```

##### 12. Find Consecutive Absentees from an Attendance Table
##### Problem: Identify employees who were absent for 3 consecutive days
```sql

```