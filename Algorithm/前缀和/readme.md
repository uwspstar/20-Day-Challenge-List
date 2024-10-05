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

好的，我们现在开始讲解30道LeetCode中常见的前缀和（Prefix Sum）相关题目。每个题目将包含详细的题目描述、中文注释代码及时间和空间复杂度分析。由于篇幅较长，我会逐步展示，每次介绍5道题目。

---

### 1. LeetCode 560: Subarray Sum Equals K（和为 K 的子数组）

**题目描述**：
给定一个整数数组 `nums` 和一个目标整数 `k`，请你统计并返回该数组中和为 `k` 的连续子数组的个数。

**代码实现**：
```python
def subarraySum(nums: List[int], k: int) -> int:
    # 使用哈希表来存储前缀和的频率
    prefix_sum_count = {0: 1}
    # 初始化前缀和与子数组计数器
    prefix_sum = 0
    count = 0
    # 遍历数组中的每个元素
    for num in nums:
        # 更新当前前缀和
        prefix_sum += num
        # 检查当前前缀和减去目标值 k 是否存在于哈希表中
        if prefix_sum - k in prefix_sum_count:
            # 存在则说明找到一个子数组，计数器增加
            count += prefix_sum_count[prefix_sum - k]
        # 更新哈希表中前缀和的频率
        if prefix_sum in prefix_sum_count:
            prefix_sum_count[prefix_sum] += 1
        else:
            prefix_sum_count[prefix_sum] = 1
    return count

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
使用前缀和及哈希表来优化寻找和为 `k` 的子数组数量。通过记录前缀和的频率，可以在 O(1) 时间复杂度内判断是否存在符合条件的子数组。

---

### 2. LeetCode 523: Continuous Subarray Sum（连续的子数组和）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，编写一个函数来判断数组中是否存在长度至少为 2 的连续子数组，其元素总和为 `k` 的倍数（即 `sum = n * k`，其中 `n` 是一个整数）。

**代码实现**：
```python
def checkSubarraySum(nums: List[int], k: int) -> bool:
    # 初始化前缀和与哈希表（存储前缀和的余数和索引）
    prefix_sum = 0
    prefix_sum_mod = {0: -1}
    # 遍历数组中的每个元素
    for i, num in enumerate(nums):
        # 更新当前前缀和
        prefix_sum += num
        # 如果 k 不为 0，计算当前前缀和对 k 的余数
        if k != 0:
            prefix_sum %= k
        # 如果当前前缀和的余数之前存在，且长度至少为 2
        if prefix_sum in prefix_sum_mod:
            if i - prefix_sum_mod[prefix_sum] > 1:
                return True
        # 记录当前余数及其索引
        else:
            prefix_sum_mod[prefix_sum] = i
    return False

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(min(n, k)) - 哈希表最多存储 n 或 k 个不同的余数
```

**题目分析**：
通过前缀和余数的性质来判断子数组的和是否为 `k` 的倍数。利用哈希表存储余数，快速判断是否存在符合条件的子数组。

---

### 3. LeetCode 525: Contiguous Array（连续数组）

**题目描述**：
给定一个二进制数组 `nums`，找到一个长度最长的子数组，该子数组内的 `0` 和 `1` 的个数相等。

**代码实现**：
```python
def findMaxLength(nums: List[int]) -> int:
    # 使用哈希表来存储前缀和的索引
    prefix_sum_index = {0: -1}
    # 初始化前缀和与最大长度
    prefix_sum = 0
    max_length = 0
    # 遍历数组中的每个元素
    for i, num in enumerate(nums):
        # 将 0 视为 -1，更新前缀和
        prefix_sum += 1 if num == 1 else -1
        # 如果当前前缀和已存在于哈希表中
        if prefix_sum in prefix_sum_index:
            # 更新最大长度
            max_length = max(max_length, i - prefix_sum_index[prefix_sum])
        else:
            # 否则记录当前前缀和及其索引
            prefix_sum_index[prefix_sum] = i
    return max_length

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
将 `0` 视为 `-1`，利用前缀和的方法来判断子数组中 `0` 和 `1` 的个数是否相等，从而找到最长的符合条件的子数组。

---

### 4. LeetCode 930: Binary Subarrays With Sum（和为 S 的二进制子数组）

**题目描述**：
给定一个二进制数组 `nums` 和一个目标值 `goal`，返回和为 `goal` 的非空子数组的个数。

