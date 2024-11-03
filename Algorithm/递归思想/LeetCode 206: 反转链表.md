### LeetCode 206: 反转链表 (Reverse Linked List)

**题目描述**：  
给定一个单链表的头节点 `head`，将该链表反转，并返回反转后的链表头节点。

[LeetCode 206: Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

---

### 解题思路

我们使用递归的方法来反转链表。递归的核心思想是逐层回溯，并在每一层中将当前节点的指针反转。

1. **递归终止条件**：
   - 如果 `head` 为空（链表为空）或者 `head.next` 为空（链表只有一个节点），直接返回 `head`，因为此时链表已处于反转状态。

2. **递归过程**：
   - 递归调用 `self.reverseList(head.next)`，直到链表的最后一个节点。这个节点将成为新的头节点 `new_head`。
   - 当递归回溯时，将每一层的 `head.next.next` 指向 `head`，实现当前节点的反转。
   - 将 `head.next` 置为 `None`，断开当前节点的原始链接，确保链表不会形成环。

3. **返回结果**：  
   - 最后返回反转后的链表头节点 `new_head`。

---

### 代码实现

```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 递归终止条件：空链表或单节点链表
        if not head or not head.next:
            return head
        
        # 递归反转子链表，并获取新头节点
        new_head = self.reverseList(head.next)
        
        # 反转指针
        head.next.next = head
        head.next = None

        # 返回新的头节点
        return new_head
```

---

### 逐行解释

1. **递归终止条件**：
   ```python
   if not head or not head.next:
       return head
   ```
   - 如果链表为空或只有一个节点，直接返回 `head`，表示反转完成。

2. **递归调用反转子链表**：
   ```python
   new_head = self.reverseList(head.next)
   ```
   - 递归调用 `self.reverseList(head.next)`，反转以 `head.next` 开始的子链表。
   - 返回的 `new_head` 是反转后的链表的新头节点。

3. **反转当前节点的指针**：
   ```python
   head.next.next = head
   head.next = None
   ```
   - `head.next.next = head` 将 `head.next` 节点的 `next` 指针指向 `head`，实现反转。
   - `head.next = None` 切断 `head` 的原指向，确保链表不会成环。

4. **返回新头节点**：
   ```python
   return new_head
   ```
   - 逐层返回 `new_head`，最终返回整个链表的新的头节点。

---

### 示例讲解：逐步解析示例步骤

假设输入链表为 `1 -> 2 -> 3`，以下是代码执行过程的逐步解释：

初始链表：`1 -> 2 -> 3`

---

**第 1 次调用：`reverseList(1)`**
- `head = 1`
- `head.next = 2`，链表还未到达末尾节点
- 递归调用 `self.reverseList(head.next)`，即 `reverseList(2)`

---

**第 2 次调用：`reverseList(2)`**
- `head = 2`
- `head.next = 3`，链表还未到达末尾节点
- 递归调用 `self.reverseList(head.next)`，即 `reverseList(3)`

---

**第 3 次调用：`reverseList(3)`**
- `head = 3`
- `head.next = None`，这是链表的最后一个节点
- 根据递归终止条件，直接返回 `head`，即节点 `3`。此时 `new_head = 3`

---

### 开始回溯并反转指针

**回溯到第 2 次调用：`reverseList(2)`**
- 当前 `head = 2`
- `new_head = 3`（即反转后的链表的头节点）

#### 反转指针操作
1. 将 `head.next.next` 指向 `head`，即 `3.next = 2`，形成部分反转链表 `3 -> 2`
2. 将 `head.next = None`，断开 `2 -> 3` 的原始链接，链表变为 `3 -> 2 -> None`
   
- 返回 `new_head = 3`

---

**回溯到第 1 次调用：`reverseList(1)`**
- 当前 `head = 1`
- `new_head = 3`（此时反转后的链表头节点）

#### 反转指针操作
1. 将 `head.next.next` 指向 `head`，即 `2.next = 1`，形成完整反转链表 `3 -> 2 -> 1`
2. 将 `head.next = None`，断开 `1 -> 2` 的原始链接，链表变为 `3 -> 2 -> 1 -> None`
   
- 返回 `new_head = 3`

---

### 最终结果

整个链表已被反转，结果为 `3 -> 2 -> 1 -> None`。

---

### 总结

- **递归思想**：通过递归逐层返回，并反转链表的每一个节点。
- **时间复杂度 O(n)**：每个节点访问一次。
- **空间复杂度 O(n)**：递归栈的深度是链表长度 `n`。

该递归方法简洁明了，适合用于理解递归思想的链表反转问题。
