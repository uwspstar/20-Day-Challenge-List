# 栈 (Stack)

## Definition
栈是一种后进先出 (LIFO, Last In First Out) 的数据结构。即最后被添加的元素最先被移除。栈常用于管理函数调用、表达式求值、回溯算法等。

## Key Concepts
- **入栈 (Push)**: 将元素添加到栈顶。
- **出栈 (Pop)**: 移除栈顶元素。
- **栈顶 (Top)**: 当前栈中最上面的元素。
- **栈的空检查 (Is Empty)**: 检查栈是否为空。
  
## 栈的主要操作
1. **Push**: 将元素添加到栈顶。
2. **Pop**: 移除并返回栈顶元素。
3. **Peek/Top**: 返回栈顶元素，但不移除它。
4. **IsEmpty**: 检查栈是否为空。

## 栈的适用场景
- 表达式求值 (如后缀表达式)。
- 递归函数的调用管理。
- 深度优先搜索 (DFS)。
- 括号匹配和语法分析。

## Python 栈实现模板
```python
class Stack:
    def __init__(self):
        self.items = []  # 初始化空栈

    def is_empty(self):
        return len(self.items) == 0  # 检查栈是否为空

    def push(self, item):
        self.items.append(item)  # 入栈

    def pop(self):
        if not self.is_empty():
            return self.items.pop()  # 出栈
        raise IndexError("pop from an empty stack")  # 处理空栈出栈错误

    def peek(self):
        if not self.is_empty():
            return self.items[-1]  # 返回栈顶元素
        raise IndexError("peek from an empty stack")  # 处理空栈查看错误

    def size(self):
        return len(self.items)  # 返回栈的大小
```

## Tips
- 使用栈时要注意栈的大小，以避免栈溢出 (stack overflow)。
- 栈的空间复杂度为 O(n)，其中 n 是栈中元素的数量。

## Warning
- 在递归深度过大时，可能会导致栈溢出。在这种情况下，可以考虑使用循环代替递归。

## Complexity Analysis
- **时间复杂度**: O(1) 对于入栈和出栈操作。
- **空间复杂度**: O(n)，用于存储栈中元素。

---

### 30 stack-related LeetCode questions

---

### 1. LeetCode 20: [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)（有效的括号）
**题目描述**：  
给定一个只包含 '(', ')', '{', '}', '[' 和 ']' 的字符串，确定输入的括号是否是有效的。

**题目分析**：  
使用栈来解决这个问题。当遇到开括号时，将其压入栈中；当遇到闭括号时，检查栈顶是否为对应的开括号。如果栈为空或不匹配，则返回 False。最终，栈为空表示括号匹配有效。

**代码实现**：

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []  # 初始化栈
        mapping = {')': '(', '}': '{', ']': '['}  # 映射表

        for char in s:
            if char in mapping:
                top_element = stack.pop() if stack else '#'  # 取出栈顶元素
                if mapping[char] != top_element:  # 检查是否匹配
                    return False
            else:
                stack.append(char)  # 压入栈中

        return not stack  # 栈为空则有效

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 最坏情况下栈大小等于字符串长度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，最多遍历一次即可检查括号是否匹配。
- **空间复杂度**：O(n)，在最坏情况下，栈可能需要存储所有开括号。

---

### 2. LeetCode 32: [Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)（最长有效括号）
**题目描述**：  
给定一个只包含 '(' 和 ')' 的字符串，找到最长有效（匹配的）括号子串的长度。

**题目分析**：  
使用栈来解决该问题。遍历字符串，将左括号的索引压入栈中。当遇到右括号时，弹出栈顶元素以匹配左括号。如果栈为空，记录当前位置；否则，计算当前有效子串长度。

**代码实现**：

