### 前缀和 (Prefix Sum)

#### Definition  
前缀和是一种常用的算法技巧，用于高效地计算数组或序列中某一段的元素之和。通过预处理一个前缀和数组，可以快速获取数组中任何子数组的和，而无需每次从头开始计算。前缀和技巧非常适合解决频繁查询区间和的问题，能够将查询的时间复杂度从 O(n) 降低到 O(1)。

#### Key Concepts  
1. **前缀和数组 (Prefix Sum Array)**: 前缀和数组的第 `i` 个元素表示原数组从起始元素到第 `i` 个元素的累计和。
2. **区间和的计算 (Range Sum Calculation)**: 使用前缀和数组可以通过公式 `prefix_sum[j] - prefix_sum[i-1]` 快速计算数组中从索引 `i` 到 `j` 的子数组之和。

#### 前缀和的步骤  
1. **计算前缀和数组**：遍历原数组，计算每个元素的前缀和，并存储在一个数组中。
2. **使用前缀和计算区间和**：通过查询前缀和数组的差值，快速得到任意区间的和。

#### 前缀和的适用场景  
- 频繁查询子数组和
- 求解二维数组的区域和
- 子数组的某些条件统计

#### Python 前缀和模板

```python
def prefix_sum(nums):
    n = len(nums)
    prefix = [0] * (n + 1)  # 初始化前缀和数组，长度为 n + 1
    for i in range(n):
        prefix[i + 1] = prefix[i] + nums[i]  # 计算前缀和
    return prefix
```

### 10 道 LeetCode 前缀和题目及详细解释

---

#### 1. LeetCode 303: 区域和检索 - 数组不可变 (Range Sum Query - Immutable)

##### Problem Description  
给定一个整数数组 `nums`，实现一个 `NumArray` 类，包含一个方法 `sumRange(i, j)`，可以返回数组中从索引 `i` 到 `j` 的元素之和。

##### 解法：前缀和  
使用前缀和数组预处理数据，使得每次查询可以在 O(1) 时间内返回区间和。

##### Python 代码：

```python
class NumArray:
    def __init__(self, nums):
        self.prefix = [0] * (len(nums) + 1)  # 初始化前缀和数组
        for i in range(len(nums)):
            self.prefix[i + 1] = self.prefix[i] + nums[i]  # 计算前缀和

    def sumRange(self, i, j):
        return self.prefix[j + 1] - self.prefix[i]  # 返回区间和
```

##### 解释：
- 在 `__init__` 方法中预处理前缀和数组，每个索引存储从 0 到当前索引的累计和。
- `sumRange` 方法使用前缀和的差值快速计算区间和。

##### 时间复杂度：  
- 初始化：O(n)  
- 查询：O(1)

##### 空间复杂度：O(n)

---

#### 2. LeetCode 560: 和为 K 的子数组 (Subarray Sum Equals K)

##### Problem Description  
给定一个整数数组和一个整数 `k`，找到该数组中和为 `k` 的连续子数组的个数。

##### 解法：前缀和 + 哈希表  
使用前缀和计算每个位置的累计和，并通过哈希表记录前缀和的出现次数，判断是否存在满足条件的子数组。

##### Python 代码：

```python
def subarraySum(nums, k):
    prefix_sum = 0  # 初始化前缀和
    count = 0  # 记录子数组数量
    prefix_sums_map = {0: 1}  # 存储前缀和出现的次数，初始前缀和为 0 出现一次
    for num in nums:
        prefix_sum += num  # 计算当前的前缀和
        if prefix_sum - k in prefix_sums_map:  # 判断是否存在和为 k 的子数组
            count += prefix_sums_map[prefix_sum - k]
        # 更新前缀和在哈希表中的出现次数
        prefix_sums_map[prefix_sum] = prefix_sums_map.get(prefix_sum, 0) + 1
    return count
```

##### 解释：
- 通过累加计算前缀和，每次查询是否存在之前的前缀和等于 `prefix_sum - k`。
- 使用哈希表记录前缀和的出现次数，以快速查询。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 3. LeetCode 238: 除自身以外数组的乘积 (Product of Array Except Self)

##### Problem Description  
给定一个整数数组 `nums`，返回一个数组 `answer`，其中 `answer[i]` 是 `nums` 中除了 `nums[i]` 之外其他元素的乘积。

##### 解法：前缀乘积  
使用前缀和后缀的乘积，计算每个位置的结果。

##### Python 代码：

