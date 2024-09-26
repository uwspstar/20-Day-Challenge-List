### 1. **What is the difference between DBMS and RDBMS?**
- **DBMS** (Database Management System) manages databases. It does not enforce relationships between tables.
- **RDBMS** (Relational Database Management System) is an advanced DBMS that enforces relationships and allows complex queries using SQL.
  
| Feature          | DBMS               | RDBMS               |
|------------------|--------------------|---------------------|
| Data Structure   | Unstructured        | Structured (Tables) |
| Relationships    | No support          | Supports relations  |
| Normalization    | Optional            | Follows normal forms|

---

### 2. **What is a Constraint in SQL? What are its types?**

A **constraint** is a rule applied to a column to enforce data integrity.  
Types:
- **NOT NULL**: Ensures a column cannot have NULL values.
- **UNIQUE**: Ensures all values in a column are different.
- **PRIMARY KEY**: A combination of NOT NULL and UNIQUE. Uniquely identifies a row.
- **FOREIGN KEY**: Enforces a link between two tables.
- **CHECK**: Ensures a condition is met.
- **DEFAULT**: Assigns a default value if none is provided.

```sql
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT CHECK (age >= 18),
    gender CHAR(1) DEFAULT 'M'
);
```

---

### 3. **What is the difference between Primary Key and Unique Key?**
- **Primary Key**: Uniquely identifies a record. Only one primary key per table, cannot be NULL.
- **Unique Key**: Ensures all values in a column are unique. Multiple unique keys allowed, can have NULL values.

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

---

### 4. **What are Triggers and types of triggers?**

A **trigger** is a set of SQL commands that automatically executes when certain events occur.  
Types:
- **BEFORE INSERT**: Executes before data is inserted.
- **AFTER INSERT**: Executes after data is inserted.
- **BEFORE UPDATE**: Executes before data is updated.
- **AFTER UPDATE**: Executes after data is updated.
  
```sql
CREATE TRIGGER update_salary
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    UPDATE audit_log SET updated_at = NOW() WHERE employee_id = NEW.emp_id;
END;
```

---

### [5. **What is a View?**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/SQL/SQL%20Interview%20Questions/View.md)

A **view** is a virtual table based on the result set of an SQL query. It allows for abstracting complex queries into simpler structures.

```sql
CREATE VIEW emp_salaries AS
SELECT emp_id, first_name, salary
FROM employees
WHERE salary > 5000;
```

---

### [6. **What is the difference between Having clause and Where clause?**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/SQL/SQL%20Interview%20Questions/HAVING%20vs%20WHERE.md)
- **WHERE**: Filters records before grouping (used with SELECT statements).
- **HAVING**: Filters records after grouping (used with GROUP BY).

```sql
SELECT department, COUNT(*)
FROM employees
WHERE active = 1
GROUP BY department
HAVING COUNT(*) > 5;
```

---

### 7. **What is Sub query or Nested query or Inner query in SQL?**

A **subquery** is a query within another query, used to perform operations based on the result of another query.

```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

---

### 8. **What is Auto Increment/ Identity column in SQL Server?**

An **Identity column** in SQL Server automatically generates unique values for a column (often used for primary keys).

```sql
CREATE TABLE students (
    id INT IDENTITY(1,1),
    name VARCHAR(50),
    age INT
);
```

---

### 9. **What are Joins in SQL?**

A **JOIN** is used to combine rows from two or more tables based on a related column.

---

### 10. **What are the types of Joins in SQL Server?**

- **INNER JOIN**: Returns only matching records.
- **LEFT JOIN**: Returns all records from the left table, and matching records from the right.
- **RIGHT JOIN**: Returns all records from the right table, and matching records from the left.
- **FULL OUTER JOIN**: Returns all records when there is a match in either table.

```sql
SELECT e.emp_id, e.name, d.department
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

---

### 11. **What is Self-Join?**

A **Self-Join** is a regular join, but the table is joined with itself.

```sql
SELECT a.name AS Employee, b.name AS Manager
FROM employees a, employees b
WHERE a.manager_id = b.emp_id;
```

---

### 12. **Write a SQL query to fetch all the Employees who are also Managers.**

```sql
SELECT DISTINCT e.name
FROM employees e
INNER JOIN employees m ON e.emp_id = m.manager_id;
```

---

### 13. **What are Indexes in SQL Server?**

An **Index** speeds up the retrieval of rows from the table. It works like a pointer to data in a table.

---

### 14. **What is Clustered index?**

A **Clustered Index** sorts the physical data rows in the table. Only one clustered index per table.

---

### 15. **What is Non-Clustered index?**

A **Non-Clustered Index** creates a logical order and uses pointers to point to the physical data.

```sql
CREATE INDEX idx_name
ON employees(name);
```

