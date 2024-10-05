# Linked List

---

### 1. LeetCode 206: Reverse Linked List（反转链表）

**题目描述**：
给定一个单链表，反转该链表，并返回反转后的链表头节点。

**题目分析**：
可以使用迭代法或递归法来反转链表。我们首先讲解迭代法。迭代法中，我们使用三个指针 `prev`、`current` 和 `next`，逐个节点反转链表指针的方向。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义反转链表的函数
    def reverseList(self, head: ListNode) -> ListNode:
        # 初始化前置指针 prev 为 None
        prev = None
        # 初始化当前指针 current 为头节点
        current = head

        # 迭代反转链表
        while current:
            # 暂存当前节点的下一节点
            next_node = current.next
            # 将当前节点的 next 指向前置节点
            current.next = prev
            # 移动前置指针和当前指针
            prev = current
            current = next_node

        # 返回反转后的链表头节点（即 prev）
        return prev

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和反转操作）。

---

### 2. LeetCode 21: Merge Two Sorted Lists（合并两个有序链表）

**题目描述**：
将两个升序排列的有序链表 `list1` 和 `list2` 合并为一个新的升序链表，并返回合并后的链表头节点。

**题目分析**：
可以使用迭代法来合并两个有序链表。我们使用一个指针 `current` 来逐个合并 `list1` 和 `list2` 中的节点，并构造新的有序链表。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义合并两个有序链表的函数
    def mergeTwoLists(self, list1: ListNode, list2: ListNode) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode()
        # 初始化当前指针
        current = dummy

        # 遍历两个链表，将较小的节点依次加入新链表
        while list1 and list2:
            if list1.val < list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next
            current = current.next

        # 如果 list1 或 list2 未遍历完，将剩余节点加入新链表
        current.next = list1 if list1 else list2

        # 返回合并后的链表头节点
        return dummy.next

# 时间复杂度：O(n + m) - n 和 m 分别是两个链表的长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是两个链表的长度，需要遍历两个链表的所有节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和合并操作）。

---

### 3. LeetCode 24: Swap Nodes in Pairs（两两交换链表中的节点）

**题目描述**：
给定一个链表，将链表中的每两个相邻节点交换，并返回交换后的链表头节点。如果节点个数是奇数，则最后一个节点不进行交换。

**题目分析**：
可以使用迭代法来交换节点。我们使用一个指针 `prev` 来指向每次交换后的节点，并使用三个指针 `first`、`second` 和 `third` 来处理节点的交换。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义两两交换链表节点的函数
    def swapPairs(self, head: ListNode) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化前置指针
        prev = dummy

        # 迭代交换相邻节点
        while head and head.next:
            # 定义要交换的两个节点
            first = head
            second = head.next

            # 交换节点
            prev.next = second
            first.next = second.next
            second.next = first

            # 移动指针
            prev = first
            head = first.next

        # 返回交换后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点交换操作）。

---

### 4. LeetCode 92: Reverse Linked List II（反转链表 II）

**题目描述**：
给定一个单链表的头节点 `head` 和两个整数 `left` 和 `right`，反转从位置 `left` 到位置 `right` 的链表节点，并返回反转后的链表头节点。

**题目分析**：
可以使用迭代法来反转链表的部分节点。首先找到 `left` 节点的前一个节点 `prev`，然后反转从 `left` 到 `right` 的链表部分，最后连接反转后的部分。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义反转链表 II 的函数
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化前置指针
        prev = dummy

        # 找到 left 节点的前一个节点
        for _ in range(left - 1):
            prev = prev.next

        # 初始化反转链表的起点和终点
        reverse_start = prev.next
        reverse_end = reverse_start.next

        # 迭代反转 left 到 right 的链表部分
        for _ in range(right - left):
            reverse_start.next = reverse_end.next
            reverse_end.next = prev.next
            prev.next = reverse_end
            reverse_end = reverse_start.next

        # 返回反转后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点反转操作）。

---

### 5. LeetCode 61: Rotate List（旋转链表）

**题目描述**：
给定一个链表，将链表向右旋转 `k` 个位置，并返回旋转后的链表头节点。

**题目分析**：
首先计算链表的长度 `n`，然后将链表变为环状结构，最后根据旋转的次数 `k` 断开环，从而完成旋

