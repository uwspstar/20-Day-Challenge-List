**为什么不推荐在 C# 代码中直接使用内联 SQL 查询**

将 SQL 查询直接写在 C# 代码中（称为内联查询）可能看起来简单，但在实际开发中，这种方法存在许多问题。以下通过一个对比示例详细说明内联查询的缺点，并解释为什么存储过程是更好的选择。

---

### **内联查询的坏例子**

以下是在 C# 代码中直接使用内联查询的示例：

```csharp
string employeeId = "1 OR 1=1"; // 恶意输入
string query = $"SELECT * FROM Employees WHERE EmployeeID = {employeeId};";

// 使用 ADO.NET 执行查询
using (SqlConnection conn = new SqlConnection("YourConnectionString"))
{
    SqlCommand cmd = new SqlCommand(query, conn);
    conn.Open();
    SqlDataReader reader = cmd.ExecuteReader();

    while (reader.Read())
    {
        Console.WriteLine($"{reader["Name"]} - {reader["Position"]}");
    }
}
```

**问题：**

1. **SQL 注入风险**  
   直接将用户输入插入查询字符串非常危险，攻击者可以通过输入恶意代码（如 `1 OR 1=1`）访问不应访问的数据。

2. **维护困难**  
   如果 SQL 语句散布在多个代码文件中，维护起来会非常麻烦。一旦业务逻辑发生变化，必须逐个定位和修改这些查询。

3. **性能优化困难**  
   数据库无法提前编译和缓存内联查询的执行计划，每次都需要重新解析和优化。

4. **代码混乱**  
   SQL 逻辑混杂在 C# 代码中，导致代码可读性差且不易测试。

---

### **推荐使用存储过程的示例**

将上述逻辑改用存储过程实现：

**存储过程：**
```sql
CREATE PROCEDURE usp_GetEmployeeByID
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;
```

**C# 代码：**
```csharp
using (SqlConnection conn = new SqlConnection("YourConnectionString"))
{
    SqlCommand cmd = new SqlCommand("usp_GetEmployeeByID", conn);
    cmd.CommandType = CommandType.StoredProcedure;

    // 添加参数，防止 SQL 注入
    cmd.Parameters.AddWithValue("@EmployeeID", 1);

    conn.Open();
    SqlDataReader reader = cmd.ExecuteReader();

    while (reader.Read())
    {
        Console.WriteLine($"{reader["Name"]} - {reader["Position"]}");
    }
}
```

---

### **对比与总结**

1. **安全性**  
   - **内联查询：** 存在 SQL 注入风险，攻击者可能通过构造恶意输入破坏数据库。  
   - **存储过程：** 使用参数化查询，防止恶意代码被执行。

2. **性能**  
   - **内联查询：** 每次执行都需要解析和生成执行计划，性能较差。  
   - **存储过程：** 存储过程在创建时编译，执行时直接使用缓存的执行计划，性能更好。

3. **可维护性**  
   - **内联查询：** SQL 散布在代码中，难以集中管理和维护。  
   - **存储过程：** 所有逻辑集中在数据库中，便于统一修改和调试。

4. **复用性**  
   - **内联查询：** 查询逻辑绑定到特定的应用程序中，其他应用无法使用。  
   - **存储过程：** 可以被多个应用程序共享，避免重复开发。

5. **代码清晰度**  
   - **内联查询：** C# 和 SQL 混在一起，代码可读性差。  
   - **存储过程：** 将 SQL 逻辑从代码中剥离，C# 代码更简洁，关注点分离。

---

### **为什么内联查询是一个坏习惯？**

**内联查询的问题根源在于：**
- **安全问题**：不适当的输入处理可能导致数据泄露或损坏。  
- **性能问题**：无法利用数据库优化特性，如执行计划缓存。  
- **开发与运维问题**：代码难以阅读、调试和维护。

---

### **总结建议**

对于任何涉及数据库的操作，**不要将 SQL 查询直接写在 C# 或其他应用程序代码中**。使用存储过程或 ORM（如 Entity Framework）来封装和处理 SQL 逻辑，不仅可以提高安全性和性能，还能减少开发和维护的成本。

作为新手，记住以下要点：
1. 使用存储过程或参数化查询代替内联查询。
2. 保持代码与数据逻辑分离，增强可读性和可维护性。
3. 永远验证和清洗用户输入，确保应用程序的安全性。