```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        stack = [-1]  # 初始化栈
        max_len = 0

        for i, char in enumerate(s):
            if char == '(':
                stack.append(i)  # 左括号入栈
            else:
                stack.pop()  # 右括号出栈
                if not stack:
                    stack.append(i)  # 空栈时记录当前位置
                else:
                    max_len = max(max_len, i - stack[-1])  # 计算最大长度

        return max_len

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 最坏情况下栈大小等于字符串长度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度。
- **空间复杂度**：O(n)，栈的空间复杂度在最坏情况下为 O(n)。

---

### 3. LeetCode 42: [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)（接雨水）
**题目描述**：  
给定一个数组表示每个位置的高度，计算能接住的雨水总量。

**题目分析**：  
使用单调栈来解决。遍历高度数组，将递减的高度压入栈。当遇到比栈顶大的高度时，计算能接住的雨水量。

**代码实现**：

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = []  # 初始化栈
        water = 0  # 存储雨水总量

        for i, h in enumerate(height):
            while stack and height[stack[-1]] < h:
                top = stack.pop()
                if not stack:
                    break
                distance = i - stack[-1] - 1
                bounded_height = min(height[stack[-1]], h) - height[top]
                water += distance * bounded_height

            stack.append(i)  # 压入当前高度索引

        return water

# 时间复杂度：O(n) - 遍历高度数组一次
# 空间复杂度：O(n) - 最坏情况下栈大小等于数组长度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是高度数组的长度。
- **空间复杂度**：O(n)，在最坏情况下栈可能需要存储所有元素。

---

### 4. LeetCode 71: [Simplify Path](https://leetcode.com/problems/simplify-path/)（简化路径）
**题目描述**：  
给定一个表示 UNIX 文件路径的字符串，将其转换为简化的路径形式。

**题目分析**：  
使用栈来解决此问题。遍历路径，根据每个部分是 ".."、"." 或普通目录，进行相应的压栈或出栈操作。

**代码实现**：

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        stack = []  # 初始化栈
        parts = path.split('/')  # 以 '/' 分割路径

        for part in parts:
            if part == '..':
                if stack:
                    stack.pop()  # 出栈回到上级目录
            elif part and part != '.':
                stack.append(part)  # 压入有效目录

        return '/' + '/'.join(stack)

# 时间复杂度：O(n) - 遍历路径一次
# 空间复杂度：O(n) - 最坏情况下栈大小等于路径长度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是路径字符串的长度。
- **空间复杂度**：O(n)，在最坏情况下栈可能需要存储所有目录名。

---

### 5. LeetCode 84: [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)（柱状图中最大的矩形）
**题目描述**：  
给定一个数组，其中每个元素代表柱状图中柱子的高度，找到能够形成的最大矩形的面积。

**题目分析**：  
使用单调栈来解决该问题。遍历高度数组，当栈顶元素大于当前元素时，计算以栈顶元素为高度的最大矩形面积。

**代码实现**：

```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []  # 初始化栈
        max_area = 0  # 最大矩形面积

        for i, h in enumerate(heights):
            while stack and heights[stack[-1]] > h:
                height = heights[stack.pop()]
                width = i if not stack else i - stack[-1] - 1
                max_area = max(max_area, height * width)
            stack.append(i)

        # 处理栈中剩余元素
        while stack:
            height = heights[stack.pop()]
            width = len(heights) if not stack else len(heights) - stack[-1] - 1
            max_area = max(max_area, height * width)

        return max_area

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 最坏情况下栈大小等于数组长度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，因为每个元素最多进栈和出栈一次。
- **空间复杂度**：O(n)，在最坏情况下栈可能需要存储所有元素。

---

### 6. LeetCode 85: [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)（最大矩形）
**题目描述**：  
给定一个仅包含 0 和 1 的矩阵，找出包含 1 的最大矩形面积。

**题目分析**：  
将矩阵的每一行视为柱状图的底部，并用单调栈计算最大矩形面积。

**代码实现**：

