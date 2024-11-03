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
该递归方法简洁明了，适合用于理解递归思想的链表反转问题。
