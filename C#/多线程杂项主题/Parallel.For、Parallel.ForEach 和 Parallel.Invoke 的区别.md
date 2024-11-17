### **Parallel.For、Parallel.ForEach 和 Parallel.Invoke 的区别、适用场景以及使用方式**

C# 中的 **`Parallel`** 类是 .NET 提供的一种高效并行处理工具，用于在多线程环境下快速执行任务。以下是 **`Parallel.For`**、**`Parallel.ForEach`** 和 **`Parallel.Invoke`** 的详细对比、适用场景和使用方式。

---

### **核心区别**

| **功能**             | **Parallel.For**                                          | **Parallel.ForEach**                                     | **Parallel.Invoke**                                      |
|----------------------|----------------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------|
| **适用场景**          | 并行处理 **固定范围内的索引**（如数组或集合的下标）。        | 并行处理 **集合的每个元素**（如列表、字典或数组等）。       | 并行执行 **多个独立的任务**，每个任务使用一个方法或表达式。 |
| **执行内容**          | 针对指定范围（如 `0..N`）执行相同的代码逻辑。                 | 针对集合的每个元素执行相同的代码逻辑。                     | 执行多个彼此独立的任务。                                   |
| **输入数据**          | 开始值和结束值（范围）。                                   | 任意集合（如 `IEnumerable<T>`）。                         | 任意数量的 `Action` 委托（或 lambda 表达式）。             |
| **输出结果**          | 不返回结果；通过共享变量存储计算结果（如累加值）。             | 不返回结果；通过共享变量存储计算结果（如累加值）。           | 无返回结果，任务相互独立，适合无共享数据的场景。             |

---

### **使用方式**

#### **1. Parallel.For**

**特点**：
- 用于处理**索引范围**的循环操作。
- 支持指定起始值和结束值。

**适用场景**：
- 针对一个数组或集合的下标操作。
- 例如：并行计算数组每个元素的累加值。

**代码示例**：

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    static void Main(string[] args)
    {
        int[] array = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
        int sum = 0;
        object lockSum = new object();

        // 使用 Parallel.For 对数组的每个下标进行并行处理
        Parallel.For(0, array.Length, i =>
        {
            lock (lockSum) // 锁定共享资源，确保线程安全
            {
                sum += array[i]; // 将当前元素值累加到总和
            }
        });

        Console.WriteLine($"Parallel.For 的结果：{sum}");
    }
}
```

---

#### **2. Parallel.ForEach**

**特点**：
- 用于处理**集合的每个元素**，集合可以是数组、列表、字典等。
- 更灵活，不需要显式使用索引。

**适用场景**：
- 针对集合中的每个元素执行相同的操作。
- 例如：对列表中的每个元素进行处理。

**代码示例**：

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
        int sum = 0;
        object lockSum = new object();

        // 使用 Parallel.ForEach 并行处理集合的每个元素
        Parallel.ForEach(numbers, number =>
        {
            lock (lockSum) // 锁定共享资源，确保线程安全
            {
                sum += number; // 将当前元素值累加到总和
            }
        });

        Console.WriteLine($"Parallel.ForEach 的结果：{sum}");
    }
}
```

---

#### **3. Parallel.Invoke**

**特点**：
- 用于**并行执行多个独立任务**，每个任务可以是一个方法或 lambda 表达式。
- 任务之间彼此独立，适合无共享资源的情况。

**适用场景**：
- 执行彼此独立的多个任务。
- 例如：同时处理三个独立的计算任务。

**代码示例**：

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main(string[] args)
    {
        // 使用 Parallel.Invoke 并行执行多个任务
        Parallel.Invoke(
            () =>
            {
                Console.WriteLine("任务 1 开始");
                Task.Delay(1000).Wait(); // 模拟耗时操作
                Console.WriteLine("任务 1 完成");
            },
            () =>
            {
                Console.WriteLine("任务 2 开始");
                Task.Delay(2000).Wait(); // 模拟耗时操作
                Console.WriteLine("任务 2 完成");
            },
            () =>
            {
                Console.WriteLine("任务 3 开始");
                Task.Delay(3000).Wait(); // 模拟耗时操作
                Console.WriteLine("任务 3 完成");
            }
        );

        Console.WriteLine("所有任务已完成");
    }
}
```

**输出示例**：
```
任务 1 开始
任务 2 开始
任务 3 开始
任务 1 完成
任务 2 完成
任务 3 完成
所有任务已完成
```

---

### **对比总结**

| **特点**            | **Parallel.For**                            | **Parallel.ForEach**                         | **Parallel.Invoke**                          |
|---------------------|---------------------------------------------|---------------------------------------------|---------------------------------------------|
| **适用数据**         | 范围（索引）                                | 集合（如数组、列表）                           | 独立任务（`Action` 委托）。                   |
| **适用场景**         | 并行处理范围内的下标操作                      | 并行处理集合中的每个元素                      | 并行执行多个独立任务。                         |
| **共享变量的处理**   | 需要锁定共享变量以防止数据竞争                  | 需要锁定共享变量以防止数据竞争                  | 任务通常彼此独立，不涉及共享变量。              |
| **并行效率**         | 高效，尤其是数据量较大时表现优异。               | 高效，适合直接对集合进行操作。                  | 适合处理彼此独立的任务；任务过多时可能引发线程争用。 |

---

### **最佳实践**

1. **选择合适的工具**：
   - 使用 **`Parallel.For`** 处理需要基于索引的操作。
   - 使用 **`Parallel.ForEach`** 处理集合的每个元素。
   - 使用 **`Parallel.Invoke`** 处理多个彼此独立的任务。

2. **线程安全**：
   - 使用 **`lock`** 或 **线程安全的类（如 `ConcurrentDictionary`）** 来保护共享变量。

3. **注意任务粒度**：
   - 任务粒度过小可能导致线程争用，过大则无法充分利用并行性能。

4. **避免资源竞争**：
   - 确保并行任务间的资源尽量独立，以提高效率。

---

### **总结**

- **`Parallel.For`** 和 **`Parallel.ForEach`** 适用于集合数据的并行处理，区别在于是否基于索引操作。
- **`Parallel.Invoke`** 适用于执行多个独立的任务。
- 在实际开发中，根据场景选择合适的工具，并注意线程安全和资源竞争问题，从而实现高效的并行代码。