转操作。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义旋转链表的函数
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next or k == 0:
            return head

        # 计算链表的长度，并将链表连接成环
        length = 1
        tail = head
        while tail.next:
            tail = tail.next
            length += 1
        tail.next = head  # 链表成环

        # 计算旋转的次数，找到新的头节点和尾节点
        k = k % length
        if k == 0:
            tail.next = None
            return head

        # 移动到新的尾节点
        new_tail = head
        for _ in range(length - k - 1):
            new_tail = new_tail.next

        # 新的头节点是新尾节点的下一个节点
        new_head = new_tail.next
        new_tail.next = None  # 断开环

        return new_head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

好的，我们继续讲解接下来的五道 LeetCode 链表题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 6. LeetCode 138: Copy List with Random Pointer（带随机指针的链表复制）

**题目描述**：
给定一个链表，其中每个节点包含一个额外的随机指针 `random`，该指针可能指向链表中的任意节点或为空。要求返回该链表的深度复制（即复制后的新链表应独立于原链表）。

**题目分析**：
可以分三步解决该问题：
1. **创建新节点**：将新节点插入到原节点之后。
2. **复制随机指针**：通过新旧节点之间的连接关系，将随机指针复制到新节点中。
3. **分离链表**：将新链表与原链表分离，返回新链表的头节点。

