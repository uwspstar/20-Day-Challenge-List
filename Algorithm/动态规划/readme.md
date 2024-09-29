# 动态规划
### 动态规划 (Dynamic Programming)

#### Definition  
动态规划是一种通过将问题分解为更小的子问题来解决复杂问题的算法技术。它利用已解决的子问题的结果来构建全局解，从而避免重复计算，提高效率。动态规划适用于具有**重叠子问题 (Overlapping Subproblems)** 和**最优子结构 (Optimal Substructure)** 性质的问题。

#### Key Concepts  
1. **状态 (State)**: 表示问题在某个时刻的状态，用一个数组或矩阵存储。
2. **状态转移方程 (State Transition Equation)**: 通过一个或多个状态转移方程将当前状态与之前的状态联系起来，用于递推计算。
3. **边界条件 (Boundary Conditions)**: 初始化状态的值，作为递推的起点。
4. **自顶向下与自底向上 (Top-Down vs. Bottom-Up)**: 自顶向下使用递归和记忆化，自底向上使用迭代和状态数组。

#### 动态规划的步骤  
1. **定义状态数组**：确定一个数组或矩阵来表示问题的状态。
2. **建立状态转移方程**：找到当前状态与之前状态之间的关系，建立递推公式。
3. **确定边界条件**：初始化状态数组的值，为后续的递推提供基础。
4. **填充状态数组**：使用状态转移方程填充整个状态数组或矩阵，求得最终解。

#### 动态规划的适用场景  
- 最长子序列问题
- 背包问题
- 矩阵路径问题
- 股票买卖问题
- 最优分割问题

#### Python 动态规划模板

```python
def dynamic_programming_example(n):
    dp = [0] * (n + 1)  # 初始化状态数组
    dp[0], dp[1] = 0, 1  # 边界条件
    for i in range(2, n + 1):  # 自底向上填充状态数组
        dp[i] = dp[i - 1] + dp[i - 2]  # 状态转移方程
    return dp[n]
```

### 10 道 LeetCode 动态规划题目及详细解释

---

#### 1. LeetCode 70: 爬楼梯 (Climbing Stairs)

##### Problem Description  
每次可以爬 1 或 2 个台阶，问到达第 `n` 个台阶有多少种不同的爬楼梯方法。

##### 解法：动态规划  
使用动态规划计算到达每个台阶的方法数，状态转移方程 `dp[i] = dp[i - 1] + dp[i - 2]`。

##### Python 代码：

```python
def climbStairs(n):
    if n <= 2:
        return n
    dp = [0] * (n + 1)  # 初始化状态数组
    dp[1], dp[2] = 1, 2  # 边界条件
    for i in range(3, n + 1):  # 自底向上填充状态数组
        dp[i] = dp[i - 1] + dp[i - 2]  # 状态转移方程
    return dp[n]
```

##### 代码行解释：
```python
    dp = [0] * (n + 1)  # 初始化长度为 n + 1 的数组 dp，每个元素初始为 0
    dp[1], dp[2] = 1, 2  # 初始化边界条件：到达第 1 级和第 2 级台阶的方法数
    for i in range(3, n + 1):  # 从第 3 级台阶开始，逐步计算到达每一级台阶的方法数
        dp[i] = dp[i - 1] + dp[i - 2]  # 使用状态转移方程：dp[i] = dp[i - 1] + dp[i - 2]
```

##### 解释：
- `dp[i]` 表示到达第 `i` 级台阶的方法数。
- `dp[i - 1]` 是到达第 `i - 1` 级台阶的方法数，`dp[i - 2]` 是到达第 `i - 2` 级台阶的方法数。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 2. LeetCode 198: 打家劫舍 (House Robber)

##### Problem Description  
给定一个非负整数数组，表示每个房屋中存放的钱，不能同时偷相邻的两个房屋，求能偷到的最大金额。

##### 解法：动态规划  
使用动态规划计算到达每个房屋时能偷到的最大金额，状态转移方程 `dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])`。

##### Python 代码：