---

### [16. **What is the difference between Clustered and Non-Clustered index?**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/SQL/SQL%20Interview%20Questions/Clustered%20vs.%20Non-Clustered%20Index.md)

| Clustered Index           | Non-Clustered Index             |
|---------------------------|---------------------------------|
| Alters physical order of data | Does not alter physical order |
| One per table              | Multiple per table             |

---

### 17. **How to create Clustered and Non-Clustered index in a table?**

```sql
-- Clustered Index
CREATE CLUSTERED INDEX idx_emp_id
ON employees(emp_id);

-- Non-Clustered Index
CREATE NONCLUSTERED INDEX idx_name
ON employees(name);
```

---

### 18. **In which column will you apply the indexing to optimize this query?**

```sql
SELECT id, class FROM student WHERE name = 'happy';
```
- **Answer**: Apply indexing on the `name` column as it is used in the `WHERE` clause.

---

### 19. **What is the difference between Stored Procedure and Functions (at least 3)?**

| Feature                   | Stored Procedure                     | Function                        |
|---------------------------|--------------------------------------|---------------------------------|
| Return Type               | Can return multiple values           | Returns a single value          |
| Use of Transactions       | Can use transactions                 | Cannot use transactions         |
| Call in SELECT            | Cannot be called in SELECT statement | Can be called in SELECT         |

---

### 20. **How to optimize a Stored Procedure or SQL Query?**

- Use **Indexes**.
- Avoid **SELECT \***.
- Use **JOINs** instead of subqueries.
- Use **query hints** if needed.

---

### 21. **What is a Cursor? Why avoid them?**

A **Cursor** is used to iterate over rows in a result set. Cursors should be avoided as they are slow and memory-intensive. Instead, use set-based operations.

---

### [22. **What is the difference between `scope_identity` and `@@identity`?**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/SQL/SQL%20Interview%20Questions/SCOPE_IDENTITY()%20vs%20%40%40IDENTITY.md)

- **`@@identity`**: Returns the last inserted identity value, regardless of the scope.
- **`scope_identity`**: Returns the last inserted identity value within the current scope.

---

### 23. **What is CTE in SQL Server?**

A **CTE** (Common Table Expression) is a temporary result set that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.

```sql
WITH EmployeeCTE AS (
    SELECT emp_id, name
    FROM employees
)
SELECT * FROM EmployeeCTE;
```

---

### [24. **What is the difference between Delete, Truncate and Drop commands?**]()

| Command   | Action                                   | Rollback | Affects Structure |
|-----------|------------------------------------------|----------|-------------------|
| **DELETE**| Deletes rows one by one                  | Yes      | No                |
| **TRUNCATE**| Deletes all rows                       | No       | No                |
| **DROP**  | Removes entire table or database         | No       | Yes               |

---

### 25. **How to get the Nth highest salary of an employee?**

```sql
SELECT DISTINCT salary
FROM employees e1
WHERE N = (SELECT COUNT(DISTINCT salary) FROM employees e2 WHERE e2.salary > e1.salary);
```

---

### [26. **(Bonus) What are ACID properties?**]()

- **Atomicity**: Transaction is all or nothing.
- **Consistency**: Data must remain consistent.
- **Isolation**: Transactions occur independently.
- **Durability**: Data persists after transaction.

---

### 27. **(Bonus) What are Magic Tables in SQL Server?**

**Magic Tables** are the special tables (`INSERTED`, `DELETED`) used within triggers to store pre and post change data during `INSERT`, `UPDATE`, and `DELETE` operations.

---

Here’s a detailed answer to each question with MSSQL code examples:

---

### 1. **Explain normalization?**

**Normalization** is the process of organizing data to minimize redundancy.

- **1NF**: Eliminate duplicate columns.
- **2NF**: Ensure that non-key columns depend on the entire primary key.
- **3NF**: Ensure non-key columns depend only on the primary key.

---

### 2. **How to implement normalization?**

**Example:**

Before Normalization:

```sql
CREATE TABLE Orders (
    OrderID INT, 
    CustomerName NVARCHAR(50),
    ProductName NVARCHAR(50),
    Price DECIMAL(10, 2)
);
```