**代码实现**：
```python
# 定义链表节点类（带随机指针）
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = x
        self.next = next
        self.random = random

# 定义解决方案的类
class Solution:
    # 定义复制带随机指针的链表的函数
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return None

        # 步骤 1：复制每个节点，并将新节点插入到原节点之后
        current = head
        while current:
            new_node = Node(current.val, current.next, None)
            current.next = new_node
            current = new_node.next

        # 步骤 2：复制随机指针
        current = head
        while current:
            if current.random:
                current.next.random = current.random.next
            current = current.next.next

        # 步骤 3：将新链表从原链表中分离
        current = head
        new_head = head.next
        while current:
            new_node = current.next
            current.next = new_node.next
            current = current.next
            if new_node.next:
                new_node.next = new_node.next.next

        return new_head

# 时间复杂度：O(n) - 遍历链表的每个节点三次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间（用于节点复制和链表分离）
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，遍历链表的每个节点三次：一次创建新节点，一次复制随机指针，一次分离链表。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点操作）。

---

### 7. LeetCode 234: Palindrome Linked List（回文链表）

**题目描述**：
给定一个链表，判断链表是否为回文结构。

**题目分析**：
可以使用快慢指针法结合链表操作来解决该问题：
1. 使用快慢指针找到链表的中间节点。
2. 反转后半部分链表。
3. 比较前半部分和反转后的后半部分是否相等。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义判断回文链表的函数
    def isPalindrome(self, head: ListNode) -> bool:
        # 步骤 1：使用快慢指针找到链表的中间节点
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 步骤 2：反转后半部分链表
        prev = None
        while slow:
            temp = slow.next
            slow.next = prev
            prev = slow
            slow = temp

        # 步骤 3：比较前半部分和反转后的后半部分链表
        left, right = head, prev
        while right:  # 注意：只需比较后半部分的长度
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True

# 时间复杂度：O(n) - 最多遍历链表两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表两次：一次找到中间节点，一次比较链表的前后部分。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 8. LeetCode 82: Remove Duplicates from Sorted List II（删除排序链表中的重复元素 II）

**题目描述**：
给定一个升序排列的链表，删除链表中所有重复的节点，只保留原始链表中没有重复出现的节点。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `prev` 和 `current` 来遍历链表，`prev` 指向当前未重复节点的最后一个节点，`current` 用于查找重复节点并删除。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除排序链表中重复元素的函数
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化前置指针
        prev = dummy

        # 遍历链表
        while head:
            # 跳过所有重复节点
            if head.next and head.val == head.next.val:
                while head.next and head.val == head.next.val:
                    head = head.next
                # 连接前置节点与后续未重复节点
                prev.next = head.next
            else:
                # 没有重复，移动前置指针
                prev = prev.next
            head = head.next

        # 返回去重后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和去重操作）。

---

### 9. LeetCode 83: Remove Duplicates from Sorted List（删除排序链表中的重复元素）

**题目描述**：
给定一个升序排列的链表，删除链表中所有重复的节点，只保留原始链表中没有重复出现的节点。

**题目分析**：
可以使用单指针法来解决该问题。遍历链表的同时检查相邻节点的值，如果值相同则跳过当前节点，否则将其加入结果链表。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除排序链表中重复元素的函数
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # 初始化当前指针
        current = head

        # 遍历链表，跳过重复节点
        while current and current.next:
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next

        # 返回去重后的链表头节点
        return head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和去重操作）。

---

### 10. LeetCode 2: Add Two Numbers（两数相加）

**题目描述**：
给定两个表示非负整数的非

空链表 `l1` 和 `l2`，它们的每位数字都是按逆序存储的，并且每个节点只能存储一位数字。将这两个数相加，并返回一个新的链表表示它们的和。

**题目分析**：
可以使用两个指针 `p1` 和 `p2` 遍历 `l1` 和 `l2`，同时维护一个进位值 `carry`，逐位相加生成新链表。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义两数相加的函数
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode()
        # 初始化当前指针和进位
        current, carry = dummy, 0

        # 遍历两个链表
        while l1 or l2 or carry:
            # 计算当前位的和
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            total = val1 + val2 + carry

            # 更新进位和当前位的值
            carry = total // 10
            current.next = ListNode(total % 10)

            # 移动指针
            current = current.next
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next

        # 返回结果链表的头节点
        return dummy.next

# 时间复杂度：O(max(n, m)) - n 和 m 分别是两个链表的长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(max(n, m))，其中 n 和 m 分别是两个链表的长度，需要遍历较长的链表。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和进位计算）。

---

好的，我们继续讲解接下来的五道 LeetCode 链表题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 11. LeetCode 445: Add Two Numbers II（两数相加 II）

**题目描述**：
给定两个表示非负整数的链表 `l1` 和 `l2`，它们的每位数字都是按照正常顺序存储的，并且每个节点只能存储一位数字。将这两个数相加，并返回一个新的链表表示它们的和。

**题目分析**：
可以使用栈来解决该问题。首先将两个链表中的所有节点值分别压入两个栈中，然后逐位弹出栈顶元素进行相加，创建新的节点并将其插入到结果链表的头部。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义两数相加 II 的函数
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        # 使用两个栈保存链表节点值
        stack1, stack2 = [], []
        
        # 将 l1 的节点值压入栈1
        while l1:
            stack1.append(l1.val)
            l1 = l1.next
        
        # 将 l2 的节点值压入栈2
        while l2:
            stack2.append(l2.val)
            l2 = l2.next

        # 初始化进位和结果链表
        carry = 0
        head = None

        # 逐位相加
        while stack1 or stack2 or carry:
            # 弹出栈顶元素进行相加
            val1 = stack1.pop() if stack1 else 0
            val2 = stack2.pop() if stack2 else 0
            total = val1 + val2 + carry

            # 更新进位
            carry = total // 10
            # 创建新节点，并将其插入到结果链表的头部
            new_node = ListNode(total % 10)
            new_node.next = head
            head = new_node

        # 返回结果链表的头节点
        return head

# 时间复杂度：O(n + m) - n 和 m 分别是两个链表的长度
# 空间复杂度：O(n + m) - 用于栈的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是两个链表的长度，需要遍历两个链表。
- **空间复杂度**：O(n + m)，使用了两个栈来保存链表节点值。

---

### 12. LeetCode 109: Convert Sorted List to Binary Search Tree（有序链表转换为二叉搜索树）

**题目描述**：
给定一个升序排列的单链表，将其转换为高度平衡的二叉搜索树。

**题目分析**：
可以使用递归法和快慢指针法来解决该问题。首先使用快慢指针找到链表的中间节点作为二叉搜索树的根节点，然后递归地将中间节点左侧和右侧的链表部分转换为左子树和右子树。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义转换有序链表为二叉搜索树的函数
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        # 辅助函数：找到链表的中间节点
        def find_middle(left, right):
            slow, fast = left, left
            while fast != right and fast.next != right:
                slow = slow.next
                fast = fast.next.next
            return slow

        # 辅助函数：递归构造二叉搜索树
        def convert_list_to_bst(left, right):
            if left == right:
                return None

            # 找到中间节点作为当前子树的根节点
            mid = find_middle(left, right)
            node = TreeNode(mid.val)

            # 递归构造左子树和右子树
            node.left = convert_list_to_bst(left, mid)
            node.right = convert_list_to_bst(mid.next, right)
            return node

        # 从链表头到链表尾递归构造二叉搜索树
        return convert_list_to_bst(head, None)

# 时间复杂度：O(n log n) - 递归构造二叉搜索树的复杂度
# 空间复杂度：O(log n) - 用于递归调用栈的空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，递归构造二叉搜索树时，每次找到中间节点的复杂度为 O(log n)，总复杂度为 O(n log n)。
- **空间复杂度**：O(log n)，用于递归调用栈的空间。

---

### 13. LeetCode 143: Reorder List（重排链表）

**题目描述**：
给定一个单链表 `L`：`L0 → L1 → … → Ln-1 → Ln`，将其重新排列为：`L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …`。

**题目分析**：
可以使用快慢指针法找到链表的中间节点，并将链表分为前后两部分，然后反转后半部分链表，最后将前半部分和反转后的后半部分交替合并。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义重排链表的函数
    def reorderList(self, head: ListNode) -> None:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next:
            return

        # 步骤 1：使用快慢指针找到链表的中间节点
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 步骤 2：将链表分为两部分，并反转后半部分链表
        second = slow.next
        slow.next = None
        prev = None
        while second:
            temp = second.next
            second.next = prev
            prev = second
            second = temp

        # 步骤 3：将前半部分与反转后的后半部分交替合并
        first, second = head, prev
        while second:
            temp1, temp2 = first.next, second.next
            first.next = second
            second.next = temp1
            first, second = temp1, temp2

# 时间复杂度：O(n) - 最多遍历链表三次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表三次：一次找到中间节点，一次反转后半部分链表，一次合并链表。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 14. LeetCode 148: Sort List（排序链表）

**题目描述**：
给定一个链表，对链表中的节点进行升序排序，并返回排序后的链表头节点。

**题目分析**：
可以使用归并排序（自顶向下）来解决该问题。首先使用快慢指针找到链表的中间节点，然后递归地将链表分为前后两部分并排序，最后合并两个有序链表。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义排序链表的函数
    def sortList(self, head: ListNode) -> ListNode:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next:
            return head

        # 使用快慢指针找到链表的中间节点
        slow, fast = head, head.next
       

 while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 分割链表，并递归排序左右两部分
        mid = slow.next
        slow.next = None
        left = self.sortList(head)
        right = self.sortList(mid)

        # 合并两个有序链表
        return self.merge(left, right)

    # 辅助函数：合并两个有序链表
    def merge(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode()
        current = dummy
        while l1 and l2:
            if l1.val < l2.val:
                current.next = l1
                l1 = l1.next
            else:
                current.next = l2
                l2 = l2.next
            current = current.next

        # 连接剩余的节点
        current.next = l1 if l1 else l2
        return dummy.next

# 时间复杂度：O(n log n) - 归并排序的复杂度
# 空间复杂度：O(log n) - 用于递归调用栈的空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，归并排序的时间复杂度。
- **空间复杂度**：O(log n)，递归调用栈的空间复杂度。

---

### 15. LeetCode 203: Remove Linked List Elements（移除链表元素）

**题目描述**：
给定一个链表和一个值 `val`，删除链表中所有等于 `val` 的节点，并返回删除后的链表头节点。

**题目分析**：
可以使用单指针法来解决该问题。遍历链表的同时检查节点的值是否等于 `val`，如果等于则跳过当前节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义移除链表元素的函数
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化当前指针
        current = dummy

        # 遍历链表，移除等于 val 的节点
        while current.next:
            if current.next.val == val:
                current.next = current.next.next
            else:
                current = current.next

        # 返回删除后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点移除）。

---

好的，我们继续讲解接下来的五道 LeetCode 链表题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 16. LeetCode 147: Insertion Sort List（链表插入排序）

**题目描述**：
对一个单链表进行插入排序，并返回排序后的链表头节点。

**题目分析**：
插入排序是稳定的排序算法，可以通过逐个遍历链表节点，并将其插入到已排序部分的合适位置来实现。为便于处理，我们可以引入一个虚拟头节点 `dummy`，每次从原链表中取下一个节点，并插入到已排序部分的链表中。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义链表插入排序的函数
    def insertionSortList(self, head: ListNode) -> ListNode:
        # 定义虚拟头节点
        dummy = ListNode(0)
        # 初始化当前节点
        current = head

        # 遍历链表，进行插入排序
        while current:
            # 暂存当前节点的下一个节点
            next_node = current.next
            # 在已排序部分中找到插入位置
            position = dummy
            while position.next and position.next.val < current.val:
                position = position.next
            # 插入当前节点到已排序部分
            current.next = position.next
            position.next = current
            # 继续处理下一个节点
            current = next_node

        # 返回排序后的链表头节点
        return dummy.next

# 时间复杂度：O(n^2) - 最差情况下，每次插入都需要遍历已排序部分
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，最差情况下，每次插入都需要遍历已排序部分。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点插入）。

---

### 17. LeetCode 86: Partition List（分隔链表）

**题目描述**：
给定一个链表和一个值 `x`，将所有小于 `x` 的节点放在大于或等于 `x` 的节点之前，并保持它们的原始相对顺序。

**题目分析**：
可以使用两个指针分别指向小于 `x` 的节点链表和大于或等于 `x` 的节点链表。遍历链表，将节点分别加入这两个链表中，最后将两个链表合并。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义分隔链表的函数
    def partition(self, head: ListNode, x: int) -> ListNode:
        # 定义两个虚拟头节点，分别用于小于 x 和大于等于 x 的链表
        smaller_head = ListNode(0)
        larger_head = ListNode(0)
        # 初始化当前指针
        smaller = smaller_head
        larger = larger_head

        # 遍历链表，将节点放入对应的链表中
        while head:
            if head.val < x:
                smaller.next = head
                smaller = smaller.next
            else:
                larger.next = head
                larger = larger.next
            head = head.next

        # 合并两个链表，并将 larger 的尾节点指向 None
        larger.next = None
        smaller.next = larger_head.next

        # 返回分隔后的链表头节点
        return smaller_head.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 18. LeetCode 328: Odd Even Linked List（奇偶链表）

**题目描述**：
给定一个单链表，将所有索引位置为奇数的节点放在索引位置为偶数的节点之前，并保持它们的原始相对顺序。

**题目分析**：
可以使用两个指针分别指向奇数位置和偶数位置的链表。遍历链表，将节点分别加入这两个链表中，最后将奇数链表的尾节点连接到偶数链表的头节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义奇偶链表的函数
    def oddEvenList(self, head: ListNode) -> ListNode:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next:
            return head

        # 初始化奇偶指针
        odd = head
        even = head.next
        even_head = even

        # 遍历链表，将奇数位置节点与偶数位置节点分离
        while even and even.next:
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next

        # 将奇数链表的尾节点连接到偶数链表的头节点
        odd.next = even_head

        # 返回处理后的链表头节点
        return head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 19. LeetCode 25: Reverse Nodes in k-Group（K 个一组翻转链表）

**题目描述**：
给定一个链表，将链表中每 `k` 个节点一组进行翻转，并返回翻转后的链表。如果节点总数不是 `k` 的倍数，则保留原顺序。

**题目分析**：
可以使用递归法或迭代法来解决该问题。首先统计链表长度，然后分段进行翻转。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义 K 个一组翻转链表的函数
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        # 检查链表是否足够长
        count = 0
        current = head
        while current and count < k:
            current = current.next
            count += 1

        # 如果长度不足 k，直接返回当前链表
        if count < k:
            return head

        # 反转前 k 个节点
        prev, current = None, head
        for _ in range(k):
            next_node = current.next
            current.next = prev
            prev = current
            current = next_node

        # 递归处理剩余节点，并连接
        if current:
            head.next = self.reverseKGroup(current, k)

        return prev

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(n/k) - 用于递归调用栈的空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(n/k)，用于递归调用栈的空间。

---

### 20. LeetCode 142: Linked List Cycle II（环形链表 II）

**题目描述**：
给定一个链表，如果链表中存在环，则返回环的起始节点。如果链表中不存在环，则返回 `null`。

**题目分析**：
可以使用快慢指针法来解决该问题。首先使用快慢指针判断链表中是否存在环，如果存在，则用两个指针分别从链表头节点和相遇点开始遍历，它们相遇的节点即为环

的起始节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义查找环形链表起始节点的函数
    def detectCycle(self, head: ListNode) -> ListNode:
        # 初始化快慢指针
        slow, fast = head, head

        # 使用快慢指针判断链表是否存在环
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                # 存在环，找到环的起始节点
                pointer = head
                while pointer != slow:
                    pointer = pointer.next
                    slow = slow.next
                return pointer

        # 不存在环
        return None

# 时间复杂度：O(n) - 最多遍历链表两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表两次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和环起点查找）。

---

好的，我们继续讲解接下来的五道 LeetCode 链表题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 21. LeetCode 138: Copy List with Random Pointer（带随机指针的链表复制）

**题目描述**：
给定一个链表，其中每个节点包含一个额外的随机指针 `random`，该指针可能指向链表中的任意节点或为空。要求返回该链表的深度复制（即复制后的新链表应独立于原链表）。

**题目分析**：
可以分三步解决该问题：
1. **创建新节点**：将新节点插入到原节点之后。
2. **复制随机指针**：通过新旧节点之间的连接关系，将随机指针复制到新节点中。
3. **分离链表**：将新链表与原链表分离，返回新链表的头节点。

**代码实现**：
```python
# 定义链表节点类（带随机指针）
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = x
        self.next = next
        self.random = random