```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if not matrix:
            return 0

        n = len(matrix[0])
        heights = [0] * n
        max_area = 0

        for row in matrix:
            for i in range(n):
                heights[i] = heights[i] + 1 if row[i] == '1' else 0

            max_area = max(max_area, self.largestRectangleArea(heights))

        return max_area

    def largestRectangleArea(self, heights: List[int]) -> int:
        stack = []
        max_area = 0

        for i, h in enumerate(heights):
            while stack and heights[stack[-1]] > h:
                height = heights[stack.pop()]
                width = i if not stack else i - stack[-1] - 1
                max_area = max(max_area, height * width)
            stack.append(i)

        while stack:
            height = heights[stack.pop()]
            width = len(heights) if not stack else len(heights) - stack[-1] - 1
            max_area = max(max_area, height * width)

        return max_area

# 时间复杂度：O(m * n) - 遍历矩阵的每个元素
# 空间复杂度：O(n) - 使用了一个栈和一个高度数组
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(m * n)，其中 m 是矩阵的行数，n 是列数。
- **空间复杂度**：O(n)，用于存储每一行的高度和单调栈。

---

### 7. LeetCode 94: [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)（二叉树的中序遍历）
**题目描述**：  
给定一个二叉树，返回其节点值的中序遍历。

**题目分析**：  
使用栈来模拟递归实现中序遍历。将左节点依次压入栈中，直到最左端节点。

**代码实现**：

```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        stack, result = [], []
        current = root

        while current or stack:
            while current:
                stack.append(current)
                current = current.left
            current = stack.pop()
            result.append(current.val)
            current = current.right

        return result

# 时间复杂度：O(n) - 遍历二叉树的每个节点
# 空间复杂度：O(n) - 最坏情况下栈大小等于树的高度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(n)，最坏情况下，栈的大小等于树的高度。

---

### 8. LeetCode 150: [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)（逆波兰表达式求值）
**题目描述**：  
给定一个逆波兰表达式，求解该表达式的值。

**题目分析**：  
使用栈来求解。遇到数字时压入栈中，遇到运算符时弹出两个元素进行计算，并将结果压回栈中。

**代码实现**：

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for token in tokens:
            if token not in "+-*/":
                stack.append(int(token))
            else:
                b, a = stack.pop(), stack.pop()
                if token == '+':
                    stack.append(a + b)
                elif token == '-':
                    stack.append(a - b)
                elif token == '*':
                    stack.append(a * b)
                elif token == '/':
                    stack.append(int(a / b))

        return stack[0]

# 时间复杂度：O(n) - 遍历令牌数组一次
# 空间复杂度：O(n) - 使用栈存储中间结果
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是表达式中令牌的数量。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有数字。

---

### 9. LeetCode 224: [Basic Calculator](https://leetcode.com/problems/basic-calculator/)（基本计算器）
**题目描述**：  
实现一个基本的计算器，支持加、减法和括号。

**题目分析**：  
使用栈来处理括号和操作数。遍历字符串，遇到数字时累加，遇到操作符时将当前结果与操作符压入栈中。

**代码实现**：

```python
class Solution:
    def calculate(self, s: str) -> int:
        stack = []
        current_number = 0
        result = 0
        sign = 1

        for char in s:
            if char.isdigit():
                current_number = current_number * 10 + int(char)
            elif char in '+-':
                result += sign * current_number
                sign = 1 if char == '+' else -1
                current_number = 0
            elif char == '(':
                stack.append(result)
                stack.append(sign)
                result = 0
                sign = 1
            elif char == ')':
                result += sign * current_number
                result *= stack.pop()
                result += stack.pop()
                current_number = 0

        return result + sign * current_number

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 使用栈存储括号内的计算结果
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有的中间结果。

---

### 16. LeetCode 456: [132 Pattern](https://leetcode.com/problems/132-pattern/)（132 模式）
**题目描述**：  
给定一个整数数组 nums，找出其中是否存在 132 模式的子序列（即存在 i < j < k 使得 nums[i] < nums[k] < nums[j]）。

**题目分析**：  
使用单调栈从右向左遍历数组。在遍历过程中，维护一个 "2" 的候选值，当遇到一个比 "2" 小的元素时，则找到了 132 模式。

**代码实现**：

```python
class Solution:
    def find132pattern(self, nums: List[int]) -> bool:
        stack = []  # 单调栈
        second = float('-inf')  # "2" 的候选值

        for num in reversed(nums):
            if num < second:
                return True
            while stack and num > stack[-1]:
                second = stack.pop()
            stack.append(num)

        return False

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 17. LeetCode 496: [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)（下一个更大元素 I）
**题目描述**：  
给定两个没有重复元素的数组 `nums1` 和 `nums2`，其中 `nums1` 是 `nums2` 的子集。找出 `nums1` 中每个元素在 `nums2` 中的下一个更大元素。

