# 数据结构：队列与栈的介绍及其实现 Data Structures: Introduction to Queues and Stacks and Their Implementations

## 1. 队列的介绍  
## 1. Introduction to Queues

### 队列是什么？  
### What is a Queue?

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle. This means that the first element added to the queue will be the first one to be removed. Queues are widely used in scenarios where tasks need to be processed in the order they arrive, such as print job management, task scheduling, and breadth-first search (BFS) in graphs.

队列是一种线性数据结构，遵循先进先出 (FIFO) 原则。这意味着第一个添加到队列的元素将是第一个被移除的元素。队列广泛用于需要按到达顺序处理任务的场景，如打印任务管理、任务调度和图中的广度优先搜索 (BFS)。

### 队列的基本操作  
### Basic Operations of a Queue

- **Enqueue**: Adds an element to the end of the queue.
- **Dequeue**: Removes an element from the front of the queue.
- **Peek/Front**: Retrieves the front element of the queue without removing it.
- **IsEmpty**: Checks if the queue is empty.

- **入队 (Enqueue)**：将元素添加到队列的末尾。
- **出队 (Dequeue)**：从队列的前面移除一个元素。
- **查看队头 (Peek/Front)**：检索队列的头部元素，但不移除它。
- **是否为空 (IsEmpty)**：检查队列是否为空。

## 2. 栈的介绍  
## 2. Introduction to Stacks

### 栈是什么？  
### What is a Stack?

A stack is a linear data structure that follows the Last-In-First-Out (LIFO) principle. This means that the last element added to the stack will be the first one to be removed. Stacks are used in various applications, including expression evaluation, backtracking algorithms, and the undo mechanism in text editors.

栈是一种线性数据结构，遵循后进先出 (LIFO) 原则。这意味着最后添加到栈中的元素将是第一个被移除的元素。栈用于各种应用场景，包括表达式求值、回溯算法和文本编辑器中的撤销机制。

### 栈的基本操作  
### Basic Operations of a Stack

- **Push**: Adds an element to the top of the stack.
- **Pop**: Removes an element from the top of the stack.
- **Peek/Top**: Retrieves the top element of the stack without removing it.
- **IsEmpty**: Checks if the stack is empty.

- **压栈 (Push)**：将元素添加到栈的顶部。
- **出栈 (Pop)**：从栈的顶部移除一个元素。
- **查看栈顶 (Peek/Top)**：检索栈顶元素，但不移除它。
- **是否为空 (IsEmpty)**：检查栈是否为空。

## 3. 队列的链表实现和数组实现  
## 3. Queue Implementation Using Linked List and Array

### 使用链表实现队列  
### Queue Implementation Using Linked List

A queue can be implemented using a linked list where each node represents an element in the queue. The `head` of the linked list represents the front of the queue, and the `tail` represents the rear of the queue.

队列可以使用链表实现，其中每个节点表示队列中的一个元素。链表的 `head` 表示队列的前端，`tail` 表示队列的后端。

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class QueueLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def enqueue(self, value):
        new_node = Node(value)
        if self.tail:
            self.tail.next = new_node
        self.tail = new_node
        if not self.head:
            self.head = new_node

    def dequeue(self):
        if not self.head:
            return None
        value = self.head.value
        self.head = self.head.next
        if not self.head:
            self.tail = None
        return value

    def peek(self):
        return self.head.value if self.head else None

    def is_empty(self):
        return self.head is None
```

**解释**：
- **enqueue**：添加新节点到队列的尾部。
- **dequeue**：移除并返回队列前端的节点。
- **peek**：查看队列前端的节点。
- **is_empty**：检查队列是否为空。

**Explanation**:
- **enqueue**: Adds a new node to the end of the queue.
- **dequeue**: Removes and returns the node at the front of the queue.
- **peek**: Retrieves the node at the front of the queue.
- **is_empty**: Checks if the queue is empty.

### 使用数组实现队列  
### Queue Implementation Using Array

A queue can also be implemented using an array. The `enqueue` operation adds an element to the end of the array, and the `dequeue` operation removes an element from the front.

队列也可以使用数组实现。`enqueue` 操作将元素添加到数组的末尾，而 `dequeue` 操作从数组的前端移除元素。

```python
class QueueArray:
    def __init__(self):
        self.queue = []

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):
        if self.is_empty():
            return None
        return self.queue.pop(0)

    def peek(self):
        return self.queue[0] if not self.is_empty() else None

    def is_empty(self):
        return len(self.queue) == 0