# 定义解决方案的类
class Solution:
    # 定义复制带随机指针的链表的函数
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return None

        # 步骤 1：复制每个节点，并将新节点插入到原节点之后
        current = head
        while current:
            new_node = Node(current.val, current.next, None)
            current.next = new_node
            current = new_node.next

        # 步骤 2：复制随机指针
        current = head
        while current:
            if current.random:
                current.next.random = current.random.next
            current = current.next.next

        # 步骤 3：将新链表从原链表中分离
        current = head
        new_head = head.next
        while current:
            new_node = current.next
            current.next = new_node.next
            current = current.next
            if new_node.next:
                new_node.next = new_node.next.next

        return new_head

# 时间复杂度：O(n) - 遍历链表的每个节点三次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间（用于节点复制和链表分离）
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，遍历链表的每个节点三次：一次创建新节点，一次复制随机指针，一次分离链表。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点操作）。

---

### 22. LeetCode 430: Flatten a Multilevel Doubly Linked List（扁平化多级双向链表）

**题目描述**：
给定一个多级双向链表，每个节点除了 `next` 和 `prev` 指针外，还有一个 `child` 指针，该指针可能指向一个单独的双向链表。将这个多级双向链表扁平化为一个普通的双向链表，并返回扁平化后的链表头节点。