**题目分析**：  
使用单调栈来找到每个元素的下一个更大元素，并将结果存入字典中。

**代码实现**：

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        stack = []
        next_greater = {}
        
        for num in nums2:
            while stack and stack[-1] < num:
                next_greater[stack.pop()] = num
            stack.append(num)
        
        return [next_greater.get(num, -1) for num in nums1]

# 时间复杂度：O(n + m) - 遍历 nums2 和 nums1
# 空间复杂度：O(n) - 栈和字典的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 是 `nums2` 的长度，m 是 `nums1` 的长度。
- **空间复杂度**：O(n)，栈和字典的大小取决于 `nums2` 的长度。

---

### 18. LeetCode 503: [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/)（下一个更大元素 II）
**题目描述**：  
给定一个循环数组，找出每个元素的下一个更大元素。

**题目分析**：  
使用单调栈遍历两遍数组，将元素索引压入栈中，并根据当前元素更新下一个更大元素。

**代码实现**：

```python
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [-1] * n
        stack = []

        for i in range(2 * n):
            while stack and nums[stack[-1]] < nums[i % n]:
                result[stack.pop()] = nums[i % n]
            if i < n:
                stack.append(i)

        return result

# 时间复杂度：O(n) - 遍历数组两次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，因为遍历数组两遍，总共时间复杂度为 O(2n) ≈ O(n)。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 19. LeetCode 581: [Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)（最短无序连续子数组）
**题目描述**：  
给定一个整数数组，找出最短的无序（未排序）连续子数组，使得对其排序后，整个数组变为有序。

**题目分析**：  
使用单调栈来找到最左边和最右边需要排序的位置。

**代码实现**：

```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        stack = []
        left, right = len(nums), 0

        for i in range(len(nums)):
            while stack and nums[stack[-1]] > nums[i]:
                left = min(left, stack.pop())
            stack.append(i)

        stack.clear()

        for i in range(len(nums) - 1, -1, -1):
            while stack and nums[stack[-1]] < nums[i]:
                right = max(right, stack.pop())
            stack.append(i)

        return right - left + 1 if right > left else 0

# 时间复杂度：O(n) - 遍历数组两次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，因为遍历数组两次。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 20. LeetCode 636: [Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions/)（函数的独占时间）
**题目描述**：  
给定一个函数调用日志，计算每个函数的独占时间。

**题目分析**：  
使用栈来模拟函数的开始和结束，计算独占时间。

**代码实现**：

```python
class Solution:
    def exclusiveTime(self, n: int, logs: List[str]) -> List[int]:
        result = [0] * n
        stack = []
        prev_time = 0

        for log in logs:
            func_id, typ, time = log.split(':')
            func_id, time = int(func_id), int(time)

            if typ == 'start':
                if stack:
                    result[stack[-1]] += time - prev_time
                stack.append(func_id)
                prev_time = time
            else:
                result[stack.pop()] += time - prev_time + 1
                prev_time = time + 1

        return result

# 时间复杂度：O(n) - 遍历日志列表一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是日志的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有函数调用。

---

### 21. LeetCode 682: [Baseball Game](https://leetcode.com/problems/baseball-game/)（棒球比赛）
**题目描述**：  
给定一个字符串数组表示棒球比赛的得分，计算最终得分。

**题目分析**：  
使用栈来模拟得分的计算，根据每一轮的得分规则进行相应的操作。

**代码实现**：

```python
class Solution:
    def calPoints(self, ops: List[str]) -> int:
        stack = []

        for op in ops:
            if op == '+':
                stack.append(stack[-1] + stack[-2])
            elif op == 'D':
                stack.append(2 * stack[-1])
            elif op == 'C':
                stack.pop()
            else:
                stack.append(int(op))

        return sum(stack)

