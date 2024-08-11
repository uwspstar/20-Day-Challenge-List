# Linked List 链表

A Linked List is a linear data structure where elements, called nodes, are stored in a sequence, with each node containing a reference (or link) to the next node in the sequence. Unlike arrays, linked lists do not require contiguous memory locations for their elements, making them flexible and efficient for certain operations, such as dynamic memory allocation, insertion, and deletion. Linked lists are commonly used in scenarios where the size of the data structure is unknown or changes frequently.  
链表是一种线性数据结构，其中的元素称为节点，它们按顺序存储，每个节点包含一个指向下一个节点的引用（或链接）。与数组不同，链表不要求元素具有连续的内存位置，这使得它们在动态内存分配、插入和删除等操作中灵活且高效。链表通常用于数据结构的大小未知或经常变化的场景。

### How Linked Lists Work 链表如何工作

1. **Node Structure**: Each node in a linked list consists of two parts: the data and a reference to the next node.  
   **节点结构**：链表中的每个节点由两部分组成：数据和指向下一个节点的引用。

2. **Head Node**: The first node in a linked list is called the head. The head node serves as the starting point for any operation on the list.  
   **头节点**：链表中的第一个节点称为头节点。头节点作为对链表进行任何操作的起点。

3. **Traversal**: To access an element in a linked list, you must start at the head and follow the links from one node to the next until you reach the desired node.  
   **遍历**：要访问链表中的元素，必须从头节点开始，沿着从一个节点到下一个节点的链接，直到到达所需的节点。

4. **Dynamic Size**: Unlike arrays, linked lists do not have a fixed size, allowing them to grow and shrink dynamically as elements are added or removed.  
   **动态大小**：与数组不同，链表没有固定大小，允许它们在添加或删除元素时动态增长或缩小。

5. **Types of Linked Lists**:  
   **链表类型**：
   - **Singly Linked List**: Each node points to the next node, and the last node points to `null` (or `None` in Python).  
     **单链表**：每个节点指向下一个节点，最后一个节点指向 `null`（或Python中的 `None`）。
   - **Doubly Linked List**: Each node has two references, one to the next node and one to the previous node.  
     **双链表**：每个节点有两个引用，一个指向下一个节点，一个指向前一个节点。
   - **Circular Linked List**: The last node points back to the head, forming a circle.  
     **循环链表**：最后一个节点指向头节点，形成一个环。

### Example of a Singly Linked List 单链表的示例

Consider a singly linked list containing the elements `3 -> 5 -> 7 -> 10`.  
考虑一个包含元素 `3 -> 5 -> 7 -> 10` 的单链表。

#### Step-by-Step Operations on a Linked List 链表上的分步操作

1. **Creating the Linked List**:  
   **创建链表**：

   - Create nodes for each element.  
     为每个元素创建节点。
   - Link the nodes together: `3 -> 5 -> 7 -> 10`.  
     将节点链接在一起：`3 -> 5 -> 7 -> 10`。

2. **Traversing the List**:  
   **遍历链表**：

   - Start at the head (`3`) and follow the links to access each node in the sequence.  
     从头节点（`3`）开始，沿着链接访问序列中的每个节点。

3. **Inserting a Node**:  
   **插入节点**：

   - To insert `8` after `7`, create a new node for `8`, update the link of `7` to point to `8`, and link `8` to `10`.  
     要在 `7` 后插入 `8`，为 `8` 创建一个新节点，更新 `7` 的链接指向 `8`，并将 `8` 链接到 `10`。

   **Updated List**: `3 -> 5 -> 7 -> 8 -> 10`  
   **更新后的链表**：`3 -> 5 -> 7 -> 8 -> 10`

4. **Deleting a Node**:  
   **删除节点**：

   - To delete `5`, update the link of `3` to point directly to `7`, bypassing `5`.  
     要删除 `5`，更新 `3` 的链接直接指向 `7`，跳过 `5`。

   **Updated List**: `3 -> 7 -> 8 -> 10`  
   **更新后的链表**：`3 -> 7 -> 8 -> 10`

