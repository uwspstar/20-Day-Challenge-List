### **Database Performance Optimization and Connection Management Standards**

#### **Purpose**
This document outlines standard practices for database performance optimization, connection management, and deadlock handling using stored procedures to enhance efficiency, security, and maintainability.

---

### **Standard Practices with C# and Stored Procedure Implementation Examples**

#### **1. SQL Deadlock Handling with Stored Procedures**

**Overview**: Implement strategies to detect, manage, and resolve SQL deadlocks using stored procedures, minimizing impact on application performance.

- **Avoid Long-Running Transactions**
  - **SQL Stored Procedure Example**:
    ```sql
    CREATE PROCEDURE UpdateOrderStatus
    @OrderID INT,
    @Status NVARCHAR(20)
    AS
    BEGIN
        BEGIN TRANSACTION;
        BEGIN TRY
            UPDATE Orders SET Status = @Status WHERE OrderID = @OrderID;
            COMMIT TRANSACTION;
        END TRY
        BEGIN CATCH
            ROLLBACK TRANSACTION;
            -- Log or handle the error
        END CATCH;
    END;
    ```

  - **C# Example to Call the Stored Procedure**:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                using (SqlCommand cmd = new SqlCommand("UpdateOrderStatus", conn))
                {
                    cmd.CommandType = System.Data.CommandType.StoredProcedure;
                    cmd.Parameters.AddWithValue("@OrderID", 123);
                    cmd.Parameters.AddWithValue("@Status", "Shipped");

                    try
                    {
                        cmd.ExecuteNonQuery();
                        Console.WriteLine("Order status updated successfully.");
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine($"Error updating order status: {ex.Message}");
                    }
                }
            }
        }
    }
    ```

- **Use Retry Logic with Exponential Backoff**
  - **C# Example for Calling Stored Procedure with Retry Logic**:
    ```csharp
    using System;
    using System.Data.SqlClient;
    using System.Threading;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            int retryCount = 3;

            for (int i = 0; i < retryCount; i++)
            {
                try
                {
                    using (SqlConnection conn = new SqlConnection(connectionString))
                    {
                        conn.Open();
                        using (SqlCommand cmd = new SqlCommand("UpdateOrderStatus", conn))
                        {
                            cmd.CommandType = System.Data.CommandType.StoredProcedure;
                            cmd.Parameters.AddWithValue("@OrderID", 1);
                            cmd.Parameters.AddWithValue("@Status", "Pending");

                            cmd.ExecuteNonQuery();
                            Console.WriteLine("Order status updated successfully.");
                            break;  // Exit if successful
                        }
                    }
                }
                catch (SqlException ex) when (ex.Number == 1205)  // Deadlock error code
                {
                    Console.WriteLine("Deadlock detected. Retrying...");
                    Thread.Sleep((int)Math.Pow(2, i) * 1000);  // Exponential backoff
                }
            }
        }
    }
    ```

#### **2. SQL Timeout Adjustment with Stored Procedures**

**Overview**: Use stored procedures to handle SQL command execution and optimize timeout settings, preventing long-running queries from affecting performance.

- **SQL Stored Procedure Example for Complex Queries**:
  ```sql
  CREATE PROCEDURE GetCustomerOrders
  @CustomerID INT
  AS
  BEGIN
      SELECT * FROM Orders WHERE CustomerID = @CustomerID;
  END;
  ```

- **C# Example to Call the Stored Procedure**:
  ```csharp
  using System;
  using System.Data.SqlClient;

  class Program
  {
      static void Main()
      {
          string connectionString = "your_connection_string";
          using (SqlConnection conn = new SqlConnection(connectionString))
          {
              conn.Open();
              using (SqlCommand cmd = new SqlCommand("GetCustomerOrders", conn))
              {
                  cmd.CommandType = System.Data.CommandType.StoredProcedure;
                  cmd.Parameters.AddWithValue("@CustomerID", 123);
                  cmd.CommandTimeout = 120;  // Set timeout to 120 seconds

                  using (SqlDataReader reader = cmd.ExecuteReader())
                  {
                      while (reader.Read())
                      {
                          Console.WriteLine(reader["OrderID"]);
                      }
                  }
              }
          }
      }
  }
  ```

- **Use Parameterized Stored Procedures**:
  - **C# Example**: Call a stored procedure with parameterized input to avoid SQL injection and optimize execution:
    ```csharp
    using (SqlCommand cmd = new SqlCommand("GetCustomerOrders", conn))
    {
        cmd.CommandType = System.Data.CommandType.StoredProcedure;
        cmd.Parameters.AddWithValue("@CustomerID", 123);
        cmd.CommandTimeout = 120;  // Set appropriate timeout

        using (SqlDataReader reader = cmd.ExecuteReader())
        {
            while (reader.Read())
            {
                Console.WriteLine(reader["OrderID"]);
            }
        }
    }
    ```

#### **3. Connection Pooling Configuration with Stored Procedures**

**Overview**: Configure and manage connection pooling effectively to optimize database interactions and reduce overhead, using stored procedures for database operations.

- **SQL Stored Procedure Example for Counting Orders**:
  ```sql
  CREATE PROCEDURE GetOrderCount
  AS
  BEGIN
      SELECT COUNT(*) AS OrderCount FROM Orders;
  END;
  ```

- **C# Example to Call the Stored Procedure with Connection Pooling**:
  ```csharp
  string connectionString = "Server=myServer;Database=myDB;User Id=myUsername;Password=myPassword;" +
                            "Pooling=True;Min Pool Size=5;Max Pool Size=100;";

  using (SqlConnection conn = new SqlConnection(connectionString))
  {
      conn.Open();
      using (SqlCommand cmd = new SqlCommand("GetOrderCount", conn))
      {
          cmd.CommandType = System.Data.CommandType.StoredProcedure;
          int orderCount = (int)cmd.ExecuteScalar();
          Console.WriteLine($"Total Orders: {orderCount}");
      }
  }
  ```

- **Implement Connection Resiliency with Stored Procedures**:
  - **C# Example**: Add retry logic for transient failures when calling a stored procedure:
    ```csharp
    int retryCount = 3;
    for (int i = 0; i < retryCount; i++)
    {
        try
        {
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                using (SqlCommand cmd = new SqlCommand("GetOrderCount", conn))
                {
                    cmd.CommandType = System.Data.CommandType.StoredProcedure;
                    int orderCount = (int)cmd.ExecuteScalar();
                    Console.WriteLine($"Total Orders: {orderCount}");
                    break;  // Exit if successful
                }
            }
        }
        catch (SqlException ex)
        {
            Console.WriteLine($"Transient error detected: {ex.Message}. Retrying...");
            Thread.Sleep(2000);  // Wait before retrying
        }
    }
    ```

#### **4. Identifying and Managing Open Connections with Stored Procedures**

**Overview**: Properly manage database connections by using stored procedures to prevent leaks, optimize resource usage, and maintain system stability.

- **SQL Stored Procedure Example for Retrieving Active Sessions**:
  ```sql
  CREATE PROCEDURE GetActiveSessions
  AS
  BEGIN
      SELECT session_id, login_name, host_name, program_name, status
      FROM sys.dm_exec_sessions
      WHERE status = 'running';
  END;
  ```

- **C# Example to Call the Stored Procedure for Session Tracking**:
  ```csharp
  using System.Data.SqlClient;

  class Program
  {
      static void Main()
      {
          string connectionString = "your_connection_string";
          using (SqlConnection conn = new SqlConnection(connectionString))
          {
              conn.Open();
              using (SqlCommand cmd = new SqlCommand("GetActiveSessions", conn))
              {
                  cmd.CommandType = System.Data.CommandType.StoredProcedure;
                  using (SqlDataReader reader = cmd.ExecuteReader())
                  {
                      while (reader.Read())
                      {
                          Console.WriteLine($"Session ID: {reader["session_id"]}, " +
                                            $"Login: {reader["login_name"]}, " +
                                            $"Program: {reader["program_name"]}");
                      }
                  }
              }
          }
      }
  }
  ```

---

### **Conclusion**

By using stored procedures instead of inline queries, the team can achieve better performance, security, and maintainability in database interactions. These examples demonstrate how stored procedures should be integrated into the application code, optimizing database interactions and adhering to best practices.

--- 

Here's a version of the team standard with C# examples demonstrating the implementation of each best practice for database performance and connection management.

---

### **Database Performance Optimization and Connection Management Standards**

#### **Purpose**
This document establishes the standard practices for database performance optimization, connection management, and deadlock handling. It guides developers to enhance the efficiency, reliability, and scalability of applications interacting with SQL Server databases.

---

### **Standard Practices with C# Implementation Examples**

#### **1. SQL Deadlock Handling**

**Overview**: Implement strategies to detect, manage, and resolve SQL deadlocks, minimizing impact on application performance.

- **Avoid Long-Running Transactions**
  - **C# Example**: Keep transaction scope minimal by placing only necessary operations inside the transaction block:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                using (SqlTransaction transaction = conn.BeginTransaction())
                {
                    try
                    {
                        SqlCommand cmd = new SqlCommand("UPDATE Orders SET Status = 'Shipped' WHERE OrderID = 123", conn, transaction);
                        cmd.ExecuteNonQuery();
                        transaction.Commit();
                        Console.WriteLine("Transaction committed.");
                    }
                    catch (Exception ex)
                    {
                        transaction.Rollback();
                        Console.WriteLine($"Transaction rolled back: {ex.Message}");
                    }
                }
            }
        }
    }
    ```