**代码实现**：
```python
def numSubarraysWithSum(nums: List[int], goal: int) -> int:
    # 使用哈希表来存储前缀和的频率
    prefix_sum_count = {0: 1}
    # 初始化前缀和与子数组计数器
    prefix_sum = 0
    count = 0
    # 遍历数组中的每个元素
    for num in nums:
        # 更新当前前缀和
        prefix_sum += num
        # 检查当前前缀和减去目标值 goal 是否存在于哈希表中
        if prefix_sum - goal in prefix_sum_count:
            count += prefix_sum_count[prefix_sum - goal]
        # 更新哈希表中前缀和的频率
        prefix_sum_count[prefix_sum] = prefix_sum_count.get(prefix_sum, 0) + 1
    return count

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
利用前缀和的特性来快速找到和为目标值的二进制子数组数量，通过哈希表记录前缀和频率，达到线性时间复杂度。

---

### 5. LeetCode 974: Subarray Sums Divisible by K（和可被 K 整除的子数组）

**题目描述**：
给定一个整数数组 `A` 和一个整数 `K`，请找到数组中和可被 `K` 整除的非空子数组的个数。

**代码实现**：
```python
def subarraysDivByK(A: List[int], K: int) -> int:
    # 使用哈希表来存储前缀和的余数频率
    prefix_sum_mod = {0: 1}
    # 初始化前缀和与子数组计数器
    prefix_sum = 0
    count = 0
    # 遍历数组中的每个元素
    for num in A:
        # 更新当前前缀和
        prefix_sum += num
        # 计算当前前缀和对 K 的余数，并处理负余数情况
        mod = prefix_sum % K
        if mod < 0:
            mod += K
        # 检查当前余数是否存在于哈希表中
        if mod in prefix_sum_mod:
            count += prefix_sum_mod[mod]
        # 更新哈希表中余数的频率
        prefix_sum_mod[mod] = prefix_sum_mod.get(mod, 0) + 1
    return count

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(K) - 哈希表最多存储 K 个不同的余数
```

**题目分析**：
通过前缀和的余数特性，快速判断和可被 `K` 整除的子数组数量。哈希表记录每个余数的出现频率，节省了遍历时间。

---

好的，我们继续讲解接下来的5道LeetCode前缀和相关题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 6. LeetCode 238: Product of Array Except Self（除自身以外数组的乘积）

**题目描述**：
给你一个整数数组 `nums`，返回数组 `answer`，其中 `answer[i]` 是 `nums` 中除了 `nums[i]` 之外其余各元素的乘积。要求时间复杂度为 O(n)，并且不使用除法。

**代码实现**：
```python
def productExceptSelf(nums: List[int]) -> List[int]:
    # 初始化结果数组，长度与 nums 相同
    res = [1] * len(nums)
    # 从左到右遍历数组，计算左侧乘积
    left_product = 1
    for i in range(len(nums)):
        res[i] = left_product
        left_product *= nums[i]
    # 从右到左遍历数组，计算右侧乘积
    right_product = 1
    for i in range(len(nums) - 1, -1, -1):
        res[i] *= right_product
        right_product *= nums[i]
    return res

# 时间复杂度：O(n) - 两次遍历数组
# 空间复杂度：O(1) - 结果数组不算在额外空间中
```

**题目分析**：
利用前缀乘积和后缀乘积，分别计算每个位置的左侧乘积和右侧乘积，再相乘得到最终结果。该方法不需要额外空间来存储中间结果。

---

### 7. LeetCode 209: Minimum Size Subarray Sum（长度最小的子数组）

**题目描述**：
给定一个含有 `n` 个正整数的数组 `nums` 和一个正整数 `s`，找出该数组中满足其和大于等于 `s` 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。

**代码实现**：
```python
def minSubArrayLen(s: int, nums: List[int]) -> int:
    # 初始化左右指针、当前和、最小长度
    left = 0
    current_sum = 0
    min_length = float('inf')
    # 遍历数组中的每个元素
    for right in range(len(nums)):
        # 更新当前和
        current_sum += nums[right]
        # 当当前和大于等于 s 时，更新最小长度并移动左指针
        while current_sum >= s:
            min_length = min(min_length, right - left + 1)
            current_sum -= nums[left]
            left += 1
    # 返回最小长度（如果没有找到符合条件的子数组，则返回 0）
    return 0 if min_length == float('inf') else min_length

# 时间复杂度：O(n) - 左右指针各遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题利用滑动窗口和前缀和来确定最小长度子数组，每次找到符合条件的子数组时，更新最小长度并移动左指针。

---

### 8. LeetCode 325: Maximum Size Subarray Sum Equals k（和为 k 的最大子数组长度）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，请找到数组中和为 `k` 的最长连续子数组，并返回其长度。

