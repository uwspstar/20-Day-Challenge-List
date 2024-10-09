# 前 k 个最大元素 (Top K Largest Elements)

## Definition
给定一个整数数组 `nums` 和一个整数 `k`，找出数组中前 `k` 个最大的元素。此问题可以使用滑动窗口技术和堆数据结构来高效地解决。

## Key Concepts
- **堆 (Heap)**: 一种特殊的树状数据结构，可以高效地找到最小值或最大值。在这个问题中，使用最小堆来维护当前找到的前 `k` 个最大元素。
- **滑动窗口 (Sliding Window)**: 在处理数组时，通过移动窗口的右边界来扩展元素，同时确保左边界在需要时更新。

## 适用场景
- 查找动态变化的数据中的前 `k` 个最大元素。
- 处理实时数据流，获取前 `k` 大值的情况。

## Python 前 k 个最大元素模板
```python
import heapq

def top_k_largest_elements(nums, k):
    if k == 0:  # 如果 k 为 0，直接返回空列表
        return []
    
    min_heap = []  # 初始化最小堆
    
    for num in nums:
        heapq.heappush(min_heap, num)  # 添加当前元素到堆
        if len(min_heap) > k:  # 当堆的大小超过 k，移除最小元素
            heapq.heappop(min_heap)
    
    return sorted(min_heap, reverse=True)  # 返回堆中的元素，按降序排序
```

## Tips
- 使用 `heapq` 模块实现最小堆，可以有效维护前 `k` 个最大元素。
- 在返回结果之前，对堆中的元素进行排序，以确保返回的结果是前 `k` 个最大元素。

## Warning
- 如果 `k` 大于数组的长度，确保处理这种边界情况，以避免错误。

## Complexity Analysis
- **时间复杂度**: O(n log k)，其中 `n` 是数组的长度，因为每个插入和删除操作的时间复杂度为 O(log k)。
- **空间复杂度**: O(k)，用于存储前 `k` 个最大元素的堆。


------

### 1. LeetCode 215: Kth Largest Element in an Array（数组中的第 K 个最大元素）
-  https://leetcode.com/problems/kth-largest-element-in-an-array/description/

**题目描述**：
给定一个未排序的整数数组 `nums`，返回其中第 `k` 个最大的元素。注意，你需要找的是数组排序后的第 `k` 个最大元素，而不是第 `k` 个不同的元素。

**解题思路**：
1. 使用堆（Heap）来解决此问题，可以维护一个大小为 `k` 的最小堆（Min Heap），从而在遍历数组的过程中高效地找到第 `k` 个最大元素。
2. 也可以使用快速选择（Quick Select）算法来优化时间复杂度，将 `k` 转换为从数组开始计算的索引，使用类似快速排序的分区方法找到第 `k` 个最大元素。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找数组中第 k 个最大元素的函数
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # 使用堆来维护数组中第 k 个最大元素
        return heapq.nlargest(k, nums)[-1]

# 时间复杂度：O(n * log k) - 遍历数组并维护堆的时间复杂度。
# 空间复杂度：O(k) - 堆的空间复杂度为 k。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log k)，遍历数组并维护堆的时间复杂度。
- **空间复杂度**：O(k)，堆的空间复杂度为 k。

**代码实现（快速选择法）**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找数组中第 k 个最大元素的函数
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # 将 k 转换为从数组开始的索引
        k = len(nums) - k

        # 定义快速选择的辅助函数
        def quickSelect(left, right):
            pivot = nums[right]
            p = left
            for i in range(left, right):
                if nums[i] <= pivot:
                    nums[p], nums[i] = nums[i], nums[p]
                    p += 1
            nums[p], nums[right] = nums[right], nums[p]
            if p > k:
                return quickSelect(left, p - 1)
            elif p < k:
                return quickSelect(p + 1, right)
            else:
                return nums[p]

        # 调用快速选择函数
        return quickSelect(0, len(nums) - 1)

# 时间复杂度：O(n) - 平均情况下的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，平均情况下的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 2. LeetCode 347: Top K Frequent Elements（前 K 个高频元素）

**题目描述**：
给定一个非空的整数数组，返回其中出现频率前 `k` 高的元素。

**解题思路**：
1. 使用哈希表（HashMap）统计每个元素的频率，并将其放入一个大小为 `k` 的最小堆中。
2. 维护一个大小为 `k` 的最小堆，遍历哈希表的键值对，并将元素及其频率加入堆中。堆的大小超过 `k` 时，弹出堆顶元素，最终堆中留下的即为出现频率前 `k` 高的元素。

