### 使用 `Semaphore` 限制线程数量

在 C# 中，`Semaphore` 是一种同步原语，用于通过指定的线程数量来控制对资源的访问。与仅允许一个线程访问临界区的 `Mutex` 或 `lock` 不同，`Semaphore` 可以允许多个线程访问资源，最多到达定义的限制。这在限制并发线程数量的场景中非常有用，比如控制数据库连接数量或限制对文件的并发访问。

### `Semaphore` 的关键概念

1. **并发访问控制**：
   - `Semaphore` 允许你指定同时访问资源的最大线程数量。
   - 当线程数量达到此限制时，试图获取 `Semaphore` 的其他线程将会等待，直到有一个线程释放 `Semaphore`。

2. **信号量计数**：
   - `Semaphore` 有一个初始计数和一个最大计数。
   - 每次一个线程进入 `Semaphore`，计数减少 1；每次一个线程退出并释放 `Semaphore`，计数增加 1。
   - 当计数达到 0 时，不允许更多线程进入，直到有线程退出并释放 `Semaphore`。

3. **Release 方法**：
   - `Release` 方法用于增加计数并释放 `Semaphore`，使其他等待线程可以进入。

### `Semaphore` 用法的基本示例

以下示例演示了使用 `Semaphore` 将访问临界区的并发线程数量限制为 3。

```csharp
using System;
using System.Threading;

class Program
{
    // 创建一个初始计数和最大计数均为 3 的 Semaphore
    private static readonly Semaphore semaphore = new Semaphore(3, 3);

    static void Main()
    {
        for (int i = 1; i <= 10; i++)
        {
            Thread thread = new Thread(AccessResource);
            thread.Name = $"Thread {i}";
            thread.Start();
        }
    }

    static void AccessResource()
    {
        Console.WriteLine($"{Thread.CurrentThread.Name} 正在等待进入...");

        semaphore.WaitOne(); // 获取 Semaphore
        try
        {
            Console.WriteLine($"{Thread.CurrentThread.Name} 已进入临界区。");
            Thread.Sleep(2000); // 模拟工作
            Console.WriteLine($"{Thread.CurrentThread.Name} 正在离开临界区。");
        }
        finally
        {
            semaphore.Release(); // 释放 Semaphore
        }
    }
}
```

### 代码解释

1. **创建一个 Semaphore**：
   - `new Semaphore(3, 3)` 创建一个初始计数和最大计数均为 3 的 `Semaphore`。
   - 这意味着最多可以有 3 个线程同时获取 `Semaphore` 并访问临界区。

2. **线程对临界区的访问**：
   - 每个线程调用 `semaphore.WaitOne()` 尝试进入临界区。
   - 如果进入临界区的线程少于 3 个，`WaitOne` 将成功，线程可以继续。
   - 如果已经有 3 个线程在临界区，其他线程将等待，直到有一个活动线程释放 `Semaphore`。

3. **释放 Semaphore**：
   - 每个线程在完成临界区工作后调用 `semaphore.Release()` 释放 `Semaphore`。
   - 这会增加计数，使等待的另一个线程可以进入临界区。

### 现实中的应用场景

- **连接池**：限制同时连接到数据库的数量，防止过载。
- **资源密集型任务**：限制同时执行 CPU 或内存密集型任务的线程数量，以避免性能下降。
- **文件访问**：控制同时访问文件的线程数量，以防止文件损坏或冲突。

### 重要注意事项

1. **始终释放 Semaphore**：
   - 确保每个进入 `Semaphore` 的线程最终都会释放它，最好使用 `try-finally` 确保调用 `Release`。
   - 如果未能释放 `Semaphore`，可能会导致死锁，等待的线程会无限期阻塞。

2. **设置合适的限制**：
   - 根据资源容量选择合适的 `Semaphore` 计数，例如，对于有连接限制的数据库，可以设置最大计数与连接限制相同。

3. **阻塞行为**：
   - 超过限制的线程将阻塞在 `WaitOne` 上，若有大量线程等待可能会影响性能。可以考虑使用 `WaitOne` 的超时参数，以便线程在指定时间内未能获取 `Semaphore` 时采取其他操作。

### 关键点与提示

- **使用 `Semaphore` 控制并发**：当需要限制线程对共享资源的并发访问时，`Semaphore` 是理想的选择。
- **考虑使用 `SemaphoreSlim` 处理进程内需求**：`SemaphoreSlim` 是 `Semaphore` 的轻量替代，适合不需要跨进程同步的场景。
- **始终使用 `try-finally` 与 `WaitOne` 和 `Release` 搭配**：确保即使在异常发生时 `Semaphore` 也能被正确释放。

### 常见面试问题

1. **`Mutex` 和 `Semaphore` 有什么区别？**
   - 解释 `Mutex` 只允许一个线程同时访问临界区，而 `Semaphore` 允许多个线程访问，数量由限制决定。

2. **什么时候会用 `Semaphore` 而不是 `lock`？**
   - 描述 `Semaphore` 适用于需要允许多个线程并发访问资源的场景，而 `lock` 只允许一个线程访问。

3. **如果线程未释放 `Semaphore` 会发生什么？**
   - 讨论未释放 `Semaphore` 会导致死锁，因为等待的线程可能会无限期阻塞。

### 总结

`Semaphore` 是 C# 中一种强大的同步工具，它允许你控制访问资源的并发线程数量。通过设置并发访问限制，可以防止资源耗尽并提高性能。使用 `try-finally` 确保在异常发生时正确释放 `Semaphore`，使 `Semaphore` 成为多线程应用中管理并发的可靠方法。