**代码实现**：
```python
def maxSubArrayLen(nums: List[int], k: int) -> int:
    # 使用哈希表来存储前缀和的索引
    prefix_sum_index = {0: -1}
    # 初始化前缀和与最大长度
    prefix_sum = 0
    max_length = 0
    # 遍历数组中的每个元素
    for i, num in enumerate(nums):
        # 更新当前前缀和
        prefix_sum += num
        # 检查当前前缀和减去目标值 k 是否存在于哈希表中
        if prefix_sum - k in prefix_sum_index:
            max_length = max(max_length, i - prefix_sum_index[prefix_sum - k])
        # 如果当前前缀和未出现在哈希表中，记录其索引
        if prefix_sum not in prefix_sum_index:
            prefix_sum_index[prefix_sum] = i
    return max_length

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
利用前缀和与哈希表来记录前缀和的索引，快速判断是否存在和为 `k` 的子数组，从而找到最长的符合条件的子数组。

---

### 9. LeetCode 1124: Longest Well-Performing Interval（最长表现良好的时间段）

**题目描述**：
当员工连续 `hours` 超过 `8` 小时时，我们称之为表现良好的时间段。给定一个整数数组 `hours`，表示每一天的工作时长，请返回表现良好的最长时间段的长度。

**代码实现**：
```python
def longestWPI(hours: List[int]) -> int:
    # 初始化前缀和与哈希表
    prefix_sum = 0
    prefix_sum_index = {}
    max_length = 0
    # 遍历数组中的每个元素
    for i, hour in enumerate(hours):
        # 工作时长超过 8 小时计为 1，反之为 -1
        prefix_sum += 1 if hour > 8 else -1
        # 如果前缀和大于 0，说明从 0 到当前的时间段表现良好
        if prefix_sum > 0:
            max_length = i + 1
        # 检查前缀和减去 1 是否存在，更新最大长度
        elif prefix_sum - 1 in prefix_sum_index:
            max_length = max(max_length, i - prefix_sum_index[prefix_sum - 1])
        # 记录前缀和首次出现的索引
        if prefix_sum not in prefix_sum_index:
            prefix_sum_index[prefix_sum] = i
    return max_length

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
将工作时长转化为前缀和，通过前缀和大于 0 来判断表现良好的时间段，并记录每个前缀和首次出现的索引，找到最长的时间段。

---

### 10. LeetCode 437: Path Sum III（二叉树路径总和 III）

**题目描述**：
给定一个二叉树的根节点 `root` 和一个目标值 `sum`，计算二叉树中路径和等于目标值的路径数量。路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

**代码实现**：
```python
def pathSum(root: Optional[TreeNode], target_sum: int) -> int:
    # 使用哈希表来存储前缀和的频率
    prefix_sum_count = {0: 1}
    # 定义一个辅助函数
    def dfs(node, current_sum):
        # 如果节点为空，返回 0
        if not node:
            return 0
        # 更新当前前缀和
        current_sum += node.val
        # 查找以当前节点为结束节点的路径数
        path_count = prefix_sum_count.get(current_sum - target_sum, 0)
        # 更新哈希表中当前前缀和的频率
        prefix_sum_count[current_sum] = prefix_sum_count.get(current_sum, 0) + 1
        # 遍历左右子树
        path_count += dfs(node.left, current_sum)
        path_count += dfs(node.right, current_sum)
        # 递归返回前恢复哈希表中前缀和的频率（回溯）
        prefix_sum_count[current_sum] -= 1
        return path_count
    
    # 调用递归函数
    return dfs(root, 0)

# 时间复杂度：O(n) - 遍历所有节点
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
该题利用前缀和的思想和深度优先搜索（DFS）结合，通过回溯方式查找每个节点为结束节点的路径数。哈希表记录前缀和的频率，可以快速查找到符合条件的路径。

---

好的，我们继续讲解接下来的5道LeetCode前缀和相关题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 11. LeetCode 1248: Count Number of Nice Subarrays（统计优美子数组）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，请你返回该数组中「优美子数组」的数量。优美子数组定义为「包含 `k` 个奇数的连续子数组」。

**代码实现**：
```python
def numberOfSubarrays(nums: List[int], k: int) -> int:
    # 使用哈希表来存储前缀和的频率
    prefix_sum_count = {0: 1}
    # 初始化前缀和与子数组计数器
    prefix_sum = 0
    count = 0
    # 遍历数组中的每个元素
    for num in nums:
        # 更新当前前缀和，遇到奇数时加 1，偶数时加 0
        prefix_sum += num % 2
        # 检查当前前缀和减去 k 是否存在于哈希表中
        if prefix_sum - k in prefix_sum_count:
            count += prefix_sum_count[prefix_sum - k]
        # 更新哈希表中前缀和的频率
        prefix_sum_count[prefix_sum] = prefix_sum_count.get(prefix_sum, 0) + 1
    return count

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
将奇数视为 1，偶数视为 0，利用前缀和的方式来记录奇数的个数，再通过哈希表查找包含 k 个奇数的子数组数量。该方法能够在 O(n) 时间内完成查找。

---

### 12. LeetCode 1395: Count Number of Teams（统计作战单位数）

**题目描述**：
给定一个整数数组 `rating`，其中 `rating[i]` 代表第 `i` 名士兵的战斗力等级。请你返回能够组成「作战单位」的数量。一个「作战单位」指的是三个士兵的组合 `(i, j, k)`，满足 `i < j < k` 且 `rating[i] < rating[j] < rating[k]` 或者 `rating[i] > rating[j] > rating[k]`。

