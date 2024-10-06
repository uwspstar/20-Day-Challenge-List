# 回溯法
### 回溯法 (Backtracking)

#### Definition  
回溯法是一种算法设计技术，用来逐步解决问题。它会尝试所有可能的选择，直到找到一个解决方案，或者发现所有选择都不能成功解决问题。回溯法通常用于解决那些需要探索所有可能解的组合问题，例如排列、组合、子集、图的颜色问题、迷宫问题等。

#### Key Concepts  
1. **递归 (Recursion)**: 回溯法通常是通过递归实现的，每个递归调用都尝试在当前路径上做出选择。
2. **决策树 (Decision Tree)**: 回溯法可以看作是在一棵决策树上进行搜索，每个节点代表一种选择，每个分支代表一种可能的决策。
3. **剪枝 (Pruning)**: 在回溯的过程中，如果发现某个选择不能导致合法解，程序会立即“剪枝”，即放弃该选择，避免进一步的无效搜索。
4. **回溯 (Backtrack)**: 当一个选择导致无效解时，程序会回到上一步，尝试另一种选择，直到所有可能的选择都被尝试完毕。

#### 回溯法的步骤  
1. **做出选择**：从当前可选择的决策中做出一个选择。
2. **递归进入下一步**：在做出选择之后，递归进入下一步，继续尝试其他的决策。
3. **回溯**：如果发现当前选择无法导致有效的解决方案，回到上一步，取消当前选择，尝试其他可能的选择。

#### 回溯法的适用场景  
- 全排列问题
- 子集问题
- 组合问题
- 图的颜色问题
- 数独问题
- 八皇后问题

#### Python 回溯法模板

```python
def backtrack(path, options):
    if 满足结束条件:
        记录结果
        return
    for option in options:
        做出选择
        backtrack(更新后的路径, 更新后的选择)
        撤销选择
```

好的，我们将逐步讲解 30 道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。以下是前五道回溯法题目的详细解析和代码实现。

---

### 1. LeetCode 46: Permutations（全排列）

**题目描述**：
给定一个不含重复数字的数组 `nums`，返回所有可能的全排列。