```python
def productExceptSelf(nums):
    n = len(nums)
    result = [1] * n  # 初始化结果数组
    prefix = 1  # 前缀乘积
    for i in range(n):
        result[i] = prefix  # 记录当前前缀乘积
        prefix *= nums[i]  # 更新前缀乘积
    suffix = 1  # 后缀乘积
    for i in range(n - 1, -1, -1):
        result[i] *= suffix  # 更新结果数组为前缀乘积 * 后缀乘积
        suffix *= nums[i]  # 更新后缀乘积
    return result
```

##### 解释：
- 使用前缀和后缀分别计算每个位置的乘积，通过两次遍历数组来实现。
- 第一次遍历计算前缀乘积，第二次遍历计算后缀乘积并更新结果。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)（不包括结果数组）

---

#### 4. LeetCode 437: 路径总和 III (Path Sum III)

##### Problem Description  
给定一个二叉树的根节点和一个整数 `targetSum`，找到二叉树中和为 `targetSum` 的路径的数量。

##### 解法：前缀和 + DFS  
使用深度优先搜索 (DFS) 遍历树，结合前缀和记录当前路径的累计和，统计满足条件的路径数量。

##### Python 代码：

```python
def pathSum(root, targetSum):
    def dfs(node, current_sum):
        if not node:
            return 0
        current_sum += node.val  # 更新当前路径和
        count = prefix_sums.get(current_sum - targetSum, 0)  # 统计满足条件的路径数量
        prefix_sums[current_sum] = prefix_sums.get(current_sum, 0) + 1  # 更新前缀和记录
        count += dfs(node.left, current_sum)  # 遍历左子树
        count += dfs(node.right, current_sum)  # 遍历右子树
        prefix_sums[current_sum] -= 1  # 回溯，恢复前缀和状态
        return count

    prefix_sums = {0: 1}  # 初始化前缀和
    return dfs(root, 0)
```

##### 解释：
- 通过 DFS 遍历二叉树，累加当前路径的前缀和。
- 使用哈希表记录当前路径和的次数，方便快速查询。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 5. LeetCode 325: 和等于 k 的最长子数组长度 (Maximum Size Subarray Sum Equals k)

##### Problem Description  
给定一个整数数组 `nums` 和一个整数 `k`，找到数组中和为 `k` 的最长子数组并返回其长度。

##### 解法：前缀和 + 哈希表  
使用前缀和计算每个位置的累计和，并使用哈希表记录每个前缀和第一次出现的位置，找到最长子数组。

##### Python 代码：

```python
def maxSubArrayLen(nums, k):
    prefix_sum = 0  # 初始化前缀和
    max_len = 0  # 记录最长子数组长度
    prefix_sums_map = {0: -1}  # 存储前缀和的索引，初始为 0 对应 -1
    for i, num in enumerate(nums):
        prefix_sum += num  # 计算当前前缀和
        if prefix_sum - k in prefix_sums_map:  # 如果存在和为 k 的子数组
            max

_len = max(max_len, i - prefix_sums_map[prefix_sum - k])
        if prefix_sum not in prefix_sums_map:  # 记录当前前缀和的首次出现索引
            prefix_sums_map[prefix_sum] = i
    return max_len
```

##### 解释：
- 使用前缀和加速区间和的计算，通过哈希表记录每个前缀和第一次出现的索引，确保找到最长子数组。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 6. LeetCode 523: 连续的子数组和 (Continuous Subarray Sum)

##### Problem Description  
给定一个整数数组和一个整数 `k`，判断数组中是否存在连续的子数组，其元素之和为 `k` 的倍数。

##### 解法：前缀和 + 同余定理  
使用前缀和加速计算，同时通过同余定理判断前缀和是否满足条件。

##### Python 代码：

```python
def checkSubarraySum(nums, k):
    prefix_sum = 0
    prefix_sums_map = {0: -1}  # 初始化前缀和哈希表
    for i, num in enumerate(nums):
        prefix_sum += num
        if k != 0:
            prefix_sum %= k  # 计算前缀和对 k 的余数
        if prefix_sum in prefix_sums_map:
            if i - prefix_sums_map[prefix_sum] > 1:  # 确保子数组长度大于 1
                return True
        else:
            prefix_sums_map[prefix_sum] = i  # 记录前缀和首次出现的索引
    return False
```

##### 解释：
- 使用同余定理，通过哈希表记录前缀和对 `k` 的余数，判断是否存在符合条件的子数组。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 7. LeetCode 724: 寻找数组的中心索引 (Find Pivot Index)

##### Problem Description  
给定一个整数数组 `nums`，找到一个中心索引，使得其左侧所有元素的和等于右侧所有元素的和。