**题目分析**：
可以使用递归或迭代法来解决该问题。对于每个节点，如果存在 `child` 指针，则将该 `child` 链表插入到当前节点与 `next` 节点之间，并继续处理后续节点。

**代码实现**：
```python
# 定义多级双向链表节点类
class Node:
    def __init__(self, val=None, prev=None, next=None, child=None):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child

# 定义解决方案的类
class Solution:
    # 定义扁平化多级双向链表的函数
    def flatten(self, head: 'Node') -> 'Node':
        # 辅助函数：递归处理多级链表的扁平化
        def flatten_dfs(node):
            # 当前节点的最后一个节点
            last = node

            # 遍历链表，处理每个节点
            while node:
                next_node = node.next

                # 如果存在子链表，递归处理子链表
                if node.child:
                    child_last = flatten_dfs(node.child)

                    # 将子链表插入到当前节点与下一个节点之间
                    node.next = node.child
                    node.child.prev = node
                    node.child = None

                    # 将子链表的最后一个节点与原下一个节点连接
                    if next_node:
                        child_last.next = next_node
                        next_node.prev = child_last

                    last = child_last
                else:
                    last = node

                # 移动到下一个节点
                node = next_node

            return last

        # 处理空链表的情况
        if not head:
            return None

        # 扁平化链表
        flatten_dfs(head)
        return head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(n) - 递归调用栈的空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的节点总数，需要遍历每个节点。
- **空间复杂度**：O(n)，递归调用栈的空间复杂度。

---

### 23. LeetCode 61: Rotate List（旋转链表）

**题目描述**：
给定一个链表，将链表向右旋转 `k` 个位置，并返回旋转后的链表头节点。

**题目分析**：
首先计算链表的长度 `n`，然后将链表变为环状结构，最后根据旋转的次数 `k` 断开环，从而完成旋转操作。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义旋转链表的函数
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next or k == 0:
            return head

        # 计算链表的长度，并将链表连接成环
        length = 1
        tail = head
        while tail.next:
            tail = tail.next
            length += 1
        tail.next = head  # 链表成环

        # 计算旋转的次数，找到新的头节点和尾节点
        k = k % length
        if k == 0:
            tail.next = None
            return head

        # 移动到新的尾节点
        new_tail = head
        for _ in range(length - k - 1):
            new_tail = new_tail.next

        # 新的头节点是新尾节点的下一个节点
        new_head = new_tail.next
        new_tail.next = None  # 断开环

        return new_head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 24. LeetCode 725: Split Linked List in Parts（分隔链表）

**题目描述**：
给定一个单链表和一个整数 `k`，将链表分隔成 `k` 个连续的部分，每个部分的长度尽可能相等。

**题目分析**：
首先计算链表的总长度 `n`，然后确定每部分的基础长度和多余节点数。遍历链表，将链表切分为 `k` 个部分，并记录每部分的头节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义分隔链表的函数
    def splitListToParts(self, root: ListNode, k: int) -> List[ListNode]:
        # 计算链表的总长度
        length = 0
        current = root
        while current:
            length += 1
            current = current.next

        # 计算每部分的基础长度和多余节点数
        part_size = length // k
        extra_nodes =

 length % k

        # 分隔链表
        parts = []
        current = root
        for _ in range(k):
            part_head = current
            for _ in range(part_size + (1 if extra_nodes > 0 else 0) - 1):
                if current:
                    current = current.next

            if current:
                temp = current.next
                current.next = None
                current = temp

            parts.append(part_head)
            if extra_nodes > 0:
                extra_nodes -= 1

        return parts

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表分隔操作）。

---

### 25. LeetCode 92: Reverse Linked List II（反转链表 II）

**题目描述**：
给定一个单链表的头节点 `head` 和两个整数 `left` 和 `right`，反转从位置 `left` 到位置 `right` 的链表节点，并返回反转后的链表头节点。

**题目分析**：
可以使用迭代法来反转链表的部分节点。首先找到 `left` 节点的前一个节点 `prev`，然后反转从 `left` 到 `right` 的链表部分，最后连接反转后的部分。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义反转链表 II 的函数
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化前置指针
        prev = dummy

        # 找到 left 节点的前一个节点
        for _ in range(left - 1):
            prev = prev.next

        # 初始化反转链表的起点和终点
        reverse_start = prev.next
        reverse_end = reverse_start.next

        # 迭代反转 left 到 right 的链表部分
        for _ in range(right - left):
            reverse_start.next = reverse_end.next
            reverse_end.next = prev.next
            prev.next = reverse_end
            reverse_end = reverse_start.next

        # 返回反转后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点反转操作）。

---

好的，我们继续讲解接下来的五道 LeetCode 链表题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 26. LeetCode 82: Remove Duplicates from Sorted List II（删除排序链表中的重复元素 II）

**题目描述**：
给定一个升序排列的链表，删除链表中所有重复的节点，只保留原始链表中没有重复出现的节点。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `prev` 和 `current` 来遍历链表，`prev` 指向当前未重复节点的最后一个节点，`current` 用于查找重复节点并删除。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除排序链表中重复元素 II 的函数
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0, head)
        # 初始化前置指针
        prev = dummy

        # 遍历链表
        while head:
            # 跳过所有重复节点
            if head.next and head.val == head.next.val:
                while head.next and head.val == head.next.val:
                    head = head.next
                # 连接前置节点与后续未重复节点
                prev.next = head.next
            else:
                # 没有重复，移动前置指针
                prev = prev.next
            head = head.next

        # 返回去重后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和去重操作）。

---

### 27. LeetCode 83: Remove Duplicates from Sorted List（删除排序链表中的重复元素）

**题目描述**：
给定一个升序排列的链表，删除链表中所有重复的节点，只保留原始链表中没有重复出现的节点。

**题目分析**：
可以使用单指针法来解决该问题。遍历链表的同时检查相邻节点的值，如果值相同则跳过当前节点，否则将其加入结果链表。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除排序链表中重复元素的函数
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        # 初始化当前指针
        current = head

        # 遍历链表，跳过重复节点
        while current and current.next:
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next

        # 返回去重后的链表头节点
        return head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和去重操作）。

---

### 28. LeetCode 708: Insert into a Sorted Circular Linked List（插入排序循环链表）

**题目描述**：
给定一个排序的循环链表，将值 `insertVal` 插入链表中，并保持链表的有序性。如果链表为空，则创建一个单节点循环链表。

**题目分析**：
遍历链表找到合适的位置进行插入，并维护循环链表的性质。如果链表为空，则直接创建一个节点并将其指向自身。

**代码实现**：
```python
# 定义循环链表节点类
class Node:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义插入排序循环链表的函数
    def insert(self, head: 'Node', insertVal: int) -> 'Node':
        # 如果链表为空，则创建一个单节点循环链表
        if not head:
            new_node = Node(insertVal)
            new_node.next = new_node
            return new_node

        # 初始化当前指针和下一个节点指针
        current = head
        while True:
            # 找到插入位置
            if (current.val <= insertVal <= current.next.val) or \
               (current.val > current.next.val and (insertVal >= current.val or insertVal <= current.next.val)):
                current.next = Node(insertVal, current.next)
                return head
            current = current.next

            # 如果遍历了一圈，直接插入到尾节点后面
            if current == head:
                current.next = Node(insertVal, current.next)
                return head