**解题思路**：
使用回溯法生成所有的排列。每次从数组中选择一个未被使用的数字，并将其加入当前排列中，直到排列的长度等于数组的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成全排列的函数
    def permute(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(path, used):
            # 如果当前排列的长度等于 nums 的长度，加入结果列表
            if len(path) == len(nums):
                result.append(path[:])
                return

            # 遍历 nums 中的每个数字
            for i in range(len(nums)):
                # 如果该数字已被使用，跳过
                if used[i]:
                    continue

                # 选择当前数字并标记为已使用
                path.append(nums[i])
                used[i] = True

                # 递归进行下一步选择
                backtrack(path, used)

                # 回溯，撤销选择并标记为未使用
                path.pop()
                used[i] = False

        # 调用回溯函数
        backtrack([], [False] * len(nums))
        return result

# 时间复杂度：O(n * n!) - 生成所有排列的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * n!)，生成所有排列的时间复杂度，其中 n 是数组的长度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 2. LeetCode 78: Subsets（子集）

**题目描述**：
给定一个不含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

**解题思路**：
使用回溯法生成所有的子集。在每个递归调用中，都可以选择将当前元素加入子集或不加入子集，直至遍历完所有元素。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成子集的函数
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 将当前路径加入结果列表
            result.append(path[:])

            # 从当前索引开始遍历所有数字
            for i in range(start, len(nums)):
                # 选择当前数字
                path.append(nums[i])

                # 递归进行下一步选择
                backtrack(i + 1, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 生成所有子集的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，生成所有子集的时间复杂度，其中 n 是数组的长度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 3. LeetCode 79: Word Search（单词搜索）

**题目描述**：
给定一个 `m x n` 的字符网格 `board` 和一个字符串 `word`，判断字符串 `word` 是否可以通过顺序连接网格中的字符形成。

**解题思路**：
使用回溯法和深度优先搜索（DFS）。从网格中的每个位置开始，尝试匹配字符串 `word` 的每个字符。如果某个路径不匹配，则进行回溯。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否存在单词路径的函数
    def exist(self, board: List[List[str]], word: str) -> bool:
        # 获取网格的行和列数
        rows, cols = len(board), len(board[0])

        # 定义回溯函数
        def backtrack(row, col, index):
            # 如果所有字符匹配成功，返回 True
            if index == len(word):
                return True

            # 检查当前坐标是否越界或字符不匹配
            if row < 0 or row >= rows or col < 0 or col >= cols or board[row][col] != word[index]:
                return False

            # 保存当前字符并标记为已访问
            temp = board[row][col]
            board[row][col] = "#"

            # 遍历四个方向
            for r, c in [(row + 1, col), (row - 1, col), (row, col + 1), (row, col - 1)]:
                if backtrack(r, c, index + 1):
                    return True

            # 回溯，恢复当前字符
            board[row][col] = temp
            return False

        # 遍历网格中的每个位置，作为起点
        for r in range(rows):
            for c in range(cols):
                if backtrack(r, c, 0):  # 如果找到路径，返回 True
                    return True

        return False  # 没有找到路径，返回 False

# 时间复杂度：O(m * n * 4^k) - 其中 m 和 n 分别是网格的行和列数，k 是字符串的长度。
# 空间复杂度：O(k) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(m * n * 4^k)，其中 m 和 n 分别是网格的行和列数，k 是字符串的长度。
- **空间复杂度**：O(k)，递归调用栈的空间复杂度。

---

### 4. LeetCode 22: Generate Parentheses（括号生成）

**题目描述**：
给定一个整数 `n`，生成所有由 `n` 对括号组成的合法括号序列。

**解题思路**：
使用回溯法生成所有可能的括号序列。每次递归时，可以选择添加一个左括号 `(` 或一个右括号 `)`，并且需要保证生成的序列合法。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成括号序列的函数
    def generateParentheses(self, n: int) -> List[str]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(path, open_count, close_count):
            # 如果生成的括号序列长度等于 2 * n，加入结果列表
            if len(path) == 2 * n:
                result.append("".join(path))
                return

            # 如果可以添加左括号
            if open_count < n:
                path.append("(")
                backtrack(path, open_count + 1, close_count)
                path.pop()

            # 如果可以添加右括号
            if close_count < open_count:
                path.append(")")
                backtrack(path, open_count, close_count + 1)
                path.pop()

        # 调用回溯函数
        backtrack([], 0, 0)
        return result

# 时间复杂度：O(4^n / √n) - 生成所有合法括号序列的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(4^n / √n)，生成所有合法括号序列的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 5. LeetCode 39: Combination Sum（组合总和）

**题目描述**：
给定一个无重复元素的数组 `candidates` 和一个目标数 `target`，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

**解题思路**：
使用回溯法进行组合求和。每次递归调用时，可以选择当前元素，并继续递归，直到当前和等于 `target` 或超过 `target` 为止。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定

义查找组合总和的函数
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(remaining, start, path):
            # 如果剩余目标为 0，说明找到一个合法组合
            if remaining == 0:
                result.append(path[:])
                return
            elif remaining < 0:  # 超过目标，直接返回
                return

            # 遍历所有可能的选择
            for i in range(start, len(candidates)):
                path.append(candidates[i])  # 选择当前元素
                backtrack(remaining - candidates[i], i, path)  # 递归调用
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(target, 0, [])
        return result

# 时间复杂度：O(n^target) - 每次递归中有多种选择。
# 空间复杂度：O(target) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^target)，每次递归中有多种选择。
- **空间复杂度**：O(target)，递归调用栈的空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 6. LeetCode 40: Combination Sum II（组合总和 II）

**题目描述**：
给定一个包含重复数字的数组 `candidates` 和一个目标数 `target`，找出所有可以使数字和为 `target` 的组合。每个数字在每个组合中只能使用一次。

**解题思路**：
使用回溯法和剪枝策略进行组合求和。先对数组进行排序，避免重复组合。在每次递归中，如果当前元素与前一个元素相同，且前一个元素尚未被使用，则跳过当前元素，以避免重复结果。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找组合总和的函数
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        # 步骤 1：对数组进行排序
        candidates.sort()
        result = []

        # 定义回溯函数
        def backtrack(start, remaining, path):
            # 如果剩余目标为 0，说明找到一个合法组合
            if remaining == 0:
                result.append(path[:])
                return

            # 遍历所有可能的选择
            for i in range(start, len(candidates)):
                # 如果当前数字大于剩余目标，则后续数字都不能被选择，剪枝
                if candidates[i] > remaining:
                    break

                # 如果当前数字与前一个数字相同，并且前一个数字尚未被使用，跳过，避免重复
                if i > start and candidates[i] == candidates[i - 1]:
                    continue

                # 选择当前数字
                path.append(candidates[i])
                # 递归进行下一步选择，注意每个数字只能使用一次，因此 start 为 i + 1
                backtrack(i + 1, remaining - candidates[i], path)
                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, target, [])
        return result

# 时间复杂度：O(2^n) - 生成所有组合的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(2^n)，每次递归中存在多种选择，最多可能生成 `2^n` 种组合。
- **空间复杂度**：O(n)，递归调用栈的深度最大为 `n`，其中 `n` 为数组的长度。

---

### 7. LeetCode 47: Permutations II（全排列 II）

**题目描述**：
给定一个包含重复数字的数组 `nums`，返回所有可能的不重复全排列。

**解题思路**：
使用回溯法生成所有排列，并在递归中加入剪枝策略来避免重复排列。可以先对数组进行排序，每次递归时，跳过与前一个数字相同且前一个数字尚未被使用的情况。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成不重复全排列的函数
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        # 步骤 1：对数组进行排序
        nums.sort()
        result = []
        used = [False] * len(nums)  # 记录当前数字是否被使用

        # 定义回溯函数
        def backtrack(path):
            # 如果当前排列的长度等于 nums 的长度，加入结果列表
            if len(path) == len(nums):
                result.append(path[:])
                return

            # 遍历 nums 中的每个数字
            for i in range(len(nums)):
                # 如果该数字已被使用，或与前一个数字相同且前一个数字尚未被使用，跳过
                if used[i] or (i > 0 and nums[i] == nums[i - 1] and not used[i - 1]):
                    continue

                # 选择当前数字并标记为已使用
                path.append(nums[i])
                used[i] = True

                # 递归进行下一步选择
                backtrack(path)

                # 回溯，撤销选择并标记为未使用
                path.pop()
                used[i] = False

        # 调用回溯函数
        backtrack([])
        return result

# 时间复杂度：O(n * n!) - 生成所有排列的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * n!)，生成所有排列的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 8. LeetCode 131: Palindrome Partitioning（分割回文串）

**题目描述**：
给定一个字符串 `s`，将其分割成若干子串，使得每个子串都是回文串。返回所有可能的分割方案。

**解题思路**：
使用回溯法生成所有分割方案。在每次递归中，判断当前子串是否是回文串，如果是，则将该子串加入当前路径，并继续递归分割剩余的字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义分割回文串的函数
    def partition(self, s: str) -> List[List[str]]:
        # 初始化结果列表
        result = []

        # 定义判断是否为回文串的函数
        def is_palindrome(substring):
            return substring == substring[::-1]

        # 定义回溯函数
        def backtrack(start, path):
            # 如果起始位置等于字符串长度，说明找到一个合法分割方案
            if start == len(s):
                result.append(path[:])
                return

            # 遍历所有可能的分割位置
            for end in range(start + 1, len(s) + 1):
                # 如果当前子串是回文串，递归继续分割
                if is_palindrome(s[start:end]):
                    path.append(s[start:end])  # 选择当前子串
                    backtrack(end, path)  # 递归调用
                    path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 每个字符都可以选择分割或不分割。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，每个字符都可以选择分割或不分割，生成所有可能的分割方案。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 9. LeetCode 216: Combination Sum III（组合总和 III）

**题目描述**：
找到所有 `k` 个数的组合，它们的和为 `n`。组合中的数字只能在 `1-9` 的范围内，每个数字最多只能使用一次。

**解题思路**：
使用回溯法和剪枝策略。每次递归中选择一个数字，将其加入当前组合中，并继续递归，直到组合的长度等于 `k` 且和等于 `n`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找组合总和的函数
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, remaining, path):
            # 如果组合的长度等于 k，且剩余目标为 0，说明找到一个合法组合
            if len(path) == k and remaining == 0:
                result.append(path[:])
                return

            # 遍历所有可能的选择
            for i in range(start, 10):
                # 如果当前数字大于剩余目标，则后续数字都不能被选择，剪枝
                if i > remaining:
                    break

                # 选择当前数字
                path.append(i)
                # 递归进行下一步选择，每个数字只能使用一次，因此 start 为 i + 1
                backtrack(i + 1, remaining - i, path)
                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(1, n, [])
        return result

