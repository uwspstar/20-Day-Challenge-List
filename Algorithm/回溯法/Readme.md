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

### 5 道 LeetCode 回溯法题目及详细解释

---

#### 1. LeetCode 46: 全排列 (Permutations)

##### Problem Description  
给定一个没有重复数字的数组，返回其所有可能的全排列。

##### 解法：回溯法  
回溯法通过逐步构建每个排列，每当长度达到数组长度时，记录该排列。

##### Python 代码：

```python
def permute(nums):
    # 定义一个递归函数 backtrack，传入参数为当前路径 path 和已使用的元素标记 used
    def backtrack(path, used):
        # 如果当前路径的长度等于给定数组的长度，说明找到了一个完整的排列
        if len(path) == len(nums):
            # 将该排列的拷贝添加到结果集中
            result.append(path[:])
            return
        
        # 遍历数组中的每个元素
        for i in range(len(nums)):
            # 如果该元素已经被使用过，跳过本次循环
            if used[i]:
                continue
            # 标记该元素已被使用
            used[i] = True
            # 将当前元素加入路径中
            path.append(nums[i])
            # 递归调用 backtrack 继续生成后续的排列
            backtrack(path, used)
            # 回溯：撤销选择，移除最后一个元素，并将该元素标记为未使用
            path.pop()
            used[i] = False

    # 初始化结果集，存放所有可能的排列
    result = []
    # 调用 backtrack 开始递归，传入空路径和未使用的标记数组
    backtrack([], [False] * len(nums))
    # 返回结果集
    return result

```

##### 解释：
- `backtrack` 递归函数用于生成全排列。
- 使用 `used` 数组来标记哪些元素已经被选择，避免重复选择。
- 递归结束条件是路径长度等于输入数组长度，此时将该路径加入结果中。

##### 时间复杂度：O(n!)  
##### 空间复杂度：O(n)

---

#### 2. LeetCode 77: 组合 (Combinations)

##### Problem Description  
给定两个整数 `n` 和 `k`，从 1 到 `n` 中选择 `k` 个数的所有组合。

##### 解法：回溯法  
我们通过递归构建每个组合，在选择数量达到 `k` 时记录该组合。

##### Python 代码：

```python
def combine(n, k):
    # 定义递归函数 backtrack，传入当前起始位置 start 和当前路径 path
    def backtrack(start, path):
        # 如果路径的长度等于 k，说明找到了一个有效的组合
        if len(path) == k:
            # 将该组合的拷贝添加到结果集中
            result.append(path[:])
            return
        
        # 从起始位置开始遍历数字
        for i in range(start, n + 1):
            # 将当前数字加入路径
            path.append(i)
            # 递归调用 backtrack，继续选择后续的数字
            backtrack(i + 1, path)
            # 回溯：撤销选择，移除最后一个数字
            path.pop()

    # 初始化结果集，存放所有组合
    result = []
    # 调用 backtrack 开始递归，传入初始起点 1 和空路径
    backtrack(1, [])
    # 返回结果集
    return result

```

##### 解释：
- `backtrack` 函数从 `start` 开始构建组合，每次递增选择的数字，直到达到 `k`。
- 使用 `path` 来记录当前的组合，达到长度 `k` 时，将其加入结果。

##### 时间复杂度：O(C(n, k))  
##### 空间复杂度：O(k)

---

#### 3. LeetCode 78: 子集 (Subsets)

##### Problem Description  
给定一个整数数组，返回该数组所有可能的子集（包括空集）。

##### 解法：回溯法  
在每个递归步骤，我们可以选择是否将当前数字加入子集中。

##### Python 代码：

```python
def subsets(nums):
    # 定义递归函数 backtrack，传入当前起始位置 start 和当前路径 path
    def backtrack(start, path):
        # 每次递归调用时，将当前路径的副本加入结果集，表示找到一个子集
        result.append(path[:])
        
        # 从起始位置开始遍历数字
        for i in range(start, len(nums)):
            # 将当前数字加入路径
            path.append(nums[i])
            # 递归调用 backtrack，继续选择后续的数字
            backtrack(i + 1, path)
            # 回溯：撤销选择，移除最后一个数字
            path.pop()

    # 初始化结果集，存放所有子集
    result = []
    # 调用 backtrack 开始递归，传入初始起点 0 和空路径
    backtrack(0, [])
    # 返回结果集
    return result

    return result
```