### Python Implementation of a Singly Linked List 单链表的Python实现

Here is the Python code to implement a simple singly linked list:  
以下是实现一个简单单链表的Python代码：

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        last = self.head
        while last.next:
            last = last.next
        last.next = new_node

    def delete(self, key):
        temp = self.head
        if temp and temp.data == key:
            self.head = temp.next
            temp = None
            return
        prev = None
        while temp and temp.data != key:
            prev = temp
            temp = temp.next
        if temp is None:
            return
        prev.next = temp.next
        temp = None

    def print_list(self):
        temp = self.head
        while temp:
            print(temp.data, end=" -> ")
            temp = temp.next
        print("None")

# Example linked list operations
llist = LinkedList()
llist.append(3)
llist.append(5)
llist.append(7)
llist.append(10)
llist.print_list()  # Output: 3 -> 5 -> 7 -> 10 -> None

llist.delete(5)
llist.print_list()  # Output: 3 -> 7 -> 10 -> None
```

This code will create a linked list with elements `3 -> 5 -> 7 -> 10`, then delete the node with value `5`, resulting in `3 -> 7 -> 10`.  
这段代码将创建一个包含元素 `3 -> 5 -> 7 -> 10` 的链表，然后删除值为 `5` 的节点，结果为 `3 -> 7 -> 10`。

### Analysis of Linked Lists 链表的分析

- **Time Complexity**:  
  **时间复杂度**：
  - Accessing an element: O(n), as you may need to traverse the entire list.  
    访问元素：O(n)，因为可能需要遍历整个链表。
  - Inserting or deleting at the beginning: O(1), as it involves updating only one or two pointers.  
    在开头插入或删除：O(1)，因为它只涉及更新一个或两个指针。
  - Inserting or deleting after a given node: O(1) once the node is found.  
    在给定节点之后插入或删除：找到节点后为 O(1)。

- **Space Complexity**: O(n), where `n` is the number of nodes in the linked list. Each node occupies memory for the data and a pointer to the next node.  
  **空间复杂度**：O(n)，其中 `n` 是链表中的节点数。每个节点占用存储数据和指向下一个节点的指针的内存。

- **Use Cases**: Linked lists are particularly useful for implementing dynamic data structures like stacks, queues, and for managing memory in operating systems. They are also ideal when frequent insertions and deletions are required, especially in scenarios where data size varies.  
  **使用案例**：链表在实现动态数据结构（如栈、队列）以及操作系统中的内存管理方面特别有用。它们在需要频繁插入和删除的场景中（尤其是在数据大小变化的情况下）非常理想。

### Example with a Doubly Linked List 示例：双链表

In a doubly linked list, each node contains references to both the next and the previous nodes, allowing traversal in both directions:  
在双链表中，每个节点包含对下一个节点和上一个节点的引用，允许双向遍历：

```
List: 1 <-> 2 <-> 3 <-> 4
```

### Conclusion 结论

A Linked List is a versatile and efficient data structure that is fundamental to many complex data structures and algorithms. Its dynamic nature allows for efficient memory usage and flexibility in handling

 varying data sizes. Linked lists are essential for scenarios where frequent insertions and deletions are required, and they form the backbone of many other data structures, such as stacks, queues, and more advanced structures like graphs and hash tables.  
链表是一种多功能且高效的数据结构，是许多复杂数据结构和算法的基础。其动态特性允许高效的内存使用和灵活处理不同数据大小。链表在需要频繁插入和删除的场景中至关重要，并且构成了许多其他数据结构的基础，如栈、队列以及更高级的结构如图和哈希表。

This method is a fundamental tool for software developers and computer scientists, enabling efficient management of dynamic data in various applications.  
这种方法是软件开发人员和计算机科学家的基本工具，能够在各种应用中高效管理动态数据。
