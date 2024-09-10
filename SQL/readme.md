# 函数
| 函数名称 | 功能 | 示例代码 | 说明 |
| --- | --- | --- | --- |
| `AVG` | 计算某列的平均值 | `SELECT AVG(Salary) FROM Employees;` | 计算员工的平均工资 |
| `COUNT` | 统计行数 | `SELECT COUNT(*) FROM Orders;` | 计算订单总数 |
| `SUM` | 计算某列的总和 | `SELECT SUM(Salary) FROM Employees;` | 计算所有员工的工资总和 |
| `MAX` | 返回某列的最大值 | `SELECT MAX(Salary) FROM Employees;` | 查找员工中的最高工资 |
| `MIN` | 返回某列的最小值 | `SELECT MIN(Salary) FROM Employees;` | 查找员工中的最低工资 |
| `ROUND` | 对数值进行四舍五入 | `SELECT ROUND(Price, 2) FROM Products;` | 将商品价格四舍五入到两位小数 |
| `DATEADD` | 添加日期或时间间隔 | `SELECT DATEADD(day, 7, '2024-01-01');` | 将日期加上 7 天 |
| `DATEDIFF` | 计算两个日期之间的差异 | `SELECT DATEDIFF(day, '2024-01-01', '2024-01-10');` | 计算两个日期之间的天数差 |
| `GETDATE()` | 获取当前日期和时间 | `SELECT GETDATE();` | 获取当前系统日期和时间 |
| `LEN` | 返回字符串的长度 | `SELECT LEN('Hello');` | 计算字符串的长度 |
| `UPPER` | 将字符串转换为大写 | `SELECT UPPER('hello');` | 将字符串转为大写 |
| `LOWER` | 将字符串转换为小写 | `SELECT LOWER('HELLO');` | 将字符串转为小写 |
| `CASE` | 条件表达式 | `SELECT CASE WHEN Salary > 50000 THEN 'High' ELSE 'Low' END FROM Employees;` | 基于员工工资分类 |



# SQL Interview in 50 Qs

