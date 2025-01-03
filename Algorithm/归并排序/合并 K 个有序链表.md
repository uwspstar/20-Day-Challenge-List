## 合并 K 个有序链表的解决方案

在计算机科学中，合并 K 个有序链表是一道经典的算法问题，通常用于测试候选人对分治策略、链表操作和时间复杂度的掌握。本文将详细讲解如何实现合并 K 个有序链表，并分析其时间复杂度和运行原理。

---

### 问题定义

给定一个包含 K 个有序链表的数组 `lists`，目标是将这些链表合并为一个有序链表并返回其头节点。每个链表的节点由以下 `ListNode` 类定义：

```python
# 单链表节点的定义
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

例如，对于以下输入：
```plaintext
lists = [
    1 -> 4 -> 5,
    1 -> 3 -> 4,
    2 -> 6
]
```
合并后的结果应为：
```plaintext
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
```

---

### 解决思路

我们可以通过**分治策略**来高效解决这个问题：

1. **两两合并**：依次合并两个链表，直到最终只剩下一个合并后的链表。
2. **优化合并顺序**：为了减少合并次数，我们可以采用分组合并的方式，例如将每两个链表合并为一个，再将结果合并。

---

### 实现代码

以下是完整的代码实现：

```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        # 如果输入为空或链表列表长度为 0，直接返回 None
        if not lists or len(lists) == 0:
            return None

        # 不断合并链表，直到剩下一个链表
        while len(lists) > 1:
            merge_list = []  # 存储每一轮合并后的链表
            for i in range(0, len(lists), 2):
                l1 = lists[i]  # 当前链表
                l2 = lists[i + 1] if (i + 1) < len(lists) else None  # 下一链表（如果存在）
                merge_list.append(self.merge_two(l1, l2))  # 合并两个链表
            lists = merge_list  # 更新列表，包含合并后的链表
        return lists[0]  # 返回最终合并后的链表

    def merge_two(self, l1, l2):
        # 合并两个有序链表
        dummy = tail = ListNode()  # 虚拟头节点，便于操作

        # 遍历两个链表，按顺序合并
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1  # 将 l1 当前节点连接到结果链表
                l1 = l1.next  # 移动 l1 指针
            else:
                tail.next = l2  # 将 l2 当前节点连接到结果链表
                l2 = l2.next  # 移动 l2 指针
            tail = tail.next  # 移动结果链表的尾指针

        # 如果还有剩余节点，直接连接
        tail.next = l1 or l2
        return dummy.next  # 返回合并后的链表（跳过虚拟头节点）
```

---

### 运行示例

#### 输入：
```plaintext
lists = [
    1 -> 4 -> 5,
    1 -> 3 -> 4,
    2 -> 6
]
```

#### 运行流程：
1. **第一轮合并**：
   - 合并 `1 -> 4 -> 5` 和 `1 -> 3 -> 4`：
     ```plaintext
     1 -> 1 -> 3 -> 4 -> 4 -> 5
     ```
   - 保留 `2 -> 6`：
     ```plaintext
     lists = [
         1 -> 1 -> 3 -> 4 -> 4 -> 5,
         2 -> 6
     ]
     ```

2. **第二轮合并**：
   - 合并 `1 -> 1 -> 3 -> 4 -> 4 -> 5` 和 `2 -> 6`：
     ```plaintext
     1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
     ```

3. **结束**：
   - 返回结果链表：
     ```plaintext
     1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
     ```

---

### 时间复杂度分析

- **单次合并时间**：假设链表总节点数为 \(N\)，合并两个链表的时间复杂度为 \(O(N)\)。
- **合并轮数**：每一轮将链表数减半，共需 \(O(\log K)\) 轮，其中 \(K\) 为链表数量。

综合时间复杂度为：
\[
O(N \log K)
\]

---

### 空间复杂度分析

由于算法只使用了常数额外空间存储中间变量，空间复杂度为：
\[
O(1)
\]

---

### 总结

这是一种高效解决合并 K 个有序链表问题的方式，利用分治策略将时间复杂度优化为 \(O(N \log K)\)。此外，代码中采用虚拟头节点简化了链表操作，提高了可读性。如果链表数量较多或链表较长，此方法依然具有良好的性能表现。

这种算法广泛应用于实际工程中，例如处理多个有序数据流、实现多路归并排序等场景。理解并掌握这一算法对算法设计和工程开发都非常重要！