**代码实现**：
```python
def numTeams(rating: List[int]) -> int:
    # 初始化作战单位计数器
    count = 0
    # 遍历每个士兵的战斗力等级
    for j in range(len(rating)):
        # 统计左侧小于和大于当前士兵的数量
        left_less, left_greater = 0, 0
        for i in range(j):
            if rating[i] < rating[j]:
                left_less += 1
            elif rating[i] > rating[j]:
                left_greater += 1
        # 统计右侧小于和大于当前士兵的数量
        right_less, right_greater = 0, 0
        for k in range(j + 1, len(rating)):
            if rating[k] < rating[j]:
                right_less += 1
            elif rating[k] > rating[j]:
                right_greater += 1
        # 更新作战单位的数量
        count += left_less * right_greater + left_greater * right_less
    return count

# 时间复杂度：O(n^2) - 两次遍历统计左侧和右侧数量
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题主要通过双重遍历的方式统计左侧和右侧小于或大于当前士兵的数量，再根据组合关系计算作战单位的数量。

---

### 13. LeetCode 1074: Number of Submatrices That Sum to Target（元素和等于目标值的子矩阵数量）

**题目描述**：
给定一个 `matrix` 和一个目标值 `target`，返回元素和等于目标值的非空子矩阵的数量。子矩阵是一个由矩阵中的一定数量的连续行和连续列组成的矩形区域。

**代码实现**：
```python
def numSubmatrixSumTarget(matrix: List[List[int]], target: int) -> int:
    # 获取矩阵的行数和列数
    rows, cols = len(matrix), len(matrix[0])
    # 初始化子矩阵计数器
    count = 0
    # 遍历每一行作为起始行
    for start_row in range(rows):
        # 初始化前缀和数组
        prefix_sum = [0] * cols
        # 遍历每一行作为结束行
        for end_row in range(start_row, rows):
            # 更新前缀和数组
            for col in range(cols):
                prefix_sum[col] += matrix[end_row][col]
            # 使用哈希表来存储前缀和的频率
            prefix_sum_count = {0: 1}
            current_sum = 0
            # 遍历前缀和数组，查找和为目标值的子矩阵数量
            for sum_val in prefix_sum:
                current_sum += sum_val
                if current_sum - target in prefix_sum_count:
                    count += prefix_sum_count[current_sum - target]
                prefix_sum_count[current_sum] = prefix_sum_count.get(current_sum, 0) + 1
    return count

# 时间复杂度：O(n^2 * m) - 每对行组合，遍历列并使用前缀和查找子矩阵
# 空间复杂度：O(m) - 使用了前缀和数组及哈希表存储列的前缀和
```

**题目分析**：
通过固定起始行和结束行的方式，将二维矩阵的问题转化为一维前缀和的问题，再使用哈希表来查找和为目标值的子矩阵数量。

---

### 14. LeetCode 238: Product of Array Except Self（除自身以外数组的乘积）

**题目描述**：
给定一个整数数组 `nums`，返回一个数组 `answer`，其中 `answer[i]` 是 `nums` 中除了 `nums[i]` 之外其余各元素的乘积。要求时间复杂度为 O(n)，并且不使用除法。

**代码实现**：
```python
def productExceptSelf(nums: List[int]) -> List[int]:
    # 初始化结果数组，长度与 nums 相同
    res = [1] * len(nums)
    # 从左到右遍历数组，计算左侧乘积
    left_product = 1
    for i in range(len(nums)):
        res[i] = left_product
        left_product *= nums[i]
    # 从右到左遍历数组，计算右侧乘积
    right_product = 1
    for i in range(len(nums) - 1, -1, -1):
        res[i] *= right_product
        right_product *= nums[i]
    return res

# 时间复杂度：O(n) - 两次遍历数组
# 空间复杂度：O(1) - 结果数组不算在额外空间中
```

**题目分析**：
利用前缀乘积和后缀乘积，分别计算每个位置的左侧乘积和右侧乘积，再相乘得到最终结果。该方法不需要额外空间来存储中间结果。

---

### 15. LeetCode 303: Range Sum Query - Immutable（区域和检索 - 不可变）

**题目描述**：
给定一个整数数组 `nums`，实现 `NumArray` 类，该类包含一个方法 `sumRange(i, j)`，返回数组中索引 `i` 到 `j`（包含 `i` 和 `j`）之间元素的总和。

**代码实现**：
```python
class NumArray:

    def __init__(self, nums: List[int]):
        # 计算前缀和数组
        self.prefix_sum = [0] * (len(nums) + 1)
        for i in range(len(nums)):
            self.prefix_sum[i + 1] = self.prefix_sum[i] + nums[i]

    def sumRange(self, left: int, right: int) -> int:
        # 利用前缀和计算区域和
        return self.prefix_sum[right + 1] - self.prefix_sum[left]

