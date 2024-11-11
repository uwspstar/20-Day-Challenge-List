```csharp
using System;
using System.Threading;

public class Program
{
    // 创建一个 ManualResetEventSlim 实例，用于一次性释放所有线程，初始为无信号状态
    private static readonly ManualResetEventSlim manualResetEvent = new ManualResetEventSlim(false);

    // 创建一个 CancellationTokenSource 实例，用于实现优雅的线程关闭
    private static readonly CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();

    public static void Main()
    {
        Console.WriteLine("按回车键释放所有线程，或输入 'exit' 停止程序。");

        // 启动3个工作线程
        for (int i = 1; i <= 3; i++)
        {
            Thread workerThread = new Thread(() => Work(cancellationTokenSource.Token))
            {
                Name = $"Thread {i}", // 设置线程名称
                IsBackground = true // 设置为后台线程，确保主线程结束后程序可以正常退出
            };
            workerThread.Start(); // 启动线程
        }

        // 处理用户输入的控制逻辑
        HandleUserInput();
        
        Console.WriteLine("服务器已停止。");
    }

    // 处理用户输入的控制方法
    private static void HandleUserInput()
    {
        while (true)
        {
            string? userInput = Console.ReadLine();

            // 如果用户输入 "exit"，则触发取消信号以优雅地停止所有线程
            if (userInput?.ToLower() == "exit")
            {
                cancellationTokenSource.Cancel(); // 触发取消信号
                break;
            }

            // 如果用户按下回车键，则释放所有等待的线程
            if (string.IsNullOrEmpty(userInput))
            {
                manualResetEvent.Set();
            }
        }
    }

    // 工作线程的方法
    private static void Work(CancellationToken cancellationToken)
    {
        Console.WriteLine($"{Thread.CurrentThread.Name} 正在等待信号...");

        // 等待信号或取消请求
        while (!cancellationToken.IsCancellationRequested)
        {
            manualResetEvent.Wait(cancellationToken); // 等待信号或取消请求

            // 检查是否有取消请求，如果有则退出循环
            if (cancellationToken.IsCancellationRequested)
            {
                Console.WriteLine($"{Thread.CurrentThread.Name} 收到取消请求，停止工作。");
                break;
            }

            // 模拟工作，释放后进行工作处理
            Thread.Sleep(1000);
            Console.WriteLine($"{Thread.CurrentThread.Name} 已被释放。");
        }
    }
}
```

### 逐行解释

1. **`private static readonly ManualResetEventSlim manualResetEvent = new ManualResetEventSlim(false);`**
   - 创建一个 `ManualResetEventSlim` 实例 `manualResetEvent`，用于一次性释放所有等待的线程，初始状态为无信号状态（`false`）。

2. **`private static readonly CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();`**
   - 创建一个 `CancellationTokenSource` 实例 `cancellationTokenSource`，用于实现优雅的线程关闭，通过取消请求通知线程终止。

3. **`Console.WriteLine("按回车键释放所有线程，或输入 'exit' 停止程序。");`**
   - 输出提示信息，告诉用户按回车键可以释放所有线程，输入 `"exit"` 可以终止程序。

4. **启动工作线程的 `for` 循环**
   - 循环启动 3 个线程，每个线程执行 `Work` 方法，并传入取消令牌。

5. **`Thread workerThread = new Thread(() => Work(cancellationTokenSource.Token))`**
   - 创建一个新线程，使用 lambda 表达式启动 `Work` 方法，并传递 `CancellationToken`，以便在需要时可以响应取消请求。

6. **`Name = $"Thread {i}", IsBackground = true`**
   - 设置线程名称（如 "Thread 1", "Thread 2"）并将其设为后台线程 (`IsBackground = true`)，确保主线程结束后程序能正常退出。

7. **`HandleUserInput();`**
   - 调用 `HandleUserInput` 方法，处理用户输入，用于控制信号发送和取消请求。

#### `HandleUserInput` 方法

8. **用户输入处理**
   - `HandleUserInput` 循环等待用户输入：
   - **`if (userInput?.ToLower() == "exit")`**：当用户输入 `"exit"` 时，触发取消信号以优雅关闭所有线程，跳出循环结束程序。
   - **`if (string.IsNullOrEmpty(userInput))`**：当用户按下回车键时，调用 `manualResetEvent.Set()`，将 `manualResetEvent` 设置为有信号状态，释放所有等待的线程。

#### `Work` 方法

9. **`Console.WriteLine($"{Thread.CurrentThread.Name} 正在等待信号...");`**
   - 输出当前线程名称，指示该线程正在等待信号。

10. **`manualResetEvent.Wait(cancellationToken);`**
    - 调用 `Wait` 方法等待信号或取消请求。通过传入 `CancellationToken`，如果收到取消请求时将自动停止等待，实现优雅的退出。

11. **取消请求检查**
    - 当 `Wait` 方法返回后，检查取消请求 (`cancellationToken.IsCancellationRequested`) 是否触发。如果是，输出线程停止消息并退出循环。

12. **工作模拟**
    - 当线程被释放时，模拟工作操作，通过 `Thread.Sleep(1000)` 休眠 1 秒，然后输出已被释放的消息。

### 最佳实践总结

- **优雅退出**：通过 `CancellationTokenSource` 实现优雅的退出机制，让所有线程在接收到取消请求后能够安全地完成当前任务后退出，避免程序强制中止。
- **后台线程**：将工作线程设置为后台线程 (`IsBackground = true`)，以确保主线程结束时程序能正常退出。
- **用户控制信号**：使用 `ManualResetEventSlim` 允许主线程控制何时释放所有工作线程，而 `CancellationToken` 确保在需要时线程可以安全地停止工作。
- **代码封装**：将用户输入处理封装在 `HandleUserInput` 方法中，使代码更清晰易读。