**代码实现**：
```python
# 导入 heapq 和 collections 模块
import heapq
from collections import Counter

# 定义解决方案的类
class Solution:
    # 定义查找前 K 个高频元素的函数
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 使用 Counter 统计每个元素的频率
        count = Counter(nums)
        # 使用堆来获取频率最高的 k 个元素
        return heapq.nlargest(k, count.keys(), key=count.get)

# 时间复杂度：O(n * log k) - 遍历哈希表并维护堆的时间复杂度。
# 空间复杂度：O(n) - 存储每个元素的频率。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log k)，遍历哈希表并维护堆的时间复杂度。
- **空间复杂度**：O(n)，存储每个元素的频率。

**代码实现（桶排序法）**：
```python
# 导入 collections 模块
from collections import Counter

# 定义解决方案的类
class Solution:
    # 定义查找前 K 个高频元素的函数
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 使用 Counter 统计每个元素的频率
        count = Counter(nums)
        # 初始化桶列表，长度为 nums 的长度 + 1
        bucket = [[] for _ in range(len(nums) + 1)]
        
        # 将每个元素按照频率放入对应的桶中
        for num, freq in count.items():
            bucket[freq].append(num)
        
        # 依次从频率最高的桶中取出元素，直到取出 k 个元素
        result = []
        for i in range(len(bucket) - 1, 0, -1):
            for num in bucket[i]:
                result.append(num)
                if len(result) == k:
                    return result

# 时间复杂度：O(n) - 遍历数组并放入桶中的时间复杂度。
# 空间复杂度：O(n) - 存储桶的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历数组并放入桶中的时间复杂度。
- **空间复杂度**：O(n)，存储桶的空间复杂度。

---

### 3. LeetCode 973: K Closest Points to Origin（距离原点最近的 K 个点）

**题目描述**：
给定一个数组 `points`，其中 `points[i] = [xi, yi]` 表示一个点的坐标。求距离原点（0, 0）最近的 `k` 个点。返回这 `k` 个点的坐标。

**解题思路**：
1. 使用堆（Heap）来维护前 `k` 个距离原点最近的点。在遍历 `points` 的过程中，计算每个点的欧几里得距离，并将点和其距离加入最大堆中（使用负值）。
2. 当堆的大小超过 `k` 时，移除堆顶元素，最终堆中留下的即为前 `k` 个距离原点最近的点。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找距离原点最近的 K 个点的函数
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        # 使用最大堆维护前 k 个距离原点最近的点
        heap = []

        # 遍历所有点
        for x, y in points:
            dist = -(x ** 2 + y ** 2)  # 使用负值存储距离
            heapq.heappush(heap, (dist, x, y))  # 将距离和坐标加入堆中
            if len(heap) > k:
                heapq.heappop(heap)  # 当堆大小超过 k 时，移除堆顶元素

        # 返回堆中的 k 个点
        return [[x, y] for (dist, x, y) in heap]

# 时间复杂度：O(n * log k) - 遍历所有点并维护堆的时间复杂度。
# 空间复杂度：O(k) - 堆的空间复杂度为 k。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log k)，遍历所有点并维护堆的时间复杂度。
- **空间复杂度**：O(k)，堆的空间复杂度为 k。

---

### 4. LeetCode 378: Kth Smallest Element in a Sorted Matrix（

有序矩阵中第 K 小的元素）

**题目描述**：
给定一个 `n x n` 的矩阵，其中每行和每列的元素都是按升序排序的，找到矩阵中第 `k` 小的元素。

**解题思路**：
1. 使用堆来解决。将矩阵中每一行的第一个元素加入最小堆中，并维护堆的大小。
2. 依次从堆中弹出最小值，并将该值所在行的下一个元素加入堆中，直到弹出第 `k` 个元素为止。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找有序矩阵中第 K 小元素的函数
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        # 使用最小堆维护前 k 个最小元素
        heap = []

        # 将矩阵中每一行的第一个元素加入最小堆
        for r in range(min(len(matrix), k)):
            heapq.heappush(heap, (matrix[r][0], r, 0))

        # 弹出第 k 小的元素
        while k > 0:
            val, r, c = heapq.heappop(heap)
            if c + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[r][c + 1], r, c + 1))
            k -= 1

        return val

# 时间复杂度：O(k * log n) - 弹出第 k 小的元素的时间复杂度。
# 空间复杂度：O(n) - 堆的空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(k * log n)，弹出第 k 小的元素的时间复杂度。
- **空间复杂度**：O(n)，堆的空间复杂度为 n。

---

好的，我们继续讲解接下来的几道与 “前 k 个最大元素” 相关的 LeetCode 题目。以下是每一道题目的详细解析、解题思路、逐行代码注释、以及时间复杂度和空间复杂度分析。

---

### 5. LeetCode 451: Sort Characters By Frequency（按字符出现频率排序）

**题目描述**：
给定一个字符串 `s`，根据字符出现的频率降序排序。如果两个字符出现的频率相同，则按字符自身顺序返回。

**解题思路**：
1. 使用哈希表 `Counter` 统计每个字符的频率。
2. 使用 `heapq` 堆将频率进行排序，或者将频率和字符放入一个数组中，根据频率降序排列，再生成新的字符串。

