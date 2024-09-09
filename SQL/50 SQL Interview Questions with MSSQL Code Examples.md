### 50 SQL 面试问题及 MSSQL 示例

以下是 50 个高级 SQL 面试问题，每个问题都配有使用 Microsoft SQL Server (MSSQL) 的示例。这些问题涵盖了各种 SQL 概念，例如窗口函数、高级连接、递归查询、事务等。

---

### 1. **什么是公用表表达式 (CTE) 及其使用方法？**

[中文] 公用表表达式 (CTE) 是在单个 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 语句执行范围内定义的临时结果集。CTE 可以是递归的或非递归的。

```sql
WITH EmployeeCTE AS (
    SELECT EmployeeID, ManagerID, FirstName, LastName
    FROM Employees
)
SELECT * 
FROM EmployeeCTE;
```

---

### 2. **解释递归 CTE，并提供一个示例。**

[中文] 递归 CTE 是一个引用自身的 CTE，通常用于返回层级数据。它在遍历树或图形时非常有用。

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

### 3. **如何在 MSSQL 中使用窗口函数？**

[中文] 窗口函数允许您对与当前行相关的一组表行执行计算。

```sql
SELECT EmployeeID, Salary, 
       RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Employees;
```

---

### 4. **什么是 SQL 中的 PIVOT 表？提供一个示例。**

[中文] SQL 中的 PIVOT 操作符允许您将行旋转为列。

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

### 5. **如何在 MSSQL 中使用 UNPIVOT 操作符？**

[中文] UNPIVOT 操作符将列转换为行。

```sql
SELECT Department, SalaryType, Salary
FROM Employees
UNPIVOT (
    Salary FOR SalaryType IN (BaseSalary, Bonus)
) AS UnpivotTable;
```

---

### 6. **如何在 MSSQL 中创建索引视图？**

[中文] 索引视图是具有唯一聚簇索引的视图。这可以提高复杂查询的性能。

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

### 7. **RANK()、DENSE_RANK() 和 ROW_NUMBER() 有什么区别？**

[中文] 这些都是对行进行排名的窗口函数：
- `ROW_NUMBER()` 为每行提供一个唯一编号。
- `RANK()` 在遇到并列时跳过排名。
- `DENSE_RANK()` 不跳过排名。

```sql
SELECT EmployeeID, 
       ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum,
       RANK() OVER (ORDER BY Salary DESC) AS RankNum,
       DENSE_RANK() OVER (ORDER BY Salary DESC) AS DenseRankNum
FROM Employees;
```

---

### 8. **什么是 MSSQL 中的 CROSS APPLY 和 OUTER APPLY？**

[中文] `CROSS APPLY` 类似于内连接，`OUTER APPLY` 类似于左外连接，但用于表值函数。

```sql
SELECT e.EmployeeID, fn.Salary
FROM Employees e
CROSS APPLY fn_GetEmployeeSalary(e.EmployeeID) fn;

SELECT e.EmployeeID, fn.Salary
FROM Employees e
OUTER APPLY fn_GetEmployeeSalary(e.EmployeeID) fn;
```

---

### 9. **如何在 MSSQL 中处理 NULL 值？**

[中文] 使用 `COALESCE()` 或 `ISNULL()` 函数来处理 `NULL` 值。

```sql
SELECT EmployeeID, 
       COALESCE(Salary, 0) AS Salary
FROM Employees;
```

---

### 10. **解释如何在 MSSQL 中使用 MERGE 语句。**

[中文] `MERGE` 语句允许您根据是否满足某个条件执行 `INSERT`、`UPDATE` 或 `DELETE` 操作。

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

### 11. **如何在 MSSQL 中计算列的累积总和？**

[中文] 可以使用 `SUM()` 函数作为窗口函数来计算累积总和。

```sql
SELECT EmployeeID, Salary, 
       SUM(Salary) OVER (ORDER BY EmployeeID) AS RunningTotal
FROM Employees;
```

---

