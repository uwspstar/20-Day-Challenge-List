# 栈 (Stack)

## Definition
栈是一种后进先出 (LIFO, Last In First Out) 的数据结构。即最后被添加的元素最先被移除。栈常用于管理函数调用、表达式求值、回溯算法等。

## Key Concepts
- **入栈 (Push)**: 将元素添加到栈顶。
- **出栈 (Pop)**: 移除栈顶元素。
- **栈顶 (Top)**: 当前栈中最上面的元素。
- **栈的空检查 (Is Empty)**: 检查栈是否为空。
  
## 栈的主要操作
1. **Push**: 将元素添加到栈顶。
2. **Pop**: 移除并返回栈顶元素。
3. **Peek/Top**: 返回栈顶元素，但不移除它。
4. **IsEmpty**: 检查栈是否为空。

## 栈的适用场景
- 表达式求值 (如后缀表达式)。
- 递归函数的调用管理。
- 深度优先搜索 (DFS)。
- 括号匹配和语法分析。

## Python 栈实现模板
```python
class Stack:
    def __init__(self):
        self.items = []  # 初始化空栈

    def is_empty(self):
        return len(self.items) == 0  # 检查栈是否为空

    def push(self, item):
        self.items.append(item)  # 入栈

    def pop(self):
        if not self.is_empty():
            return self.items.pop()  # 出栈
        raise IndexError("pop from an empty stack")  # 处理空栈出栈错误

    def peek(self):
        if not self.is_empty():
            return self.items[-1]  # 返回栈顶元素
        raise IndexError("peek from an empty stack")  # 处理空栈查看错误

    def size(self):
        return len(self.items)  # 返回栈的大小
```

## Tips
- 使用栈时要注意栈的大小，以避免栈溢出 (stack overflow)。
- 栈的空间复杂度为 O(n)，其中 n 是栈中元素的数量。

## Warning
- 在递归深度过大时，可能会导致栈溢出。在这种情况下，可以考虑使用循环代替递归。

## Complexity Analysis
- **时间复杂度**: O(1) 对于入栈和出栈操作。
- **空间复杂度**: O(n)，用于存储栈中元素。

---

If you have any questions or need further modifications, feel free to ask!
