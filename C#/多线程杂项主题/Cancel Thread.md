```csharp
using System;
using System.Threading;

class Program
{
    // 用于指示是否取消线程的布尔变量
    static bool cancelThread = false;

    static void Main()
    {
        // 创建并启动新线程，执行 Work 方法
        Thread thread = new Thread(Work);
        thread.Start();

        Console.WriteLine("按下 'c' 以取消工作");
        
        // 获取用户输入，如果输入 'c' 则设置 cancelThread 为 true，表示取消线程
        var input = Console.ReadLine();
        if (input == "c")
        {
            cancelThread = true;
        }

        // 等待线程完成，确保主线程在工作线程结束后才继续执行
        thread.Join();

        // 等待用户按下回车键以结束程序
        Console.ReadLine();
    }

    // 执行工作任务的函数
    static void Work()
    {
        Console.WriteLine("开始执行工作任务...");

        // 模拟一个循环的工作任务
        for (int i = 0; i < 100000; i++)
        {
            // 检查是否收到取消请求
            if (cancelThread)
            {
                Console.WriteLine($"用户请求取消，当前迭代次数: {i}");
                break;  // 跳出循环，停止工作
            }

            // 使用 SpinWait 模拟耗时任务，这里可以理解为占用 CPU 的计算任务
            Thread.SpinWait(300000);
        }

        // 如果没有被取消，任务执行完成
        Console.WriteLine("工作任务已完成");
    }
}
```

### 代码解释
1. **bool cancelThread = false**:  初始化 `cancelThread` 变量，用于标记是否取消工作线程。
2. **Thread thread = new Thread(Work)**:  创建一个新线程，并指定 `Work` 方法为该线程的执行体。
3. **thread.Start()**: 启动线程，开始执行 `Work` 方法。
4. **Console.ReadLine() 与条件判断**: 等待用户输入，如果输入 `'c'`，则将 `cancelThread` 设置为 `true`，表示用户希望取消工作。
5. **thread.Join()**: 主线程等待工作线程完成，以确保所有工作完成后再继续。
6. **Work 方法中的循环**: 循环执行模拟任务，如果 `cancelThread` 为 `true`，则在控制台输出取消信息并跳出循环。

### 最佳实践
- **线程控制变量**： 使用共享布尔变量 `cancelThread` 以跨线程通讯方式安全终止线程。
- **线程安全**：避免过于频繁的线程锁定，使用标记变量检查状态
