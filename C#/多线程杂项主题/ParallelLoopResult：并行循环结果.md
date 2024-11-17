### **ParallelLoopResult：并行循环结果**

在 C# 中，使用 **`Parallel.For`** 或 **`Parallel.ForEach`** 并行循环时，这些方法会返回一个 **`ParallelLoopResult`** 对象。通过这个对象，可以查看并行循环的执行结果，例如循环是否完整执行或被中途停止。

---

### **ParallelLoopResult 的属性**

| **属性**                  | **类型**       | **描述**                                              |
|---------------------------|----------------|------------------------------------------------------|
| **IsCompleted**           | `bool`         | 指示循环是否完整运行完所有迭代，没有被 `Stop` 或 `Break` 提前终止。 |
| **LowestBreakIteration**  | `long?`        | 如果调用了 `Break()`，此属性返回最小的中断迭代索引。若未调用 `Break()`，则为 `null`。 |

---

### **关键功能**

1. **完成状态（`IsCompleted`）**：
   - 如果循环运行了所有迭代，则返回 `true`。
   - 如果循环被 `Stop()` 或 `Break()` 提前停止，则返回 `false`。

2. **中断迭代索引（`LowestBreakIteration`）**：
   - 当循环被 `Break()` 停止时，返回触发 `Break()` 的最小索引值。
   - 如果未调用 `Break()`，此属性为 `null`。

---

### **示例代码**

#### **1. 使用 `Parallel.For` 获取结果**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        ParallelLoopResult result = Parallel.For(0, 10, (i, state) =>
        {
            Console.WriteLine($"正在处理第 {i} 次迭代");

            if (i == 5)
            {
                Console.WriteLine("调用 Break()");
                state.Break(); // 停止后续更高索引的迭代
            }
        });

        // 查看循环结果
        Console.WriteLine($"循环是否完成：{result.IsCompleted}");
        Console.WriteLine($"最低中断迭代索引：{result.LowestBreakIteration}");
    }
}
```

**输出**（线程执行顺序可能不同）：
```
正在处理第 0 次迭代
正在处理第 1 次迭代
正在处理第 2 次迭代
正在处理第 3 次迭代
正在处理第 4 次迭代
正在处理第 5 次迭代
调用 Break()
循环是否完成：False
最低中断迭代索引：5
```

**解释**：
- **`IsCompleted`**：由于调用了 `Break()`，返回 `false`，表示循环未完整执行。
- **`LowestBreakIteration`**：返回 `5`，因为 `Break()` 在第 5 次迭代被调用。

---

#### **2. 使用 `Stop()` 查看结果**

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        ParallelLoopResult result = Parallel.For(0, 10, (i, state) =>
        {
            Console.WriteLine($"正在处理第 {i} 次迭代");

            if (i == 3)
            {
                Console.WriteLine("调用 Stop()");
                state.Stop(); // 停止所有新迭代
            }
        });

        // 查看循环结果
        Console.WriteLine($"循环是否完成：{result.IsCompleted}");
        Console.WriteLine($"最低中断迭代索引：{result.LowestBreakIteration}");
    }
}
```

**输出**（线程执行顺序可能不同）：
```
正在处理第 0 次迭代
正在处理第 1 次迭代
正在处理第 2 次迭代
正在处理第 3 次迭代
调用 Stop()
循环是否完成：False
最低中断迭代索引：
```

**解释**：
- **`IsCompleted`**：由于调用了 `Stop()`，返回 `false`，表示循环未完整执行。
- **`LowestBreakIteration`**：返回 `null`，因为 `Break()` 未被调用。

---

### **Stop 和 Break 的比较**

| **功能**                  | **Stop()**                                | **Break()**                               |
|---------------------------|-------------------------------------------|------------------------------------------|
| **IsCompleted**           | 总是返回 `false`                         | 如果调用了 `Break()`，返回 `false`。         |
| **LowestBreakIteration**  | 返回 `null`                              | 返回调用 `Break()` 的最小索引值。             |
| **行为**                  | 阻止所有新迭代，无论索引大小。             | 阻止高于当前索引的迭代，但允许低于当前索引的迭代完成。 |

---

### **适用场景**

1. **检查是否完整执行**：
   - 使用 `IsCompleted` 来判断循环是否运行完所有迭代。
   
2. **分析中断位置**：
   - 使用 `LowestBreakIteration` 查看触发 `Break()` 的迭代索引。

3. **调试和日志记录**：
   - 利用 `ParallelLoopResult` 的属性记录并行循环的执行情况，便于分析和调试。

---

### **最佳实践**

1. **结合 Stop 和 Break**：
   - 根据需求选择使用 `Stop()` 或 `Break()` 来终止循环，并使用 `ParallelLoopResult` 进行检查。

2. **记录执行状态**：
   - 在复杂的并行逻辑中，记录 `ParallelLoopResult` 的状态，便于诊断问题。

3. **避免过度依赖顺序**：
   - `Break()` 对迭代顺序敏感，因此在无序并行处理中优先考虑 `Stop()`。

---

### **总结**

- **`ParallelLoopResult`** 是分析并行循环执行状态的重要工具。
- **关键属性**：
  - `IsCompleted`：判断循环是否完整运行。
  - `LowestBreakIteration`：确定触发 `Break()` 的最低索引。
- 通过灵活使用 `Stop()` 和 `Break()`，结合 `ParallelLoopResult`，可以更精确地控制和监测并行循环的执行流程，提高程序的鲁棒性。