### 12. **什么是窗口聚合函数，它与 GROUP BY 有何不同？**

[中文] 窗口聚合函数允许您在不对结果集进行分组的情况下对行进行聚合计算。

```sql
SELECT EmployeeID, Salary, 
       AVG(Salary) OVER (PARTITION BY Department) AS AvgSalary
FROM Employees;
```

---

### 13. **如何在 SQL 中处理重复数据？**

[中文] 使用 `DISTINCT` 删除重复数据，或使用 `ROW_NUMBER()` 标识并删除重复项。

```sql
WITH CTE AS (
    SELECT EmployeeID, FirstName, LastName, 
           ROW_NUMBER() OVER (PARTITION BY FirstName, LastName ORDER BY EmployeeID) AS RowNum
    FROM Employees
)
DELETE FROM CTE WHERE RowNum > 1;
```

---

### 14. **如何在 MSSQL 中找到第 N 高的薪水？**

[中文] 使用 `OFFSET` 和 `FETCH` 子句来查找第 N 高的薪水。

```sql
SELECT Salary
FROM Employees
ORDER BY Salary DESC
OFFSET 3 ROWS FETCH NEXT 1 ROWS ONLY;  -- 第四高的薪水
```

---

### 15. **什么是相关子查询？提供一个示例。**

[中文] 相关子查询是指在子查询中引用外部查询中的列。

```sql
SELECT e1.EmployeeID, e1.FirstName, e1.Salary
FROM Employees e1
WHERE e1.Salary > (SELECT AVG(e2.Salary) 
                   FROM Employees e2
                   WHERE e2.Department = e1.Department);
```

---

### 16. **如何在 MSSQL 中使用索引优化查询？**

[中文] 索引通过允许更快地访问数据来提高查询性能。

```sql
CREATE NONCLUSTERED INDEX IX_Employees_Salary 
ON Employees (Salary);
```

---

### 17. **解释如何在 MSSQL 中使用触发器。**

[中文] 触发器是当某个事件发生在表上时自动运行的存储过程。

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

### 18. **聚簇索引和非聚簇索引有什么区别？**

[中文] 聚簇索引对表的数据行进行排序并存储，而非聚簇索引为索引创建一个独立的结构。

```sql
CREATE CLUSTERED INDEX IX_Employees_EmployeeID
ON Employees (EmployeeID);

CREATE NONCLUSTERED INDEX IX_Employees_LastName
ON Employees (LastName);
```

---

### 19. **如何在 MSSQL 中执行 FULL OUTER JOIN？**

[中文] `FULL OUTER JOIN` 返回在左表或右表中都有匹配记录的所有记录。

```sql
SELECT e.EmployeeID, d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d
ON e.DepartmentID = d.DepartmentID;
```

---

### 20. **如何在 MSSQL 中处理错误？**

[中文] 可以使用 `TRY...CATCH` 块来处理 MSSQL 中的错误。

```sql
BEGIN TRY
    INSERT INTO Employees (EmployeeID, FirstName) VALUES (1, 'John');
END TRY
BEGIN CATCH
    PRINT ERROR_MESSAGE();
END CATCH;
```

---

### 21. **如何在 MSSQL 中检索当前数据库的名称？**

[中文] 使用 `DB_NAME()` 函数检索当前数据库名称。

```sql
SELECT DB_NAME() AS DatabaseName;
```

---

### 22. **什么是 MSSQL 中的游标？**

[中文] 游标是一个用于逐行检索数据的数据库对象。

```sql
DECLARE EmployeeCursor CURSOR FOR
SELECT EmployeeID,

 FirstName FROM Employees;

OPEN EmployeeCursor;
FETCH NEXT FROM EmployeeCursor;
CLOSE EmployeeCursor;
DEALLOCATE EmployeeCursor;
```

---

### 23. **如何在 MSSQL 中创建临时表？**

[中文] 临时表在会话或事务期间临时存储数据。

