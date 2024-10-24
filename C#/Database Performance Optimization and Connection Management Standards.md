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

This version emphasizes the use of stored procedures, making the codebase more maintainable and secure. Let me know if you need more modifications!
