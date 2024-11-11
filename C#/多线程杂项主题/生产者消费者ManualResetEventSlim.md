### 生产者消费者 ManualResetEventSlim

```mermaid
flowchart TD
    Start["Start Program"] --> |Main| StartConsumers
    Start --> |Main| RunProducer
    
    subgraph QueueControl["Queue Control Mechanism"]
        direction TB
        consumeEvent["consumeEvent (ManualResetEventSlim)"]
        produceEvent["produceEvent (ManualResetEventSlim)"]
    end
    
    subgraph ProducerConsumer["Producer & Consumer Threads"]
        direction TB
        
        RunProducer["RunProducer - Producer Logic"]
        ProduceItems["ProduceItems - Produce Items to Queue"]
        Consume["Consume - Consumer Logic"]
        ConsumerThreads["StartConsumers - Create Consumer Threads"]
    end
    
    ConsumerThreads --> |Creates Consumers| Consume
    
    RunProducer --> |Wait for produceEvent| ProduceItems
    RunProducer -.-> |Waits for 'p' input| ProduceItems
    ProduceItems --> |Enqueue items to queue| queue((Queue))
    queue --> Consume
    
    Consume --> |Dequeue items from queue| ConsumerCount["Increment consumerCount"]
    ConsumerCount --> |Checks if all consumers done| ResetEvents["Reset Events for Producer"]
    
    ResetEvents --> |Reset consumeEvent and allow Producer| RunProducer
    
    consumeEvent --> |Signals when items ready| Consume
    produceEvent --> |Allows Producer to produce items| RunProducer
    
    NoteStart["System waits for 'p' input to produce items"]
    NoteConsumers["Consumers consume items until queue is empty"]
    
    RunProducer --> NoteStart
    Consume --> NoteConsumers
```

```csharp
using System;
using System.Collections.Generic;
using System.Threading;

public class Program
{
    // 队列，用于存储生产者生成的项目
    private static readonly Queue<int> queue = new Queue<int>();

    // ManualResetEventSlim 控制消费者的等待
    private static readonly ManualResetEventSlim consumeEvent = new ManualResetEventSlim(false);

    // ManualResetEventSlim 控制生产者的等待
    private static readonly ManualResetEventSlim produceEvent = new ManualResetEventSlim(true);

    // 记录已完成消费的消费者数量
    private static int consumerCount = 0;

    // 锁对象，用于同步更新 consumerCount
    private static readonly object lockConsumerCount = new object();

    public static void Main()
    {
        // 启动消费者线程
        StartConsumers();

        // 启动生产者逻辑
        RunProducer();
    }

    // 启动消费者线程的方法
    private static void StartConsumers()
    {
        for (int i = 0; i < 3; i++)
        {
            Thread consumerThread = new Thread(Consume)
            {
                Name = $"Consumer {i + 1}", // 设置消费者线程名称
                IsBackground = true // 设置为后台线程
            };
            consumerThread.Start();
        }
    }

    // 生产者逻辑方法
    private static void RunProducer()
    {
        while (true)
        {
            // 等待生产者事件信号
            produceEvent.Wait();

            // 重置生产事件，防止过多生产
            produceEvent.Reset();

            Console.WriteLine("输入 'p' 以生产新项目");

            // 等待用户输入控制生产
            var input = Console.ReadLine() ?? "";

            // 当用户输入 'p' 时，触发生产操作
            if (input.ToLower() == "p")
            {
                ProduceItems(); // 调用生产项目的方法
                consumeEvent.Set(); // 设置消费事件，通知消费者开始消费
            }
        }
    }

    // 生成项目的方法
    private static void ProduceItems()
    {
        for (int i = 1; i <= 10; i++)
        {
            queue.Enqueue(i); // 将项目加入队列
            Console.WriteLine($"Produced: {i}");
        }
    }

    // 消费者的逻辑
    private static void Consume()
    {
        while (true)
        {
            // 等待消费事件的信号
            consumeEvent.Wait();

            // 从队列中取出项目进行消费
            while (queue.TryDequeue(out int item))
            {
                Thread.Sleep(500); // 模拟消费时间
                Console.WriteLine($"Consumed: {item} from thread: {Thread.CurrentThread.Name}");
            }

            // 更新消费者计数，检查是否所有消费者已完成消费
            lock (lockConsumerCount)
            {
                consumerCount++;

                if (consumerCount == 3)
                {
                    // 当所有消费者完成消费时，重置消费事件，允许生产者继续生产
                    consumeEvent.Reset();
                    produceEvent.Set();
                    consumerCount = 0; // 重置计数器

                    Console.WriteLine("****************");
                    Console.WriteLine("**** More Please! *****");
                    Console.WriteLine("****************");
                }
            }
        }
    }
}
```
---