# 时间复杂度：O(n) - 遍历操作数组一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是操作数组的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有得分。

---

### 22. LeetCode 739: [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)（每日温度）
**题目描述**：  
给定一个数组 `temperatures`，表示每天的温度，返回一个数组 `answer`，其中 `answer[i]` 表示从第 `i` 天开始，需要经过几天才能等到更高的温度。如果之后没有更高的温度，`answer[i] = 0`。

**题目分析**：  
使用单调栈来解决这个问题。遍历数组时，将当前元素的索引压入栈中，并在找到比栈顶元素大的值时计算天数。

**代码实现**：

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        answer = [0] * len(temperatures)

        for i, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                prev_index = stack.pop()
                answer[prev_index] = i - prev_index
            stack.append(i)

        return answer

# 时间复杂度：O(n) - 遍历温度数组一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是温度数组的长度，每个元素最多进栈和出栈一次。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 23. LeetCode 768: [Max Chunks To Make Sorted II](https://leetcode.com/problems/max-chunks-to-make-sorted-ii/)（最多能完成排序的块 II）
**题目描述**：  
给定一个数组，计算最多可以将数组分成几个“块”，使得对每个块排序后，整个数组是有序的。

**题目分析**：  
使用单调栈来维护当前块的最大值，遍历数组时，如果遇到比当前块最大值小的元素，则将其与栈顶元素合并。

**代码实现**：

```python
class Solution:
    def maxChunksToSorted(self, arr: List[int]) -> int:
        stack = []

        for num in arr:
            if not stack or stack[-1] <= num:
                stack.append(num)
            else:
                max_in_chunk = stack.pop()
                while stack and stack[-1] > num:
                    stack.pop()
                stack.append(max_in_chunk)

        return len(stack)

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 24. LeetCode 772: [Basic Calculator III](https://leetcode.com/problems/basic-calculator-iii/)（基本计算器 III）
**题目描述**：  
实现一个带有加减乘除和括号的基本计算器，返回计算结果。

**题目分析**：  
使用两个栈来处理操作数和操作符，遇到括号时递归处理。

**代码实现**：

```python
class Solution:
    def calculate(self, s: str) -> int:
        def helper(s: List[str]) -> int:
            stack = []
            num = 0
            sign = '+'

            while s:
                char = s.pop(0)
                if char.isdigit():
                    num = num * 10 + int(char)
                if char == '(':
                    num = helper(s)
                if not char.isdigit() or not s:
                    if sign == '+':
                        stack.append(num)
                    elif sign == '-':
                        stack.append(-num)
                    elif sign == '*':
                        stack.append(stack.pop() * num)
                    elif sign == '/':
                        stack.append(int(stack.pop() / num))

                    sign = char
                    num = 0

                if char == ')':
                    break

            return sum(stack)

        return helper(list(s))

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，遍历字符串一次即可完成计算。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有操作数和操作符。

---

### 25. LeetCode 844: [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)（退格字符串比较）
**题目描述**：  
给定两个字符串 `s` 和 `t`，判断它们在经过退格操作后是否相等。

**题目分析**：  
使用栈来处理退格操作。遍历字符串时，遇到字符就压入栈中，遇到退格符 '#' 时弹出栈顶元素。

**代码实现**：

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def build(string):
            stack = []
            for char in string:
                if char != '#':
                    stack.append(char)
                elif stack:
                    stack.pop()
            return ''.join(stack)

        return build(s) == build(t)

# 时间复杂度：O(n + m) - 遍历两个字符串
# 空间复杂度：O(n + m) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是字符串 `s` 和 `t` 的长度。
- **空间复杂度**：O(n + m)，栈在最坏情况下需要存储所有字符。

---

