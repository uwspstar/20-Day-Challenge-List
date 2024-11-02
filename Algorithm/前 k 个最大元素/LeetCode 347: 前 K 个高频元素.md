### LeetCode 347: 前 K 个高频元素 (Top K Frequent Elements)

**题目描述**：  
给定一个整数数组 `nums` 和一个整数 `k`，返回出现次数最多的 `k` 个元素。可以按任意顺序返回结果。

[LeetCode 347: Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

**解题思路**：
使用 **哈希表和最小堆** 来高效地找到频率最高的 `k` 个元素：
1. 统计每个元素的频率，存储在字典中。
2. 利用 Python 的 `heapq` 库构建一个大小为 `k` 的最小堆。堆中仅保留频率最高的 `k` 个元素。
3. 最小堆会根据频率自动排序，每当堆的大小超过 `k` 时，移除频率较低的元素，确保堆中始终是当前频率最高的 `k` 个元素。
4. 最后，从堆中提取元素，得到结果。

### 代码实现

```python
from typing import List
import heapq
from collections import Counter

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 统计每个元素的频率
        count = Counter(nums)

        # 使用最小堆保留频率最高的 k 个元素
        # 堆中存储 (频率, 元素) 的元组，便于按频率排序
        min_heap = []
        
        # 遍历频率字典，维护一个大小为 k 的最小堆
        for num, freq in count.items():
            heapq.heappush(min_heap, (freq, num))
            if len(min_heap) > k:
                heapq.heappop(min_heap)
        
        # 提取堆中的元素，返回结果
        return [num for freq, num in min_heap]
```

### 复杂度分析

- **时间复杂度**：O(n log k)，其中 n 是数组 `nums` 的长度，k 是需要保留的元素个数。
  - 统计频率的时间复杂度为 O(n)。
  - 遍历频率表时，每次 `heappush` 和 `heappop` 操作的时间复杂度为 O(log k)，总共需要进行 n 次。
- **空间复杂度**：O(n)，需要额外的空间来存储频率计数和堆。

### 示例讲解

假设输入 `nums = [1, 1, 1, 2, 2, 3]` 和 `k = 2`。步骤如下：

1. **统计频率**：
   - `count = {1: 3, 2: 2, 3: 1}`，表示数字 `1` 出现了 3 次，数字 `2` 出现了 2 次，数字 `3` 出现了 1 次。

2. **构建大小为 k 的最小堆**：
   - 先将 `(3, 1)` 入堆，堆中状态：`[(3, 1)]`
   - 再将 `(2, 2)` 入堆，堆中状态：`[(2, 2), (3, 1)]`
   - 再将 `(1, 3)` 入堆，堆中状态：`[(1, 3), (3, 1), (2, 2)]`
   - 此时堆的大小超过 `k = 2`，弹出频率最小的元素 `(1, 3)`，堆中状态：`[(2, 2), (3, 1)]`

3. **提取堆中元素**：
   - 堆中仅剩频率最高的两个元素：`[(2, 2), (3, 1)]`
   - 返回结果 `[2, 1]`。

### 总结

- 使用堆能够高效地处理需要找出前 `k` 个高频元素的问题。
- 堆方法适合需要按顺序维护 `k` 个最大或最小元素的场景。