# 时间复杂度：O(1) - 每次检索时间复杂度为常数
# 空间复杂度：O(n) - 前缀和数组占用 O(n) 的空间
```

**题目分析**：
利用前缀和数组来实现区域和的快速查询。在构建前缀和数组时消耗 O(n) 的时间和空间，查询区域和时只需常数

时间。

---

好的，我们继续讲解接下来的5道LeetCode前缀和相关题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 16. LeetCode 304: Range Sum Query 2D - Immutable（二维区域和检索 - 不可变）

**题目描述**：
给定一个 `m x n` 的整数矩阵 `matrix`，请实现 `NumMatrix` 类，该类包含一个方法 `sumRegion(row1, col1, row2, col2)`，该方法返回矩阵中从 `(row1, col1)` 到 `(row2, col2)` 范围内元素的总和。

**代码实现**：
```python
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        # 获取矩阵的行数和列数
        rows, cols = len(matrix), len(matrix[0]) if matrix else 0
        # 初始化前缀和矩阵，行列均比原矩阵多 1
        self.prefix_sum = [[0] * (cols + 1) for _ in range(rows + 1)]
        # 计算二维前缀和矩阵
        for r in range(1, rows + 1):
            for c in range(1, cols + 1):
                self.prefix_sum[r][c] = (matrix[r - 1][c - 1]
                                         + self.prefix_sum[r - 1][c]
                                         + self.prefix_sum[r][c - 1]
                                         - self.prefix_sum[r - 1][c - 1])

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        # 计算指定区域的总和
        return (self.prefix_sum[row2 + 1][col2 + 1]
                - self.prefix_sum[row1][col2 + 1]
                - self.prefix_sum[row2 + 1][col1]
                + self.prefix_sum[row1][col1])

# 时间复杂度：O(1) - 每次检索时间复杂度为常数
# 空间复杂度：O(m * n) - 前缀和矩阵占用 O(m * n) 的空间
```

**题目分析**：
使用二维前缀和矩阵来实现区域和的快速查询。前缀和矩阵在构建时需要遍历整个矩阵，但在查询时只需常数时间即可得到指定区域的和。

---

### 17. LeetCode 2381: Shift 2D Grid（2D 网格迁移）

**题目描述**：
给定一个 `m x n` 的整数矩阵 `grid` 和一个整数 `k`，每次操作将矩阵中每个元素向右移动一个位置，并且矩阵的最后一个元素会被移动到第一行的第一个位置。请你返回经过 `k` 次迁移后的矩阵。

**代码实现**：
```python
def shiftGrid(grid: List[List[int]], k: int) -> List[List[int]]:
    # 获取矩阵的行数和列数
    rows, cols = len(grid), len(grid[0])
    # 将矩阵展开成一维数组
    flat = [grid[r][c] for r in range(rows) for c in range(cols)]
    # 计算实际需要移动的次数（取模处理）
    k = k % (rows * cols)
    # 对一维数组进行切片操作并重新排列
    flat = flat[-k:] + flat[:-k]
    # 将一维数组重新填充回二维矩阵
    return [[flat[r * cols + c] for c in range(cols)] for r in range(rows)]

# 时间复杂度：O(m * n) - 遍历矩阵一次
# 空间复杂度：O(m * n) - 需要一个一维数组存储展开后的矩阵元素
```

**题目分析**：
通过将二维矩阵展开为一维数组，使用切片操作实现快速的元素迁移，再将一维数组重新填充回二维矩阵。

---

### 18. LeetCode 363: Max Sum of Rectangle No Larger Than K（不超过 K 的最大矩形和）

**题目描述**：
给定一个 `m x n` 的矩阵 `matrix` 和一个整数 `k`，请你找出矩阵中和不超过 `k` 的最大矩形和。

**代码实现**：
```python
def maxSumSubmatrix(matrix: List[List[int]], k: int) -> int:
    import bisect
    # 获取矩阵的行数和列数
    rows, cols = len(matrix), len(matrix[0])
    max_sum = float('-inf')
    # 遍历每一列作为起始列
    for left in range(cols):
        # 初始化行的前缀和
        row_sums = [0] * rows
        # 遍历每一列作为结束列
        for right in range(left, cols):
            # 更新每行的前缀和
            for r in range(rows):
                row_sums[r] += matrix[r][right]
            # 初始化当前行前缀和的集合和当前和
            prefix_sums = [0]
            current_sum = 0
            # 遍历行前缀和
            for sum_val in row_sums:
                current_sum += sum_val
                # 使用二分查找法找到当前和减去 k 的最小前缀和位置
                idx = bisect.bisect_left(prefix_sums, current_sum - k)
                if idx < len(prefix_sums):
                    max_sum = max(max_sum, current_sum - prefix_sums[idx])
                # 插入当前和到前缀和集合中
                bisect.insort(prefix_sums, current_sum)
    return max_sum

# 时间复杂度：O(min(m, n)^2 * max(m, n) * log(max(m, n))) - 双重遍历列，并使用二分查找
# 空间复杂度：O(max(m, n)) - 存储每行的前缀和
```

**题目分析**：
将二维矩阵压缩成一维前缀和，然后使用二分查找法查找和不超过 `k` 的最大矩形和。通过逐列压缩前缀和，可以有效减少遍历次数。

---

### 19. LeetCode 238: Product of Array Except Self（除自身以外数组的乘积）

**题目描述**：
给定一个整数数组 `nums`，返回一个数组 `answer`，其中 `answer[i]` 是 `nums` 中除了 `nums[i]` 之外其余各元素的乘积。要求时间复杂度为 O(n)，并且不使用除法。

**代码实现**：
```python
def productExceptSelf(nums: List[int]) -> List[int]:
    # 初始化结果数组，长度与 nums 相同
    res = [1] * len(nums)
    # 从左到右遍历数组，计算左侧乘积
    left_product = 1
    for i in range(len(nums)):
        res[i] = left_product
        left_product *= nums[i]
    # 从右到左遍历数组，计算右侧乘积
    right_product = 1
    for i in range(len(nums) - 1, -1, -1):
        res[i] *= right_product
        right_product *= nums[i]
    return res