- **Use Retry Logic with Exponential Backoff for Deadlocks**
  - **C# Example**: Implement retry logic with exponential backoff to handle deadlocks:
    ```csharp
    using System;
    using System.Data.SqlClient;
    using System.Threading;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            int retryCount = 3;

            for (int i = 0; i < retryCount; i++)
            {
                try
                {
                    using (SqlConnection conn = new SqlConnection(connectionString))
                    {
                        conn.Open();
                        SqlCommand cmd = new SqlCommand("UPDATE Orders SET Status = 'Pending' WHERE OrderID = 1", conn);
                        cmd.ExecuteNonQuery();
                        Console.WriteLine("Update successful");
                        break;  // Exit loop if successful
                    }
                }
                catch (SqlException ex) when (ex.Number == 1205)  // SQL error code for deadlock
                {
                    Console.WriteLine("Deadlock detected. Retrying...");
                    Thread.Sleep((int)Math.Pow(2, i) * 1000);  // Exponential backoff
                }
            }
        }
    }
    ```

#### **2. SQL Timeout Adjustment**

**Overview**: Set optimal SQL command timeouts to prevent long-running queries from affecting system performance while ensuring necessary operations complete successfully.

- **Use Parameterized Queries**
  - **C# Example**: Use parameterized queries to prevent SQL injection and optimize query execution:
    ```csharp
    using System;
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand("SELECT * FROM Customers WHERE Name = @name", conn);
                cmd.Parameters.AddWithValue("@name", "Smith");
                cmd.CommandTimeout = 120;  // Set timeout to 120 seconds

                using (SqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine(reader["Name"]);
                    }
                }
            }
        }
    }
    ```

