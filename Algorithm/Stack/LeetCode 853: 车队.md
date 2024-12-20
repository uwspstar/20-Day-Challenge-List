这是 **LeetCode 853: 车队 (Car Fleet)** 问题的解决方案。它使用栈来计算从各自位置出发的汽车能否组成车队，并返回最终形成的车队数量。

---

### LeetCode 853: 车队 (Car Fleet)

**题目描述**：  
在一条单向车道上，有 `n` 辆汽车，每辆车的位置和速度分别由 `position[i]` 和 `speed[i]` 表示。所有汽车最终会行驶到目标 `target`。如果一辆更慢的车在前，且被后面的更快的车追上，它们会组成一个车队，以较慢车的速度继续前行。请计算并返回最终车队的数量。

[LeetCode 853: Car Fleet](https://leetcode.com/problems/car-fleet/)

---

### 解题思路

1. **排序汽车位置**：
   - 首先，我们将汽车按位置 `position` 从远到近进行排序（即离目标最近的在前），这样可以按顺序从后往前检查每辆车是否会被后面更快的车追上。

2. **计算到达目标所需时间**：
   - 对于每辆车，计算从当前位置 `position[i]` 到达目标位置 `target` 所需的时间，公式为 `(target - position[i]) / speed[i]`。

3. **使用栈模拟车队**：
   - 从离目标最远的车开始向前检查每辆车的时间：
     - 如果当前车所需时间大于栈顶的时间，则说明当前车不会追上栈顶的车队，形成新的车队，因此将其时间加入栈。
     - 如果当前车所需时间小于等于栈顶的时间，说明它会追上栈顶的车队（或已经是车队的一部分），则弹出栈顶时间，因为它们最终会合并成一个车队。
   - 最后栈中时间的数量即为最终的车队数量。

---

### 代码实现

```python
from typing import List

class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        # 初始化一个空栈用于记录车队的到达时间
        stack = []
        
        # 将每辆车的位置和速度组成对，并按位置从远到近排序
        pair = [(p, s) for p, s in zip(position, speed)]
        pair.sort(reverse=True)
        
        # 遍历排序后的每辆车
        for p, s in pair:
            # 计算该车到达目标的时间
            time = (target - p) / s
            # 将时间加入栈，如果这辆车会组成新的车队
            stack.append(time)
            # 如果栈中有两个以上的车队时间，且当前车会追上前一个车队，则合并
            if len(stack) >= 2 and stack[-1] <= stack[-2]:
                stack.pop()  # 弹出当前车的时间
        
        # 栈中剩下的时间即为车队数量
        return len(stack)
```

---

### 逐步执行示例

假设输入为 `target = 12`，`position = [10, 8, 0, 5, 3]`，`speed = [2, 4, 1, 1, 3]`。

#### 步骤 1：按位置排序

按位置从远到近排序后，我们得到 `pair = [(10, 2), (8, 4), (5, 1), (3, 3), (0, 1)]`。

#### 步骤 2：遍历每辆车并计算到达时间

1. **车 `(10, 2)`**：
   - 计算时间：`(12 - 10) / 2 = 1.0`
   - 栈状态：`[1.0]`
   
2. **车 `(8, 4)`**：
   - 计算时间：`(12 - 8) / 4 = 1.0`
   - 栈状态：`[1.0, 1.0]`
   - 由于 `stack[-1] <= stack[-2]`，弹出当前时间
   - 栈状态：`[1.0]`（车 `(8, 4)` 会追上 `(10, 2)`，合并成一个车队）

3. **车 `(5, 1)`**：
   - 计算时间：`(12 - 5) / 1 = 7.0`
   - 栈状态：`[1.0, 7.0]`（新的车队）

4. **车 `(3, 3)`**：
   - 计算时间：`(12 - 3) / 3 = 3.0`
   - 栈状态：`[1.0, 7.0, 3.0]`
   - 由于 `stack[-1] <= stack[-2]`，弹出当前时间
   - 栈状态：`[1.0, 7.0]`（车 `(3, 3)` 会追上 `(5, 1)`，合并成一个车队）

5. **车 `(0, 1)`**：
   - 计算时间：`(12 - 0) / 1 = 12.0`
   - 栈状态：`[1.0, 7.0, 12.0]`（新的车队）

#### 最终结果

栈中的三个时间 `[1.0, 7.0, 12.0]` 代表了最终的 3 个车队，返回 `3`。

---

### 复杂度分析

- **时间复杂度**：O(n log n)，排序 `position` 和 `speed` 的时间复杂度为 O(n log n)，遍历每辆车需要 O(n)。
- **空间复杂度**：O(n)，存储 `pair` 和 `stack` 需要 O(n) 空间。

---

### 总结

该解法通过排序和栈的方式，模拟了车队的形成过程：
- 先按距离目标位置从远到近排序，再逐步计算时间并检测是否会形成新的车队。
- 栈中剩余的时间数即为车队数量。

这是一个高效且直观的解法，符合题目要求的时间复杂度。
