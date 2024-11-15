### **C# 中的任务延续：`Wait`、`WaitAll` 和 `Result`**

任务延续（Task Continuation）指在任务完成后执行的操作。在 C# 中，可以使用 `Wait`、`WaitAll` 和 `Result` 等方法来控制任务的同步和结果获取。以下是详细解释和代码示例。

---

### **1. `Wait`: 阻塞等待单个任务**

- **描述**：
  `Wait` 会阻塞当前线程，直到任务完成。它不返回值，仅用于等待任务结束。

- **代码示例**：
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 定义一个异步运行的任务
        Task task = Task.Run(() =>
        {
            Console.WriteLine("任务正在运行...");
            Task.Delay(2000).Wait(); // 模拟延迟
            Console.WriteLine("任务已完成。");
        });

        // 使用 Wait 阻塞等待任务完成
        Console.WriteLine("等待任务完成...");
        task.Wait();
        Console.WriteLine("任务已结束。");
    }
}
```

- **输出**：
  ```
  任务正在运行...
  等待任务完成...
  任务已完成。
  任务已结束。
  ```

- **关键点**：
  - `Wait` 是阻塞调用，会暂停当前线程直到任务完成。
  - 适用于需要确保任务完成后再继续的场景。

---

### **2. `WaitAll`: 阻塞等待多个任务**

- **描述**：
  `WaitAll` 会阻塞当前线程，直到所有任务集合中的任务都完成。

- **代码示例**：
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 定义多个任务
        Task[] tasks = new Task[3];

        tasks[0] = Task.Run(() =>
        {
            Task.Delay(1000).Wait();
            Console.WriteLine("任务 1 已完成。");
        });

        tasks[1] = Task.Run(() =>
        {
            Task.Delay(2000).Wait();
            Console.WriteLine("任务 2 已完成。");
        });

        tasks[2] = Task.Run(() =>
        {
            Task.Delay(1500).Wait();
            Console.WriteLine("任务 3 已完成。");
        });

        // 使用 WaitAll 阻塞直到所有任务完成
        Console.WriteLine("等待所有任务完成...");
        Task.WaitAll(tasks);
        Console.WriteLine("所有任务已完成。");
    }
}
```

- **输出**：
  ```
  等待所有任务完成...
  任务 1 已完成。
  任务 3 已完成。
  任务 2 已完成。
  所有任务已完成。
  ```

- **关键点**：
  - `WaitAll` 适用于需要确保一组任务全部完成后再继续的场景。
  - 任务的完成顺序与任务在数组中的索引无关，取决于每个任务的执行时间。

---

### **3. `Result`: 阻塞等待并获取任务结果**

- **描述**：
  `Result` 会阻塞当前线程，直到任务完成，并获取任务的返回值。它适用于 `Task<T>` 类型的任务。

- **代码示例**：
```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 定义一个返回结果的任务
        Task<int> task = Task.Run(() =>
        {
            Console.WriteLine("计算结果中...");
            Task.Delay(2000).Wait(); // 模拟延迟
            return 42; // 返回结果
        });

        // 使用 Result 阻塞并获取结果
        Console.WriteLine("等待任务结果...");
        int result = task.Result;
        Console.WriteLine($"任务结果：{result}");
    }
}
```

- **输出**：
  ```
  计算结果中...
  等待任务结果...
  任务结果：42
  ```

- **关键点**：
  - `Result` 会阻塞当前线程直到任务完成，并返回任务的结果。
  - 适用于需要任务返回值来继续后续操作的场景。

---

### **优化：使用 `async` 和 `await` 实现非阻塞式任务**

使用 `async` 和 `await` 可以实现非阻塞式任务，能够更高效地利用资源，提升并发能力。

#### **单任务示例**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 异步执行任务
        await PerformTaskAsync();

        Console.WriteLine("任务已完成。");
    }

    static async Task PerformTaskAsync()
    {
        Console.WriteLine("任务正在运行...");
        await Task.Delay(2000); // 异步模拟延迟
        Console.WriteLine("任务已完成。");
    }
}
```

---

#### **多任务示例**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // 定义并启动多个任务
        var tasks = new[]
        {
            PerformTaskAsync("任务 1", 1000),
            PerformTaskAsync("任务 2", 2000),
            PerformTaskAsync("任务 3", 1500)
        };

        // 异步等待所有任务完成
        await Task.WhenAll(tasks);

        Console.WriteLine("所有任务已完成。");
    }

    static async Task PerformTaskAsync(string taskName, int delay)
    {
        Console.WriteLine($"{taskName} 正在运行...");
        await Task.Delay(delay); // 异步延迟
        Console.WriteLine($"{taskName} 已完成。");
    }
}
```

---

### **优化的优势**

1. **改进的可扩展性**：
   - 线程不会被阻塞，允许更多任务同时运行，提高了资源利用率。

2. **避免死锁**：
   - 在 GUI 或 ASP.NET 应用中，`async`/`await` 防止了常见的死锁问题。

3. **更清晰的错误处理**：
   - 使用 `try-catch` 结构结合 `await`，实现更清晰的错误处理。

4. **更高的响应性**：
   - 在 GUI 或 Web 应用中，UI 和服务器线程在任务运行时保持响应。

---

### **总结**

- **阻塞方法**（`Wait`、`WaitAll`、`Result`）简单易用，但可能导致资源浪费和响应性下降。
- **非阻塞方法**（`async` 和 `await`）更高效，适合现代应用场景，特别是高并发任务或需要保持 UI 响应的场景。
- 优先使用 `async` 和 `await`，结合 `Task.WhenAll` 或 `Task.WhenAny` 处理多个任务的场景。