- **Optimize Query Execution by Splitting Complex Queries**
  - **C# Example**: Use temporary tables to simplify and optimize complex queries:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "SELECT * INTO #TempOrders FROM Orders WHERE OrderDate > '2023-01-01'; " +
                    "SELECT * FROM #TempOrders WHERE Status = 'Pending';", conn);
                cmd.CommandTimeout = 120;  // Set command timeout

                using (SqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine(reader["OrderID"]);
                    }
                }
            }
        }
    }
    ```

#### **3. Connection Pooling Configuration**

**Overview**: Configure and manage connection pooling effectively to optimize database interactions and reduce overhead.

- **Set Appropriate Pool Sizes**
  - **C# Example**: Configure connection pooling in the connection string:
    ```csharp
    string connectionString = "Server=myServer;Database=myDB;User Id=myUsername;Password=myPassword;" +
                              "Pooling=True;Min Pool Size=5;Max Pool Size=100;";

    using (SqlConnection conn = new SqlConnection(connectionString))
    {
        conn.Open();
        SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM Orders", conn);
        int count = (int)cmd.ExecuteScalar();
        Console.WriteLine($"Total Orders: {count}");
    }
    ```

- **Implement Connection Resiliency**
  - **C# Example**: Add retry logic to manage transient connection failures:
    ```csharp
    int retryCount = 3;
    for (int i = 0; i < retryCount; i++)
    {
        try
        {
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM Customers", conn);
                int count = (int)cmd.ExecuteScalar();
                Console.WriteLine($"Total Customers: {count}");
                break;  // Exit if successful
            }
        }
        catch (SqlException ex)
        {
            Console.WriteLine($"Transient error detected: {ex.Message}. Retrying...");
            Thread.Sleep(2000);  // Wait before retrying
        }
    }
    ```

#### **4. Identifying and Managing Open Connections**

**Overview**: Properly manage database connections to prevent leaks, optimize resource usage, and maintain system stability.

- **Ensure Proper Closing of Connections**
  - **C# Example**: Use `using` statements to automatically close connections:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand("SELECT * FROM Orders WHERE Status = 'Shipped'", conn);

                using (SqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine(reader["OrderID"]);
                    }
                }
            }  // Connection is closed here automatically
        }
    }
    ```