After 3NF:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName NVARCHAR(50)
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName NVARCHAR(50),
    Price DECIMAL(10, 2)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT FOREIGN KEY REFERENCES Customers(CustomerID),
    ProductID INT FOREIGN KEY REFERENCES Products(ProductID)
);
```

---

### 3. **What is denormalization?**

**Denormalization** is the process of adding redundancy to improve read performance at the cost of increased write operations.

**Example**:

```sql
CREATE TABLE OrdersWithCustomerInfo (
    OrderID INT, 
    CustomerName NVARCHAR(50),
    ProductID INT,
    Price DECIMAL(10, 2)
);
```

---

### [4. **Explain OLTP vs OLAP?**]()

- **OLTP (Online Transaction Processing)**: Focuses on managing transaction-oriented applications (e.g., banking systems).
- **OLAP (Online Analytical Processing)**: Focuses on complex queries for data analysis (e.g., business reporting).

---

### 5. **Explain 1st, 2nd, and 3rd Normal form?**

- **1NF**: Remove repeating groups.
- **2NF**: Remove partial dependency (i.e., each column should depend on the whole primary key).
- **3NF**: Remove transitive dependency (i.e., each non-primary column should depend only on the primary key).

---

### 6. **Primary Key vs Unique Key?**

| Feature            | Primary Key                     | Unique Key                      |
|--------------------|----------------------------------|----------------------------------|
| Uniqueness         | Must be unique                   | Must be unique                  |
| Nullability        | Cannot contain NULL              | Can contain one NULL            |

---

### 7. **Differentiate between Char vs Varchar?**

| Feature            | Char                             | Varchar                         |
|--------------------|----------------------------------|----------------------------------|
| Fixed/Variable     | Fixed-length                     | Variable-length                 |
| Storage Size       | Always uses defined length       | Uses actual data size           |

---

### 8. **Differentiate between Char vs NChar?**

| Feature            | Char                             | NChar                           |
|--------------------|----------------------------------|----------------------------------|
| Character Set      | ASCII                            | Unicode                         |
| Storage Size       | 1 byte per character             | 2 bytes per character           |

---

### 9. **What’s the size of Char vs NChar?**

- **Char**: 1 byte per character.
- **NChar**: 2 bytes per character.

---

### 10. **What is the use of Index?**

Indexes are used to improve query performance by allowing faster retrieval of data.

---

### 11. **How does it make search faster?**

Indexes use B-trees or similar structures, allowing quick search, insertion, and deletion of records.

**Example**:

```sql
CREATE INDEX idx_Name ON Employees(Name);
```

---

### 12. **What are the two types of Indexes?**

- **Clustered Index**
- **Non-Clustered Index**

---

### 13. **Clustered vs Non-Clustered index?**

| Feature            | Clustered Index                   | Non-Clustered Index               |
|--------------------|------------------------------------|-----------------------------------|
| Data organization  | Reorganizes the actual table data  | Stores separately from data       |
| Number per table   | Only one allowed                   | Multiple allowed                  |

---

### 14. **Function vs Stored Procedures?**

| Feature              | Function                           | Stored Procedure                  |
|----------------------|-------------------------------------|-----------------------------------|
| Return type          | Returns a single value              | Can return multiple values        |
| Can use in SELECT    | Yes                                 | No                                |

---

### 15. **What are triggers and why do you need it?**

A **trigger** is a stored procedure that automatically runs when certain events occur on a table.

**Example**:

```sql
CREATE TRIGGER trgAfterInsert 
ON Employees
AFTER INSERT 
AS 
BEGIN 
    PRINT 'New row inserted';
END;
```

---

### 16. **What are types of triggers?**

- **AFTER Trigger**
- **INSTEAD OF Trigger**

---

### 17. **Differentiate between After trigger vs Instead Of?**

- **AFTER**: Executes after the triggering event.
- **INSTEAD OF**: Executes instead of the triggering event.

---

### 18. **What is need of Identity?**

An **identity** column generates unique numbers automatically.

**Example**:

```sql
CREATE TABLE Orders (
    OrderID INT IDENTITY(1,1),
    ProductName NVARCHAR(50)
);
```

---

### 19. **Explain transactions and how to implement it?**

A **transaction** is a unit of work that is either fully completed or fully rolled back.

**Example**:

```sql
BEGIN TRANSACTION;
    INSERT INTO Orders (ProductName) VALUES ('Product A');
COMMIT TRANSACTION;
```

---

### 20. **What are inner joins?**

An **inner join** returns rows that have matching values in both tables.

**Example**:

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
INNER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 21. **Explain Left join?**

A **left join** returns all rows from the left table and matching rows from the right table.

**Example**:

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
LEFT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 22. **Explain Right join?**

A **right join** returns all rows from the right table and matching rows from the left table.

**Example**:

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
RIGHT JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 23. **Explain Full outer joins?**

A **full outer join** returns all rows when there is a match in either table.

**Example**:

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
FULL OUTER JOIN Departments d ON e.DepartmentID = d.DepartmentID;
```

---

### 24. **Explain Cross joins?**

A **cross join** returns the Cartesian product of the two tables.

**Example**:

```sql
SELECT e.Name, d.DepartmentName
FROM Employees e
CROSS JOIN Departments d;
```

---