**代码实现**：
```python
# 导入 collections 模块
from collections import Counter

# 定义解决方案的类
class Solution:
    # 定义按字符出现频率排序的函数
    def frequencySort(self, s: str) -> str:
        # 使用 Counter 统计每个字符的频率
        count = Counter(s)
        # 将字符和频率排序（按频率降序排列）
        sorted_chars = sorted(count.items(), key=lambda item: -item[1])
        # 按频率生成排序后的字符串
        result = "".join([char * freq for char, freq in sorted_chars])
        return result

# 时间复杂度：O(n * log n) - 对字符和频率进行排序的时间复杂度。
# 空间复杂度：O(n) - 存储字符和频率的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，对字符和频率进行排序的时间复杂度。
- **空间复杂度**：O(n)，存储字符和频率的空间复杂度。

---

### 6. LeetCode 658: Find K Closest Elements（找到 K 个最接近的元素）

**题目描述**：
给定一个排序好的数组 `arr` 和两个整数 `k` 和 `x`，返回数组中最接近 `x` 的 `k` 个数，返回结果也需要按升序排序。

**解题思路**：
1. 使用二分查找找到与 `x` 最接近的元素索引，然后使用滑动窗口找到最接近的 `k` 个元素。
2. 或者使用堆，将每个元素与 `x` 的距离存入堆中，维护堆的大小为 `k`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最接近的 K 个元素的函数
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        # 使用二分查找找到最接近 x 的元素的起始位置
        left, right = 0, len(arr) - k

        while left < right:
            mid = (left + right) // 2
            # 比较 mid 和 mid + k 元素与 x 的距离
            if x - arr[mid] > arr[mid + k] - x:
                left = mid + 1
            else:
                right = mid

        # 返回长度为 k 的最接近元素子数组
        return arr[left:left + k]

# 时间复杂度：O(log(n - k) + k) - 二分查找的时间复杂度和返回子数组的时间复杂度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log(n - k) + k)，二分查找的时间复杂度和返回子数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 7. LeetCode 692: Top K Frequent Words（前 K 个高频单词）

**题目描述**：
给定一个字符串数组 `words` 和一个整数 `k`，返回其中出现频率最高的 `k` 个单词。返回的答案应该按频率降序排序，如果两个单词的频率相同，则按字典序升序排序。

**解题思路**：
1. 使用哈希表 `Counter` 统计每个单词的频率。
2. 使用堆（Heap）来维护频率最高的 `k` 个单词，按频率降序排序，字母升序排序。

**代码实现**：
```python
# 导入 heapq 和 collections 模块
import heapq
from collections import Counter

# 定义解决方案的类
class Solution:
    # 定义查找前 K 个高频单词的函数
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        # 使用 Counter 统计每个单词的频率
        count = Counter(words)
        # 使用堆来获取频率最高的 k 个单词
        return heapq.nlargest(k, count.keys(), key=lambda word: (-count[word], word))

# 时间复杂度：O(n * log k) - 遍历哈希表并维护堆的时间复杂度。
# 空间复杂度：O(n) - 存储每个单词的频率。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log k)，遍历哈希表并维护堆的时间复杂度。
- **空间复杂度**：O(n)，存储每个单词的频率。

---

### 8. LeetCode 973: K Closest Points to Origin（距离原点最近的 K 个点）

**题目描述**：
给定一个数组 `points`，其中 `points[i] = [xi, yi]` 表示一个点的坐标。求距离原点（0, 0）最近的 `k` 个点。返回这 `k` 个点的坐标。

**解题思路**：
1. 使用堆（Heap）来维护前 `k` 个距离原点最近的点。在遍历 `points` 的过程中，计算每个点的欧几里得距离，并将点和其距离加入最大堆中（使用负值）。
2. 当堆的大小超过 `k` 时，移除堆顶元素，最终堆中留下的即为前 `k` 个距离原点最近的点。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找距离原点最近的 K 个点的函数
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        # 使用最大堆维护前 k 个距离原点最近的点
        heap = []

        # 遍历所有点
        for x, y in points:
            dist = -(x ** 2 + y ** 2)  # 使用负值存储距离
            heapq.heappush(heap, (dist, x, y))  # 将距离和坐标加入堆中
            if len(heap) > k:
                heapq.heappop(heap)  # 当堆大小超过 k 时，移除堆顶元素

        # 返回堆中的 k 个点
        return [[x, y] for (dist, x, y) in heap]

# 时间复杂度：O(n * log k) - 遍历所有点并维护堆的时间复杂度。
# 空间复杂度：O(k) - 堆的空间复杂度为 k。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log k)，遍历所有点并维护堆的时间复杂度。
- **空间复杂度**：O(k)，堆的空间复杂度为 k。

---

### 9. LeetCode 378: Kth Smallest Element in a Sorted Matrix（有序矩阵中第 K 小的元素）

**题目描述**：
给定一个 `n x n` 的矩阵，其中每行和每列的元素都是按升序排序的，找到矩阵中第 `k` 小的元素。