- **Track Active Connections Regularly**
  - **C# Example**: Use DMVs to audit and monitor active connections from the application:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "SELECT session_id, login_name, host_name, program_name, status " +
                    "FROM sys.dm_exec_sessions WHERE status = 'running';", conn);

                using (SqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine($"Session ID: {reader["session_id"]}, " +
                                          $"Login: {reader["login_name"]}, " +
                                          $"Program: {reader["program_name"]}");
                    }
                }
            }
        }
    }
    ```

#### **5. Advanced Caching Strategies**

**Overview**: Implement caching strategies to reduce database load and improve response times.

- **Use Distributed Caching (e.g., Redis)**
  - **C# Example**: Implement Redis caching for frequently accessed data:
    ```csharp
    using StackExchange.Redis;

    class Program
    {
        static void Main()
        {
            var cache = ConnectionMultiplexer.Connect("localhost").GetDatabase();

            // Set cache value
            cache.StringSet("cachedDataKey", "CachedData");

            // Get cache value
            string cachedValue = cache.StringGet("cachedDataKey");
            Console.WriteLine($"Cached Value: {cachedValue}");
        }
    }
    ```

### **6. Query Store Analysis** (continued)

**Overview**: Use Query Store to track query performance and identify issues for optimization.

- **Analyze High-Duration Queries** 
  - **C# Example**: Use SQL queries to retrieve query performance metrics from Query Store:
    ```csharp
    using System;
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "SELECT TOP 5 query_id, avg_duration, last_execution_time " +
                    "FROM sys.query_store_plan " +
                    "WHERE avg_duration > 1000 " +  // Filter queries with high average duration
                    "ORDER BY avg_duration DESC;", conn);

                using (SqlDataReader reader = cmd.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine($"Query ID: {reader["query_id"]}, " +
                                          $"Avg Duration: {reader["avg_duration"]}, " +
                                          $"Last Exec Time: {reader["last_execution_time"]}");
                    }
                }
            }
        }
    }
    ```

#### **7. Regular Database Maintenance**

**Overview**: Routine database maintenance ensures optimal performance and reduces fragmentation.

- **Rebuild Indexes and Update Statistics**
  - **C# Example**: Execute SQL commands for index rebuilding and statistics updates:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand("ALTER INDEX ALL ON Orders REBUILD; EXEC sp_updatestats;", conn);
                cmd.CommandTimeout = 300;  // Set a higher timeout for maintenance tasks
                cmd.ExecuteNonQuery();
                Console.WriteLine("Indexes rebuilt and statistics updated.");
            }
        }
    }
    ```

#### **8. Compression for Large Tables**

**Overview**: Use data compression to improve I/O performance for large tables.

- **Enable Data Compression**
  - **C# Example**: Use SQL commands to apply row or page compression to tables:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "ALTER TABLE LargeOrders REBUILD WITH (DATA_COMPRESSION = PAGE);", conn);
                cmd.ExecuteNonQuery();
                Console.WriteLine("Table compression applied.");
            }
        }
    }
    ```

#### **9. Use of Resource Governor for Workload Management**

**Overview**: Resource Governor manages SQL Server workloads by controlling resource consumption based on priorities.

- **Implement Resource Governor**
  - **C# Example**: Use SQL commands to configure resource pools and manage workload resources:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "CREATE RESOURCE POOL FastPool WITH (MAX_CPU_PERCENT=50);" +
                    "ALTER RESOURCE GOVERNOR RECONFIGURE;", conn);
                cmd.ExecuteNonQuery();
                Console.WriteLine("Resource Governor configured.");
            }
        }
    }
    ```

#### **10. In-Memory OLTP for High-Concurrency Workloads**

**Overview**: Use In-Memory OLTP (Hekaton) to improve performance for high-concurrency transactions.

- **Create In-Memory Tables**
  - **C# Example**: Use SQL commands to create in-memory tables for faster transaction processing:
    ```csharp
    using System.Data.SqlClient;

    class Program
    {
        static void Main()
        {
            string connectionString = "your_connection_string";
            using (SqlConnection conn = new SqlConnection(connectionString))
            {
                conn.Open();
                SqlCommand cmd = new SqlCommand(
                    "CREATE TABLE InMemoryOrders " +
                    "(OrderID INT PRIMARY KEY NONCLUSTERED, OrderDate DATETIME) " +
                    "WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY);", conn);
                cmd.ExecuteNonQuery();
                Console.WriteLine("In-Memory table created.");
            }
        }
    }
    ```

#### **11. Implementing Advanced Caching Strategies**

**Overview**: Implement caching strategies to offload frequently accessed data from the database and improve response times.

- **Implement Redis Caching**
  - **C# Example**: Use Redis for distributed caching of frequently accessed data:
    ```csharp
    using StackExchange.Redis;

    class Program
    {
        static void Main()
        {
            var cache = ConnectionMultiplexer.Connect("localhost").GetDatabase();

            // Set a value in cache
            cache.StringSet("OrderCount", "500");

            // Retrieve the value from cache
            string orderCount = cache.StringGet("OrderCount");
            Console.WriteLine($"Cached Order Count: {orderCount}");
        }
    }
    ```

---

### **Conclusion**
By adhering to these standard practices with C# implementation examples, the team can maintain consistent database performance, optimize resource utilization, and build robust, scalable systems. These guidelines ensure that best practices are consistently implemented, improving user satisfaction, reducing downtime, and ensuring efficient operations across all database-driven applications.
                                         
