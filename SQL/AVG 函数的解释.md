### AVG 函数的解释

`AVG` 函数是 SQL 中用于计算数值列的平均值的聚合函数。

---

### **语法**

```sql
SELECT AVG(column_name) FROM table_name;
```

- **column_name**：要计算平均值的列名。
- **table_name**：包含该列的表名。

---

### **示例**

假设我们有一个名为 `Students` 的表，包含 `Score` 列，用于存储学生的分数。我们想要计算所有学生的平均分数：

```sql
SELECT AVG(Score) AS AverageScore
FROM Students;
```

**输出**：
```
AverageScore
------------
85.6
```

这个查询会返回所有学生的平均分数，假设平均值是 85.6。

---

### **用法场景**

1. **计算某列的平均值**
   ```sql
   SELECT AVG(Salary) AS AverageSalary
   FROM Employees;
   ```

   该查询将返回 `Employees` 表中 `Salary` 列的平均工资。

2. **结合 `GROUP BY` 使用**
   ```sql
   SELECT Department, AVG(Salary) AS AverageSalary
   FROM Employees
   GROUP BY Department;
   ```

   该查询将按部门分组，返回每个部门的平均工资。

---

### **警告**

- `AVG` 函数只对数值列有效。如果列包含非数值数据，查询将会报错。
- `NULL` 值不会影响 `AVG` 的计算，`AVG` 函数会自动忽略 `NULL`。

---

### **结论**

`AVG` 是 SQL 中常用的聚合函数之一，用于计算一组数据的平均值。它非常适合用于统计分析，例如计算工资的平均值、成绩的平均分等。

---

Let me know if you need further explanations or examples!