**解题思路**：
1. 使用堆来解决。将矩阵中每一行的第一个元素加入最小堆中，并维护堆的大小。
2. 依次从堆中弹出最小值，并将该值所在行的下一个元素加入堆中，直到弹出第 `k` 个元素为止。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找有序矩阵中第 K 小元素的函数
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        # 使用最小堆维护前 k 个最小元素
        heap = []

        # 将矩阵中每一行的第一个元素加入最小堆
        for r in range(min

(len(matrix), k)):
            heapq.heappush(heap, (matrix[r][0], r, 0))

        # 弹出第 k 小的元素
        while k > 0:
            val, r, c = heapq.heappop(heap)
            if c + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[r][c + 1], r, c + 1))
            k -= 1

        return val

# 时间复杂度：O(k * log n) - 弹出第 k 小的元素的时间复杂度。
# 空间复杂度：O(n) - 堆的空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(k * log n)，弹出第 k 小的元素的时间复杂度。
- **空间复杂度**：O(n)，堆的空间复杂度为 n。

---

好的，我们继续讲解剩余与 “前 k 个最大元素” 相关的 LeetCode 题目。以下是每一道题目的详细解析、解题思路、逐行代码注释、以及时间复杂度和空间复杂度分析。

---

### 10. LeetCode 373: Find K Pairs with Smallest Sums（查找和最小的 K 对数字）

**题目描述**：
给定两个升序排列的整数数组 `nums1` 和 `nums2`，以及一个整数 `k`。定义一对数 `(u, v)`，其中一个数 `u` 来自 `nums1`，一个数 `v` 来自 `nums2`。找到和最小的 `k` 个数对。

**解题思路**：
1. 使用最小堆（Min Heap）来维护前 `k` 个和最小的数对。每次将 `nums1` 的第一个元素与 `nums2` 的前 `k` 个元素组成数对并加入堆中。
2. 弹出堆顶元素（和最小的数对），并将弹出元素中 `nums1` 对应的下一个元素与 `nums2` 中当前的元素组成新的数对加入堆中，直到找到 `k` 个数对。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找和最小的 K 对数字的函数
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        # 如果两个数组为空，直接返回空列表
        if not nums1 or not nums2:
            return []

        # 初始化最小堆
        heap = []
        # 将 nums1 中第一个元素与 nums2 的前 k 个元素组成的数对加入堆中
        for i in range(min(k, len(nums1))):
            heapq.heappush(heap, (nums1[i] + nums2[0], i, 0))

        # 初始化结果列表
        result = []

        # 弹出前 k 个和最小的数对
        while heap and len(result) < k:
            # 弹出堆顶元素
            _, i, j = heapq.heappop(heap)
            result.append([nums1[i], nums2[j]])
            # 如果 j + 1 仍在 nums2 范围内，则将 (i, j+1) 数对加入堆中
            if j + 1 < len(nums2):
                heapq.heappush(heap, (nums1[i] + nums2[j + 1], i, j + 1))

        return result

# 时间复杂度：O(k * log k) - 每次从堆中弹出元素并加入新数对的时间复杂度。
# 空间复杂度：O(k) - 堆的最大空间复杂度为 k。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(k * log k)，每次从堆中弹出元素并加入新数对的时间复杂度。
- **空间复杂度**：O(k)，堆的最大空间复杂度为 k。

---

### 11. LeetCode 295: Find Median from Data Stream（数据流中的中位数）

**题目描述**：
设计一个数据结构，支持数据流中数据的插入，并能够在常数时间内返回中位数。

**解题思路**：
1. 使用两个堆：一个最大堆 `max_heap` 用于存储较小的一半数据，一个最小堆 `min_heap` 用于存储较大的一半数据。
2. 确保 `max_heap` 中的所有元素都小于 `min_heap` 中的所有元素，并且 `max_heap` 中的元素个数等于或大于 `min_heap` 中的元素个数。这样，当数据总数为奇数时，中位数就是 `max_heap` 的堆顶；当数据总数为偶数时，中位数是两个堆顶元素的平均值。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义 MedianFinder 类
class MedianFinder:
    def __init__(self):
        # 初始化最小堆和最大堆
        self.min_heap = []  # 存储较大的一半数据
        self.max_heap = []  # 存储较小的一半数据（取负值存储）

    # 插入数据流中的新元素
    def addNum(self, num: int) -> None:
        # 将新元素加入最大堆
        heapq.heappush(self.max_heap, -num)
        # 确保最大堆中的最大值小于最小堆中的最小值
        heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap))

        # 如果最小堆的元素个数多于最大堆，则将最小堆的最小值移至最大堆
        if len(self.min_heap) > len(self.max_heap):
            heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap))

    # 获取数据流中的中位数
    def findMedian(self) -> float:
        # 如果两个堆的元素个数相等，中位数为两个堆顶元素的平均值
        if len(self.max_heap) == len(self.min_heap):
            return (-self.max_heap[0] + self.min_heap[0]) / 2
        # 否则，中位数为最大堆的堆顶元素
        else:
            return -self.max_heap[0]

