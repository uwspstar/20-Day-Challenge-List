### LeetCode 155: 最小栈 (Min Stack)

**题目描述**：  
设计一个支持 `push`, `pop`, `top`, 和 `getMin` 操作的最小栈。  
- `push(x)` -- 将元素 x 推入栈中。
- `pop()` -- 删除栈顶的元素。
- `top()` -- 获取栈顶元素。
- `getMin()` -- 检索栈中的最小元素。

[LeetCode 155: Min Stack](https://leetcode.com/problems/min-stack/)

**代码实现**：
```python
# 定义最小栈的类
class MinStack:

    def __init__(self):
        # 初始化两个栈：一个用于存储所有元素，一个用于存储最小值
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        # 将元素推入栈中
        self.stack.append(val)
        # 如果最小栈为空或当前元素小于等于最小栈的栈顶元素，将其推入最小栈
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        # 弹出栈顶元素，如果栈顶元素等于最小栈的栈顶元素，则同时弹出最小栈的栈顶元素
        if self.stack.pop() == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self) -> int:
        # 返回栈顶元素
        return self.stack[-1]

    def getMin(self) -> int:
        # 返回最小栈的栈顶元素，即最小值
        return self.min_stack[-1]

# 时间复杂度：所有操作均为 O(1) - 因为每个操作只涉及栈的栈顶。
# 空间复杂度：O(n) - 需要额外的栈来存储最小值。
```

**题目分析**：
我们需要设计一个支持常数时间复杂度的最小栈。为实现这一点，可以使用两个栈：  
- 一个用于存储所有元素的主栈。
- 一个用于存储当前最小值的辅助栈。

**解决方案详解**：

- **初始化**：
  - 创建两个栈：`stack` 用于存储所有元素，`min_stack` 用于存储最小值。

- **push**：
  - 将元素推入主栈。
  - 如果辅助栈为空或当前元素小于等于辅助栈的栈顶元素，将其推入辅助栈。

- **pop**：
  - 弹出主栈的栈顶元素，如果该元素等于辅助栈的栈顶元素，则同时弹出辅助栈的栈顶元素。

- **top**：
  - 返回主栈的栈顶元素。

- **getMin**：
  - 返回辅助栈的栈顶元素（当前最小值）。

**复杂度分析**：
- **时间复杂度**：所有操作均为 O(1)，因为每个操作仅涉及栈的栈顶。
- **空间复杂度**：O(n)，其中 n 是栈中元素的数量，最坏情况下，最小栈和主栈存储相同数量的元素。

**示例讲解**：

#### 示例 1:

```python
minStack = MinStack()
minStack.push(-2)  # stack: [-2], min_stack: [-2]
minStack.push(0)   # stack: [-2, 0], min_stack: [-2]
minStack.push(-3)  # stack: [-2, 0, -3], min_stack: [-2, -3]
minStack.getMin()  # 返回 -3
minStack.pop()     # stack: [-2, 0], min_stack: [-2]
minStack.top()     # 返回 0
minStack.getMin()  # 返回 -2
```

- 初始状态，`minStack`为空。
- `push(-2)`，将-2推入两个栈中。
- `push(0)`，仅推入主栈。
- `push(-3)`，将-3推入两个栈中。
- `getMin()` 返回 `-3`，是当前最小值。
- `pop()` 弹出 -3，同时从辅助栈中弹出。
- `top()` 返回 0，当前栈顶元素。
- `getMin()` 返回 `-2`，更新的最小值。

**总结**：
- 使用双栈结构可在常数时间内完成最小值检索，适用于类似栈操作的题目。