```python
def rob(nums):
    if not nums:
        return 0
    if len(nums) <= 2:
        return max(nums)
    dp = [0] * len(nums)  # 初始化状态数组
    dp[0], dp[1] = nums[0], max(nums[0], nums[1])  # 边界条件
    for i in range(2, len(nums)):  # 自底向上填充状态数组
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])  # 状态转移方程
    return dp[-1]  # 返回能偷到的最大金额
```

##### 代码行解释：
```python
    dp = [0] * len(nums)  # 初始化长度为 len(nums) 的数组 dp，每个元素初始为 0
    dp[0], dp[1] = nums[0], max(nums[0], nums[1])  # 初始化前两个房屋的状态
    for i in range(2, len(nums)):  # 从第 3 个房屋开始，逐步计算每个房屋能偷到的最大金额
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])  # 使用状态转移方程：dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])
```

##### 解释：
- `dp[i]` 表示到达第 `i` 个房屋时能偷到的最大金额。
- 每个房屋只能选择偷或不偷，如果偷第 `i` 个房屋，则不能偷第 `i - 1` 个房屋。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 3. LeetCode 300: 最长递增子序列 (Longest Increasing Subsequence)

##### Problem Description  
给定一个无序整数数组，找到其中最长递增子序列的长度。

##### 解法：动态规划  
使用动态规划计算以每个元素结尾的最长递增子序列长度，状态转移方程 `dp[i] = max(dp[i], dp[j] + 1)`，其中 `j < i` 且 `nums[i] > nums[j]`。

##### Python 代码：

```python
def lengthOfLIS(nums):
    if not nums:
        return 0
    dp = [1] * len(nums)  # 初始化状态数组，每个元素初始为 1
    for i in range(len(nums)):
        for j in range(i):
            if nums[i] > nums[j]:  # 只有在 nums[i] > nums[j] 时，才能更新 dp[i]
                dp[i] = max(dp[i], dp[j] + 1)  # 状态转移方程
    return max(dp)  # 返回最长递增子序列的长度
```

##### 代码行解释：
```python
    dp = [1] * len(nums)  # 初始化长度为 len(nums) 的数组 dp，每个元素初始为 1
    for i in range(len(nums)):  # 遍历每个元素，计算以该元素结尾的最长递增子序列长度
        for j in range(i):  # 遍历当前元素之前的所有元素
            if nums[i] > nums[j]:  # 如果当前元素大于前面的元素
                dp[i] = max(dp[i], dp[j] + 1)  # 使用状态转移方程：dp[i] = max(dp[i], dp[j] + 1)
```

##### 解释：
- `dp[i]` 表示以第 `i` 个元素结尾的最长递增子序列的长度。
- 通过遍历 `i` 前面的所有元素 `j` 来更新 `dp[i]`。

##### 时间复杂度：O(n^2)  
##### 空间复杂度：O(n)

---

#### 4. LeetCode 53: 最大子数组和 (Maximum Subarray)

##### Problem Description  
给定一个整数数组 `nums`，找到具有最大和的连续子数组，并返回其和。

##### 解法：动态规划  
使用动态规划计算以每个元素

结尾的最大子数组和，状态转移方程 `dp[i] = max(nums[i], dp[i - 1] + nums[i])`。

##### Python 代码：

```python
def maxSubArray(nums):
    if not nums:
        return 0
    dp = [0] * len(nums)  # 初始化状态数组
    dp[0] = nums[0]  # 边界条件
    for i in range(1, len(nums)):  # 从第 2 个元素开始
        dp[i] = max(nums[i], dp[i - 1] + nums[i])  # 状态转移方程
    return max(dp)  # 返回最大子数组和
```

##### 代码行解释：
```python
    dp = [0] * len(nums)  # 初始化长度为 len(nums) 的数组 dp，每个元素初始为 0
    dp[0] = nums[0]  # 初始化第一个元素的状态
    for i in range(1, len(nums)):  # 从第 2 个元素开始，逐步计算以每个元素结尾的最大子数组和
        dp[i] = max(nums[i], dp[i - 1] + nums[i])  # 使用状态转移方程：dp[i] = max(nums[i], dp[i - 1] + nums[i])
```

