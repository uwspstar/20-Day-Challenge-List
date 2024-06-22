# "immutable" and "mutable"

In programming, "immutable" and "mutable" are terms used to describe whether the state of an object can be changed after it is created.

在编程中，“不可变”和“可变”是用来描述对象创建后其状态是否可以改变的术语。

### Immutable
**Immutable** objects cannot be altered once they are created. This means that any changes to an object result in the creation of a new object. Examples in Python include tuples, strings, and frozensets.

### 不可变
**不可变**对象一旦创建就不能被修改。这意味着对对象的任何改变都会导致创建一个新对象。Python中的例子包括元组、字符串和冻结集。

### Mutable
**Mutable** objects can be changed after they are created. This allows modifications to the object without creating a new one. Examples in Python include lists, dictionaries, and sets.

### 可变
**可变**对象创建后可以改变。这允许对对象进行修改而不创建新对象。Python中的例子包括列表、字典和集合。

Here's a Python code example to demonstrate the concept:

这里有一个Python代码示例来演示这个概念：

```python
# Immutable example with a tuple
immutable_tuple = (1, 2, 3)
try:
    immutable_tuple[0] = 4  # Attempting to change an immutable tuple
except TypeError as e:
    print("Error:", e)

# Mutable example with a list
mutable_list = [1, 2, 3]
mutable_list[0] = 4  # Changing the first element of the list
print("Updated List:", mutable_list)
```

Here's a comparison table summarizing the differences:

这是一个总结差异的比较表：

| Aspect | Immutable | Mutable |
|--------|-----------|---------|
| Changeability | Cannot be changed after creation | Can be changed after creation |
| Examples | Tuple, String, Frozenset | List, Dictionary, Set |
| Performance | Generally faster to access | Slower to access but flexible |
| Use Case | Use when you need a constant data value | Use when you need to change the data over time |

| 方面     | 不可变       | 可变         |
|--------|-----------|---------|
| 可改变性 | 创建后不能改变 | 创建后可以改变 |
| 例子     | 元组、字符串、冻结集 | 列表、字典、集合 |
| 性能     | 通常访问更快 | 访问较慢但灵活 |
| 使用情况  | 需要常量数据值时使用 | 需要随时间改变数据时使用 |


### 与 immutable 字符串不同, 列表是 mutable 类型，其内容可以改变

In Python, data types are categorized into immutable and mutable types based on whether they can be modified after their creation. Here's a detailed look at which types are immutable and which are mutable:

在Python中，数据类型根据创建后是否可以修改分为不可变类型和可变类型。以下是哪些类型是不可变的，哪些类型是可变的详细介绍：

### Immutable Types (不可变类型)
Immutable types include:
不可变类型包括：

- **Integers (整数)**: Once an integer is created, its value cannot be changed.
- **Floating-point numbers (浮点数)**: Similar to integers, the value of a floating-point number is fixed upon creation.
- **Strings (字符串)**: Strings cannot be altered once they are created. Any operation that modifies a string actually creates a new string.
- **Tuples (元组)**: Tuples are collections that are ordered and unchangeable.
- **Frozensets (冻结集)**: These are just like sets but immutable.

### Mutable Types (可变类型)
Mutable types include:
可变类型包括：

- **Lists (列表)**: Lists can be modified in many ways — elements can be added, removed, or changed.
- **Dictionaries (字典)**: The contents of a dictionary can be altered at any time — elements can be added, removed, or modified.
- **Sets (集合)**: Sets are collections that can be modified by adding or removing items.

Here's a Python code example showing the immutability of a tuple and the mutability of a list:

这里有一个Python代码示例，展示了元组的不可变性和列表的可变性：

```python
# Immutable tuple
immutable_tuple = (1, 2, 3)
try:
    immutable_tuple[0] = 'a'  # Trying to change an immutable tuple
except TypeError as e:
    print("Immutable type error:", e)

# Mutable list
mutable_list = [1, 2, 3]
mutable_list[0] = 'a'  # Changing element of the list
print("Mutable list changed:", mutable_list)
```

And here is a comparison table:

这是一个比较表：

| Type | Mutable | Example | Modification Example |
|------|---------|---------|----------------------|
| Integer | No | `x = 5` | N/A |
| Float | No | `x = 5.5` | N/A |
| String | No | `x = "hello"` | N/A |
| Tuple | No | `x = (1, 2, 3)` | N/A |
| Frozenset | No | `x = frozenset([1, 2, 3])` | N/A |
| List | Yes | `x = [1, 2, 3]` | `x[0] = 'a'` |
| Dictionary | Yes | `x = {'key': 'value'}` | `x['new_key'] = 'new_value'` |
| Set | Yes | `x = {1, 2, 3}` | `x.add(4)` |

| 类型     | 可变性 | 示例                  | 修改示例                       |
|------|------|---------------------|-------------------------------|
| 整数     | 否   | `x = 5`             | 不适用                         |
| 浮点数    | 否   | `x = 5.5`           | 不适用                         |
| 字符串    | 否   | `x = "hello"`       | 不适用                         |
| 元组     | 否   | `x = (1, 2, 3)`     | 不适用                         |
| 冻结集    | 否   | `x = frozenset([1, 2, 3])` | 不适用                 |
| 列表     | 是   | `x = [1, 2, 3]`     | `x[0] = 'a'`                  |
| 字典     | 是   | `x = {'key': 'value'}` | `x['new_key'] = 'new_value'` |
| 集合     | 是   | `x = {1, 2, 3}`     | `x.add(4)`                    |

That's correct! In Python, when you assign a list to a new variable, you're not actually creating a new independent copy of the list. Instead, the new variable refers to the same list. Changes made through any variable referencing this list will be visible through all variables referencing the same list.

没错！在Python中，当你将一个列表赋值给一个新变量时，你实际上并没有创建一个新的独立的列表副本。相反，新变量引用了相同的列表。通过引用这个列表的任何变量所做的更改都会通过所有引用同一个列表的变量看到。

Here's a Python code example to demonstrate this behavior:

这里有一个Python代码示例来演示这种行为：

```python
original_list = [1, 2, 3]
assigned_list = original_list  # Assigning the original list to a new variable

assigned_list[0] = 99  # Changing an element via the assigned variable

print("Original List:", original_list)  # Output will show the changed list
print("Assigned List:", assigned_list)  # Output will be the same as the original list
```

The output of this code will show that both `original_list` and `assigned_list` have been updated to `[99, 2, 3]`. This is because both variables refer to the same list object in memory.

这段代码的输出将显示`original_list`和`assigned_list`都被更新为`[99, 2, 3]`。这是因为两个变量都引用了内存中同一个列表对象。