# 时间复杂度：O(log n) - 每次插入新元素的时间复杂度，其中 n 是数据流中元素的个数。
# 空间复杂度：O(n) - 堆的最大空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log n)，每次插入新元素的时间复杂度。
- **空间复杂度**：O(n)，堆的最大空间复杂度为 n。

---

### 12. LeetCode 703: Kth Largest Element in a Stream（数据流中的第 K 大元素）

**题目描述**：
设计一个数据结构，可以在数据流中插入整数，并能够返回数据流中第 `k` 大的元素。

**解题思路**：
1. 使用最小堆（Min Heap）来维护前 `k` 大的元素。每次插入新元素时，如果堆的大小小于 `k`，则直接加入堆中；否则，如果新元素大于堆顶元素，则替换堆顶元素。
2. 堆的大小始终保持为 `k`，堆顶元素即为数据流中的第 `k` 大元素。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义 KthLargest 类
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.k = k
        self.min_heap = []
        # 将初始数组中的元素加入堆中，并保持堆的大小为 k
        for num in nums:
            self.add(num)

    # 插入数据流中的新元素
    def add(self, val: int) -> int:
        # 如果堆的大小小于 k，则直接加入堆中
        if len(self.min_heap) < self.k:
            heapq.heappush(self.min_heap, val)
        # 否则，如果新元素大于堆顶元素，则替换堆顶元素
        elif val > self.min_heap[0]:
            heapq.heapreplace(self.min_heap, val)

        # 返回第 k 大的元素（堆顶元素）
        return self.min_heap[0]

# 时间复杂度：O(log k) - 每次插入新元素的时间复杂度，其中 k 为堆的大小。
# 空间复杂度：O(k) - 堆的最大空间复杂度为 k。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log k)，每次插入新元素的时间复杂度。
- **空间复杂度**：O(k)，堆的最大空间复杂度为 k。

---

### 13. LeetCode 1499: Max Value of Equation（方程的最大值）

**题目描述**：
给定一个数组 `points`，其中 `points[i] = [xi, yi]` 表示一个点的坐标，要求找到满足 `|xi - xj| <= k` 的 `i` 和 `j`（其中 `i < j`）使得方程 `yi + yj + |xi - xj|` 的值最大化。

**解题思路**：
1. 使用优先队列或单调队列来维护一个 `yi - xi` 的值，并在遍历 `points` 的过程中找到最大值。
2. 在遍历 `points` 时，维护一个满足 `|xi - xj| <= k` 的最大值，并更新最终结果。