##### 解释：
- `dp[i]` 表示以第 `i` 个元素结尾的最大子数组和。
- 如果 `dp[i - 1] + nums[i]` 大于 `nums[i]`，则将当前元素加入子数组。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 5. LeetCode 62: 不同路径 (Unique Paths)

##### Problem Description  
一个机器人位于 `m x n` 网格的左上角 (起点)，它只能向下或向右移动，问有多少种不同的路径到达网格的右下角 (终点)。

##### 解法：动态规划  
使用动态规划计算到达每个格子的路径数量，状态转移方程 `dp[i][j] = dp[i - 1][j] + dp[i][j - 1]`。

##### Python 代码：

```python
def uniquePaths(m, n):
    dp = [[1] * n for _ in range(m)]  # 初始化状态矩阵，每个元素初始为 1
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]  # 状态转移方程
    return dp[-1][-1]  # 返回到达右下角的路径数量
```

##### 代码行解释：
```python
    dp = [[1] * n for _ in range(m)]  # 初始化 m x n 的矩阵 dp，每个元素初始为 1，表示每个格子初始路径数量为 1
    for i in range(1, m):  # 从第 1 行开始，逐行计算每个格子的路径数量
        for j in range(1, n):  # 从第 1 列开始，逐列计算每个格子的路径数量
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]  # 使用状态转移方程：dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
```

##### 解释：
- `dp[i][j]` 表示从起点到达格子 `(i, j)` 的路径数量。
- 每个格子的路径数量等于上方格子的路径数量加左边格子的路径数量。

##### 时间复杂度：O(m * n)  
##### 空间复杂度：O(m * n)

---

#### 6. LeetCode 322: 零钱兑换 (Coin Change)

##### Problem Description  
给定不同面额的硬币和一个总金额，计算凑成该金额所需的最少硬币个数。如果无法凑成该金额，返回 `-1`。

##### 解法：动态规划  
使用动态规划计算凑成每个金额所需的最少硬币数量，状态转移方程 `dp[i] = min(dp[i], dp[i - coin] + 1)`。

##### Python 代码：

```python
def coinChange(coins, amount):
    dp = [float('inf')] * (amount + 1)  # 初始化状态数组，每个元素初始为无穷大
    dp[0] = 0  # 边界条件
    for coin in coins:  # 遍历每个硬币
        for i in range(coin, amount + 1):  # 更新状态数组
            dp[i] = min(dp[i], dp[i - coin] + 1)  # 状态转移方程
    return dp[amount] if dp[amount] != float('inf') else -1  # 返回结果
```

##### 代码行解释：
```python
    dp = [float('inf')] * (amount + 1)  # 初始化长度为 amount + 1 的数组 dp，每个元素初始为无穷大
    dp[0] = 0  # 初始化边界条件：凑成金额 0 所需的硬币数量为 0
    for coin in coins:  # 遍历每个硬币
        for i in range(coin, amount + 1):  # 从当前硬币的面额开始，逐步计算凑成每个金额所需的最少硬币数量
            dp[i] = min(dp[i], dp[i - coin] + 1)  # 使用状态转移方程：dp[i] = min(dp[i], dp[i - coin] + 1)
```

##### 解释：
- `dp[i]` 表示凑成金额 `i` 所需的最少硬币数量。
- 通过遍历每个硬币的面额更新 `dp` 数组。

##### 时间复杂度：O(n * amount)  
##### 空间复杂度：O(amount)

--- 

#### 7. LeetCode 1143: 最长公共子序列 (Longest Common Subsequence)

##### Problem Description  
给定两个字符串 `text1` 和 `text2`，返回它们的最长公共子序列的长度。子序列是指通过删除原字符串中的一些字符而不改变剩余字符顺序的字符串。