##### 解释：
- 每次递归调用时，我们将当前路径加入结果，因为子集的长度不固定。
- 遍历数组时，我们递增 `start`，避免重复选择相同的数字。

##### 时间复杂度：O(2^n)  
##### 空间复杂度：O(n)

---

#### 4. LeetCode 39: 组合总和 (Combination Sum)

##### Problem Description  
给定一个无重复元素的数组 `candidates` 和一个目标值 `target`，找出所有可以使数字和为目标值的组合。数组中的数字可以无限制重复选取。

##### 解法：回溯法  
每次选择一个数字后，我们继续递归减小目标值 `target`，直到 `target` 为 0。

##### Python 代码：

```python
def combinationSum(candidates, target):
    # 定义递归函数 backtrack，传入当前起始位置 start、当前路径 path 和剩余目标值 target
    def backtrack(start, path, target):
        # 如果剩余目标值为 0，说明找到了一个有效的组合
        if target == 0:
            result.append(path[:])
            return
        # 从起始位置开始遍历候选数
        for i in range(start, len(candidates)):
            # 如果当前候选数大于剩余目标值，跳过本次循环
            if candidates[i] > target:
                continue
            # 将当前候选数加入路径
            path.append(candidates[i])
            # 递归调用 backtrack，继续选择，target 减去当前选择的数字
            backtrack(i, path, target - candidates[i])
            # 回溯：撤销选择，移除最后一个数字
            path.pop()

    # 初始化结果集，存放所有组合
    result = []
    # 调用 backtrack 开始递归，传入初始起点 0、空路径和目标值
    backtrack(0, [], target)
    # 返回结果集
    return result
```

##### 解释：
- `backtrack` 函数递归减小目标值，当 `target` 为 0 时，记录当前路径。
- 递归遍历每个候选数，并允许重复选择。

##### 时间复杂度：O(2^n)  
##### 空间复杂度：O(target)

---

#### 5. LeetCode 51: N 皇后问题 (N-Queens)

##### Problem Description  
在一个 `n x n` 的棋盘上放置 `n` 个皇后，使得它们不能互相攻击。

##### 解法：回溯法  
使用回溯法在每一行中尝试放置一个皇后，递归检查是否可以继续放置。

##### Python 代码：

```python
def solveNQueens(n):
    # 定义递归函数 backtrack，传入当前行 row、对角线和列的集合以及棋盘 board
    def backtrack(row, diagonals, antiDiagonals, cols, board):
        # 如果所有行都放置了皇后，记录当前棋盘的结果
        if row == n:
            result.append(["".join(row) for row in board])
            return
        # 遍历当前行中的每一列，尝试放置皇后
        for col in range(n):
            # 如果当前列或对角线已有皇后，跳过本次循环
            if col in cols or (row - col) in diagonals or (row + col) in antiDiagonals:
                continue
            # 标记当前列和对角线
            cols.add(col)
            diagonals.add(row - col)
            antiDiagonals.add(row + col)
            # 在当前棋盘中放置皇后
            board[row][col] = 'Q'
            # 递归调用 backtrack，处理下一行
            backtrack(row + 1, diagonals, antiDiagonals, cols, board)
            # 回溯：移除皇后，撤销选择
            cols.remove(col)
            diagonals.remove(row - col)
            antiDiagonals.remove(row + col)
            board[row][col] = '.'

    # 初始化结果集，存放所有解
    result = []
    # 初始化空棋盘
    board = [['.'] * n for _ in range(n)]
    # 调用 backtrack 开始递归，传入初始行和空的对角线、列集合
    backtrack(0, set(), set(), set(), board)
    # 返回结果集
    return result
```

##### 解释：
- `backtrack` 函数通过递归放置皇后，并检查是否有冲突。
- 使用集合 `cols`、`diagonals` 和 `antiDiagonals` 来记录列和对角线，避免冲突。

##### 时间复杂度：O(n!)  
##### 空间复杂度：O(n)

---

### Conclusion  
回溯法是一种非常灵活且强大的算法，适合解决各种组合和排列问题。通过递归探索决策树，并使用剪枝来优化性能，我们可以高效地解决复杂问题。