**代码实现**：
```python


# 导入 collections 模块
from collections import deque

# 定义解决方案的类
class Solution:
    # 定义查找方程最大值的函数
    def findMaxValueOfEquation(self, points: List[List[int]], k: int) -> int:
        # 初始化双端队列和最大值
        deque = collections.deque()
        max_value = float("-inf")

        # 遍历所有点
        for x, y in points:
            # 移除不满足 |xi - xj| <= k 的点
            while deque and x - deque[0][1] > k:
                deque.popleft()

            # 如果队列不为空，则更新最大值
            if deque:
                max_value = max(max_value, y + x + deque[0][0])

            # 维护队列的单调性（存储 y - x 的值）
            while deque and y - x >= deque[-1][0]:
                deque.pop()

            # 将当前点加入队列
            deque.append((y - x, x))

        return max_value

# 时间复杂度：O(n) - 遍历所有点的时间复杂度，其中 n 是点的个数。
# 空间复杂度：O(n) - 双端队列的最大空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历所有点的时间复杂度。
- **空间复杂度**：O(n)，双端队列的最大空间复杂度。

---

好的，我们继续讲解剩余的与 “前 k 个最大元素” 相关的 LeetCode 题目。以下是每一道题目的详细解析、解题思路、逐行代码注释、以及时间复杂度和空间复杂度分析。

---

### 14. LeetCode 1167: Minimum Cost to Connect Sticks（连接棒材的最低成本）

**题目描述**：
给定一个整数数组 `sticks`，其中 `sticks[i]` 表示第 `i` 根棒材的长度。你可以连接任意两根棒材，并将其长度相加作为新棒材的长度。每次连接的成本为新棒材的长度。返回将所有棒材连成一根所需的最低成本。

**解题思路**：
1. 使用最小堆（Min Heap）来解决。每次从堆中弹出最小的两根棒材，将它们相加，并将新棒材加入堆中。
2. 反复执行以上操作，直到堆中只剩下一根棒材时，所有连接操作的总成本即为所需的最低成本。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义计算连接棒材的最低成本的函数
    def connectSticks(self, sticks: List[int]) -> int:
        # 初始化最小堆
        heapq.heapify(sticks)
        total_cost = 0

        # 当堆中至少有两根棒材时
        while len(sticks) > 1:
            # 弹出最小的两根棒材
            first = heapq.heappop(sticks)
            second = heapq.heappop(sticks)
            # 计算新棒材的长度并加入堆中
            cost = first + second
            heapq.heappush(sticks, cost)
            # 更新总成本
            total_cost += cost

        return total_cost

# 时间复杂度：O(n * log n) - 每次连接操作需要弹出和加入堆中元素的时间复杂度。
# 空间复杂度：O(n) - 堆的最大空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，每次连接操作需要弹出和加入堆中元素的时间复杂度。
- **空间复杂度**：O(n)，堆的最大空间复杂度。

---

### 15. LeetCode 378: Kth Smallest Element in a Sorted Matrix（有序矩阵中第 K 小的元素）

**题目描述**：
给定一个 `n x n` 的矩阵，其中每行和每列的元素都是按升序排序的，找到矩阵中第 `k` 小的元素。

**解题思路**：
1. 使用最小堆（Min Heap）来维护前 `k` 个最小的元素。在遍历矩阵的过程中，将每一行的第一个元素加入最小堆中，并维护堆的大小。
2. 弹出堆顶元素，并将弹出元素所在行的下一个元素加入堆中，直到弹出第 `k` 个元素为止。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找有序矩阵中第 K 小元素的函数
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        # 初始化最小堆
        heap = []

        # 将矩阵中每一行的第一个元素加入最小堆
        for r in range(min(len(matrix), k)):
            heapq.heappush(heap, (matrix[r][0], r, 0))

        # 弹出第 k 小的元素
        while k > 0:
            val, r, c = heapq.heappop(heap)
            if c + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[r][c + 1], r, c + 1))
            k -= 1

        return val

# 时间复杂度：O(k * log n) - 弹出第 k 小的元素的时间复杂度。
# 空间复杂度：O(n) - 堆的空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(k * log n)，弹出第 k 小的元素的时间复杂度。
- **空间复杂度**：O(n)，堆的空间复杂度为 n。

---

### 16. LeetCode 1046: Last Stone Weight（最后一块石头的重量）

**题目描述**：
给定一组石头的重量，每次从中选出两块石头，并将较大的一块减去较小的一块，直到最后只剩下一块或没有石头。返回最后剩下的石头的重量。

**解题思路**：
1. 使用最大堆（通过取负值来模拟）。每次从堆中弹出两块石头，计算新的重量，并将其重新加入堆中。
2. 当堆中只剩下一块或没有石头时，返回剩余石头的重量。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义计算最后一块石头重量的函数
    def lastStoneWeight(self, stones: List[int]) -> int:
        # 将石头的重量取负值加入最大堆
        heap = [-stone for stone in stones]
        heapq.heapify(heap)

        # 当堆中至少有两块石头时
        while len(heap) > 1:
            # 弹出两块最大的石头
            first = -heapq.heappop(heap)
            second = -heapq.heappop(heap)
            # 如果两块石头的重量不同，将剩余的重量加入堆中
            if first != second:
                heapq.heappush(heap, -(first - second))

        # 返回剩余石头的重量（如果没有剩余石头，则返回 0）
        return -heap[0] if heap else 0

# 时间复杂度：O(n * log n) - 每次弹出和加入堆中元素的时间复杂度。
# 空间复杂度：O(n) - 堆的最大空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，每次弹出和加入堆中元素的时间复杂度。
- **空间复杂度**：O(n)，堆的最大空间复杂度。

---

### 17. LeetCode 767: Reorganize String（重构字符串）

**题目描述**：
给定一个字符串 `s`，重新排列其中的字符，使得相邻的字符不相同。如果可以实现，则返回重排后的字符串；如果无法实现，则返回空字符串。

**解题思路**：
1. 使用哈希表 `Counter` 统计每个字符的频率，并将频率较高的字符加入最大堆中。
2. 每次从堆中弹出两个字符，将它们放入结果字符串中，并更新剩余频率。当堆中没有剩余字符时，返回结果字符串。

**代码实现**：
```python
# 导入 collections 和 heapq 模块
import heapq
from collections import Counter

# 定义解决方案的类
class Solution:
    # 定义重构字符串的函数
    def reorganizeString(self, s: str) -> str:
        # 使用 Counter 统计每个字符的频率
        count = Counter(s)
        # 初始化最大堆（存储字符的负频率和字符）
        heap = [(-freq, char) for char, freq in count.items()]
        heapq.heapify(heap)

        # 初始化结果字符串和前一个字符
        prev_char, prev_freq = None, 0
        result = []

        # 弹出堆中的字符，重构字符串
        while heap:
            freq, char = heapq.heappop(heap)
            # 将当前字符加入结果字符串
            result.append(char)

            # 如果前一个字符还有剩余频率，则将其重新加入堆中
            if prev_freq < 0:
                heapq.heappush(heap, (prev_freq, prev_char))

            # 更新前一个字符和剩余频率
            prev_char, prev_freq = char, freq + 1

        # 如果结果字符串的长度等于原字符串的长度，则返回结果字符串
        return "".join(result) if len(result) == len(s) else ""