```csharp
// 等待生产者事件信号
produceEvent.Wait();
```

**解释**：`produceEvent.Wait();` 会让生产者线程等待，直到 `produceEvent` 被设置为有信号状态。这一行的目的是控制生产者在每一轮生产前都需要等待一个信号。通过这种方式，我们可以确保在当前的生产任务完成后，消费者准备好再次消费时才允许生产者继续生产。这种控制机制避免了生产过多资源，导致队列中的项目积压。

---

```csharp
// 重置生产事件，防止过多生产
produceEvent.Reset();
```

**解释**：`produceEvent.Reset();` 将 `produceEvent` 重置为无信号状态，阻止生产者立即再次进入生产流程。每次生产完成后，都要重置生产事件信号，这样可以防止生产者连续生产，直到消费者处理完当前的项目并请求新的生产。这种方式能够有效地协调生产者和消费者的工作，使得生产和消费之间保持同步，避免了资源浪费和潜在的过量生产问题。

```csharp
consumeEvent.Reset();
```

**解释**：`consumeEvent.Reset();` 将 `consumeEvent` 事件重置为无信号状态，阻止消费者线程继续消费。此行代码的目的是在所有消费者完成当前消费任务后，停止消费者的操作，等待下一轮生产完成后再开启消费。这一操作确保了消费者不会在生产者未生产新项目时继续尝试消费，从而避免了无效的循环等待。

---

```csharp
produceEvent.Set();
```

**解释**：`produceEvent.Set();` 将 `produceEvent` 事件设置为有信号状态，通知生产者可以开始新一轮的生产。此行代码的目的是在所有消费者完成当前消费并重置 `consumeEvent` 后，释放生产者线程，让生产者可以进入下一轮的生产操作。这种控制方式保证了生产者和消费者之间的协调工作，即只有当当前的消费任务完成后，生产者才会被允许生产新的项目，避免了资源的积压和浪费。

---

### 代码逐行解释

1. **`private static void Main()`**  
   - 主方法，程序的入口，启动消费者线程并运行生产者逻辑。

2. **`private static void StartConsumers()`**
   - 用于启动消费者线程的辅助方法。创建 3 个消费者线程，并将它们设为后台线程，以确保主线程结束后程序能正常退出。

3. **`private static void RunProducer()`**
   - 生产者的主逻辑。等待用户输入 `'p'` 来生成新项目，当输入匹配时调用 `ProduceItems()` 方法生成项目。

4. **`private static void ProduceItems()`**
   - 生成项目的辅助方法。循环生成 10 个项目并将它们添加到队列中，便于消费者消费。

5. **`private static void Consume()`**
   - 消费者线程的工作方法。等待消费事件的信号（`consumeEvent.Wait()`），在信号为有信号状态时从队列中取出项目进行消费。每个线程消费一个项目后，检查是否所有消费者都已完成消费。

6. **`lock (lockConsumerCount)`**
   - 使用锁保护 `consumerCount` 变量，确保多个消费者线程同步更新计数。当所有消费者完成时，重置 `consumeEvent` 并允许生产者继续生产新项目。

### 最佳实践总结

- **逻辑分离**：将生产者逻辑和消费者线程的启动分离到单独的方法 `RunProducer()` 和 `StartConsumers()` 中，增强代码的可读性和维护性。
- **后台线程**：设置消费者线程为后台线程，以确保主线程结束时可以自动终止，避免阻塞程序退出。
- **线程安全**：使用锁对象 `lockConsumerCount` 来保护 `consumerCount`，确保多线程环境下的线程安全。
- **事件控制**：`ManualResetEventSlim` 的 `Set` 和 `Reset` 控制线程的同步，确保生产和消费的有序进行，避免资源浪费。