##### 解法：动态规划  
使用二维动态规划数组 `dp`，`dp[i][j]` 表示 `text1` 的前 `i` 个字符与 `text2` 的前 `j` 个字符的最长公共子序列长度。状态转移方程为：  
- 如果 `text1[i-1] == text2[j-1]`，则 `dp[i][j] = dp[i-1][j-1] + 1`
- 否则 `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

##### Python 代码：

```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]  # 初始化二维状态数组
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i - 1] == text2[j - 1]:  # 如果当前字符相等
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:  # 否则取左边或上边的最大值
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[-1][-1]  # 返回二维数组右下角的值
```

##### 代码行解释：
```python
    dp = [[0] * (n + 1) for _ in range(m + 1)]  # 初始化大小为 (m + 1) x (n + 1) 的二维数组 dp，初始值均为 0
    for i in range(1, m + 1):  # 遍历 text1 的所有字符
        for j in range(1, n + 1):  # 遍历 text2 的所有字符
            if text1[i - 1] == text2[j - 1]:  # 如果 text1 和 text2 当前字符相同
                dp[i][j] = dp[i - 1][j - 1] + 1  # 状态转移方程：dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])  # 状态转移方程：取左边或上边的最大值
```

##### 解释：
- `dp[i][j]` 表示 `text1` 的前 `i` 个字符与 `text2` 的前 `j` 个字符的最长公共子序列长度。
- 通过遍历 `text1` 和 `text2`，逐步填充 `dp` 数组，最后返回 `dp[m][n]`。

##### 时间复杂度：O(m * n)  
##### 空间复杂度：O(m * n)

---

#### 8. LeetCode 64: 最小路径和 (Minimum Path Sum)

##### Problem Description  
给定一个包含非负整数的 `m x n` 网格 `grid`，请找出一条从左上角到右下角的路径，使得路径上的数字总和最小。每次只能向下或向右移动。

##### 解法：动态规划  
使用动态规划数组 `dp`，`dp[i][j]` 表示到达格子 `(i, j)` 的最小路径和。状态转移方程为：  
- 如果是第一行，则 `dp[i][j] = dp[i][j - 1] + grid[i][j]`
- 如果是第一列，则 `dp[i][j] = dp[i - 1][j] + grid[i][j]`
- 其他情况下，`dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]`

##### Python 代码：

```python
def minPathSum(grid):
    m, n = len(grid), len(grid[0])
    dp = [[0] * n for _ in range(m)]  # 初始化二维状态数组
    dp[0][0] = grid[0][0]  # 起点初始化为 grid[0][0]
    for i in range(1, m):  # 初始化第一列的路径和
        dp[i][0] = dp[i - 1][0] + grid[i][0]
    for j in range(1, n):  # 初始化第一行的路径和
        dp[0][j] = dp[0][j - 1] + grid[0][j]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]  # 状态转移方程
    return dp[-1][-1]  # 返回到达右下角的最小路径和
```

##### 代码行解释：
```python
    dp = [[0] * n for _ in range(m)]  # 初始化 m x n 的二维数组 dp，初始值均为 0
    dp[0][0] = grid[0][0]  # 初始化起点的值
    for i in range(1, m):  # 遍历第一列的所有格子
        dp[i][0] = dp[i - 1][0] + grid[i][0]  # 初始化第一列的路径和
    for j in range(1, n):  # 遍历第一行的所有格子
        dp[0][j] = dp[0][j - 1] + grid[0][j]  # 初始化第一行的路径和
    for i in range(1, m):  # 遍历除第一行和第一列外的所有格子
        for j in range(1, n):  # 遍历每一列
            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]  # 状态转移方程：dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]
