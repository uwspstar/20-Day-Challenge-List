### **简介**

`DATEADD` 是 Microsoft SQL Server 中的一个函数，用于在给定日期上加上指定的时间间隔（如天、月或年）。

### **语法**

```sql
DATEADD(datepart, number, date)
```

### **参数**

- **datepart**：指定要添加值的日期部分。
  - 常用的 `datepart` 值包括：
    - `year`：年
    - `quarter`：季度
    - `month`：月
    - `day`：天
    - `week`：周
    - `hour`：小时
    - `minute`：分钟
    - `second`：秒
- **number**：要添加到日期的数值，可以是正数或负数。
- **date**：开始日期，可以是 `datetime`、`smalldatetime`、`date` 或 `time` 数据类型。

### **示例**

下面是一个将给定日期加 10 天的例子：

```sql
SELECT DATEADD(day, 10, '2024-01-01') AS ResultDate;
```

**输出**：
```
ResultDate
-----------------------
2024-01-11 00:00:00.000
```

### **常见用例**

1. **给日期加天**
   ```sql
   SELECT DATEADD(day, 5, '2024-02-28') AS NewDate;
   ```

2. **给日期加月**
   ```sql
   SELECT DATEADD(month, 2, '2024-02-28') AS NewDate;
   ```

3. **从日期中减去年**
   ```sql
   SELECT DATEADD(year, -1, '2024-02-28') AS NewDate;
   ```

### **实际应用**

在查询基于相对时间的历史数据或未来数据时，`DATEADD` 很有用。例如，要查找最近 30 天内创建的记录：

```sql
SELECT *
FROM Orders
WHERE OrderDate >= DATEADD(day, -30, GETDATE());
```

### **警告**

- 如果日期超出范围，函数可能会返回错误。
- 在月末添加月份时，结果可能会有所不同，具体取决于结果月份中的天数。

### **与其他函数的比较**

| 函数        | 用途                                |
|-------------|-------------------------------------|
| `DATEADD`   | 向日期添加特定时间间隔               |
| `DATEDIFF`  | 返回两个日期之间的差异               |
| `GETDATE()` | 返回当前的日期和时间                 |

### **总结**

`DATEADD` 是 MSSQL 中一个强大的函数，可以帮助您在给定日期上加上特定的时间间隔。

---

Let me know if you need further clarification!