# 时间复杂度：O(n * log n) - 遍历字符并维护堆的时间复杂度。
# 空间复杂度：O(n) - 存储字符及其频率的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，遍历字符并维护堆的时间复杂度。
- **空间复杂度**：O(n)，存储字符及其频率的空间复杂度。



---

### 18. LeetCode 253: Meeting Rooms II（会议室 II）

**题目描述**：
给定一个会议时间安排的数组，每个会议时间都用一个长度为 2 的数组表示 `[start, end]`。返回会议室的最小数量。

**解题思路**：
1. 将所有会议按起始时间排序，然后使用最小堆来记录当前正在进行的会议结束时间。
2. 每次新会议开始时，将其加入堆中，如果堆顶元素的结束时间早于新会议的开始时间，则移除堆顶元素，表示该会议室空闲，可以复用。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义计算会议室最小数量的函数
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        # 如果没有会议，则返回 0
        if not intervals:
            return 0

        # 按会议的开始时间排序
        intervals.sort(key=lambda x: x[0])
        # 初始化最小堆
        heap = []
        heapq.heappush(heap, intervals[0][1])  # 将第一个会议的结束时间加入堆中

        # 遍历所有会议
        for i in range(1, len(intervals)):
            # 如果当前会议的开始时间大于等于堆顶会议的结束时间，则移除堆顶元素
            if intervals[i][0] >= heap[0]:
                heapq.heappop(heap)
            # 将当前会议的结束时间加入堆中
            heapq.heappush(heap, intervals[i][1])

        # 堆的大小即为需要的会议室数量
        return len(heap)

# 时间复杂度：O(n * log n) - 按会议的开始时间排序的时间复杂度。
# 空间复杂度：O(n) - 堆的最大空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，按会议的开始时间排序的时间复杂度。
- **空间复杂度**：O(n)，堆的最大空间复杂度。

---

好的，我们继续讲解剩余与“前 k 个最大元素”相关的 LeetCode 题目。以下是每一道题目的详细解析、解题思路、逐行代码注释、以及时间复杂度和空间复杂度分析。

---

### 19. LeetCode 378: Kth Smallest Element in a Sorted Matrix（有序矩阵中第 K 小的元素）

**题目描述**：
给定一个 `n x n` 的矩阵，其中每行和每列的元素都是按升序排序的，找到矩阵中第 `k` 小的元素。

**解题思路**：
1. 使用最小堆（Min Heap）来维护前 `k` 个最小的元素。在遍历矩阵的过程中，将每一行的第一个元素加入最小堆中，并维护堆的大小。
2. 弹出堆顶元素，并将弹出元素所在行的下一个元素加入堆中，直到弹出第 `k` 个元素为止。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找有序矩阵中第 K 小元素的函数
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        # 初始化最小堆
        heap = []

        # 将矩阵中每一行的第一个元素加入最小堆
        for r in range(min(len(matrix), k)):
            heapq.heappush(heap, (matrix[r][0], r, 0))

        # 弹出第 k 小的元素
        while k > 0:
            val, r, c = heapq.heappop(heap)
            if c + 1 < len(matrix[0]):
                heapq.heappush(heap, (matrix[r][c + 1], r, c + 1))
            k -= 1

        return val

# 时间复杂度：O(k * log n) - 弹出第 k 小的元素的时间复杂度。
# 空间复杂度：O(n) - 堆的空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(k * log n)，弹出第 k 小的元素的时间复杂度。
- **空间复杂度**：O(n)，堆的空间复杂度为 n。

---

### 20. LeetCode 295: Find Median from Data Stream（数据流中的中位数）

**题目描述**：
设计一个数据结构，支持数据流中数据的插入，并能够在常数时间内返回中位数。

**解题思路**：
1. 使用两个堆：一个最大堆 `max_heap` 用于存储较小的一半数据，一个最小堆 `min_heap` 用于存储较大的一半数据。
2. 确保 `max_heap` 中的所有元素都小于 `min_heap` 中的所有元素，并且 `max_heap` 中的元素个数等于或大于 `min_heap` 中的元素个数。这样，当数据总数为奇数时，中位数就是 `max_heap` 的堆顶；当数据总数为偶数时，中位数是两个堆顶元素的平均值。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义 MedianFinder 类
class MedianFinder:
    def __init__(self):
        # 初始化最小堆和最大堆
        self.min_heap = []  # 存储较大的一半数据
        self.max_heap = []  # 存储较小的一半数据（取负值存储）

    # 插入数据流中的新元素
    def addNum(self, num: int) -> None:
        # 将新元素加入最大堆
        heapq.heappush(self.max_heap, -num)
        # 确保最大堆中的最大值小于最小堆中的最小值
        heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap))

        # 如果最小堆的元素个数多于最大堆，则将最小堆的最小值移至最大堆
        if len(self.min_heap) > len(self.max_heap):
            heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap))

    # 获取数据流中的中位数
    def findMedian(self) -> float:
        # 如果两个堆的元素个数相等，中位数为两个堆顶元素的平均值
        if len(self.max_heap) == len(self.min_heap):
            return (-self.max_heap[0] + self.min_heap[0]) / 2
        # 否则，中位数为最大堆的堆顶元素
        else:
            return -self.max_heap[0]

