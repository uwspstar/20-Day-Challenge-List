The `CASE WHEN ... THEN ... END` statement in MSSQL allows for conditional logic within a query. It works similarly to the `if-else` logic in programming languages, enabling you to return different values based on conditions.

### **语法**

```sql
CASE 
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE resultN
END
```

- **condition1, condition2, ...**：这些是逻辑条件。
- **result1, result2, ...**：条件为 `TRUE` 时返回的值或表达式。
- **ELSE resultN**：如果没有满足的条件时返回的默认值（可选）。

### **示例 1：使用 `CASE` 对数据进行分类**

假设您有一个名为 `Employees` 的表，包含 `Salary` 列。您想按工资等级对员工进行分类：

```sql
SELECT 
    EmployeeName,
    Salary,
    CASE 
        WHEN Salary > 100000 THEN '高薪'
        WHEN Salary BETWEEN 50000 AND 100000 THEN '中等薪水'
        ELSE '低薪'
    END AS SalaryCategory
FROM Employees;
```

**解释**：
- 如果员工的工资超过 100,000，他们将被归类为 "高薪"。
- 如果工资在 50,000 到 100,000 之间，他们将被归类为 "中等薪水"。
- 否则，他们将被归类为 "低薪"。

**输出**:

| EmployeeName | Salary  | SalaryCategory |
|--------------|---------|----------------|
| John Doe     | 120000  | 高薪           |
| Jane Smith   | 75000   | 中等薪水        |
| Tom Clark    | 40000   | 低薪           |

### **示例 2：在 `UPDATE` 语句中使用 `CASE`**

您还可以在 `UPDATE` 查询中使用 `CASE` 来有条件地修改数据。例如，您想根据当前工资加薪：

```sql
UPDATE Employees
SET Salary = CASE 
                WHEN Salary < 50000 THEN Salary * 1.1
                WHEN Salary BETWEEN 50000 AND 100000 THEN Salary * 1.05
                ELSE Salary * 1.02
             END;
```

**解释**：
- 如果工资少于 50,000，工资增加 10%。
- 如果工资在 50,000 到 100,000 之间，工资增加 5%。
- 工资超过 100,000 的员工加薪 2%。

### **示例 3：结合聚合函数使用 `CASE`**

在聚合查询中，您可以使用 `CASE` 根据条件对数据进行分组或过滤。例如，统计不同工资等级的员工人数：

```sql
SELECT 
    COUNT(CASE WHEN Salary > 100000 THEN 1 END) AS 高薪人数,
    COUNT(CASE WHEN Salary BETWEEN 50000 AND 100000 THEN 1 END) AS 中等薪水人数,
    COUNT(CASE WHEN Salary < 50000 THEN 1 END) AS 低薪人数
FROM Employees;
```

**输出**:

| 高薪人数 | 中等薪水人数 | 低薪人数 |
|---------|--------------|----------|
| 3       | 5            | 2        |

### **警告**

- 如果没有满足任何 `WHEN` 条件且没有指定 `ELSE`，则 `CASE` 表达式将返回 `NULL`。
- 确保您的 `CASE` 表达式处理所有可能的情况，以避免意外结果。

---

This template provides a thorough understanding of the `CASE` statement usage in MSSQL. Let me know if you need further clarification!
