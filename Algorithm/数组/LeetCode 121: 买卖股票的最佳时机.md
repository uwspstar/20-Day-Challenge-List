### LeetCode 121: 买卖股票的最佳时机 (Best Time to Buy and Sell Stock)

**题目描述**：  
给定一个表示股票价格的数组 `prices`，其中 `prices[i]` 是第 `i` 天的价格。你只能在某一天买入这只股票，并在未来的某一天卖出，计算你可以获得的最大利润。如果无法获得利润，返回 0。

[LeetCode 121: Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

---

### 解题思路

1. **初始化最低买入价格和最大利润**：  
   - 使用 `buy` 来记录当前遇到的最低买入价格，初始为第一个元素 `prices[0]`。
   - 使用 `max_p` 来记录当前最大利润，初始为 0（即没有利润）。

2. **遍历每一天的价格**：  
   - 如果当天价格 `p` 比 `buy` 更低，则更新 `buy`，因为更低的买入价格可能带来更高的利润。
   - 如果当天价格 `p` 高于 `buy`，计算以当前价格卖出的利润 `p - buy`，并更新 `max_p` 为最大利润。

3. **返回结果**：  
   - 遍历结束后，`max_p` 就是最大利润。

---

### 代码实现

```python
from typing import List

class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # 初始化买入价格和最大利润
        buy = prices[0]
        max_p = 0
        
        # 从第二天开始遍历价格
        for p in prices[1:]:
            if p < buy:
                # 更新最低买入价格
                buy = p
            else:
                # 计算当前利润并更新最大利润
                max_p = max(max_p, p - buy)
        
        return max_p
```

---

### 逐行解释

1. **初始化最低买入价格和最大利润**：
   ```python
   buy = prices[0]
   max_p = 0
   ```
   - `buy` 初始化为第 0 天的价格，即买入价格的最低值。
   - `max_p` 初始化为 0，表示当前最大利润。

2. **遍历每一天的价格，从第 1 天开始**：
   ```python
   for p in prices[1:]:
   ```
   - 逐步遍历 `prices` 数组，从第二天的价格 `prices[1]` 开始。

3. **检查是否更新买入价格**：
   ```python
   if p < buy:
       buy = p
   ```
   - 如果当天价格 `p` 小于 `buy`，则更新 `buy` 为更低的价格，因为这样可以获得更高的潜在利润。

4. **计算当前利润并更新最大利润**：
   ```python
   else:
       max_p = max(max_p, p - buy)
   ```
   - 如果 `p >= buy`，计算当前利润 `p - buy`，并将 `max_p` 更新为两者之间的较大值，确保 `max_p` 存储的是当前的最大利润。

5. **返回结果**：
   ```python
   return max_p
   ```
   - 返回 `max_p`，即可获得的最大利润。

---

### 示例讲解：逐步解析示例步骤

假设输入 `prices = [7, 1, 5, 3, 6, 4]`：

1. **初始化**：
   - `buy = 7`, `max_p = 0`

2. **第 1 天价格 = 1**：
   - `p = 1`
   - `p < buy`，更新 `buy = 1`
   - `max_p` 不变，仍为 0

3. **第 2 天价格 = 5**：
   - `p = 5`
   - `p >= buy`，计算 `p - buy = 5 - 1 = 4`
   - 更新 `max_p = max(0, 4) = 4`

4. **第 3 天价格 = 3**：
   - `p = 3`
   - `p >= buy`，计算 `p - buy = 3 - 1 = 2`
   - `max_p` 不变，仍为 4

5. **第 4 天价格 = 6**：
   - `p = 6`
   - `p >= buy`，计算 `p - buy = 6 - 1 = 5`
   - 更新 `max_p = max(4, 5) = 5`

6. **第 5 天价格 = 4**：
   - `p = 4`
   - `p >= buy`，计算 `p - buy = 4 - 1 = 3`
   - `max_p` 不变，仍为 5

**最终结果**：最大利润 `max_p = 5`

---

### 总结

- **一次遍历实现 O(n) 复杂度**：该算法只需一次遍历，时间复杂度为 O(n)。
- **常量空间 O(1)**：只需要几个额外的变量来存储 `buy` 和 `max_p`，所以空间复杂度为 O(1)。
- **最优买卖策略**：通过跟踪最低买入价格和最大利润，算法高效地计算出最佳买卖时机。