```sql
CREATE TABLE #TempEmployee (
    EmployeeID INT,
    FirstName VARCHAR(100)
);

INSERT INTO #TempEmployee (EmployeeID, FirstName)
VALUES (1, 'John');
```

---

### 24. **什么是 MSSQL 中的分区表？**

[中文] 分区将表根据某一列的值拆分为多个部分。

```sql
CREATE PARTITION FUNCTION pfEmployees (INT)
AS RANGE LEFT FOR VALUES (100, 200, 300);
```

---

### 25. **如何在 MSSQL 中实现事务？**

[中文] 事务允许您将一组操作作为单个工作单元执行。

```sql
BEGIN TRANSACTION;

INSERT INTO Employees (EmployeeID, FirstName, LastName) 
VALUES (1, 'John', 'Doe');

COMMIT;
```

---

### 26. **如何在 MSSQL 中使用 ROLLBACK？**

[中文] 如果发生错误，可以使用 `ROLLBACK` 撤销事务。

```sql
BEGIN TRANSACTION;

INSERT INTO Employees (EmployeeID, FirstName) VALUES (1, 'John');

IF @@ERROR <> 0
    ROLLBACK;
ELSE
    COMMIT;
```

---

### 27. **HAVING 和 WHERE 有什么区别？**

[中文] `WHERE` 在聚合之前过滤行，`HAVING` 在聚合之后过滤行。

```sql
SELECT Department, COUNT(EmployeeID)
FROM Employees
GROUP BY Department
HAVING COUNT(EmployeeID) > 10;
```

---

### 28. **如何在 MSSQL 中使用 EXISTS？**

[中文] `EXISTS` 检查子查询中是否存在行。

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

### 29. **如何使用索引优化查询？**

[中文] 在经常使用的列上添加索引以提高查询性能。

```sql
CREATE INDEX IX_Employee_Salary ON Employees (Salary);
```

---

### 30. **INNER JOIN 和 LEFT JOIN 有什么区别？**

[中文] `INNER JOIN` 返回在两个表中具有匹配值的行。`LEFT JOIN` 返回左表中的所有行以及右表中的匹配行。

```sql
SELECT e.EmployeeID, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 31. **如何在 MSSQL 中处理死锁？**

[中文] 通过处理错误和实现重试逻辑来解决死锁。

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

### 32. **如何在 MSSQL 中仅返回前 N 行？**

[中文] 使用 `TOP` 或 `OFFSET-FETCH` 只返回特定数量的行。

```sql
SELECT TOP 10 * FROM Employees;
```

---

### 33. **什么是窗口函数，为什么它们很重要？**

[中文] 窗口函数允许您在不将结果集折叠为组的情况下执行操作。

```sql
SELECT EmployeeID, Salary, 
       AVG(Salary) OVER (PARTITION BY DepartmentID) AS AvgDeptSalary
FROM Employees;
```

---

### 34. **如何在 MSSQL 中检索第二高的薪水？**

[中文] 使用 `DISTINCT` 和 `ORDER BY` 以及 `OFFSET-FETCH`。

```sql
SELECT DISTINCT Salary
FROM Employees
ORDER BY Salary DESC
OFFSET 1 ROWS FETCH NEXT 1 ROWS ONLY;
```

---

### 35. **DELETE 和 TRUNCATE 在 MSSQL 中有什么区别？**

[中文] `DELETE` 一次删除一行，并记录每次删除。`TRUNCATE` 通过释放页面删除所有行，速度更快，但无法回滚。

```sql
DELETE FROM Employees WHERE EmployeeID = 1;
TRUNCATE TABLE Employees;
```

---

### 36. **索引的作用是什么，如何在 MSSQL 中创建索引？**

[中文] 索引用于加速数据检索。

```sql
CREATE INDEX IX_Employee_LastName 
ON Employees (LastName);
```

---

### 37. **什么是计算列，如何在 MSSQL 中创建它？**

[中文] 计算列是一个通过表达式计算的虚拟列。

```sql
ALTER TABLE Employees
ADD FullName AS (FirstName + ' ' + LastName);
```

---

### 38. **`ISNULL()` 和 `COALESCE()` 有什么区别？**

[中文] `ISNULL()` 接受两个参数并返回第一个非空值。`COALESCE()` 可以接受多个参数，并返回列表中第一个非空值。

```sql
SELECT ISNULL(Salary, 0) FROM Employees;
SELECT COALESCE(Salary, Bonus, 0) FROM Employees;
```

---

### 39. **如何在 MSSQL 中创建存储过程？**

[中文] 存储过程是可以重复使用的保存查询。

```sql
CREATE PROCEDURE GetEmployeeDetails
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;
```

---

### 40. **如何在 MSSQL 中使用 CASE 语句？**

[中文] `CASE` 用于在查询中执行条件逻辑。

```sql
SELECT EmployeeID, Salary, 
       CASE 
           WHEN Salary > 50000 THEN 'High'
           ELSE 'Low'
       END AS SalaryCategory