# 时间复杂度：O(n) - 两次遍历数组
# 空间复杂度：O(1) - 结果数组不算在额外空间中
```

**题目分析**：
通过前缀乘积和后缀乘积的方式计算每个位置的乘积，不使用除法，并且只需常量空间来保存中间结果。

---

### 20. LeetCode 1170: Compare Strings by Frequency of the Smallest Character（通过最小字符频次比较字符串）

**题目描述**：
给定两个字符串数组 `queries` 和 `words`，对于 `queries` 中的每个查询字符串，计算它的最小字符频次，并返回一个数组 `answer`，其中 `answer[i]` 是 `queries[i]` 的最小字符频次小于 `words` 中最小字符频次的数量。

**代码实现**：
```python
def numSmallerByFrequency(queries: List[str], words: List[str]) -> List[int]:
    # 定义辅助函数，计算最小字符频次
    def f(s):
        return s.count(min(s))

    # 计算每个查询字符串和单词的最小字符频次
    queries_freq = [f(query) for query in queries]
    words_freq = [f(word) for word in words]
    # 对单词的最小字符频次进行排序
    words_freq.sort()
    result = []
    # 遍历每个查询字符串的最小字符频次
    for q_freq in queries_freq:
        # 计算比 q_freq 大的单词数量（使用二分查找）
        count = len(words_freq) - bisect.bisect_right(words_freq, q_freq)
        result.append(count)
    return result

# 时间复杂

度：O((m + n) * log n) - 计算频次后排序，并使用二分查找
# 空间复杂度：O(n) - 存储 words 的频次结果
```

**题目分析**：
计算最小字符的频次，并使用二分查找法判断每个查询字符串的频次小于 `words` 中频次的数量。通过排序和二分查找能够有效提升查询效率。

---

好的，我们继续讲解接下来的5道LeetCode前缀和相关题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 21. LeetCode 124: Binary Tree Maximum Path Sum（二叉树中的最大路径和）

**题目描述**：
给定一个非空二叉树的根节点 `root`，返回其最大路径和。路径被定义为从树中任意节点出发，沿父节点-子节点连接，达到任意节点的路径，路径至多包含一个拐点（即不能回头）。

**代码实现**：
```python
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        # 初始化全局最大路径和
        self.max_sum = float('-inf')
        
        # 定义一个辅助函数，返回某个节点的最大路径和
        def get_max_gain(node):
            if not node:
                return 0
            # 递归计算左右子树的最大贡献值（若为负则舍弃）
            left_gain = max(get_max_gain(node.left), 0)
            right_gain = max(get_max_gain(node.right), 0)
            
            # 更新当前节点的最大路径和
            current_max_path = node.val + left_gain + right_gain
            # 更新全局最大路径和
            self.max_sum = max(self.max_sum, current_max_path)
            
            # 返回该节点的最大贡献值（单边）
            return node.val + max(left_gain, right_gain)
        
        # 调用辅助函数计算最大路径和
        get_max_gain(root)
        return self.max_sum

# 时间复杂度：O(n) - 遍历每个节点一次
# 空间复杂度：O(h) - 递归调用栈的空间，h 为树的高度
```

**题目分析**：
通过递归计算每个节点的最大路径和，使用前缀和思想来追踪从某个节点开始的最大路径和，递归返回每个节点的最大贡献值，从而找到全局最大路径和。

---

### 22. LeetCode 974: Subarray Sums Divisible by K（和可被 K 整除的子数组）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `K`，找到数组中和可被 `K` 整除的非空子数组的个数。

**代码实现**：
```python
def subarraysDivByK(nums: List[int], K: int) -> int:
    # 使用哈希表来存储前缀和的余数频率
    prefix_sum_count = {0: 1}
    # 初始化前缀和与子数组计数器
    prefix_sum = 0
    count = 0
    # 遍历数组中的每个元素
    for num in nums:
        # 更新当前前缀和
        prefix_sum += num
        # 计算当前前缀和对 K 的余数，并处理负余数情况
        mod = prefix_sum % K
        if mod < 0:
            mod += K
        # 检查当前余数是否存在于哈希表中
        if mod in prefix_sum_count:
            count += prefix_sum_count[mod]
        # 更新哈希表中余数的频率
        prefix_sum_count[mod] = prefix_sum_count.get(mod, 0) + 1
    return count