# 时间复杂度：O(n) - 最多遍历链表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和节点插入操作）。

---

### 29. LeetCode 369: Plus One Linked List（链表加一）

**题目描述**：
给定一个表示非负整数的单链表，其中每个节点包含一个数字，将该数字加一，并返回处理后的链表。

**题目分析**：
可以使用递归法或迭代法来解决该问题。递归法中，从链表尾节点开始向头节点回溯，并在回溯时处理进位问题。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义链表加一的函数
    def plusOne(self, head: ListNode) -> ListNode:
        # 辅助函数：递归处理链表加一
        def dfs(node):
            if not node:
                return 1  # 递归到链表尾部，返回进位 1

            carry = dfs(node.next)  # 递归处理下一个节点
            val = node.val + carry  # 计算当前节点的新值
            node.val = val % 10  # 更新当前节点的值
            return val // 10  # 返回进位

        # 处理链表加一
        carry = dfs(head)
        if carry:  # 如果有进位，创建一个新头节点
            new_head = ListNode(1)
            new_head.next = head
            return new_head
        else:
            return head

# 时间复杂度：O(n) - 遍历链表的每个节点
# 空间复杂度：O(n) - 用于递归调用栈的空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点。
- **空间复杂度**：O(n)，用于递归调用栈的空间复杂度。