| #   | Note    | Title                                                        | Difficulty | Solution                                                   |
|-----|---------|---------------------------------------------------------------|------------|------------------------------------------------------------|
| 1   |         | [1757 Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products) | Easy       | [Solution](https://codebitwave.com/leetcode-sql-1757-recyclable-and-low-fat-products/)                                                |
| 2   |         | [584 Find Customer Referee](https://leetcode.com/problems/find-customer-referee) | Easy       | [Solution]()                                                |
| 3   |         | [595 Big Countries](https://leetcode.com/problems/big-countries) | Easy       | [Solution]()                                                |
| 4   |         | [1148 Article Views I](https://leetcode.com/problems/article-views-i) | Easy       | [Solution]()                                                |
| 5   |         | [Invalid Tweets](https://leetcode.com/problems/invalid-tweets) | Easy       | [Solution]()                                                |
| 6   |         | [Basic Joins: Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier) | Easy       | [Solution]()                                                |
| 7   |         | [Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i) | Easy       | [Solution]()                                                |
| 8   |         | [1581 Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions) | Easy       | [Solution]()                                                |
| 9   |         | [197 Rising Temperature](https://leetcode.com/problems/rising-temperature) | Easy       | [Solution]()                                                |
| 10  |         | [1661 Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine) | Easy       | [Solution]()                                                |
| 11  |         | [Employee Bonus](https://leetcode.com/problems/employee-bonus) | Easy       | [Solution]()                                                |
| 12  |         | [Students and Examinations](https://leetcode.com/problems/students-and-examinations) | Easy       | [Solution]()                                                |
| 13  |         | [Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports) | Medium     | [Solution]()                                                |
| 14  |         | [Confirmation Rate](https://leetcode.com/problems/confirmation-rate) | Medium     | [Solution]()                                                |
| 15  |         | [Not Boring Movies](https://leetcode.com/problems/not-boring-movies) | Easy       | [Solution]()                                                |
| 16  |         | [Average Selling Price](https://leetcode.com/problems/average-selling-price) | Easy       | [Solution]()                                                |
| 17  |         | [Project Employees I](https://leetcode.com/problems/project-employees-i) | Easy       | [Solution]()                                                |
| 18  |         | [Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest) | Easy       | [Solution]()                                                |
| 19  |         | [Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage) | Easy       | [Solution]()                                                |
| 20  |         | [Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i) | Medium     | [Solution]()                                                |
| 21  |         | [Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii) | Medium     | [Solution]()                                                |
| 22  |         | [Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv) | Medium     | [Solution]()                                                |
| 23  |         | [Sorting and Grouping: Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher) | Easy       | [Solution]()                                                |
| 24  |         | [User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i) | Easy       | [Solution]()                                                |
| 25  |         | [Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii) | Medium     | [Solution]()                                                |
| 26  |         | [Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students) | Easy       | [Solution]()                                                |
| 27  |         | [Find Followers Count](https://leetcode.com/problems/find-followers-count) | Easy       | [Solution]()                                                |
| 28  |         | [Biggest Single Number](https://leetcode.com/problems/biggest-single-number) | Easy       | [Solution]()                                                |
| 29  |         | [Customers Who Bought All Products](https://leetcode.com/problems/customers-who-bought-all-products) | Medium     | [Solution]()                                                |
| 30  |         | [Advanced Select and Joins: The Number of Employees Which Report to Each Employee](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee) | Easy       | [Solution]()                                                |
| 31  |         | [Primary Department for Each Employee](https://leetcode.com/problems/primary-department-for-each-employee) | Easy       | [Solution]()                                                |
| 32  |         | [Triangle Judgement](https://leetcode.com/problems/triangle-judgement) | Easy       | [Solution]()                                                |
| 33  |         | [Consecutive Numbers](https://leetcode.com/problems/consecutive-numbers) | Medium     | [Solution]()                                                |
| 34  |         | [Product Price at a Given Date](https://leetcode.com/problems/product-price-at-a-given-date) | Medium     | [Solution]()                                                |
| 35  |         | [Last Person to Fit in the Bus](https://leetcode.com/problems/last-person-to-fit-in-the-bus) | Medium     | [Solution]()                                                |
| 36  |         | [Count Salary Categories](https://leetcode.com/problems/count-salary-categories) | Medium     | [Solution]()                                                |
| 37  |         | [Subqueries: Employees Whose Manager Left the Company](https://leetcode.com/problems/employees-whose-manager-left-the-company) | Easy       | [Solution]()                                                |
| 38  |         | [Exchange Seats](https://leetcode.com/problems/exchange-seats) | Medium     | [Solution]()                                                |
| 39  |         | [Movie Rating](https://leetcode.com/problems/movie-rating)    | Medium     | [Solution]()                                                |
| 40  |         | [Restaurant Growth](https://leetcode.com/problems/restaurant-growth) | Medium     | [Solution]()                                                |
| 41  |         | [Friend Requests II: Who Has the Most Friends](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends) | Medium     | [Solution]()                                                |
| 42  |         | [Investments in 2016](https://leetcode.com/problems/investments-in-2016) | Medium     | [Solution]()                                                |
| 43  |         | [Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries) | Hard       | [Solution]()                                                |
| 44  |         | [Advanced String Functions / Regex / Clause: Fix Names in a Table](https://leetcode.com/problems/fix-names-in-a-table) | Easy       | [Solution]()                                                |
| 45  |         | [Patients With a Condition](https://leetcode.com/problems/patients-with-a-condition) | Easy       | [Solution]()                                                |
| 46  |         | [Delete Duplicate Emails](https://leetcode.com/problems/delete-duplicate-emails) | Easy       | [Solution]()                                                |
| 47  |         | [Second Highest Salary](https://leetcode.com/problems/second-highest-salary) | Medium     | [Solution]()                                                |
| 48  |         | [Group Sold Products By The Date](https://leetcode.com/problems/group-sold-products-by-the-date) | Easy       | [Solution]()                                                |
| 49  |         | [List the Products Ordered in a Period](https://leetcode.com/problems/list-the-products-ordered-in-a-period) | Easy       | [Solution]()                                                |
| 50  |         | [Find Users With Valid E-Mails](https://leetcode.com/problems/find-users-with-valid-e-mails) | Easy       | [Solution]()                                                |

------

### 50 SQL Interview Questions with MSSQL Code Examples

Below is a list of advanced SQL interview questions, each paired with examples using Microsoft SQL Server (MSSQL). These questions cover various SQL concepts such as window functions, advanced joins, recursive queries, transactions, and more.

---

### 1. **What is a Common Table Expression (CTE) and how is it used?**

[English] A CTE is a temporary result set defined within the execution scope of a single `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs can be recursive or non-recursive.

```sql
WITH EmployeeCTE AS (
    SELECT EmployeeID, ManagerID, FirstName, LastName
    FROM Employees
)
SELECT * 
FROM EmployeeCTE;
```

---

### 2. **Explain Recursive CTE and provide an example.**

[English] Recursive CTE is a CTE that references itself to return hierarchical data. It's useful for traversing trees or graphs.

```sql
WITH ManagerHierarchy AS (
    SELECT EmployeeID, ManagerID, FirstName, LastName
    FROM Employees
    WHERE ManagerID IS NULL
    UNION ALL
    SELECT e.EmployeeID, e.ManagerID, e.FirstName, e.LastName
    FROM Employees e
    INNER JOIN ManagerHierarchy mh ON e.ManagerID = mh.EmployeeID
)
SELECT * FROM ManagerHierarchy;
```

---

### 3. **How do you use a window function in MSSQL?**

[English] Window functions allow you to perform calculations across a set of table rows that are related to the current row.

```sql
SELECT EmployeeID, Salary, 
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```

---

### 4. **What is a PIVOT table in SQL? Provide an example.**

[English] The PIVOT operator in SQL allows you to rotate rows into columns.

```sql
SELECT * 
FROM (
    SELECT Department, Salary 
    FROM Employees
) AS SourceTable
PIVOT (
    SUM(Salary) 
    FOR Department IN ([HR], [IT], [Sales])
) AS PivotTable;
```

---

### 5. **How do you use the UNPIVOT operator in MSSQL?**

[English] The UNPIVOT operator converts columns into rows.

```sql
SELECT Department, SalaryType, Salary
FROM Employees
UNPIVOT (
    Salary FOR SalaryType IN (BaseSalary, Bonus)
) AS UnpivotTable;
```

---

### 6. **How do you create an indexed view in MSSQL?**

[English] An indexed view is a view with a unique clustered index. This allows better performance for complex queries.

```sql
CREATE VIEW EmployeeView
WITH SCHEMABINDING 
AS 
SELECT EmployeeID, SUM(Salary) AS TotalSalary
FROM dbo.Employees
GROUP BY EmployeeID;
GO
CREATE UNIQUE CLUSTERED INDEX IX_EmployeeView 
ON EmployeeView (EmployeeID);
```

---

### 7. **What is the difference between RANK(), DENSE_RANK(), and ROW_NUMBER()?**

[English] These are window functions that rank rows:
- `ROW_NUMBER()` provides a unique number for each row.
- `RANK()` leaves gaps in numbering after ties.
- `DENSE_RANK()` does not leave gaps.

```sql
SELECT EmployeeID, 
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum,
       RANK() OVER (ORDER BY Salary DESC) AS RankNum,
       DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRankNum
FROM Employees;
```

---

### 8. **What are CROSS APPLY and OUTER APPLY in MSSQL?**

[English] `CROSS APPLY` is like an inner join and `OUTER APPLY` is like a left outer join but for table-valued functions.

```sql
SELECT e.EmployeeID, fn.Salary
FROM Employees e
CROSS APPLY fn_GetEmployeeSalary(e.EmployeeID) fn;

SELECT e.EmployeeID, fn.Salary
FROM Employees e
OUTER APPLY fn_GetEmployeeSalary(e.EmployeeID) fn;
```

---

### 9. **How do you handle NULL values in MSSQL?**

[English] Use the `COALESCE()` or `ISNULL()` functions to handle `NULL` values.

```sql
SELECT EmployeeID, 
       COALESCE(Salary, 0) AS Salary
FROM Employees;
```

---

### 10. **Explain how you can use a MERGE statement in MSSQL.**

[English] The `MERGE` statement allows you to perform `INSERT`, `UPDATE`, or `DELETE` operations based on whether a condition is met.

```sql
MERGE INTO Employees AS Target
USING UpdatedEmployees AS Source
ON Target.EmployeeID = Source.EmployeeID
WHEN MATCHED THEN 
    UPDATE SET Target.Salary = Source.Salary
WHEN NOT MATCHED THEN
    INSERT (EmployeeID, FirstName, LastName, Salary)
    VALUES (Source.EmployeeID, Source.FirstName, Source.LastName, Source.Salary);
```

---

### 11. **How would you calculate the running total of a column in MSSQL?**

[English] You can use the `SUM()` function as a window function to calculate running totals.

```sql
SELECT EmployeeID, Salary, 
       SUM(Salary) OVER (ORDER BY EmployeeID) AS RunningTotal
FROM Employees;
```

---

### 12. **What is a windowed aggregate function and how is it different from a GROUP BY?**

[English] Windowed aggregate functions allow you to calculate aggregates across rows without grouping the result set.

```sql
SELECT EmployeeID, Salary, 
       AVG(Salary) OVER (PARTITION BY Department) AS AvgSalary
FROM Employees;
```

---

### 13. **How do you handle duplicates in SQL?**

[English] Use `DISTINCT` to remove duplicates or use `ROW_NUMBER()` to identify and remove duplicates.

```sql
WITH CTE AS (
    SELECT EmployeeID, FirstName, LastName, 
           ROW_NUMBER() OVER (PARTITION BY FirstName, LastName ORDER BY EmployeeID) AS RowNum
    FROM Employees
)
DELETE FROM CTE WHERE RowNum > 1;
```

---

### 14. **How would you find the nth highest salary in MSSQL?**

[English] Use the `OFFSET` and `FETCH` clause to find the nth highest salary.

```sql
SELECT Salary
FROM Employees
ORDER BY Salary DESC
OFFSET 3 ROWS FETCH NEXT 1 ROWS ONLY;  -- For the 4th highest salary
```

---

### 15. **What is a correlated subquery? Provide an example.**

[English] A correlated subquery is a subquery that refers to columns in the outer query.

```sql
SELECT e1.EmployeeID, e1.FirstName, e1.Salary
FROM Employees e1
WHERE e1.Salary > (SELECT AVG(e2.Salary) 
                   FROM Employees e2
                   WHERE e2.Department = e1.Department);
```

---

### 16. **How do you optimize a query with indexes in MSSQL?**

[English] Indexes improve query performance by allowing faster access to data.

```sql
CREATE NONCLUSTERED INDEX IX_Employees_Salary 
ON Employees (Salary);
```

---

### 17. **Explain how to use a trigger in MSSQL.**

[English] A trigger is a stored procedure that automatically runs when certain events occur on a table.

```sql
CREATE TRIGGER trg_AfterInsert 
ON Employees
AFTER INSERT
AS
BEGIN
    INSERT INTO AuditLog (Event, EventDate)
    VALUES ('Employee Inserted', GETDATE());
END;
```

---

### 18. **What is the difference between a clustered and non-clustered index?**

[English] A clustered index sorts and stores the data rows of the table, while a non-clustered index creates a separate structure for the index.

```sql
CREATE CLUSTERED INDEX IX_Employees_EmployeeID
ON Employees (EmployeeID);

CREATE NONCLUSTERED INDEX IX_Employees_LastName
ON Employees (LastName);
```

---

### 19. **How do you perform a FULL OUTER JOIN in MSSQL?**

[English] A `FULL OUTER JOIN` returns all records when there is a match in either the left or right table.

```sql
SELECT e.EmployeeID, d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```

---

### 20. **How do you perform error handling in MSSQL?**

[English] You can use `TRY...CATCH` blocks to handle errors in MSSQL.

```sql
BEGIN TRY
    INSERT INTO Employees (EmployeeID, FirstName) VALUES (1, 'John');
END TRY
BEGIN CATCH
    PRINT ERROR_MESSAGE();
END CATCH;
```

---

### 21. **How do you retrieve the current database name in MSSQL?**

[English] You can use the `DB_NAME()` function to retrieve the current database name.

```sql
SELECT DB_NAME() AS DatabaseName;
```

---

### 22. **What is a cursor in MSSQL?**

[English] A cursor is a database object used to retrieve data row-by-row.

```sql
DECLARE EmployeeCursor CURSOR FOR
SELECT EmployeeID, FirstName FROM Employees;

OPEN EmployeeCursor;
FETCH NEXT FROM EmployeeCursor;
CLOSE EmployeeCursor;
DEALLOCATE EmployeeCursor;
```

---

### 23. **How do you create a temporary table in MSSQL?**

[English] Temporary tables store data temporarily during the session or transaction.

```sql
CREATE TABLE

 #TempEmployee (
    EmployeeID INT,
    FirstName VARCHAR(100)
);

INSERT INTO #TempEmployee (EmployeeID, FirstName)
VALUES (1, 'John');
```

---

### 24. **What is a partitioned table in MSSQL?**

[English] Partitioning splits a table into multiple parts based on the values of a column.

```sql
CREATE PARTITION FUNCTION pfEmployees (INT)
AS RANGE LEFT FOR VALUES (100, 200, 300);
```

---

### 25. **How do you implement transactions in MSSQL?**

[English] Transactions allow you to execute a set of operations as a single unit of work.

```sql
BEGIN TRANSACTION;

INSERT INTO Employees (EmployeeID, FirstName, LastName) 
VALUES (1, 'John', 'Doe');

COMMIT;
```

---

### 26. **How do you use `ROLLBACK` in MSSQL?**

[English] Use `ROLLBACK` to undo a transaction if an error occurs.

```sql
BEGIN TRANSACTION;

INSERT INTO Employees (EmployeeID, FirstName) VALUES (1, 'John');

IF @@ERROR <> 0
    ROLLBACK;
ELSE
    COMMIT;
```

---

### 27. **What is the difference between `HAVING` and `WHERE`?**

[English] `WHERE` filters rows before aggregation, while `HAVING` filters after aggregation.

```sql
SELECT Department, COUNT(EmployeeID)
FROM Employees
GROUP BY Department
HAVING COUNT(EmployeeID) > 10;
```

---

### 28. **How do you use `EXISTS` in MSSQL?**

[English] `EXISTS` checks for the existence of rows in a subquery.

```sql
SELECT EmployeeID, FirstName 
FROM Employees
WHERE EXISTS (
    SELECT 1 
    FROM Salaries 
    WHERE Salaries.EmployeeID = Employees.EmployeeID
);
```

---

### 29. **How do you optimize queries using indexes?**

[English] Add indexes on frequently used columns to improve query performance.

```sql
CREATE INDEX IX_Employee_Salary ON Employees (Salary);
```

---

### 30. **What is the difference between `INNER JOIN` and `LEFT JOIN`?**

[English] `INNER JOIN` returns rows that have matching values in both tables. `LEFT JOIN` returns all rows from the left table and matched rows from the right table.

```sql
SELECT e.EmployeeID, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 31. **How do you handle deadlocks in MSSQL?**

[English] Deadlocks can be resolved by handling errors and implementing retry logic.

```sql
BEGIN TRY
    BEGIN TRANSACTION;
    -- transaction logic
    COMMIT;
END TRY
BEGIN CATCH
    IF XACT_STATE() = -1
        ROLLBACK;
END CATCH;
```

---

### 32. **How do you return only the first N rows in a query in MSSQL?**

[English] Use `TOP` or `OFFSET-FETCH` to return only a specific number of rows.

```sql
SELECT TOP 10 * FROM Employees;
```

---

### 33. **What are window functions and why are they important?**

[English] Window functions allow you to perform operations across a set of table rows without collapsing them into groups.

```sql
SELECT EmployeeID, Salary, 
       AVG(Salary) OVER (PARTITION BY DepartmentID) AS AvgDeptSalary
FROM Employees;
```

---

### 34. **How do you retrieve the second highest salary in MSSQL?**

[English] Use `DISTINCT` with `ORDER BY` and `OFFSET-FETCH`.

```sql
SELECT DISTINCT Salary
FROM Employees
ORDER BY Salary DESC
OFFSET 1 ROWS FETCH NEXT 1 ROWS ONLY;
```

---

### 35. **What is the difference between DELETE and TRUNCATE in MSSQL?**

[English] `DELETE` removes rows one at a time and logs each deletion. `TRUNCATE` removes all rows by deallocating pages and is faster but cannot be rolled back.

```sql
DELETE FROM Employees WHERE EmployeeID = 1;
TRUNCATE TABLE Employees;
```

---

### 36. **What is the purpose of an index and how do you create one in MSSQL?**

[English] Indexes are used to speed up the retrieval of data.

```sql
CREATE INDEX IX_Employee_LastName 
ON Employees (LastName);
```

---

### 37. **What is a computed column and how do you create it in MSSQL?**

[English] A computed column is a virtual column that is calculated using an expression.

```sql
ALTER TABLE Employees
ADD FullName AS (FirstName + ' ' + LastName);
```

---

### 38. **What is the difference between `ISNULL()` and `COALESCE()`?**

[English] `ISNULL()` takes two arguments and returns the first non-null value. `COALESCE()` can take multiple arguments and returns the first non-null value from the list.

```sql
SELECT ISNULL(Salary, 0) FROM Employees;
SELECT COALESCE(Salary, Bonus, 0) FROM Employees;
```

---

### 39. **How do you create a stored procedure in MSSQL?**

[English] Stored procedures are saved queries that can be reused.

```sql
CREATE PROCEDURE GetEmployeeDetails
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;
```

---

### 40. **How do you use the CASE statement in MSSQL?**

[English] `CASE` is used to perform conditional logic in queries.

```sql
SELECT EmployeeID, Salary, 
       CASE 
           WHEN Salary > 50000 THEN 'High'
           ELSE 'Low'
       END AS SalaryCategory
FROM Employees;
```

---

### 41. **How do you perform conditional aggregation in MSSQL?**

[English] Use `CASE` within aggregate functions to conditionally include rows.

```sql
SELECT Department, 
       SUM(CASE WHEN Salary > 50000 THEN Salary ELSE 0 END) AS HighSalarySum
FROM Employees
GROUP BY Department;
```

---

### 42. **How do you handle NULL values when concatenating strings in MSSQL?**

[English] Use the `ISNULL()` or `COALESCE()` functions to replace `NULL` with an empty string.

```sql
SELECT FirstName + ' ' + ISNULL(LastName, '') AS FullName FROM Employees;
```

---

### 43. **What is the difference between UNION and UNION ALL?**

[English] `UNION` removes duplicates, while `UNION ALL` keeps all duplicates.

```sql
SELECT EmployeeID FROM Employees
UNION
SELECT EmployeeID FROM Salaries;

SELECT EmployeeID FROM Employees
UNION ALL
SELECT EmployeeID FROM Salaries;
```

---

### 44. **How do you dynamically execute a SQL query in MSSQL?**

[English] Use `EXEC()` or `sp_executesql` for dynamic SQL.

```sql
DECLARE @SQL NVARCHAR(MAX) = 'SELECT * FROM Employees';
EXEC (@SQL);
```

---

### 45. **What is a table-valued function in MSSQL?**

[English] A table-valued function returns a table and can be used like a view in a `SELECT` statement.

```sql
CREATE FUNCTION fn_GetEmployeesByDept (@DepartmentID INT)
RETURNS TABLE
AS
RETURN 
(
    SELECT EmployeeID, FirstName, LastName 
    FROM Employees 
    WHERE DepartmentID = @DepartmentID
);
```

---

### 46. **What is a scalar function in MSSQL?**

[English] A scalar function returns a single value.

```sql
CREATE FUNCTION fn_GetFullName (@FirstName NVARCHAR(100), @LastName NVARCHAR(100))
RETURNS NVARCHAR(200)
AS
BEGIN
    RETURN @FirstName + ' ' + @LastName;
END;
```

---

### 47. **What is the use of CROSS JOIN in MSSQL?**

[English] `CROSS JOIN` returns the Cartesian product of two tables.

```sql
SELECT * 
FROM Employees CROSS JOIN Departments;
```

---

### 48. **What is the purpose of CTEs over subqueries in MSSQL?**

[English] CTEs make complex queries more readable and reusable within the same query.

```sql
WITH EmployeeCTE AS (
    SELECT EmployeeID, FirstName, Salary 
    FROM Employees 
    WHERE Salary > 50000
)
SELECT * FROM EmployeeCTE;
```

---

### 49. **How do you rename a table in MSSQL?**

[English] Use `sp_rename` to rename a table.

```sql
EXEC sp_rename 'Employees', 'Staff';
```

---

### 50. **What is the difference between a primary key and a unique key?**

[English] A primary key uniquely identifies each record and does not allow `NULL`, while a unique key allows one `NULL` and enforces uniqueness.

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Email NVARCHAR(100) UNIQUE
);
```

---

### Conclusion

These 50 advanced SQL questions and MSSQL examples provide a comprehensive overview of key SQL concepts and features that are commonly tested in technical interviews. Understanding these concepts and mastering their application will help you tackle advanced SQL challenges effectively.