##### 解法：前缀和  
计算数组的总和，通过前缀和找到满足条件的中心索引。

##### Python 代码：

```python
def pivotIndex(nums):
    total_sum = sum(nums)  # 计算数组的总和
    left_sum = 0  # 初始化左侧前缀和
    for i, num in enumerate(nums):
        if left_sum == total_sum - left_sum - num:  # 判断是否为中心索引
            return i
        left_sum += num  # 更新左侧前缀和
    return -1  # 如果没有找到，返回 -1
```

##### 解释：
- 使用前缀和计算左侧元素和，判断当前索引是否满足左侧和等于右侧和。
- 通过遍历数组快速找到中心索引。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 8. LeetCode 560: 二维数组区域和检索 (Range Sum Query 2D - Immutable)

##### Problem Description  
给定一个二维矩阵，计算某个子矩形区域的元素总和。

##### 解法：二维前缀和  
通过预处理二维前缀和矩阵，快速计算任意子矩形的和。

##### Python 代码：

```python
class NumMatrix:
    def __init__(self, matrix):
        if not matrix or not matrix[0]:
            return
        m, n = len(matrix), len(matrix[0])
        self.prefix = [[0] * (n + 1) for _ in range(m + 1)]  # 初始化二维前缀和矩阵
        for i in range(m):
            for j in range(n):
                self.prefix[i + 1][j + 1] = self.prefix[i + 1][j] + self.prefix[i][j + 1] - self.prefix[i][j] + matrix[i][j]

    def sumRegion(self, row1, col1, row2, col2):
        return self.prefix[row2 + 1][col2 + 1] - self.prefix[row2 + 1][col1] - self.prefix[row1][col2 + 1] + self.prefix[row1][col1]
```

##### 解释：
- 使用二维前缀和矩阵快速计算任意子矩形区域的和。
- `sumRegion` 方法通过前缀和的差值计算区域和。

##### 时间复杂度：  
- 初始化：O(m * n)  
- 查询：O(1)

##### 空间复杂度：O(m * n)

---

#### 9. LeetCode 1124: 表现良好的最长时间段 (Longest Well-Performing Interval)

##### Problem Description  
给定一个整数数组 `hours`，数组中的元素表示每一天的工作时间，找到表现良好的最长时间段，其中表现良好意味着工作时间大于 8 小时。

##### 解法：前缀和 + 栈  
将工作时间转换为 1 和 -1，通过前缀和加速计算表现良好的最长时间段。

##### Python 代码：

```python
def longestWPI(hours):
    score = 0
    prefix_sums_map = {}  # 记录前缀和的首次出现位置
    max_len = 0  # 记录最长时间段
    for i, h in enumerate(hours):
        score += 1 if h > 8 else -1  # 大于 8 小时计为 1，否则计为 -1
        if score > 0:
            max_len = i + 1
        elif score - 1 in prefix_sums_map:
            max_len = max(max_len, i - prefix_sums_map[score - 1])
        if score not in prefix_sums_map:
            prefix_sums_map[score] = i  # 记录前缀和的首次出现位置
    return max_len
```

##### 解释：
- 将数组中的工作时间转换为 1 和 -1，表示表现良好或不良。
- 使用前缀和找到满足条件的最长时间段。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 10. LeetCode 1524: 和为奇数的子数组数目 (Number of Sub-arrays With Odd Sum)

##### Problem Description  
给定一个整数数组 `arr`，返回和为奇数的子数组的数目。

##### 解法：前缀和 + 同余  
通过前缀和计算每个子数组的和，使用奇偶性判断和为奇数的子数组。

##### Python 代码：

```python
def numOfSubarrays(arr):
    prefix_sum = 0
    odd_count = 0
    even_count = 1  # 初始前缀和为 0 视为偶数
    result = 0
    for num in arr:
        prefix_sum += num
        if prefix_sum % 2 == 0:  # 偶数前缀和
            result += odd_count
            even_count += 1
        else:  # 奇数前缀和
            result += even_count
            odd_count += 1
    return result % (10**9 + 7)
```

##### 解释：
- 使用前缀和加速计算子数组和的奇偶性，统计和为奇数的子数组数量。
- 通过前缀和的奇偶性判断当前子数组是否满足条件。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

### Conclusion  
前缀和是一种非常高效的算法技巧，通过预处理前缀和数组或矩阵，可以在常数时间内快速查询区间和。前缀和常用于解决子数组和、区间和查询等问题，有助于提高算法的效率。
