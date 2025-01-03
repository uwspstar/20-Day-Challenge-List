### 并行 (Parallelism) vs 并发 (Concurrency)

并行和并发是计算机科学中两个重要的概念，经常用于描述多任务执行的方式。虽然它们有一定的联系，但在实际实现和应用中存在显著区别。

#### **核心区别：**

| 特点           | 并行 (Parallelism)                                          | 并发 (Concurrency)                                     |
|----------------|------------------------------------------------------------|-------------------------------------------------------|
| **定义**       | 多个任务**同时**执行，利用多核 CPU 提高效率。                | 多个任务**交替**执行，在同一时间段内“看起来”同时运行。 |
| **任务分配**   | 不同的任务分配到不同的 CPU 核心，同时运行。                  | 任务在单个或多个 CPU 核心上快速切换。                 |
| **硬件依赖**   | 强依赖多核或多处理器硬件支持。                               | 不依赖多核硬件，只需要支持多任务调度的系统。           |
| **目标**       | 提高处理能力，缩短运行时间。                                 | 提高任务切换效率，增强响应能力。                      |
| **示例**       | 同时运行多个科学计算程序。                                   | 在浏览器中同时加载多个网页或任务调度。                |


#### 1. **并行 (Parallelism)**

- **特点**：多个任务真正同时执行。
- **实现方式**：需要多核 CPU，任务被分配到不同的核心上。
- **场景**：适用于 CPU 密集型任务，如大数据计算、科学运算。
- **形象比喻**：假设有两个人（两个 CPU 核心）同时抬两块石头，每个人负责一块。

#### 2. **并发 (Concurrency)**

- **特点**：多个任务交替执行，看起来在同时运行，但实际上是快速切换。
- **实现方式**：通过操作系统的时间分片技术。
- **场景**：适用于 I/O 密集型任务，如网络请求、文件读取。
- **形象比喻**：一个人（单核 CPU）抬两块石头，但快速切换抬石头的顺序，让别人以为在同时完成。


### **对比图解：并行 vs 并发**

#### 图 1: 并发 (Concurrency)
```mermaid
gantt
    title Concurrency Task Execution
    dateFormat  YYYY-MM-DD
    section CPU Core 1
    Task A           :a1, 2024-01-01, 1d
    Task B           :b1, after a1, 1d
    Task A (Round 2) :a2, after b1, 1d
    Task B (Round 2) :b2, after a2, 1d
```

- **说明**：
  - 单核 CPU 通过时间片切换执行任务 A 和任务 B。
  - 在一个时间点上，只有一个任务在运行。

---

#### 图 2: 并行 (Parallelism)
```mermaid
gantt
    title 并行任务执行示意图
    section CPU Core 1
    Task A    :active,  a1, 0, 4s
    section CPU Core 2
    Task B    :active,  b1, 0, 4s
```

- **说明**：
  - 两个 CPU 核心分别执行任务 A 和任务 B。
  - 两个任务真正同时运行，不存在切换开销。

---

### **应用场景**

| 场景                | 并行                                      | 并发                                     |
|---------------------|------------------------------------------|-----------------------------------------|
| **科学计算**         | 是                                         | 否                                      |
| **Web 服务器**       | 是                                         | 是                                      |
| **文件下载和处理**   | 否                                         | 是                                      |
| **高性能计算**       | 是                                         | 否                                      |

 

### **总结 (Key Takeaways)**

1. **并行是硬件层面的“同时”，并发是逻辑层面的“同时”。**
2. 并行可以视为更高效的并发，但需要硬件支持。
3. 理解场景和需求，选择合适的模式优化系统性能。


```mermaid
flowchart TD
    subgraph notParallel[不是并发，也不是并行]
        direction LR
        CPU1[CPU Core 1]
        Task1[Task 1]
        Task2[Task 2]
        CPU1 --> Task1 --> Task2
        Note1[一个CPU核心依次执行每个任务，因此任务A在任务B之前完成。]
    end
```

```mermaid
flowchart TD
    subgraph parallelNotConcurrency[并发，但不是并行]
        direction LR
        CPU2[CPU Core 1]
        Task1_2[Task 1]
        Task2_2[Task 2]
        CPU2 --> Task1_2 -.-> Task2_2
        Note2[一个CPU核心依次执行每个任务，使得任务A和任务B可以大致在同一时间完成。]
    end
```

```mermaid
flowchart TD
    subgraph concurrencyNotParallel[并行，但不是并发]
        direction LR
        CPU3[CPU Core 1]
        CPU4[CPU Core 2]
        Task1_3[Task 1]
        Task2_3[Task 2]
        CPU3 --> Task1_3
        CPU4 --> Task2_3
        Note3[两个CPU核心依次执行每个任务，因此任务A在任务B之前完成。]
    end
```

```mermaid
flowchart TD
    subgraph concurrencyAndParallel[并发，且并行]
        direction LR
        CPU5[CPU Core 1]
        CPU6[CPU Core 2]
        Task1_4[Task 1]
        Task2_4[Task 2]
        Task3_4[Task 3]
        Task4_4[Task 4]
        CPU5 --> Task1_4 -.-> Task3_4
        CPU6 --> Task2_4 -.-> Task4_4
        Note4[两个CPU核心同时执行每个任务，因此两个任务大致在同一时间完成。]
    end
```

#### 1. **不是并发，也不是并行**
   - **描述**：一个 CPU 核心依次执行每个任务，因此任务 A 在任务 B 之前完成。
   - **CPU 资源**：单核 CPU。

#### 2. **并发，但不是并行**
   - **描述**：一个 CPU 核心依次执行任务，但时间片交替，使得任务 A 和任务 B 看起来在同一时间完成。
   - **CPU 资源**：单核 CPU。

#### 3. **并行，但不是并发**
   - **描述**：两个 CPU 核心独立执行任务，每个任务的顺序是固定的。
   - **CPU 资源**：多核 CPU。

#### 4. **并发，且并行**
   - **描述**：两个 CPU 核心同时处理任务，并且时间片交替调度使任务完成效率最高。
   - **CPU 资源**：多核 CPU。
