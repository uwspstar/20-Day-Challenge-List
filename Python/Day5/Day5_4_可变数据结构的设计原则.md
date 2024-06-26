# 可变数据结构的设计原则
In Python, methods that modify lists like `insert`, `remove`, or `sort` do not return any value; they return the default value `None`. This is a design principle for all mutable data structures in Python. 

在 Python 中，像 `insert`、`remove` 或 `sort` 这样修改列表的方法不会返回任何值；它们返回默认值 `None`。这是 Python 中所有可变数据结构的设计原则。

### Explanation | 解释

#### English
This behavior follows a common programming pattern called "Command-Query Separation" (CQS). According to this principle, methods that change the state of an object (commands) should return nothing (i.e., `None`) to signal that their primary operation is to perform a modification. This helps in preventing side effects during method chaining or unexpected behaviors in more complex data manipulations.

#### 中文
这种行为遵循一种常见的编程模式，称为“命令-查询分离”(CQS)。根据这一原则，改变对象状态的方法（命令）应该不返回任何东西（即 `None`），以表明它们的主要操作是进行修改。这有助于在方法链中防止副作用或在更复杂的数据操作中防止意外行为。

### Practical Examples | 实用示例

#### English
When you use the `sort()` method on a list, it rearranges the elements of the list in place and returns `None`. This indicates that the primary purpose of the method is to modify the list, not to produce a new value.

#### 中文
当你在列表上使用 `sort()` 方法时，它会就地重新排列列表的元素，并返回 `None`。这表明该方法的主要目的是修改列表，而不是产生一个新值。

```python
my_list = [3, 1, 2]
result = my_list.sort()
print(result)  # Outputs: None
print(my_list)  # Outputs: [1, 2, 3]
```

#### English
Similarly, the `remove()` method deletes an item from the list and returns `None`. This makes it clear that the function's role is to alter the list's content.

#### 中文
同样，`remove()` 方法从列表中删除一个项目并返回 `None`。这明确表明了函数的作用是更改列表的内容。

```python
my_list = ['a', 'b', 'c']
my_list.remove('b')
print(my_list)  # Outputs: ['a', 'c']
```

### Conclusion | 结论

Understanding that methods which modify Python's mutable data structures return `None` helps programmers avoid misusing return values and emphasizes the intent of these methods as operations that alter the state of the object rather than functions that compute and return new data values.

理解修改 Python 可变数据结构的方法返回 `None` 可以帮助程序员避免误用返回值，并强调这些方法的意图是改变对象状态的操作，而不是计算并返回新数据值的函数。
