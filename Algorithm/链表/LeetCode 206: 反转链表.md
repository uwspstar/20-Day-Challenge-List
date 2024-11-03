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

---

这是 **LeetCode 206: 反转链表** 问题的完整解答，包括两种常用的解法：递归方法和迭代方法。

---

### LeetCode 206: 反转链表 (Reverse Linked List)

**题目描述**：  
给定一个单链表的头节点 `head`，将该链表反转，并返回反转后的链表头节点。

[LeetCode 206: Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

---

### 解法一：递归方法

递归的核心思想是逐层回溯，并在每一层中将当前节点的指针反转。

1. **递归终止条件**：
   - 如果 `head` 为空（链表为空）或者 `head.next` 为空（链表只有一个节点），直接返回 `head`，因为此时链表已处于反转状态。

2. **递归过程**：
   - 递归调用 `self.reverseList(head.next)`，直到链表的最后一个节点。这个节点将成为新的头节点 `new_head`。
   - 在回溯时，将当前节点的 `next` 指针反转，使 `head.next.next = head`。
   - 将当前节点的 `next` 置为 `None`，断开当前节点的原始链接，确保链表不会形成环。

3. **返回结果**：  
   - 最后返回反转后的链表头节点 `new_head`。

---

#### 代码实现（递归）

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

### 示例：递归反转链表 `1 -> 2 -> 3`

假设输入链表为 `1 -> 2 -> 3`，以下是代码的执行过程：

1. **初始调用**：`reverseList(1)`，递归调用直到到达链表末尾。
2. **回溯**：从链表的末尾节点 `3` 开始，将每一层的 `next` 指针反转。
   - `3 -> 2`
   - `2 -> 1`
   - 返回结果为 `3 -> 2 -> 1 -> None`

---

### 解法二：迭代方法

迭代方法使用两个指针 `prev` 和 `curr` 来逐步反转链表的指针，直到链表完全反转。

1. **初始化指针**：
   - `prev` 指向 `None`，表示反转后链表的末尾。
   - `curr` 指向 `head`，即当前节点。

2. **遍历链表**：
   - 在每次迭代中，将当前节点的 `next` 指向 `prev`，反转指针。
   - 移动 `prev` 和 `curr` 指针到下一个节点。
   
3. **返回结果**：
   - 当 `curr` 为 `None` 时，链表已完全反转，`prev` 为新的头节点。

---

#### 代码实现（迭代）

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head
        
        while curr:
            # 暂存下一节点
            next_temp = curr.next
            # 反转当前节点指针
            curr.next = prev
            # 移动 prev 和 curr 指针
            prev = curr
            curr = next_temp
        
        return prev
```

---

### 示例：迭代反转链表 `1 -> 2 -> 3`

假设输入链表为 `1 -> 2 -> 3`，代码的执行过程如下：

1. **初始状态**：
   - `prev = None`
   - `curr = 1`

2. **第 1 步**：
   - `next_temp = 2`（暂存下一个节点）
   - `curr.next = prev`，即 `1 -> None`
   - 更新 `prev = 1`，`curr = 2`

3. **第 2 步**：
   - `next_temp = 3`
   - `curr.next = prev`，即 `2 -> 1`
   - 更新 `prev = 2`，`curr = 3`

4. **第 3 步**：
   - `next_temp = None`
   - `curr.next = prev`，即 `3 -> 2`
   - 更新 `prev = 3`，`curr = None`

最终链表反转为 `3 -> 2 -> 1 -> None`。

---

### 复杂度分析

- **时间复杂度**：O(n)，无论是递归还是迭代，遍历链表的每个节点一次。
- **空间复杂度**：
  - **递归方法**：O(n)，递归栈的深度等于链表长度。
  - **迭代方法**：O(1)，只使用了常量额外空间。

---

### 总结

- **递归方法**：适合使用递归的链表反转解法，逐层回溯反转指针，结构清晰。
- **迭代方法**：更节省空间的常数空间解法，适用于较长链表。

这两种方法都是反转链表的经典解法，递归方法更直观，迭代方法更节省空间。
