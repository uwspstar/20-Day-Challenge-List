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

---

### Semaphore 与 SemaphoreSlim 的区别

`Semaphore` 和 `SemaphoreSlim` 都是用于控制线程访问共享资源的同步原语。它们的作用类似，但在用例、性能和资源消耗方面有明显的区别。

#### 1. **目的和使用场景**

- **Semaphore**：
  - 设计用于跨进程的同步场景，可以在多个进程间共享。
  - 适用于多个应用程序或不同进程的线程之间需要协调访问的资源限制。
  - 由于支持跨进程，因此资源消耗较高。

- **SemaphoreSlim**：
  - 一种轻量化的版本，**仅适用于单进程** 内部的线程同步。
  - 适合单个应用程序内部的资源限制，例如线程池或共享资源。
  - 占用内存和系统资源较少，适合不需要跨进程同步的高性能应用。

#### 2. **性能**

- **Semaphore**：
  - 使用内核级对象进行同步，这在跨进程通信中更可靠，但在获取和释放锁方面相对较慢。
  - 适合需要更高稳定性和跨进程信号传递的场景，即使性能略有下降。

- **SemaphoreSlim**：
  - 采用内核级和用户级的组合实现，专为不需要跨进程的场景而优化，锁的获取和释放更快。
  - 由于开销更小，因此适合需要快速锁定和释放的单进程高性能应用场景。

#### 3. **内存和资源消耗**

- **Semaphore**：
  - 由于支持跨进程同步，占用的资源更多，内存占用更大。
  - 更适合多进程或系统级的应用场景，适用于多个应用或进程需要协调访问同一共享资源的情况。

- **SemaphoreSlim**：
  - 占用的内存和系统资源较少，效率更高。
  - 尽量使用托管的用户级构造，仅在必要时使用内核级同步（例如锁争用较高时）。

#### 4. **API 不同之处**

- **Semaphore**：
  - 使用 `WaitOne()` 方法获取锁，使用 `Release()` 方法释放锁。
  - 可以指定初始计数和最大计数，灵活控制允许进入的线程数量。

- **SemaphoreSlim**：
  - 同样使用 `Wait()` 和 `Release()` 方法，但支持异步方法（`WaitAsync()`），适合 .NET 的异步编程。
  - 更好地集成了 `async/await` 异步编程模式，适合现代 .NET 应用程序中的资源管理。

#### 5. **常见用例对比**

| 特性                | Semaphore                                      | SemaphoreSlim                              |
|--------------------|------------------------------------------------|--------------------------------------------|
| **跨进程使用**     | 支持，可以在多个进程之间共享                      | 不支持，仅限于单进程内部使用                |
| **理想的使用场景** | 多进程应用、系统级资源                          | 单个应用程序、线程池、单进程资源            |
| **资源使用**       | 资源消耗较高                                    | 资源消耗较低                               |
| **性能**           | 较慢，因使用内核级同步                           | 较快，因使用用户级同步                     |
| **异步支持**       | 不支持                                         | 支持，适合异步编程                          |

### 代码示例

以下是使用 `Semaphore` 控制对共享资源的访问的示例：

#### 使用 `Semaphore` 的示例

```csharp
using System;
using System.Threading;

class Program
{
    private static readonly Semaphore semaphore = new Semaphore(2, 2); // 允许最多2个线程同时进入

    static void Main()
    {
        for (int i = 1; i <= 5; i++)
        {
            Thread thread = new Thread(AccessResource);
            thread.Name = $"Thread {i}";
            thread.Start();
        }
    }

    static void AccessResource()
    {
        Console.WriteLine($"{Thread.CurrentThread.Name} 正在等待进入...");
        
        semaphore.WaitOne(); // 获取信号量
        try
        {
            Console.WriteLine($"{Thread.CurrentThread.Name} 已进入临界区。");
            Thread.Sleep(1000); // 模拟工作
        }
        finally
        {
            Console.WriteLine($"{Thread.CurrentThread.Name} 正在释放信号量。");
            semaphore.Release(); // 释放信号量
        }
    }
}
```

#### 使用 `SemaphoreSlim` 的示例

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

class Program
{
    private static readonly SemaphoreSlim semaphoreSlim = new SemaphoreSlim(2, 2); // 允许最多2个线程同时进入

    static async Task Main()
    {
        for (int i = 1; i <= 5; i++)
        {
            int threadNumber = i;
            _ = Task.Run(async () => await AccessResourceAsync(threadNumber));
        }

        await Task.Delay(5000); // 等待所有任务完成
    }

    static async Task AccessResourceAsync(int threadNumber)
    {
        Console.WriteLine($"Thread {threadNumber} 正在等待进入...");

        await semaphoreSlim.WaitAsync(); // 异步获取信号量
        try
        {
            Console.WriteLine($"Thread {threadNumber} 已进入临界区。");
            await Task.Delay(1000); // 模拟异步工作
        }
        finally
        {
            Console.WriteLine($"Thread {threadNumber} 正在释放信号量。");
            semaphoreSlim.Release(); // 释放信号量
        }
    }
}
```

### 总结

- **Semaphore** 更适合跨进程同步的场景，适用于在多个应用或进程间协调资源访问。由于使用内核级同步，资源消耗更高，因此性能较 `SemaphoreSlim` 稍低。
- **SemaphoreSlim** 是一个轻量化、仅限单进程的替代方案，设计用于单进程中的高性能场景。它在速度上更快，并且支持异步操作，适合现代 .NET 应用程序中的资源管理。
- 
