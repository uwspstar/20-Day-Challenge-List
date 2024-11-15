### LeetCode 23: 合并K个升序链表 (Merge k Sorted Lists)  
[LeetCode 题目链接](https://leetcode.com/problems/merge-k-sorted-lists/)

#### **题目描述**：
给你一个 `k` 个链表的数组，每个链表都已经按升序排序。请你将所有链表合并到一个升序链表中，返回合并后的链表。

---

#### 示例输入输出：

**输入**：
```plaintext
lists = [
    [1, 4, 5],
    [1, 3, 4],
    [2, 6]
]
```

**输出**：
```plaintext
[1, 1, 2, 3, 4, 4, 5, 6]
```

---

### **Python 实现代码**：

```python
import heapq
from typing import List

def merge_k_sorted_lists(lists: List[List[int]]) -> List[int]:
    # 最小堆，存储 (值, 列表索引, 元素索引)
    min_heap = []
    
    # 初始化堆，将每个列表的第一个元素加入堆中
    for i, lst in enumerate(lists):
        if lst:  # 确保列表非空
            heapq.heappush(min_heap, (lst[0], i, 0))
    
    result = []
    
    # 从堆中提取元素并添加到结果列表
    while min_heap:
        val, list_index, element_index = heapq.heappop(min_heap)
        result.append(val)
        
        # 如果列表还有剩余元素，将下一个元素加入堆中
        if element_index + 1 < len(lists[list_index]):
            next_val = lists[list_index][element_index + 1]
            heapq.heappush(min_heap, (next_val, list_index, element_index + 1))
    
    return result

# 示例调用
lists = [
    [1, 4, 5],
    [1, 3, 4],
    [2, 6]
]
print(merge_k_sorted_lists(lists))  # 输出: [1, 1, 2, 3, 4, 4, 5, 6]
```

---

### **代码逐行解析**：

1. **导入依赖**：
   ```python
   import heapq
   from typing import List
   ```
   - `heapq` 提供最小堆实现。
   - `List` 是输入类型的注解。

2. **初始化最小堆**：
   ```python
   min_heap = []
   ```
   - 最小堆用于存储当前每个链表的最小值，便于快速提取最小值。

3. **填充初始堆**：
   ```python
   for i, lst in enumerate(lists):
       if lst:  # 确保列表非空
           heapq.heappush(min_heap, (lst[0], i, 0))
   ```
   - 遍历每个链表，将其第一个元素、链表索引和元素索引加入堆中。

4. **从堆中提取最小值**：
   ```python
   val, list_index, element_index = heapq.heappop(min_heap)
   result.append(val)
   ```
   - 使用 `heapq.heappop` 提取堆顶元素（当前最小值），并将其加入结果列表。

5. **加入下一个元素**：
   ```python
   if element_index + 1 < len(lists[list_index]):
       next_val = lists[list_index][element_index + 1]
       heapq.heappush(min_heap, (next_val, list_index, element_index + 1))
   ```
   - 如果提取的元素所在链表还有剩余元素，将下一个元素加入堆中。

6. **返回结果**：
   ```python
   return result
   ```
   - 返回最终合并的有序列表。

---

### **时间复杂度分析 (Big O)**：

- **时间复杂度**：  
  O(N log K)，其中 `N` 是所有链表中元素的总数，`K` 是链表的数量。  
  - 堆操作的复杂度为 O(log K)，每个元素会被插入和提取一次，总共操作 `N` 次。

- **空间复杂度**：  
  O(K)，用于存储堆中最多 `K` 个元素。

---

### **示例运行讲解**：

**输入**：
```python
lists = [
    [1, 4, 5],
    [1, 3, 4],
    [2, 6]
]
```

#### 初始化堆：
1. 堆中加入每个链表的第一个元素：
   ```plaintext
   [(1, 0, 0), (1, 1, 0), (2, 2, 0)]
   ```

#### 第一步提取堆顶：
1. 提取 `(1, 0, 0)`，结果列表变为 `[1]`。
2. 将 `lists[0][1] = 4` 加入堆：
   ```plaintext
   [(1, 1, 0), (2, 2, 0), (4, 0, 1)]
   ```

#### 第二步提取堆顶：
1. 提取 `(1, 1, 0)`，结果列表变为 `[1, 1]`。
2. 将 `lists[1][1] = 3` 加入堆：
   ```plaintext
   [(2, 2, 0), (4, 0, 1), (3, 1, 1)]
   ```

#### 第三步提取堆顶：
1. 提取 `(2, 2, 0)`，结果列表变为 `[1, 1, 2]`。
2. 将 `lists[2][1] = 6` 加入堆：
   ```plaintext
   [(3, 1, 1), (4, 0, 1), (6, 2, 1)]
   ```

#### 重复此过程，最终结果为：
```plaintext
[1, 1, 2, 3, 4, 4, 5, 6]
```

---

### **总结**：

1. 使用最小堆可以高效地合并 `k` 个升序链表。
2. 每次从堆中提取当前最小值，并加入其后继元素，确保堆大小始终为 `k`。
3. 适用于所有升序排序的链表合并问题。

最终结果：  
```plaintext
[1, 1, 2, 3, 4, 4, 5, 6]
```
