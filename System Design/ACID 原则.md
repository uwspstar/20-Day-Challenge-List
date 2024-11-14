### ACID 原则

---

### 1. 原子性 (Atomicity)

原子性意味着事务中的所有操作必须全部成功或全部失败。如果事务中的任何操作失败，则整个事务会回滚，数据库状态不发生变化。

```mermaid
flowchart TD
    Start[开始事务] --> Write1[写入操作 1]
    Write1 --> Write2[写入操作 2]
    Write2 --> Write3[写入操作 3]
    Write3 --> Success[成功提交]
    Write3 --> Failure[发生失败]
    Failure --> Rollback[回滚事务]
    Rollback --> End[事务失败，回到初始状态]
    Success --> End[事务成功，数据提交]
```

### 2. 一致性 (Consistency)

一致性确保在事务执行前后的数据库状态保持一致。事务必须符合数据库的完整性约束，以确保没有任何损坏的数据写入数据库。

```mermaid
flowchart TD
    Start[事务开始] --> CheckRules[检查一致性规则]
    CheckRules -->|符合约束| Execute[执行操作]
    Execute --> CheckConsistency[检查一致性]
    CheckConsistency -->|一致| Commit[提交事务]
    Commit --> End[事务成功完成]
    CheckRules -->|不符合约束| Abort[中止事务]
    Abort --> End[事务失败，状态回滚]
```

### 3. 隔离性 (Isolation)

隔离性确保并发事务之间互不干扰。一个事务的执行不应影响到其他并发事务，保持数据库的独立性。

```mermaid
flowchart TD
    TransactionA[事务 A - 写入操作] --> ExecuteA[执行事务 A]
    TransactionB[事务 B - 读取操作] --> ExecuteB[执行事务 B]
    ExecuteA --> IsolationCheck[隔离检查]
    ExecuteB --> IsolationCheck
    IsolationCheck --> CommitA[事务 A 提交]
    IsolationCheck --> CommitB[事务 B 提交]
    CommitA --> EndA[事务 A 完成]
    CommitB --> EndB[事务 B 完成]
```

### 4. 持久性 (Durability)

持久性意味着一旦事务提交成功，其对数据库的更改将永久保存，即使系统崩溃或断电，数据依然不会丢失。

```mermaid
flowchart TD
    Start[事务开始] --> WriteDB[写入数据库]
    WriteDB --> Commit[提交事务]
    Commit --> Backup[创建备份]
    Backup --> End[事务完成，数据持久化]
    Commit --> FailureCheck[检查系统状态]
    FailureCheck --> Restore[恢复数据]
    Restore --> End[系统恢复，数据不丢失]
```

---

### ACID 原则总结

- **原子性**：事务中的所有操作要么全部成功，要么全部失败。
- **一致性**：事务的执行不会破坏数据库的完整性。
- **隔离性**：并发事务之间互不干扰。
- **持久性**：事务提交后数据持久保存。

这些原则在数据库事务管理中非常重要，确保数据的可靠性和一致性，适用于大部分关系型数据库系统，如 MySQL、PostgreSQL 和 Oracle。