# 时间复杂度：O(log n) - 每次插入新元素的时间复杂度，其中 n 是数据流中元素的个数。
# 空间复杂度：O(n) - 堆的最大空间复杂度为 n。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log n)，每次插入新元素的时间复杂度。
- **空间复杂度**：O(n)，堆的最大空间复杂度为 n。

---

### 21. LeetCode 218: The Skyline Problem（天际线问题）

**题目描述**：
给定一个建筑物列表 `buildings`，每个建筑物是一个三元组 `[left, right, height]`，表示从 `left` 到 `right` 的建筑物高度为 `height`。绘制所有建筑物的天际线，并返回天际线的关键点。

**解题思路**：
1. 将每个建筑物的左右边界及其高度记录为关键点（负高度表示建筑物左边界，正高度表示建筑物右边界）。
2. 将所有关键点按 `x` 坐标排序，然后使用最大堆（Heap）来维护当前建筑物的最高高度。
3. 在遍历关键点的过程中，更新最大堆，并记录每个高度变化点作为天际线的关键点。

**代码实现**：
```python
# 导入 heapq 模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义解决天际线问题的函数
    def getSkyline(self, buildings: List[List[int]]) -> List[List[int]]:
        # 将所有建筑物的左右边界及其高度记录为关键点
        events = []
        for left, right, height in buildings:
            events.append((left, -height, right))  # 记录建筑物的左边界
            events.append((right, 0, None))  # 记录建筑物的右边界（高度为 0）

        # 将所有关键点按 x 坐标进行排序
        events.sort()

        # 初始化结果列表和最大堆
        result = [[0, 0]]
        heap = [(0, float("inf"))]  # 最大堆（存储高度和右边界）

        # 遍历所有关键点
        for x, negH, right in events:
            # 将所有右边界小于等于当前 x 坐标的建筑物从堆中移除
            while heap[0][1] <= x:
                heapq.heappop(heap)

            # 如果当前是建筑物的左边界，则将其加入堆中
            if negH:
                heapq.heappush(heap, (negH, right))

            # 如果当前高度发生变化，则将其记录为天际线的关键点
            max_height = -heap[0][0]
            if result[-1][1] != max_height:
                result.append([x, max_height])

        # 返回天际线的关键点（去除初始点 [0, 0]）
        return result[1:]

# 时间复杂度：O(n * log n) - 对所有关键点进行排序和维护堆的时间复杂度。
# 空间复杂度：O(n) - 存储所有关键点的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * log n)，对所有关键点进行排序和维护堆的时间复杂度。
- **空间复杂度**：O(n)，存储所有关键点的空间复杂度。

---

### 22. LeetCode 239: Sliding Window Maximum（滑动窗口最大值）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，在 `nums` 中找出长度为 `k` 的所有子数组的最大值，返回这些最大值组成的列表。

**解题思路**：
1. 使用双端队列（Deque）来维护当前滑动窗口的最大值。每次滑动窗口向右移动时，移除队列中超出窗口的元素，并将当前元素加入队列中。
2. 队列的第一个元素始终是当前窗口中的最大值，每次窗口右移时将其记录在结果列表中。

**代码实现**：
```python
# 导入 collections 模块
from collections

 import deque

# 定义解决方案的类
class Solution:
    # 定义查找滑动窗口最大值的函数
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # 初始化结果列表和双端队列
        result = []
        deq = deque()  # 存储当前滑动窗口中元素的索引

        # 遍历整个数组
        for i in range(len(nums)):
            # 如果队列的首个元素超出当前窗口，移除它
            if deq and deq[0] < i - k + 1:
                deq.popleft()

            # 移除队列中所有比当前元素小的元素（这些元素不可能成为最大值）
            while deq and nums[deq[-1]] < nums[i]:
                deq.pop()

            # 将当前元素的索引加入队列
            deq.append(i)

            # 当窗口大小达到 k 时，记录当前窗口的最大值
            if i >= k - 1:
                result.append(nums[deq[0]])

        return result

# 时间复杂度：O(n) - 每个元素最多被加入和移除队列一次。
# 空间复杂度：O(k) - 存储滑动窗口中最多 k 个元素的索引。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，每个元素最多被加入和移除队列一次。
- **空间复杂度**：O(k)，存储滑动窗口中最多 k 个元素的索引。