FROM Employees;
```

---

### 41. **如何在 MSSQL 中执行条件聚合？**

[中文] 在聚合函数中使用 `CASE` 来有条件地包含行。

```sql
SELECT Department, 
       SUM(CASE WHEN Salary > 50000 THEN Salary ELSE 0 END) AS HighSalarySum
FROM Employees
GROUP BY Department;
```

---

### 42. **在 MSSQL 中连接字符串时如何处理 NULL 值？**

[中文] 使用 `ISNULL()` 或 `COALESCE()` 函数将 `NULL` 替换为空字符串。

```sql
SELECT FirstName + ' ' + ISNULL(LastName, '') AS FullName FROM Employees;
```

---

### 43. **UNION 和 UNION ALL 有什么区别？**

[中文] `UNION` 删除重复项，`UNION ALL` 保留所有重复项。

```sql
SELECT EmployeeID FROM Employees
UNION
SELECT EmployeeID FROM Salaries;

SELECT EmployeeID FROM Employees
UNION ALL
SELECT EmployeeID FROM Salaries;
```

---

### 44. **如何在 MSSQL 中动态执行 SQL 查询？**

[中文] 使用 `EXEC()` 或 `sp_executesql` 来执行动态 SQL。

```sql
DECLARE @SQL NVARCHAR(MAX) = 'SELECT * FROM Employees';
EXEC (@SQL);
```

---

### 45. **什么是 MSSQL 中的表值函数？**

[中文] 表值函数返回一个表，可以像视图一样在 `SELECT` 语句中使用。

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

### 46. **什么是 MSSQL 中的标量函数？**

[中文] 标量函数返回一个单一值。

```sql
CREATE FUNCTION fn_GetFullName (@FirstName NVARCHAR(100), @LastName NVARCHAR(100))
RETURNS NVARCHAR(200)
AS
BEGIN
    RETURN @FirstName + ' ' + @LastName;
END;
```

---

### 47. **MSSQL 中 CROSS JOIN 的作用是什么？**

[中文] `CROSS JOIN` 返回两个表的笛卡尔积。

```sql
SELECT * 
FROM Employees CROSS JOIN Departments;
```

---

### 48. **在 MSSQL 中，CTE 与子查询相比有什么优势？**

[中文] CTE 使复杂查询更具可读性，并且可以在同一个查询中重复使用。

```sql
WITH EmployeeCTE AS (
    SELECT EmployeeID, FirstName, Salary 
    FROM Employees 
    WHERE Salary > 50000
)
SELECT * FROM EmployeeCTE;
```

---

### 49. **如何在 MSSQL 中重命名表？**

[中文] 使用 `sp_rename` 重命名表。

```sql
EXEC sp_rename 'Employees', 'Staff';
```

---

### 50. **主键与唯一键有什么区别？**

[中文] 主键唯一标识每条记录，并且不允许 `NULL` 值，而唯一键允许一个 `NULL` 值，并强制唯一性。

```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Email NVARCHAR(100) UNIQUE
);
```
