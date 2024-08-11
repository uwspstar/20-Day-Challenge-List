# Doubly Linked List 双向链表

A Doubly Linked List is an extension of the singly linked list where each node contains two references: one to the next node and one to the previous node. This structure allows for traversal in both directions (forward and backward), providing greater flexibility in certain operations, such as reverse traversal, easier node deletion, and insertion. Doubly linked lists are particularly useful in scenarios where frequent insertions and deletions are required at both ends of the list.  
双向链表是单向链表的扩展，其中每个节点包含两个引用：一个指向下一个节点，另一个指向前一个节点。这种结构允许双向遍历（前向和后向），在某些操作中提供了更大的灵活性，例如反向遍历、更容易的节点删除和插入。双向链表在需要在链表两端频繁插入和删除的场景中特别有用。

### How Doubly Linked Lists Work 双向链表如何工作

1. **Node Structure**: Each node in a doubly linked list consists of three parts: the data, a reference to the next node, and a reference to the previous node.  
   **节点结构**：双向链表中的每个节点由三部分组成：数据、指向下一个节点的引用和指向前一个节点的引用。

2. **Head and Tail Nodes**: The first node in the list is called the head, and the last node is called the tail. The head's previous reference is `null` (or `None` in Python), and the tail's next reference is `null`.  
   **头节点和尾节点**：链表中的第一个节点称为头节点，最后一个节点称为尾节点。头节点的前向引用为 `null`（或Python中的 `None`），尾节点的后向引用为 `null`。

3. **Traversal**: Nodes can be traversed in both forward and backward directions by following the next and previous references, respectively.  
   **遍历**：可以通过分别跟随下一个和前一个引用来前向和后向遍历节点。

4. **Insertion and Deletion**: Inserting or deleting nodes in a doubly linked list requires updating both the next and previous references of the adjacent nodes. This allows for more efficient operations compared to a singly linked list, especially when deleting a node.  
   **插入和删除**：在双向链表中插入或删除节点需要更新相邻节点的下一个和前一个引用。这使得操作比单链表更高效，尤其是在删除节点时。

5. **Circular Doubly Linked List**: In a circular doubly linked list, the tail's next reference points to the head, and the head's previous reference points to the tail, forming a circular structure.  
   **循环双向链表**：在循环双向链表中，尾节点的下一个引用指向头节点，头节点的前一个引用指向尾节点，形成一个循环结构。

### Example of a Doubly Linked List 双向链表的示例

Consider a doubly linked list containing the elements `3 <-> 5 <-> 7 <-> 10`.  
考虑一个包含元素 `3 <-> 5 <-> 7 <-> 10` 的双向链表。

#### Step-by-Step Operations on a Doubly Linked List 双向链表上的分步操作

1. **Creating the Doubly Linked List**:  
   **创建双向链表**：

   - Create nodes for each element.  
     为每个元素创建节点。
   - Link the nodes together: `3 <-> 5 <-> 7 <-> 10`.  
     将节点链接在一起：`3 <-> 5 <-> 7 <-> 10`。

2. **Traversing the List Forward**:  
   **前向遍历链表**：

   - Start at the head (`3`) and follow the next references to access each node in the sequence.  
     从头节点（`3`）开始，沿着下一个引用访问序列中的每个节点。

3. **Traversing the List Backward**:  
   **后向遍历链表**：

   - Start at the tail (`10`) and follow the previous references to access each node in reverse order.  
     从尾节点（`10`）开始，沿着前一个引用以相反顺序访问每个节点。

4. **Inserting a Node**:  
   **插入节点**：

   - To insert `8` after `7`, create a new node for `8`, update the next reference of `7` to point to `8`, the previous reference of `8` to point to `7`, and link `8` to `10`.  
     要在 `7` 后插入 `8`，为 `8` 创建一个新节点，更新 `7` 的下一个引用指向 `8`，`8` 的前一个引用指向 `7`，并将 `8` 链接到 `10`。

   **Updated List**: `3 <-> 5 <-> 7 <-> 8 <-> 10`  
   **更新后的链表**：`3 <-> 5 <-> 7 <-> 8 <-> 10`

5. **Deleting a Node**:  
   **删除节点**：

   - To delete `5`, update the next reference of `3` to point to `7`, and the previous reference of `7` to point to `3`.  
     要删除 `5`，更新 `3` 的下一个引用指向 `7`，并更新 `7` 的前一个引用指向 `3`。

   **Updated List**: `3 <-> 7 <-> 8 <-> 10`  
   **更新后的链表**：`3 <-> 7 <-> 8 <-> 10`