# 时间复杂度：O(n) - 遍历数组一次，并在哈希表中查找和更新元素
# 空间复杂度：O(K) - 哈希表最多存储 K 个不同的余数
```

**题目分析**：
通过前缀和的余数特性，快速判断和可被 `K` 整除的子数组数量。哈希表记录每个余数的出现频率，能够在 O(n) 时间内完成查找。

---

### 23. LeetCode 2013: Detect Squares（检测正方形）

**题目描述**：
设计一个数据结构 `DetectSquares` 来检测正方形，每个添加的点是 `(x, y)` 坐标，并实现以下功能：
1. `add(point)`：在数据结构中添加一个点。
2. `count(point)`：返回以 `point` 为顶点之一的正方形的数量。

**代码实现**：
```python
class DetectSquares:

    def __init__(self):
        # 使用哈希表存储每个点的出现次数
        self.points_count = defaultdict(int)

    def add(self, point: List[int]) -> None:
        # 更新点的出现次数
        self.points_count[tuple(point)] += 1

    def count(self, point: List[int]) -> int:
        x, y = point
        total_squares = 0
        # 遍历所有可能的点
        for (px, py), cnt in self.points_count.items():
            # 排除非对角线的点
            if abs(px - x) != abs(py - y) or px == x or py == y:
                continue
            # 计算其他两个顶点的坐标
            if (px, y) in self.points_count and (x, py) in self.points_count:
                total_squares += cnt * self.points_count[(px, y)] * self.points_count[(x, py)]
        return total_squares

# 时间复杂度：
# add() - O(1)，每次添加点的时间复杂度为常数
# count() - O(n)，遍历所有点并判断是否形成正方形
# 空间复杂度：O(n) - 存储所有点及其出现次数
```

**题目分析**：
利用哈希表记录每个点的坐标及其出现次数，在 `count` 操作时遍历所有可能形成正方形的对角线顶点，快速统计能够形成正方形的数量。

---

### 24. LeetCode 325: Maximum Size Subarray Sum Equals k（和为 k 的最大子数组长度）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，请找到数组中和为 `k` 的最长连续子数组，并返回其长度。

**代码实现**：
```python
def maxSubArrayLen(nums: List[int], k: int) -> int:
    # 使用哈希表来存储前缀和的索引
    prefix_sum_index = {0: -1}
    # 初始化前缀和与最大长度
    prefix_sum = 0
    max_length = 0
    # 遍历数组中的每个元素
    for i, num in enumerate(nums):
        # 更新当前前缀和
        prefix_sum += num
        # 检查当前前缀和减去目标值 k 是否存在于哈希表中
        if prefix_sum - k in prefix_sum_index:
            max_length = max(max_length, i - prefix_sum_index[prefix_sum - k])
        # 如果当前前缀和未出现在哈希表中，记录其索引
        if prefix_sum not in prefix_sum_index:
            prefix_sum_index[prefix_sum] = i
    return max_length

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(n) - 哈希表最多存储 n 个不同的前缀和
```

**题目分析**：
利用前缀和与哈希表来记录前缀和的索引，快速判断是否存在和为 `k` 的子数组，从而找到最长的符合条件的子数组。

---

### 25. LeetCode 1423: Maximum Points You Can Obtain from Cards（从卡片中获取的最大点数）

**题目描述**：
给定一个整数数组 `cardPoints` 和一个整数 `k`，每次操作你可以从卡片的开头或者结尾取一张卡片，直到取出 `k` 张卡片。请你返回可以获得的最大点数。

**代码实现**：
```python
def maxScore(cardPoints: List[int], k: int) -> int:
    # 计算卡片总点数
    total_points = sum(cardPoints)
    # 如果取出的卡片数等于卡片总数，返回总点数
    if len(cardPoints) == k:
        return total_points
    
    # 计算滑动窗口的初始和（取 n - k 个卡片的最小和）
    window_size = len(cardPoints) - k
    min_window_sum = sum(cardPoints[:window_size])
    current_window_sum = min_window_sum
    # 移动滑动窗口，寻找最小和
    for i in range(window_size, len(cardPoints)):
        current_window_sum += cardPoints[i] - cardPoints[i - window_size]
        min_window_sum = min(min_window_sum, current_window_sum)
    
    # 最大点数 = 总点数 - 最小窗口和
    return total_points - min_window_sum

# 时间复杂度：O(n) - 计算总点数和滑动窗口
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
利用滑动窗口

的方式计算剩余卡片的最小和，再用卡片总和减去该最小和，即为取出 `k` 张卡片能够得到的最大点数。

---

好的，我们继续讲解接下来的5道LeetCode前缀和相关题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 26. LeetCode 724: Find Pivot Index（寻找数组的中心索引）

**题目描述**：
给定一个整数数组 `nums`，请找出数组中一个 **中心索引** `pivot`，使得 `pivot` 左侧的所有元素之和等于 `pivot` 右侧的所有元素之和。如果不存在，则返回 `-1`。如果有多个中心索引，则返回最左边的那个。