# 时间复杂度：O(2^n) - 生成所有组合的时间复杂度。
# 空间复杂度：O(k) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**

：O(2^n)，生成所有组合的时间复杂度。
- **空间复杂度**：O(k)，递归调用栈的空间复杂度。

---

### 10. LeetCode 77: Combinations（组合）

**题目描述**：
给定两个整数 `n` 和 `k`，返回 `1` 到 `n` 中所有可能的 `k` 个数的组合。

**解题思路**：
使用回溯法生成所有组合。在每次递归中，从当前索引开始选择一个数字，并将其加入当前组合中，直到组合的长度等于 `k`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成组合的函数
    def combine(self, n: int, k: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 如果组合的长度等于 k，加入结果列表
            if len(path) == k:
                result.append(path[:])
                return

            # 从当前索引开始遍历所有可能的选择
            for i in range(start, n + 1):
                path.append(i)  # 选择当前数字
                backtrack(i + 1, path)  # 递归进行下一步选择
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(1, [])
        return result

# 时间复杂度：O(C(n, k)) - 生成所有组合的时间复杂度。
# 空间复杂度：O(k) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(C(n, k))，生成所有组合的时间复杂度。
- **空间复杂度**：O(k)，递归调用栈的空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 11. LeetCode 90: Subsets II（子集 II）

**题目描述**：
给定一个可能包含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。解集不能包含重复的子集。

**解题思路**：
使用回溯法生成所有子集。在递归中加入剪枝策略，避免生成重复子集。先对数组进行排序，确保相同的数字在递归中是连续的，如果当前数字与前一个数字相同且前一个数字尚未被使用，则跳过当前数字。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成子集的函数
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        # 步骤 1：对数组进行排序
        nums.sort()
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 将当前路径加入结果列表
            result.append(path[:])

            # 从当前索引开始遍历所有数字
            for i in range(start, len(nums)):
                # 如果当前数字与前一个数字相同，且前一个数字尚未被使用，跳过
                if i > start and nums[i] == nums[i - 1]:
                    continue

                # 选择当前数字
                path.append(nums[i])

                # 递归进行下一步选择
                backtrack(i + 1, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 生成所有子集的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，生成所有子集的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 12. LeetCode 51: N-Queens（N 皇后问题）

**题目描述**：
给定一个整数 `n`，返回所有不同的 N 皇后问题的解决方案。每种解法中，`n` 个皇后互不攻击。

**解题思路**：
使用回溯法和剪枝策略。每次递归时，在当前行选择一个位置放置皇后，并确保皇后不会与之前放置的皇后发生冲突（不在同一列、不在同一条对角线上）。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义解决 N 皇后问题的函数
    def solveNQueens(self, n: int) -> List[List[str]]:
        # 初始化结果列表
        result = []
        # 定义列、主对角线、副对角线的集合，用于记录皇后是否已占据该位置
        cols = set()
        diag1 = set()
        diag2 = set()

        # 定义回溯函数
        def backtrack(row, state):
            # 如果当前行等于 n，说明找到一个合法解法
            if row == n:
                result.append(["".join(row_state) for row_state in state])
                return

            # 遍历当前行中的所有列
            for col in range(n):
                # 如果当前列或对角线已被占用，跳过
                if col in cols or (row - col) in diag1 or (row + col) in diag2:
                    continue

                # 做出选择，将皇后放置在 (row, col)
                cols.add(col)
                diag1.add(row - col)
                diag2.add(row + col)
                state[row][col] = "Q"

                # 递归进行下一行
                backtrack(row + 1, state)

                # 回溯，撤销选择
                cols.remove(col)
                diag1.remove(row - col)
                diag2.remove(row + col)
                state[row][col] = "."

        # 初始化棋盘
        board = [["."] * n for _ in range(n)]
        # 调用回溯函数
        backtrack(0, board)
        return result

# 时间复杂度：O(n!) - N 皇后问题的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n!)，N 皇后问题的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 13. LeetCode 52: N-Queens II（N 皇后问题 II）

**题目描述**：
给定一个整数 `n`，返回所有不同的 N 皇后问题的解决方案个数。

**解题思路**：
与 LeetCode 51 类似，只需要在找到一个合法解法时更新计数器 `count`，而不是保存所有解法。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算 N 皇后问题解法数量的函数
    def totalNQueens(self, n: int) -> int:
        # 初始化计数器
        count = 0
        # 定义列、主对角线、副对角线的集合
        cols = set()
        diag1 = set()
        diag2 = set()

        # 定义回溯函数
        def backtrack(row):
            nonlocal count
            # 如果当前行等于 n，说明找到一个合法解法
            if row == n:
                count += 1
                return

            # 遍历当前行中的所有列
            for col in range(n):
                # 如果当前列或对角线已被占用，跳过
                if col in cols or (row - col) in diag1 or (row + col) in diag2:
                    continue

                # 做出选择，将皇后放置在 (row, col)
                cols.add(col)
                diag1.add(row - col)
                diag2.add(row + col)

                # 递归进行下一行
                backtrack(row + 1)

                # 回溯，撤销选择
                cols.remove(col)
                diag1.remove(row - col)
                diag2.remove(row + col)

        # 调用回溯函数
        backtrack(0)
        return count

# 时间复杂度：O(n!) - N 皇后问题的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n!)，N 皇后问题的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 14. LeetCode 60: Permutation Sequence（第 k 个排列）

**题目描述**：
给定整数 `n` 和 `k`，返回 [1, 2, 3, ... , n] 组成的序列的第 `k` 个排列。

**解题思路**：
利用回溯法和剪枝策略。通过计算阶乘值来剪枝每次递归中的选择。可以先计算所有可能排列的个数，并直接跳过不符合条件的排列。

**代码实现**：
```python
# 导入数学模块
import math

# 定义解决方案的类
class Solution:
    # 定义计算第 k 个排列的函数
    def getPermutation(self, n: int, k: int) -> str:
        # 初始化候选数字列表和结果字符串
        candidates = [str(i) for i in range(1, n + 1)]
        result = []

        # 将 k 转为基数为 0 的索引
        k -= 1

        # 计算每一位的数字选择
        for i in range(n, 0, -1):
            # 计算当前阶乘值
            fact = math.factorial(i - 1)
            # 确定当前选择数字的索引
            index = k // fact
            # 将该数字加入结果
            result.append(candidates.pop(index))
            # 更新 k 值
            k %= fact

        return "".join(result)

# 时间复杂度：O(n^2) - 删除候选数字的操作。
# 空间复杂度：O(n) - 存储候选数字的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，删除候选数字的操作时间复杂度。
- **空间复杂度**：O(n)，用于存储候选数字列表的空间复杂度。

---

### 15. LeetCode 93: Restore IP Addresses（复原 IP 地址）

**题目描述**：
给定一个只包含数字的字符串，返回所有可能的 IP 地址格式。IP 地址

由四个十进制数构成，每个数的范围是 0 到 255，且不能有前导 0。

**解题思路**：
使用回溯法生成所有可能的 IP 地址格式。每次递归中，可以选择一个数字或两个数字或三个数字作为当前段，并且保证生成的 IP 地址合法。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成合法 IP 地址的函数
    def restoreIpAddresses(self, s: str) -> List[str]:
        # 如果字符串长度不符合 IP 地址要求，直接返回空列表
        if len(s) < 4 or len(s) > 12:
            return []

        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 如果路径中有 4 个段，且遍历完字符串，说明找到一个合法 IP 地址
            if len(path) == 4 and start == len(s):
                result.append(".".join(path))
                return

            # 如果路径中有 4 个段，但尚未遍历完字符串，或尚未形成 4 个段，但遍历完字符串，直接返回
            if len(path) == 4 or start == len(s):
                return

            # 遍历所有可能的段（1 到 3 个字符）
            for length in range(1, 4):
                # 如果起始位置加段的长度超过字符串长度，跳过
                if start + length > len(s):
                    break

                # 提取当前段
                segment = s[start:start + length]

                # 检查当前段是否合法（不能有前导 0，且值在 0 到 255 之间）
                if (segment.startswith("0") and len(segment) > 1) or int(segment) > 255:
                    continue

                # 选择当前段
                path.append(segment)

                # 递归进行下一段选择
                backtrack(start + length, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(3^4) - 每次递归中有三种选择，最多生成 81 种可能。
# 空间复杂度：O(4) - 递归调用栈的深度最大为 4。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(3^4)，每次递归中有三种选择，最多生成 81 种可能。
- **空间复杂度**：O(4)，递归调用栈的深度最大为 4。

---

好的，我们继续讲解接下来的五道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 16. LeetCode 131: Palindrome Partitioning（分割回文串）

**题目描述**：
给定一个字符串 `s`，将其分割成若干子串，使得每个子串都是回文串。返回所有可能的分割方案。

**解题思路**：
使用回溯法生成所有分割方案。在每次递归中，判断当前子串是否是回文串，如果是，则将该子串加入当前路径，并继续递归分割剩余的字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义分割回文串的函数
    def partition(self, s: str) -> List[List[str]]:
        # 初始化结果列表
        result = []

        # 定义判断是否为回文串的函数
        def is_palindrome(substring):
            return substring == substring[::-1]

        # 定义回溯函数
        def backtrack(start, path):
            # 如果起始位置等于字符串长度，说明找到一个合法分割方案
            if start == len(s):
                result.append(path[:])
                return

            # 遍历所有可能的分割位置
            for end in range(start + 1, len(s) + 1):
                # 如果当前子串是回文串，递归继续分割
                if is_palindrome(s[start:end]):
                    path.append(s[start:end])  # 选择当前子串
                    backtrack(end, path)  # 递归调用
                    path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 每个字符都可以选择分割或不分割。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，每个字符都可以选择分割或不分割，生成所有可能的分割方案。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 17. LeetCode 491: Increasing Subsequences（递增子序列）

**题目描述**：
给定一个整数数组 `nums`，找到所有递增子序列的集合。递增子序列的长度至少为 2，且子序列中的元素顺序与原数组一致。

**解题思路**：
使用回溯法生成所有递增子序列。在每次递归中，跳过当前元素或者将其加入子序列。如果当前元素比前一个元素小，则跳过该元素，避免生成递减子序列。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找递增子序列的函数
    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 如果路径中的子序列长度大于等于 2，加入结果列表
            if len(path) >= 2:
                result.append(path[:])

            # 使用集合避免同一层级的重复选择
            used = set()
            # 遍历所有可能的选择
            for i in range(start, len(nums)):
                # 如果当前数字已被选择或比上一个数字小，跳过
                if (path and nums[i] < path[-1]) or nums[i] in used:
                    continue

                # 选择当前数字
                used.add(nums[i])
                path.append(nums[i])
                backtrack(i + 1, path)  # 递归进行下一步选择
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(2^n) - 生成所有可能的子序列。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(2^n)，生成所有可能的子序列。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 18. LeetCode 46: Permutations（全排列）

**题目描述**：
给定一个不含重复数字的数组 `nums`，返回所有可能的全排列。

**解题思路**：
使用回溯法生成所有的排列。每次从数组中选择一个未被使用的数字，并将其加入当前排列中，直到排列的长度等于数组的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成全排列的函数
    def permute(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(path, used):
            # 如果当前排列的长度等于 nums 的长度，加入结果列表
            if len(path) == len(nums):
                result.append(path[:])
                return

            # 遍历 nums 中的每个数字
            for i in range(len(nums)):
                # 如果该数字已被使用，跳过
                if used[i]:
                    continue

                # 选择当前数字并标记为已使用
                path.append(nums[i])
                used[i] = True

                # 递归进行下一步选择
                backtrack(path, used)

                # 回溯，撤销选择并标记为未使用
                path.pop()
                used[i] = False

        # 调用回溯函数
        backtrack([], [False] * len(nums))
        return result

# 时间复杂度：O(n * n!) - 生成所有排列的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * n!)，生成所有排列的时间复杂度，其中 n 是数组的长度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 19. LeetCode 78: Subsets（子集）

**题目描述**：
给定一个不含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

**解题思路**：
使用回溯法生成所有的子集。在每个递归调用中，都可以选择将当前元素加入子集或不加入子集，直至遍历完所有元素。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成子集的函数
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 将当前路径加入结果列表
            result.append(path[:])

            # 从当前索引开始遍历所有数字
            for i in range(start, len(nums)):
                # 选择当前数字
                path.append(nums[i])

                # 递归进行下一步选择
                backtrack(i + 1, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 生成所有子集的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，生成所有子集的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 20. LeetCode 93: Restore IP Addresses（复原 IP 地址）

**题目描述**：
给定一个只包含数字的字符串，返回所有可能的 IP 地址格式。IP 地址由四个十进制数构成，每个数的范围是 0 到 255，且不能有前导 0。

**解题思路**：
使用回溯法生成所有可能的 IP 地址格式。每次递归中，可以选择一个数字、两个数字或三个数字作为当前段，并且保证生成的 IP 地址合法。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成合法 IP 地址的函数
    def restoreIpAddresses(self, s: str) -> List[str]:
        # 如果字符串长度不符合 IP 地址要求，直接返回空列表
        if len(s) < 4 或 len(s) > 12:
            return []

        result = []

        # 定义回

溯函数
        def backtrack(start, path):
            # 如果路径中有 4 个段，且遍历完字符串，说明找到一个合法 IP 地址
            if len(path) == 4 and start == len(s):
                result.append(".".join(path))
                return

            # 如果路径中有 4 个段，但尚未遍历完字符串，或尚未形成 4 个段，但遍历完字符串，直接返回
            if len(path) == 4 or start == len(s):
                return

            # 遍历所有可能的段（1 到 3 个字符）
            for length in range(1, 4):
                # 如果起始位置加段的长度超过字符串长度，跳过
                if start + length > len(s):
                    break

                # 提取当前段
                segment = s[start:start + length]

                # 检查当前段是否合法（不能有前导 0，且值在 0 到 255 之间）
                if (segment.startswith("0") and len(segment) > 1) or int(segment) > 255:
                    continue

                # 选择当前段
                path.append(segment)

                # 递归进行下一段选择
                backtrack(start + length, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(3^4) - 每次递归中有三种选择，最多生成 81 种可能。
# 空间复杂度：O(4) - 递归调用栈的深度最大为 4。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(3^4)，每次递归中有三种选择，最多生成 81 种可能。
- **空间复杂度**：O(4)，递归调用栈的深度最大为 4。

---

好的，我们继续讲解接下来的五道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 21. LeetCode 131: Palindrome Partitioning（分割回文串）

**题目描述**：
给定一个字符串 `s`，将其分割成若干子串，使得每个子串都是回文串。返回所有可能的分割方案。

**解题思路**：
使用回溯法生成所有分割方案。在每次递归中，判断当前子串是否是回文串，如果是，则将该子串加入当前路径，并继续递归分割剩余的字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义分割回文串的函数
    def partition(self, s: str) -> List[List[str]]:
        # 初始化结果列表
        result = []

        # 定义判断是否为回文串的函数
        def is_palindrome(substring):
            return substring == substring[::-1]

        # 定义回溯函数
        def backtrack(start, path):
            # 如果起始位置等于字符串长度，说明找到一个合法分割方案
            if start == len(s):
                result.append(path[:])
                return

            # 遍历所有可能的分割位置
            for end in range(start + 1, len(s) + 1):
                # 如果当前子串是回文串，递归继续分割
                if is_palindrome(s[start:end]):
                    path.append(s[start:end])  # 选择当前子串
                    backtrack(end, path)  # 递归调用
                    path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 每个字符都可以选择分割或不分割。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，每个字符都可以选择分割或不分割，生成所有可能的分割方案。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 22. LeetCode 784: Letter Case Permutation（字母大小写全排列）

**题目描述**：
给定一个字符串 `s`，返回它的所有可能的字母大小写全排列。字符串中的每个字母都可以是大写或小写。

**解题思路**：
使用回溯法生成所有字母大小写的排列。在每次递归中，如果当前字符是字母，则可以将其转化为大写或小写，然后继续递归。如果当前字符是数字，则直接加入结果。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成字母大小写全排列的函数
    def letterCasePermutation(self, s: str) -> List[str]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(index, path):
            # 如果路径的长度等于字符串的长度，说明生成一个合法排列
            if index == len(s):
                result.append("".join(path))
                return

            # 处理当前字符
            if s[index].isalpha():  # 如果当前字符是字母
                # 将当前字母转为小写
                path.append(s[index].lower())
                backtrack(index + 1, path)
                path.pop()  # 回溯，撤销选择

                # 将当前字母转为大写
                path.append(s[index].upper())
                backtrack(index + 1, path)
                path.pop()  # 回溯，撤销选择
            else:
                # 当前字符是数字，直接加入路径
                path.append(s[index])
                backtrack(index + 1, path)
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(2^n) - 每个字母都有两种选择，生成所有排列。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(2^n)，每个字母都有两种选择，生成所有排列。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 23. LeetCode 967: Numbers With Same Consecutive Differences（具有相同差值的数字）

**题目描述**：
给定两个整数 `N` 和 `K`，返回所有长度为 `N` 且相邻数字的差值为 `K` 的正整数。

**解题思路**：
使用回溯法生成所有符合条件的数字。在每次递归中，从上一个数字的末尾出发，根据 `K` 的值生成下一个数字，直到生成长度为 `N` 的数字。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成具有相同差值的数字的函数
    def numsSameConsecDiff(self, N: int, K: int) -> List[int]:
        # 如果 N 等于 1，返回 0 到 9 的所有数字
        if N == 1:
            return [i for i in range(10)]

        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(n, num):
            # 如果生成的数字长度为 N，加入结果列表
            if n == N:
                result.append(num)
                return

            # 获取当前数字的最后一个数字
            last_digit = num % 10

            # 生成下一个数字
            if last_digit + K < 10:  # 向上递增
                backtrack(n + 1, num * 10 + last_digit + K)
            if K > 0 and last_digit - K >= 0:  # 向下递减
                backtrack(n + 1, num * 10 + last_digit - K)

        # 从 1 到 9 作为起始数字
        for num in range(1, 10):
            backtrack(1, num)
        return result

# 时间复杂度：O(2^N) - 每个数字的生成有两个选择。
# 空间复杂度：O(N) - 递归调用栈的深度最大为 N。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(2^N)，每个数字的生成有两个选择。
- **空间复杂度**：O(N)，递归调用栈的深度最大为 N。

---

### 24. LeetCode 77: Combinations（组合）

**题目描述**：
给定两个整数 `n` 和 `k`，返回 `1` 到 `n` 中所有可能的 `k` 个数的组合。

**解题思路**：
使用回溯法生成所有组合。在每次递归中，从当前索引开始选择一个数字，并将其加入当前组合中，直到组合的长度等于 `k`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成组合的函数
    def combine(self, n: int, k: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 如果组合的长度等于 k，加入结果列表
            if len(path) == k:
                result.append(path[:])
                return

            # 从当前索引开始遍历所有可能的选择
            for i in range(start, n + 1):
                path.append(i)  # 选择当前数字
                backtrack(i + 1, path)  # 递归进行下一步选择
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(1, [])
        return result

# 时间复杂度：O(C(n, k)) - 生成所有组合的时间复杂度。
# 空间复杂度：O(k) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(C(n, k))，生成所有组合的时间复杂度。
- **空间复杂度**：O(k)，递归调用栈的空间复杂度。

---

### 25. LeetCode 78: Subsets（子集）

**题目描述**：
给定一个不含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

**解题思路**：
使用回溯法生成所有的子集。在每个递归调用中，都可以选择将当前元素加入子集或不加入子集，直至遍历完所有元素。

**代码实现**：


```python
# 定义解决方案的类
class Solution:
    # 定义生成子集的函数
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 将当前路径加入结果列表
            result.append(path[:])

            # 从当前索引开始遍历所有数字
            for i in range(start, len(nums)):
                # 选择当前数字
                path.append(nums[i])

                # 递归进行下一步选择
                backtrack(i + 1, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 生成所有子集的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，生成所有子集的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 回溯法题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 26. LeetCode 47: Permutations II（全排列 II）

**题目描述**：
给定一个包含重复数字的数组 `nums`，返回所有可能的不重复全排列。

**解题思路**：
使用回溯法生成所有排列，并在递归中加入剪枝策略来避免重复排列。可以先对数组进行排序，每次递归时，跳过与前一个数字相同且前一个数字尚未被使用的情况。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成不重复全排列的函数
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        # 步骤 1：对数组进行排序
        nums.sort()
        result = []
        used = [False] * len(nums)  # 记录当前数字是否被使用

        # 定义回溯函数
        def backtrack(path):
            # 如果当前排列的长度等于 nums 的长度，加入结果列表
            if len(path) == len(nums):
                result.append(path[:])
                return

            # 遍历 nums 中的每个数字
            for i in range(len(nums)):
                # 如果该数字已被使用，或与前一个数字相同且前一个数字尚未被使用，跳过
                if used[i] or (i > 0 and nums[i] == nums[i - 1] and not used[i - 1]):
                    continue

                # 选择当前数字并标记为已使用
                path.append(nums[i])
                used[i] = True

                # 递归进行下一步选择
                backtrack(path)

                # 回溯，撤销选择并标记为未使用
                path.pop()
                used[i] = False

        # 调用回溯函数
        backtrack([])
        return result

# 时间复杂度：O(n * n!) - 生成所有排列的时间复杂度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * n!)，生成所有排列的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 27. LeetCode 78: Subsets（子集）

**题目描述**：
给定一个不含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

**解题思路**：
使用回溯法生成所有的子集。在每个递归调用中，都可以选择将当前元素加入子集或不加入子集，直至遍历完所有元素。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成子集的函数
    def subsets(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 将当前路径加入结果列表
            result.append(path[:])

            # 从当前索引开始遍历所有数字
            for i in range(start, len(nums)):
                # 选择当前数字
                path.append(nums[i])

                # 递归进行下一步选择
                backtrack(i + 1, path)

                # 回溯，撤销选择
                path.pop()

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 生成所有子集的时间复杂度，其中 n 是 nums 的长度。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，生成所有子集的时间复杂度。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 28. LeetCode 77: Combinations（组合）

**题目描述**：
给定两个整数 `n` 和 `k`，返回 `1` 到 `n` 中所有可能的 `k` 个数的组合。

**解题思路**：
使用回溯法生成所有组合。在每次递归中，从当前索引开始选择一个数字，并将其加入当前组合中，直到组合的长度等于 `k`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义生成组合的函数
    def combine(self, n: int, k: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(start, path):
            # 如果组合的长度等于 k，加入结果列表
            if len(path) == k:
                result.append(path[:])
                return

            # 从当前索引开始遍历所有可能的选择
            for i in range(start, n + 1):
                path.append(i)  # 选择当前数字
                backtrack(i + 1, path)  # 递归进行下一步选择
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(1, [])
        return result

# 时间复杂度：O(C(n, k)) - 生成所有组合的时间复杂度。
# 空间复杂度：O(k) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(C(n, k))，生成所有组合的时间复杂度。
- **空间复杂度**：O(k)，递归调用栈的空间复杂度。

---

### 29. LeetCode 39: Combination Sum（组合总和）

**题目描述**：
给定一个无重复元素的数组 `candidates` 和一个目标数 `target`，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

**解题思路**：
使用回溯法进行组合求和。每次递归调用时，可以选择当前元素，并继续递归，直到当前和等于 `target` 或超过 `target` 为止。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找组合总和的函数
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        # 初始化结果列表
        result = []

        # 定义回溯函数
        def backtrack(remaining, start, path):
            # 如果剩余目标为 0，说明找到一个合法组合
            if remaining == 0:
                result.append(path[:])
                return
            elif remaining < 0:  # 超过目标，直接返回
                return

            # 遍历所有可能的选择
            for i in range(start, len(candidates)):
                path.append(candidates[i])  # 选择当前元素
                backtrack(remaining - candidates[i], i, path)  # 递归调用
                path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(target, 0, [])
        return result

# 时间复杂度：O(n^target) - 每次递归中有多种选择。
# 空间复杂度：O(target) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^target)，每次递归中有多种选择。
- **空间复杂度**：O(target)，递归调用栈的空间复杂度。

---

### 30. LeetCode 131: Palindrome Partitioning（分割回文串）

**题目描述**：
给定一个字符串 `s`，将其分割成若干子串，使得每个子串都是回文串。返回所有可能的分割方案。

**解题思路**：
使用回溯法生成所有分割方案。在每次递归中，判断当前子串是否是回文串，如果是，则将该子串加入当前路径，并继续递归分割剩余的字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义分割回文串的函数
    def partition(self, s: str) -> List[List[str]]:
        # 初始化结果列表
        result = []

        # 定义判断是否为回文串的函数
        def is_palindrome(substring):
            return substring == substring[::-1]

        # 定义回溯函数
        def backtrack(start, path):
            # 如果起始位置等于字符串长度，说明找到一个合法分割方案
            if start == len(s):
                result.append(path[:])
                return

            # 遍历所有可能的分割位置
            for end in range(start + 1, len(s) + 1):
                # 如果当前子串是回文串，递归继续分割


                if is_palindrome(s[start:end]):
                    path.append(s[start:end])  # 选择当前子串
                    backtrack(end, path)  # 递归调用
                    path.pop()  # 回溯，撤销选择

        # 调用回溯函数
        backtrack(0, [])
        return result

# 时间复杂度：O(n * 2^n) - 每个字符都可以选择分割或不分割。
# 空间复杂度：O(n) - 递归调用栈的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * 2^n)，每个字符都可以选择分割或不分割，生成所有可能的分割方案。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。
