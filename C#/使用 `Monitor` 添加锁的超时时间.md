### 使用 `Monitor` 添加锁的超时时间

在 C# 中，`Monitor` 类相较于 `lock` 语句提供了更细致的控制。`Monitor` 的一个重要功能是可以在尝试获取锁时设置超时时间，这允许线程在指定时间内尝试获取锁。如果在超时时间内无法获得锁，线程可以执行替代操作，而不是无限等待。这种方法有助于避免死锁并提高程序响应性。

### `Monitor.TryEnter` 的语法

```csharp
bool Monitor.TryEnter(object obj, int millisecondsTimeout);
```

- **`obj`**: 要加锁的对象（必须是所有线程中共享的同一对象）。
- **`millisecondsTimeout`**: 等待锁的最长时间（以毫秒为单位）。
  - `0` 表示不等待（立即返回）。
  - `Timeout.Infinite`（-1）表示无限等待。

`Monitor.TryEnter` 如果在指定时间内成功获取锁，则返回 `true`；如果超时未能获取锁，则返回 `false`。

---

### 示例：使用带超时的 `Monitor`

以下示例中，`Monitor.TryEnter` 使用 500 毫秒的超时时间。如果在这段时间内未能获得锁，线程将跳过临界区代码并执行替代操作。

```csharp
using System;
using System.Threading;

class Program
{
    private static readonly object lockObject = new object();
    private static int sharedResource = 0;

    static void Main(string[] args)
    {
        Thread t1 = new Thread(AccessResource);
        Thread t2 = new Thread(AccessResource);

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();
    }

    static void AccessResource()
    {
        // 尝试获取锁，超时为 500 毫秒
        if (Monitor.TryEnter(lockObject, 500))
        {
            try
            {
                // 临界区
                Console.WriteLine("锁被线程 " + Thread.CurrentThread.ManagedThreadId + " 获得");
                sharedResource++;
                Console.WriteLine("共享资源更新为: " + sharedResource);
                Thread.Sleep(1000); // 模拟工作
            }
            finally
            {
                // 释放锁
                Monitor.Exit(lockObject);
                Console.WriteLine("锁被线程 " + Thread.CurrentThread.ManagedThreadId + " 释放");
            }
        }
        else
        {
            // 如果在超时时间内未获得锁，执行替代操作
            Console.WriteLine("线程 " + Thread.CurrentThread.ManagedThreadId + " 未能在超时时间内获得锁。");
        }
    }
}
```

### 代码解释

1. **带超时的锁尝试**：
   - `Monitor.TryEnter(lockObject, 500)` 试图以 500 毫秒的超时时间获取 `lockObject` 的锁。
   - 如果成功，则进入临界区；否则，执行替代操作。

2. **临界区**：
   - 在 `try` 块内，临界区代码对 `sharedResource` 进行更新。
   - `Thread.Sleep(1000);` 模拟临界区内的工作，演示锁的持有时间。

3. **释放锁**：
   - `finally` 块确保在临界区完成后调用 `Monitor.Exit(lockObject);` 释放锁，即使发生异常时也会释放锁。

4. **替代操作**：
   - 如果在超时时间内未能获得锁，`else` 块会执行，允许线程跳过临界区并继续其他操作。

### 使用 `Monitor.TryEnter` 的优势

- **防止死锁**：超时可以减少死锁风险，因为线程不会无限等待锁。
- **非阻塞选项**：如果在指定时间内无法获取锁，线程可以继续执行其他任务或采取替代措施，从而提高应用程序响应性。
- **可控等待**：超时允许开发者控制线程等待锁的时间，有助于避免性能瓶颈。

---

### 关键点与提示

- **始终在 `finally` 块中使用 `Monitor.Exit`**：以确保即使临界区中发生异常，锁也会被释放。
- **选择合适的超时时间**：考虑程序响应性要求，选择合理的等待时间。
- **避免在临界区内执行长时间操作**：为了减少竞争，使用锁时尽量避免在临界区内执行耗时的操作。

---

### 常见面试问题

1. **`lock` 和 `Monitor` 有什么区别？**
   - 解释 `lock` 是 `Monitor.Enter` 和 `Monitor.Exit` 的语法糖，具有隐含的 `try-finally` 结构。讨论使用 `Monitor` 的场景，例如使用 `Monitor.TryEnter` 来设置超时。

2. **`Monitor.TryEnter` 如何帮助避免死锁？**
   - 描述通过在获取锁时设置超时，防止线程无限等待，从而减少死锁的风险。

3. **为什么建议在 `finally` 块中使用 `Monitor.Exit`？**
   - 确保即使抛出异常，锁也会被释放，防止锁泄露和潜在的死锁。

---

### 总结

使用带超时的 `Monitor.TryEnter` 为锁的获取增加了灵活性，使线程避免无限等待，从而提高响应性并减少死锁风险。这种方法在需要避免长时间阻塞的场景中特别有用。通过设置合适的超时时间并正确释放锁，`Monitor` 有助于在多线程应用中实现安全、高效的资源管理。