**代码实现**：
```python
def pivotIndex(nums: List[int]) -> int:
    # 计算数组的总和
    total_sum = sum(nums)
    # 初始化左侧和为 0
    left_sum = 0
    # 遍历数组中的每个元素
    for i, num in enumerate(nums):
        # 检查当前索引是否为中心索引
        if left_sum == total_sum - left_sum - num:
            return i
        # 更新左侧和
        left_sum += num
    # 如果未找到中心索引，返回 -1
    return -1

# 时间复杂度：O(n) - 遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
利用前缀和的思想，判断当前索引的左侧和是否等于右侧和。通过遍历数组并逐步更新左侧和，可以在 O(n) 时间内找到中心索引。

---

### 27. LeetCode 1480: Running Sum of 1d Array（一维数组的动态和）

**题目描述**：
给定一个整数数组 `nums`，请返回一个新数组 `runningSum`，其中 `runningSum[i]` 是 `nums` 中前 `i` 个元素的和（即 `runningSum[i] = nums[0] + nums[1] + ... + nums[i]`）。

**代码实现**：
```python
def runningSum(nums: List[int]) -> List[int]:
    # 初始化第一个元素的动态和
    for i in range(1, len(nums)):
        # 当前元素的动态和为之前所有元素之和
        nums[i] += nums[i - 1]
    return nums

# 时间复杂度：O(n) - 遍历数组一次，更新每个元素的动态和
# 空间复杂度：O(1) - 原地更新数组，不使用额外空间
```

**题目分析**：
通过遍历数组，逐步更新每个元素的动态和，原地修改数组，从而实现 O(n) 的时间复杂度和 O(1) 的空间复杂度。

---

### 28. LeetCode 1574: Shortest Subarray to be Removed to Make Array Sorted（使数组有序的最短子数组）

**题目描述**：
给定一个整数数组 `arr`，返回一个子数组的最短长度，使得删除该子数组后，剩余数组有序（非递减）。如果数组本身已经是非递减的，则返回 0。

**代码实现**：
```python
def findLengthOfShortestSubarray(arr: List[int]) -> int:
    n = len(arr)
    # 找到从左到右的最长递增子数组
    left = 0
    while left + 1 < n and arr[left] <= arr[left + 1]:
        left += 1
    # 如果整个数组已经有序
    if left == n - 1:
        return 0

    # 找到从右到左的最长递增子数组
    right = n - 1
    while right > 0 and arr[right - 1] <= arr[right]:
        right -= 1

    # 最短删除长度初始化为删除左侧或右侧所有元素
    result = min(n - left - 1, right)

    # 尝试删除中间元素，保留前缀和后缀
    i, j = 0, right
    while i <= left and j < n:
        if arr[i] <= arr[j]:
            result = min(result, j - i - 1)
            i += 1
        else:
            j += 1

    return result

# 时间复杂度：O(n) - 遍历数组确定前后递增子数组并计算删除长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
通过找到数组的左侧最长递增子数组和右侧最长递增子数组，确定需要删除的中间部分的最小长度，再逐步判断前缀和后缀的组合，找到删除的最短子数组。

---

### 29. LeetCode 198: House Robber（打家劫舍）

**题目描述**：
你是一个专业的小偷，计划偷窃沿街的房屋。每间房屋都藏有一定的现金，并且相邻的两间房屋不能同时被偷。给定一个代表每个房屋存放金额的非负整数数组 `nums`，计算你在不触动警报的情况下能够偷窃到的最高金额。

**代码实现**：
```python
def rob(nums: List[int]) -> int:
    # 初始化两个变量用于记录当前房屋和前一间房屋的最大金额
    prev_max, curr_max = 0, 0
    # 遍历每个房屋的金额
    for num in nums:
        # 更新当前房屋的最大金额
        temp = curr_max
        curr_max = max(prev_max + num, curr_max)
        prev_max = temp
    return curr_max

# 时间复杂度：O(n) - 遍历每个房屋一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
使用动态规划的思想，记录当前房屋的最大金额和前一个房屋的最大金额，避免相邻房屋被同时偷窃。最终结果为所有房屋的最大偷窃金额。

---

### 30. LeetCode 1310: XOR Queries of a Subarray（子数组的异或查询）

**题目描述**：
给定一个整数数组 `arr`，以及多个查询 `queries`，每个查询包含两个整数 `left` 和 `right`，返回从 `left` 到 `right` 的子数组元素的异或结果。

**代码实现**：
```python
def xorQueries(arr: List[int], queries: List[List[int]]) -> List[int]:
    # 计算前缀异或数组
    prefix_xor = [0] * (len(arr) + 1)
    for i in range(len(arr)):
        prefix_xor[i + 1] = prefix_xor[i] ^ arr[i]
    # 处理每个查询
    result = []
    for left, right in queries:
        # 计算从 left 到 right 的异或结果
        result.append(prefix_xor[right + 1] ^ prefix_xor[left])
    return result

# 时间复杂度：O(n + m) - 构建前缀异或数组及处理 m 个查询
# 空间复杂度：O(n) - 存储前缀异或数组
```

**题目分析**：
使用前缀异或数组来快速计算任意子数组的异或结果，通过前缀异或数组的性质，可以在 O(1) 的时间内计算任意子数组的异或和。