### 26. LeetCode 901: [Online Stock Span](https://leetcode.com/problems/online-stock-span/)（股票价格跨度）
**题目描述**：  
实现一个 `StockSpanner` 类，计算股票在当前时间跨度内的价格。

**题目分析**：  
使用单调栈来维护价格和跨度，遍历过程中计算每个价格的跨度。

**代码实现**：

```python
class StockSpanner:
    def __init__(self):
        self.stack = []  # 单调栈

    def next(self, price: int) -> int:
        span = 1
        while self.stack and self.stack[-1][0] <= price:
            span += self.stack.pop()[1]
        self.stack.append((price, span))
        return span

# 时间复杂度：O(n) - 遍历所有价格一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是股票价格的数量，每个价格最多进栈和出栈一次。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有价格。

---

### 27. LeetCode 946: [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/)（验证栈序列）
**题目描述**：  
给定两个序列 `pushed` 和 `popped`，判断它们是否为有效的栈操作序列。

**题目分析**：  
使用栈模拟进栈和出栈操作，遍历 `pushed` 序列，按需出栈。

**代码实现**：

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stack = []
        j = 0

        for num in pushed:
            stack.append(num)
            while stack and stack[-1] == popped[j]:
                stack.pop()
                j += 1

        return not stack

# 时间复杂度：O(n) - 遍历 pushed 序列一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是序列的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有元素。

---

### 28. LeetCode 1003: [Check If Word Is Valid After Substitutions](https://leetcode.com/problems/check-if-word-is-valid-after-substitutions/)（检查替换后的词是否有效）
**题目描述**：  
给定一个字符串，判断其是否可以通过多次替换 "abc" 为空字符串得到一个空字符串。

**题目分析**：  
使用栈来存储字符，遇到 "abc" 时弹出栈顶元素。

**代码实现**：

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []

        for char in s:
            stack.append(char)
            if len(stack) >= 3 and stack[-3:] == ['a', 'b', 'c']:
                stack.pop()
                stack.pop()
                stack.pop()

        return not stack

# 时间复杂度：O(n) - 遍历

字符串一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有字符。

---

### 29. LeetCode 1047: [Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)（移除字符串中的所有相邻重复项）
**题目描述**：  
给定一个字符串，删除其中的所有相邻重复项，直到结果中不包含任何相邻的重复字符。

**题目分析**：  
使用栈来逐一遍历字符串中的字符。当遇到和栈顶元素相同的字符时，将栈顶元素弹出，否则将当前字符压入栈中。

**代码实现**：

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []

        for char in s:
            if stack and stack[-1] == char:
                stack.pop()  # 删除相邻的重复字符
            else:
                stack.append(char)  # 压入栈中

        return ''.join(stack)

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，每个字符最多进栈和出栈一次。
- **空间复杂度**：O(n)，在最坏情况下，栈可能需要存储所有字符。

---

### 30. LeetCode 1249: [Minimum Remove to Make Valid Parentheses](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/)（移除无效括号使其有效）
**题目描述**：  
给定一个字符串 `s`，其包含小写字母和括号。需要最少删除一些字符，以使得剩下的字符串是一个有效的括号表达式。

**题目分析**：  
使用栈来标记需要删除的括号索引。在遍历字符串时，遇到 '(' 时将其索引压入栈中，遇到 ')' 时弹出栈顶元素；遍历结束后，栈中剩余的元素就是多余的 '('。

**代码实现**：

```python
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack = []  # 存储无效括号的索引
        s = list(s)  # 转为列表方便修改

        for i, char in enumerate(s):
            if char == '(':
                stack.append(i)
            elif char == ')':
                if stack:
                    stack.pop()
                else:
                    s[i] = ''  # 多余的 ')'

        while stack:
            s[stack.pop()] = ''  # 多余的 '('

        return ''.join(s)

# 时间复杂度：O(n) - 遍历字符串一次
# 空间复杂度：O(n) - 栈的大小
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，遍历字符串一次即可。
- **空间复杂度**：O(n)，栈在最坏情况下需要存储所有括号的索引。