### Python Implementation of a Doubly Linked List 双向链表的Python实现

Here is the Python code to implement a simple doubly linked list:  
以下是实现一个简单双向链表的Python代码：

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:
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
        new_node.prev = last

    def delete(self, key):
        temp = self.head
        if temp and temp.data == key:
            self.head = temp.next
            if self.head:
                self.head.prev = None
            temp = None
            return
        while temp and temp.data != key:
            temp = temp.next
        if temp is None:
            return
        if temp.next:
            temp.next.prev = temp.prev
        if temp.prev:
            temp.prev.next = temp.next
        temp = None

    def print_list_forward(self):
        temp = self.head
        while temp:
            print(temp.data, end=" <-> ")
            temp = temp.next
        print("None")

    def print_list_backward(self):
        temp = self.head
        if not temp:
            return
        while temp.next:
            temp = temp.next
        while temp:
            print(temp.data, end=" <-> ")
            temp = temp.prev
        print("None")

# Example doubly linked list operations
dllist = DoublyLinkedList()
dllist.append(3)
dllist.append(5)
dllist.append(7)
dllist.append(10)
dllist.print_list_forward()  # Output: 3 <-> 5 <-> 7 <-> 10 <-> None
dllist.print_list_backward()  # Output: 10 <-> 7 <-> 5 <-> 3 <-> None

dllist.delete(5)
dllist.print_list_forward()  # Output: 3 <-> 7 <-> 10 <-> None
dllist.print_list_backward()  # Output: 10 <-> 7 <-> 3 <-> None
```

This code will create a doubly linked list with elements `3 <-> 5 <-> 7 <-> 10`, then delete the node with value `5`, resulting in `3 <-> 7 <-> 10`.  
这段代码将创建一个包含元素 `3 <-> 5 <-> 7 <-> 10` 的双向链表，然后删除值为 `5` 的节点，结果为 `3 <-> 7 <-> 10`。

### Analysis of Doubly Linked Lists 双向链表的分析

- **Time Complexity**:  
  **时间复杂度**：
  - Accessing an element: O(n), as you may need to traverse the entire list.  
    访问元素：O(n)，因为可能需要遍历整个链表。
  - Inserting or deleting at the beginning or end: O(1), as it involves updating only one or two pointers.  
    在开头或末尾插入或删除：O(1)，因为它只涉及更新一个或两个指针。
  - Inserting or deleting after a given node: O

(1) once the node is found.  
    在给定节点之后插入或删除：找到节点后为 O(1)。

- **Space Complexity**: O(n), where `n` is the number of nodes in the linked list. Each node occupies memory for the data and two pointers (next and previous).  
  **空间复杂度**：O(n)，其中 `n` 是链表中的节点数。每个节点占用存储数据和两个指针（下一个和前一个）的内存。

- **Use Cases**: Doubly linked lists are particularly useful for implementing advanced data structures like deques, where elements can be efficiently added or removed from both ends. They are also used in scenarios requiring bidirectional traversal, such as in navigation systems, text editors (for undo/redo operations), and in memory management.  
  **使用案例**：双向链表在实现高级数据结构（如双端队列）时特别有用，可以从两端高效地添加或删除元素。它们还用于需要双向遍历的场景，例如导航系统、文本编辑器（用于撤销/重做操作）和内存管理。

### Example with a Circular Doubly Linked List 示例：循环双向链表

In a circular doubly linked list, the tail's next reference points to the head, and the head's previous reference points to the tail, forming a circular structure:  
在循环双向链表中，尾节点的下一个引用指向头节点，头节点的前一个引用指向尾节点，形成一个循环结构：

```
List: 1 <-> 2 <-> 3 <-> 4 <-> 1 (back to head)
```

### Conclusion 结论

A Doubly Linked List is a versatile and powerful data structure that provides bidirectional traversal, making it ideal for scenarios where elements need to be accessed or modified from both ends. Its structure allows for efficient insertion, deletion, and traversal operations, particularly in applications that require flexible data manipulation. Doubly linked lists are foundational to many advanced data structures and algorithms, making them an essential tool in computer science.  
双向链表是一种多功能且强大的数据结构，提供双向遍历，使其非常适合需要从两端访问或修改元素的场景。其结构允许高效的插入、删除和遍历操作，尤其是在需要灵活数据操作的应用中。双向链表是许多高级数据结构和算法的基础，使其成为计算机科学中的一种重要工具。

This method is crucial for software developers and computer scientists, enabling efficient management of data in dynamic and complex applications.  
这种方法对于软件开发人员和计算机科学家至关重要，能够在动态和复杂的应用中高效管理数据。
