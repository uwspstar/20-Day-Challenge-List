### LeetCode 202: 快乐数 (Happy Number)

**题目描述**：  
对于一个正整数 `n`，我们定义一个过程：每次将数字的每一位平方后相加，如果最终结果为 `1`，则 `n` 是一个快乐数。如果这个过程产生循环而无法得到 `1`，则 `n` 不是快乐数。  
要求编写一个算法来判断 `n` 是否为快乐数。

[LeetCode 202: Happy Number](https://leetcode.com/problems/happy-number/)

---

### 解题思路

1. **快慢指针检测循环**：
   - 使用类似于链表中检测循环的快慢指针方法来判断是否进入循环。
   - 定义两个指针 `slow` 和 `fast`：
     - `slow` 每次执行一次平方和计算。
     - `fast` 每次执行两次平方和计算。
   - 如果 `slow` 和 `fast` 相遇，说明 `n` 进入了循环，意味着 `n` 不是快乐数。
   - 如果 `fast` 指针最终到达 `1`，则说明 `n` 是快乐数。

2. **辅助函数 `sumOfSquares`**：
   - 计算一个数字 `n` 的每一位的平方和，返回该值。
   - 例如，对于 `n = 19`，`sumOfSquares(19) = 1^2 + 9^2 = 82`。

---

### 代码实现

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        # 初始化快慢指针
        slow, fast = n, self.sumOfSquares(n)

        # 使用快慢指针检测循环
        while slow != fast:
            fast = self.sumOfSquares(fast)
            fast = self.sumOfSquares(fast)
            slow = self.sumOfSquares(slow)
        
        # 如果快指针最终到达 1，则 n 是快乐数
        return True if fast == 1 else False
    
    def sumOfSquares(self, n: int) -> int:
        output = 0

        # 计算 n 的每一位平方和
        while n:
            digit = n % 10
            output += digit ** 2
            n = n // 10
        return output
```

---

### 逐行解释

1. **初始化快慢指针**：
   ```python
   slow, fast = n, self.sumOfSquares(n)
   ```
   - `slow` 初始为 `n` 本身。
   - `fast` 初始为 `sumOfSquares(n)`，即 `n` 的每位数字平方和。

2. **检测循环**：
   ```python
   while slow != fast:
       fast = self.sumOfSquares(fast)
       fast = self.sumOfSquares(fast)
       slow = self.sumOfSquares(slow)
   ```
   - 如果 `slow` 和 `fast` 相遇，则说明出现循环。
   - 每次循环中，`fast` 执行两次平方和计算，而 `slow` 执行一次。

3. **判断结果**：
   ```python
   return True if fast == 1 else False
   ```
   - 如果 `fast` 最终等于 `1`，则说明 `n` 是快乐数，返回 `True`；否则，返回 `False`。

4. **辅助函数 `sumOfSquares`**：
   ```python
   def sumOfSquares(self, n: int) -> int:
       output = 0
       while n:
           digit = n % 10
           output += digit ** 2
           n = n // 10
       return output
   ```
   - 逐位计算 `n` 的每位数字的平方和并返回。

---

### 示例讲解

假设输入 `n = 19`：

1. **初始状态**：`slow = 19`，`fast = sumOfSquares(19) = 82`

2. **迭代过程**：
   - 第 1 步：  
     - `slow = sumOfSquares(19) = 82`
     - `fast = sumOfSquares(sumOfSquares(82)) = sumOfSquares(68) = 100`
   - 第 2 步：  
     - `slow = sumOfSquares(82) = 68`
     - `fast = sumOfSquares(sumOfSquares(100)) = sumOfSquares(1) = 1`
   
   - 此时 `fast = 1`，意味着 `n = 19` 是一个快乐数。

---

### 复杂度分析

- **时间复杂度**：O(log n)，对于每次计算平方和操作，最多需要处理 `log n` 位数字。
- **空间复杂度**：O(1)，只需要常量空间来存储 `slow` 和 `fast`。

---

### 总结

这段代码使用了快慢指针检测循环的技巧来判断是否是快乐数：
- 快慢指针可以高效检测循环。
- 通过平方和操作逐步计算每一位的平方和并判断是否到达 `1`。
