```csharp
using System;
using System.Threading;

public class Program
{
    // 创建一个 AutoResetEvent 实例，用于线程间的信号传递
    private static readonly AutoResetEvent autoResetEvent = new AutoResetEvent(false);
    
    // 创建一个 CancellationTokenSource 实例，用于优雅退出
    private static readonly CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
    
    public static void Main()
    {
        Console.WriteLine("服务器正在运行。输入 'go' 继续，输入 'exit' 停止。");

        // 启动工作线程
        for (int i = 0; i < 3; i++)
        {
            Thread workerThread = new Thread(Worker)
            {
                Name = $"Worker {i + 1}",
                IsBackground = true // 设置为后台线程，确保程序可以正常退出
            };
            workerThread.Start(cancellationTokenSource.Token); // 将取消令牌传递给工作线程
        }

        // 主线程处理用户输入
        HandleUserInput();
        
        Console.WriteLine("服务器已停止。");
    }

    // 处理用户输入的方法
    private static void HandleUserInput()
    {
        while (true)
        {
            string? userInput = Console.ReadLine();

            // 如果输入为 "exit"，则触发取消并退出
            if (userInput?.ToLower() == "exit")
            {
                cancellationTokenSource.Cancel(); // 发出取消信号
                break;
            }

            // 如果输入为 "go"，则向工作线程发出信号
            if (userInput?.ToLower() == "go")
            {
                autoResetEvent.Set();
            }
        }
    }

    // 工作线程的执行方法
    private static void Worker(object? cancellationTokenObj)
    {
        // 确保提供了 CancellationToken，否则抛出异常
        if (cancellationTokenObj is not CancellationToken cancellationToken)
        {
            throw new ArgumentException("需要提供 CancellationToken", nameof(cancellationTokenObj));
        }

        while (!cancellationToken.IsCancellationRequested)
        {
            Console.WriteLine($"{Thread.CurrentThread.Name} 正在等待信号。");

            // 等待主线程的信号
            autoResetEvent.WaitOne();

            // 检查取消请求，如果有则退出
            if (cancellationToken.IsCancellationRequested)
            {
                Console.WriteLine($"{Thread.CurrentThread.Name} 收到退出请求，停止工作。");
                break;
            }

            Console.WriteLine($"{Thread.CurrentThread.Name} 收到信号并继续执行。");
            
            // 模拟处理时间
            Thread.Sleep(2000);
        }
    }
}
```

### 代码逐行说明

1. **`private static readonly AutoResetEvent autoResetEvent = new AutoResetEvent(false);`**
   - 创建一个 `AutoResetEvent` 实例 `autoResetEvent`，初始状态为无信号（`false`），用于主线程与工作线程之间的信号传递。

2. **`private static readonly CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();`**
   - 创建一个 `CancellationTokenSource` 实例 `cancellationTokenSource`，用于在程序退出时发出取消信号，实现优雅退出。

3. **`public static void Main()`**
   - 主程序入口，输出服务器启动信息并启动工作线程，同时处理用户输入。

4. **`for (int i = 0; i < 3; i++) { ... }`**
   - 循环创建并启动 3 个工作线程，每个线程调用 `Worker` 方法。

5. **`Thread workerThread = new Thread(Worker) { Name = $"Worker {i + 1}", IsBackground = true };`**
   - 创建一个新的 `Thread` 实例并设置线程名称（例如 "Worker 1"、"Worker 2"），将其设为后台线程 (`IsBackground = true`)，确保主线程结束时工作线程自动退出。

6. **`workerThread.Start(cancellationTokenSource.Token);`**
   - 启动工作线程，并将 `CancellationToken` 传递给线程，以便在需要时能够检查取消请求。

7. **`HandleUserInput();`**
   - 调用 `HandleUserInput` 方法处理用户输入，等待用户输入 `"go"` 或 `"exit"` 指令。

8. **`Console.WriteLine("服务器已停止。");`**
   - 主线程在用户输入 `"exit"` 后输出服务器停止信息，表示程序即将退出。

#### `HandleUserInput` 方法

9. **`string? userInput = Console.ReadLine();`**
   - 从控制台读取用户输入。

10. **`if (userInput?.ToLower() == "exit") { cancellationTokenSource.Cancel(); break; }`**
    - 检查用户输入是否为 `"exit"`，如果是，则发出取消信号（`cancellationTokenSource.Cancel()`）并退出循环。

11. **`if (userInput?.ToLower() == "go") { autoResetEvent.Set(); }`**
    - 检查用户输入是否为 `"go"`，如果是，则调用 `autoResetEvent.Set()` 发出信号，让一个工作线程继续执行。

#### `Worker` 方法

12. **`if (cancellationTokenObj is not CancellationToken cancellationToken) { ... }`**
    - 检查传递的参数是否为 `CancellationToken`，如果不是，则抛出 `ArgumentException` 异常，以确保工作线程正确获取到取消令牌。

13. **`while (!cancellationToken.IsCancellationRequested) { ... }`**
    - 循环检查 `CancellationToken` 是否已请求取消。如果没有，继续执行线程工作；如果有，则跳出循环。

14. **`autoResetEvent.WaitOne();`**
    - 调用 `WaitOne()` 方法等待主线程的信号。线程将阻塞，直到 `autoResetEvent` 设置为有信号状态。

15. **`if (cancellationToken.IsCancellationRequested) { ... }`**
    - 在收到信号后，再次检查取消请求。如果收到取消信号，则输出退出信息并跳出循环停止工作。

16. **`Console.WriteLine($"{Thread.CurrentThread.Name} 收到信号并继续执行。");`**
    - 输出线程收到信号的信息。

17. **`Thread.Sleep(2000);`**
    - 使用 `Thread.Sleep(2000)` 模拟线程工作处理时间。

### 最佳实践总结

- **优雅退出**：通过 `CancellationTokenSource` 实现优雅退出，确保线程在程序结束前能够完成当前任务。
- **后台线程**：将工作线程设为后台线程，以确保主线程结束时程序能正常退出。
- **信号控制**：使用 `AutoResetEvent` 控制主线程与工作线程的同步，仅在需要时让一个线程继续执行。
