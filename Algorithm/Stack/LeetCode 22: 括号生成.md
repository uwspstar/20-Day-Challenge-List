### LeetCode 22: 括号生成 (Generate Parentheses)

**题目描述**：  
给定一个正整数 `n`，编写一个函数生成所有可能的并且有效的 `n` 对括号的组合。

[LeetCode 22: Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义生成括号的函数
    def generateParenthesis(self, n: int) -> List[str]:
        # 初始化栈和结果列表
        stk = []
        res = []

        # 定义回溯函数
        def backtrack(open_count, close_count):
            # 如果左括号和右括号都用完，加入结果
            if open_count == close_count == n:
                res.append("".join(stk))
                return

            # 如果左括号数量小于 n，添加左括号
            if open_count < n:
                stk.append("(")
                backtrack(open_count + 1, close_count)
                stk.pop()

            # 如果右括号数量小于左括号数量，添加右括号
            if close_count < open_count:
                stk.append(")")
                backtrack(open_count, close_count + 1)
                stk.pop()

        # 调用回溯函数
        backtrack(0, 0)

        return res

# 时间复杂度：O(4^n / sqrt(n)) - 生成有效括号组合的卡特兰数。
# 空间复杂度：O(n) - 栈的最大深度为 n。
```

**题目分析**：
这道题可以用回溯算法来解决，逐步构造括号组合，并确保生成的每个组合都是有效的。  
主要思路是：  
- 每当我们可以插入一个左括号时，就插入一个左括号。
- 只有在插入的右括号数量小于左括号时，才可以插入右括号。

**解决方案详解**：

- **初始化**：
  - 使用两个变量 `open_count` 和 `close_count` 分别记录已经插入的左括号和右括号数量。
  - 使用 `stk` 存储当前的括号组合，使用 `res` 存储最终结果。

- **回溯逻辑**：
  - 如果 `open_count` 和 `close_count` 都等于 `n`，则生成一个完整的括号组合，将其加入结果列表。
  - 如果 `open_count` 小于 `n`，则可以插入一个左括号。
  - 如果 `close_count` 小于 `open_count`，则可以插入一个右括号。
  - 回溯过程中，需注意在递归结束后弹出最近插入的括号。

- **返回结果**：
  - 返回存储所有有效组合的结果列表 `res`。

**复杂度分析**：
- **时间复杂度**：O(4^n / √n)，生成括号组合的数量符合卡特兰数的增长。
- **空间复杂度**：O(n)，栈的最大深度是 n，因为最多有 n 对括号。

**示例讲解**：

#### 示例 1:

```python
输入: n = 3
```
- 初始状态：`open_count = 0, close_count = 0, stk = []`
- 递归生成：
  - `"((()))"`
  - `"(()())"`
  - `"(())()"`
  - `"()(())"`
  - `"()()()"`
- 最终结果：`["((()))", "(()())", "(())()", "()(())", "()()()"]`

**总结**：
- 回溯法适用于生成所有可能组合的问题，可以通过条件约束生成合法的解集。
- 本题利用回溯生成所有可能的括号组合，确保生成的每个组合都有效。
---
This code generates all valid combinations of `n` pairs of parentheses using **backtracking**. Let's walk through the code and provide a detailed explanation, including a step-by-step example.

### LeetCode 22: 括号生成 (Generate Parentheses)

**题目描述**：  
给定一个正整数 `n`，编写一个函数生成所有可能的并且有效的 `n` 对括号的组合。

[LeetCode 22: Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义生成括号的函数
    def generateParenthesis(self, n: int) -> List[str]:
        # 初始化栈和结果列表
        stk = []
        res = []

        # 定义回溯函数
        def backtrack(open_n, close_n):
            # 如果左括号和右括号都用完，加入结果
            if open_n == close_n == n:
                s = "".join(stk)
                res.append(s)
                return

            # 如果左括号数量小于 n，添加左括号
            if open_n < n:
                stk.append("(")
                backtrack(open_n + 1, close_n)
                stk.pop()
            
            # 如果右括号数量小于左括号数量，添加右括号
            if close_n < open_n:
                stk.append(")")
                backtrack(open_n, close_n + 1)
                stk.pop()

        # 调用回溯函数
        backtrack(0, 0)
        return res

# 时间复杂度：O(4^n / sqrt(n)) - 生成有效括号组合的卡特兰数。
# 空间复杂度：O(n) - 栈的最大深度为 n。
```

**题目分析**：
使用 **回溯法** 生成有效的括号组合。我们通过条件约束，逐步构建每个组合，并在遇到有效组合时添加到结果中。  
回溯过程中，通过两个计数器 `open_n` 和 `close_n` 追踪当前使用的左、右括号数目。  
- 仅当 `open_n < n` 时才允许添加左括号。
- 仅当 `close_n < open_n` 时才允许添加右括号，这确保了括号组合的有效性。

**解决方案详解**：

- **初始化**：定义空列表 `stk` 存储当前路径，`res` 存储所有有效组合。
- **回溯逻辑**：
  - 当 `open_n == close_n == n` 时，说明已经构成一个完整的组合，将其加入结果。
  - 若 `open_n < n`，可以加入一个左括号并继续递归。
  - 若 `close_n < open_n`，可以加入一个右括号继续递归。
  - 每次递归结束后，使用 `pop` 撤销上一步操作，回到上一个状态。
  
---

### 示例讲解：逐步解析示例步骤（中文）

假设 `n = 2`，我们需要生成所有包含 2 对括号的组合。

1. **初始状态**：
   - `open_n = 0`，`close_n = 0`，`stk = []`。

2. **第 1 步：加入左括号** `(`：
   - `open_n = 1`，`close_n = 0`，`stk = ["("]`。
   - 继续递归，因为 `open_n < n`。

3. **第 2 步：再加入左括号** `(`：
   - `open_n = 2`，`close_n = 0`，`stk = ["(", "("]`。
   - 继续递归，因为 `open_n == n`，此时无法再加入左括号。

4. **第 3 步：加入右括号** `)`：
   - `open_n = 2`，`close_n = 1`，`stk = ["(", "(", ")"]`。
   - 继续递归，因为 `close_n < open_n`。

5. **第 4 步：再加入右括号** `)`：
   - `open_n = 2`，`close_n = 2`，`stk = ["(", "(", ")", ")"]`。
   - 此时，`open_n == close_n == n`，构成有效组合 `"(()))"`，将其加入 `res`。

6. **回溯**：
   - 返回到上一步，撤销最后的 `)`，`stk = ["(", "(", ")"]`。
   - 再次回溯，撤销 `)`，`stk = ["(", "("]`。

7. **探索其他组合**：
   - 从第 1 步中，加入 `)` 形成另一个路径，继续执行回溯。

最终，所有组合会在 `res` 中生成，即 `["(())", "()()"]`。