---

### 30. LeetCode 1171: Remove Zero Sum Consecutive Nodes from Linked List（删除链表中和为零的连续节点）

**题目描述**：
给定一个链表，删除链表中所有连续和为零的节点，并返回删除后的链表。

**题目分析**：
可以使用哈希表来记录前缀和的位置。遍历链表并计算前缀和，当出现重复的前缀和时，说明从上一个相同前缀和到当前节点的所有节点和为零，应将这些节点删除。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除和为零的连续节点的函数
    def removeZeroSumSublists(self, head: ListNode)

 -> ListNode:
        # 定义虚拟头节点，便于处理边界情况
        dummy = ListNode(0)
        dummy.next = head

        # 使用哈希表记录前缀和的位置
        prefix_sum = 0
        prefix_dict = {0: dummy}

        # 遍历链表，计算前缀和，并记录位置
        current = head
        while current:
            prefix_sum += current.val
            prefix_dict[prefix_sum] = current
            current = current.next

        # 再次遍历链表，删除和为零的连续节点
        prefix_sum = 0
        current = dummy
        while current:
            prefix_sum += current.val
            current.next = prefix_dict[prefix_sum].next
            current = current.next

        # 返回删除后的链表头节点
        return dummy.next

# 时间复杂度：O(n) - 遍历链表的每个节点两次
# 空间复杂度：O(n) - 使用了哈希表记录前缀和
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，需要遍历链表的每个节点两次。
- **空间复杂度**：O(n)，使用了哈希表记录前缀和。