```

**解释**：
- **enqueue**：将元素添加到数组的末尾。
- **dequeue**：移除并返回数组前端的元素。
- **peek**：查看数组前端的元素。
- **is_empty**：检查队列是否为空。

**Explanation**:
- **enqueue**: Adds an element to the end of the array.
- **dequeue**: Removes and returns the element at the front of the array.
- **peek**: Retrieves the element at the front of the array.
- **is_empty**: Checks if the queue is empty.

## 4. 栈的数组实现  
## 4. Stack Implementation Using Array

A stack can be implemented using an array where the `push` operation adds an element to the end of the array (top of the stack), and the `pop` operation removes the element from the end.

栈可以使用数组实现，其中 `push` 操作将元素添加到数组的末尾（栈顶），`pop` 操作从数组末尾移除元素。

```python
class StackArray:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if self.is_empty():
            return None
        return self.stack.pop()

    def peek(self):
        return self.stack[-1] if not self.is_empty() else None

    def is_empty(self):
        return len(self.stack) == 0
```

**解释**：
- **push**：将元素添加到数组的末尾（栈顶）。
- **pop**：移除并返回数组末尾的元素（栈顶）。
- **peek**：查看数组末尾的元素（栈顶）。
- **is_empty**：检查栈是否为空。

**Explanation**:
- **push**: Adds an element to the end of the array (top of the stack).
- **pop**: Removes and returns the element at the end of the array (top of the stack).
- **peek**: Retrieves the element at the end of the array (top of the stack).
- **is_empty**: Checks if the stack is empty.

## 5. 环形队列用数组实现  
## 5. Circular Queue Implementation Using Array

A circular queue is a more efficient implementation of a queue using an array, where the end of the array wraps around to the beginning. This avoids the need to shift elements and allows the queue to efficiently utilize space.

环形队列是一种更高效的队列实现方式，使用数组，其中数组的末尾环绕到开头。这避免了需要移动元素，并允许队列有效利用空间。

### 实现代码
### Implementation Code

```python
class CircularQueue:
    def __init__(self, k):
        self.queue = [None] * k
        self.max_size = k
        self.front = 0
        self.rear = 0
        self.size = 0

    def enqueue(self, value):
        if self.is_full():
            return False
        self.queue[self.rear] = value
        self.rear = (self.rear + 1) % self.max_size
        self.size += 1
        return True

    def dequeue(self):
        if self.is_empty():
            return None
        value = self.queue[self.front]
        self.queue[self.front] = None
        self.front = (self.front + 1) % self.max_size
        self.size -= 1
        return value



    def peek(self):
        if self.is_empty():
            return None
        return self.queue[self.front]

    def is_empty(self):
        return self.size == 0

    def is_full(self):
        return self.size == self.max_size
```

**解释**：
- **enqueue**：将元素添加到队列的 `rear` 位置，并更新 `rear` 指针，使用模运算确保环绕。
- **dequeue**：从队列的 `front` 位置移除元素，并更新 `front` 指针，使用模运算确保环绕。
- **peek**：查看 `front` 位置的元素。
- **is_empty**：检查队列是否为空。
- **is_full**：检查队列是否已满。

**Explanation**:
- **enqueue**: Adds an element to the `rear` position of the queue and updates the `rear` pointer, using modulo to ensure wrap-around.
- **dequeue**: Removes the element from the `front` position of the queue and updates the `front` pointer, using modulo to ensure wrap-around.
- **peek**: Retrieves the element at the `front` position.
- **is_empty**: Checks if the queue is empty.
- **is_full**: Checks if the queue is full.

## 总结  
## Conclusion

Understanding the implementation of fundamental data structures like queues and stacks is essential for solving various computational problems. By implementing these structures using both arrays and linked lists, and by exploring more advanced concepts like circular queues, developers can build efficient and effective solutions tailored to specific scenarios.

理解队列和栈等基本数据结构的实现对于解决各种计算问题至关重要。通过使用数组和链表实现这些结构，并探索诸如环形队列等更高级的概念，开发人员可以构建针对特定场景的高效解决方案。
