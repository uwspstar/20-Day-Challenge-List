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
