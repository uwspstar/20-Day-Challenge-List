### **任务延续（Task Continuation）：`Task.WhenAll` 和 `Task.WhenAny`**

在 **C#** 中，`Task.WhenAll` 和 `Task.WhenAny` 是用于处理多个任务集合的任务延续方法。这些方法可以让你在所有任务完成或任意一个任务完成后继续执行。

---

### **1. `Task.WhenAll`**

- **描述**：
  - 等待**所有任务**完成。
  - 返回一个表示所有任务完成的单个任务。
  - 如果任务有返回值，可以汇总所有任务的结果。

---

#### **代码示例：基本使用 `Task.WhenAll`**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 定义多个任务
        Task task1 = Task.Run(async () =>
        {
            Console.WriteLine("任务 1 开始...");
            await Task.Delay(2000); // 模拟延迟
            Console.WriteLine("任务 1 完成。");
        });

        Task task2 = Task.Run(async () =>
        {
            Console.WriteLine("任务 2 开始...");
            await Task.Delay(1000); // 模拟延迟
            Console.WriteLine("任务 2 完成。");
        });

        // 等待所有任务完成
        Console.WriteLine("等待所有任务完成...");
        await Task.WhenAll(task1, task2);
        Console.WriteLine("所有任务已完成。");
    }
}
```

#### **输出**：
```
任务 1 开始...
任务 2 开始...
任务 2 完成。
任务 1 完成。
等待所有任务完成...
所有任务已完成。
```

---

#### **代码示例：汇总任务结果**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 定义多个有返回值的任务
        Task<int> task1 = Task.Run(async () =>
        {
            await Task.Delay(1000); // 模拟延迟
            return 10; // 返回结果
        });

        Task<int> task2 = Task.Run(async () =>
        {
            await Task.Delay(2000); // 模拟延迟
            return 20; // 返回结果
        });

        // 等待所有任务完成并汇总结果
        int[] results = await Task.WhenAll(task1, task2);

        // 输出结果
        Console.WriteLine($"任务 1 的结果：{results[0]}");
        Console.WriteLine($"任务 2 的结果：{results[1]}");
        Console.WriteLine($"结果总和：{results[0] + results[1]}");
    }
}
```

#### **输出**：
```
任务 1 的结果：10
任务 2 的结果：20
结果总和：30
```

---

### **2. `Task.WhenAny`**

- **描述**：
  - 等待**任意一个任务**完成。
  - 返回第一个完成的任务。
  - 常用于需要最快响应的场景。

---

#### **代码示例：基本使用 `Task.WhenAny`**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 定义多个任务
        Task task1 = Task.Run(async () =>
        {
            Console.WriteLine("任务 1 开始...");
            await Task.Delay(2000); // 模拟延迟
            Console.WriteLine("任务 1 完成。");
        });

        Task task2 = Task.Run(async () =>
        {
            Console.WriteLine("任务 2 开始...");
            await Task.Delay(1000); // 模拟延迟
            Console.WriteLine("任务 2 完成。");
        });

        // 等待任意一个任务完成
        Console.WriteLine("等待任意任务完成...");
        Task firstCompletedTask = await Task.WhenAny(task1, task2);

        Console.WriteLine("一个任务已完成！");
    }
}
```

#### **输出**：
```
任务 1 开始...
任务 2 开始...
任务 2 完成。
等待任意任务完成...
一个任务已完成！
任务 1 完成。
```

---

#### **代码示例：处理第一个完成的任务结果**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 定义多个有返回值的任务
        Task<int> task1 = Task.Run(async () =>
        {
            await Task.Delay(2000); // 模拟延迟
            return 10; // 返回结果
        });

        Task<int> task2 = Task.Run(async () =>
        {
            await Task.Delay(1000); // 模拟延迟
            return 20; // 返回结果
        });

        // 等待任意一个任务完成
        Task<int> firstCompletedTask = (Task<int>)await Task.WhenAny(task1, task2);

        // 输出第一个完成的任务结果
        Console.WriteLine($"第一个完成任务的结果：{firstCompletedTask.Result}");
    }
}
```

#### **输出**：
```
第一个完成任务的结果：20
```

---

### **`Task.WhenAll` 与 `Task.WhenAny` 的对比**

| **特性**                 | **Task.WhenAll**                           | **Task.WhenAny**                           |
|--------------------------|--------------------------------------------|--------------------------------------------|
| **完成条件**             | 等待所有任务完成                           | 等待任意一个任务完成                       |
| **结果处理**             | 汇总所有任务的结果                         | 返回第一个完成任务的结果                   |
| **适用场景**             | 需要所有任务都完成的情况                   | 需要最快任务响应的情况                     |
| **性能**                 | 等待最慢的任务完成                         | 一旦有任务完成即可继续                     |

---

### **提示**

1. **异常处理**：
   - `Task.WhenAll` 会将所有任务的异常聚合为一个 `AggregateException`。
   - 使用 `try-catch` 捕获异常。

   ```csharp
   try
   {
       await Task.WhenAll(task1, task2);
   }
   catch (Exception ex)
   {
       Console.WriteLine($"错误：{ex.Message}");
   }
   ```

2. **任务取消**：
   - `Task.WhenAll` 即使某些任务被取消，也会等待其余任务完成。
   - `Task.WhenAny` 会在第一个任务完成后立即返回，无论其状态如何。

3. **优化性能**：
   - 在需要最快结果的情况下使用 `Task.WhenAny`，例如同时从多个数据源查询数据。

---

### **总结**

- **`Task.WhenAll`**：适用于需要等待所有任务完成并汇总结果的场景。
- **`Task.WhenAny`**：适用于只需要任意一个任务完成即可继续的场景。
- 通过这两个方法可以轻松处理多个任务，并实现高效的异步编程。