```

##### 解释：
- `dp[i][j]` 表示到达格子 `(i, j)` 的最小路径和。
- 通过填充 `dp` 数组，逐步计算到达每个格子的最小路径和。

##### 时间复杂度：O(m * n)  
##### 空间复杂度：O(m * n)

---

#### 9. LeetCode 221: 最大正方形 (Maximal Square)

##### Problem Description  
在一个 `m x n` 的二维二进制矩阵中，找到只包含 `1` 的最大正方形，并返回其面积。

##### 解法：动态规划  
使用动态规划数组 `dp`，`dp[i][j]` 表示以 `(i, j)` 为右下角的最大正方形的边长。状态转移方程为：  
- 如果 `matrix[i][j] == '1'`，则 `dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1`

##### Python 代码：

```python
def maximalSquare(matrix):
    if not matrix:
        return 0
    m, n = len(matrix), len(matrix[0])
    dp = [[0] * n for _ in range(m)]  # 初始化二维状态数组
    max_side = 0  # 记录最大正方形的边长
    for i in range(m):
        for j in range(n):
            if matrix[i][j] == '1':  # 只有当矩阵中的值为 '1' 时，才进行计算
                if i == 0 or j == 0:  # 边界情况
                    dp[i][j] = 1
                else:
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1
                max_side = max(max_side, dp[i][j])  # 更新最大正方形的边长
    return max_side * max_side  # 返回最大正方形的面积
```

##### 代码行解释：
```python
    dp = [[0] * n for _ in range(m)]  # 初始化 m x n 的二维数组 dp，初始值均为 0
    max_side = 0  # 初始化最大正方形的边长
    for i in range(m):  # 遍历每一行
        for j in range(n):  # 遍历每一列
            if

 matrix[i][j] == '1':  # 只有当矩阵中的值为 '1' 时，才进行计算
                if i == 0 or j == 0:  # 边界情况
                    dp[i][j] = 1
                else:
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1  # 状态转移方程：dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1
                max_side = max(max_side, dp[i][j])  # 更新最大正方形的边长
```

##### 解释：
- `dp[i][j]` 表示以 `(i, j)` 为右下角的最大正方形的边长。
- 通过填充 `dp` 数组找到最大正方形的边长，返回其面积。

##### 时间复杂度：O(m * n)  
##### 空间复杂度：O(m * n)

---

#### 10. LeetCode 152: 乘积最大子数组 (Maximum Product Subarray)

##### Problem Description  
给定一个整数数组 `nums`，找出一个乘积最大的连续子数组，并返回该子数组的乘积。

##### 解法：动态规划  
使用动态规划计算以每个元素结尾的最大和最小乘积，状态转移方程为：  
- `max_product[i] = max(nums[i], nums[i] * max_product[i - 1], nums[i] * min_product[i - 1])`
- `min_product[i] = min(nums[i], nums[i] * max_product[i - 1], nums[i] * min_product[i - 1])`

##### Python 代码：

```python
def maxProduct(nums):
    if not nums:
        return 0
    max_product = min_product = result = nums[0]  # 初始化状态
    for i in range(1, len(nums)):
        # 使用临时变量存储 max_product，以便更新 min_product
        temp_max = max(nums[i], nums[i] * max_product, nums[i] * min_product)
        min_product = min(nums[i], nums[i] * max_product, nums[i] * min_product)
        max_product = temp_max
        result = max(result, max_product)  # 更新最大乘积
    return result
```

##### 代码行解释：
```python
    max_product = min_product = result = nums[0]  # 初始化最大乘积、最小乘积和结果
    for i in range(1, len(nums)):  # 遍历数组
        temp_max = max(nums[i], nums[i] * max_product, nums[i] * min_product)  # 计算当前元素的最大乘积
        min_product = min(nums[i], nums[i] * max_product, nums[i] * min_product)  # 计算当前元素的最小乘积
        max_product = temp_max  # 更新最大乘积
        result = max(result, max_product)  # 更新全局最大乘积
```

##### 解释：
- `max_product` 和 `min_product` 分别表示以当前元素结尾的最大和最小乘积。
- 遍历数组时，记录全局最大乘积。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

### Conclusion  
动态规划是一种强大的算法策略，适用于解决一类复杂问题，通过分解子问题和记忆化，可以显著提高算法效率。掌握动态规划的状态定义、状态转移方程和边界条件能够帮助解决各种最优子结构问题，如子序列、矩阵路径和背包问题。
