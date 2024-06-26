# 数据结构
- https://docs.python.org/zh-cn/3/tutorial/datastructures.html#

在计算机科学中，数据结构是存储、组织和管理数据的方式，用于有效地访问和修改数据。Python作为一种高级编程语言，内置了多种强大的数据结构，它们使得数据操作和处理更加便捷和高效。这里将详细介绍Python中的主要数据结构，包括它们的特点、用途以及如何在Python中使用它们。

### Python内置的主要数据结构

1. **列表（List）**
   - **特点**：列表是可变的，能够存储不同类型的元素，支持动态大小调整。
   - **用途**：适用于需要顺序访问、添加、移除和替换元素的场合。
   - **示例**：
     ```python
     # 创建和使用列表
     my_list = [1, 2, 3, 'hello']
     my_list.append(4)  # 添加元素
     print(my_list)  # 输出: [1, 2, 3, 'hello', 4]
     ```

2. **元组（Tuple）**
   - **特点**：元组是不可变的，一旦创建就不能更改其内容。
   - **用途**：适用于存储不应更改的数据，如函数从多个值返回时。
   - **示例**：
     ```python
     # 创建和使用元组
     coordinates = (10, 20)
     print(coordinates)  # 输出: (10, 20)
     ```

3. **字典（Dictionary）**
   - **特点**：字典存储键值对，键必须是唯一的且通常是不可变类型，如字符串或元组。
   - **用途**：适用于通过键快速访问、添加、修改和删除数据的场合。
   - **示例**：
     ```python
     # 创建和使用字典
     capitals = {'France': 'Paris', 'Italy': 'Rome'}
     capitals['Spain'] = 'Madrid'  # 添加新元素
     print(capitals)  # 输出: {'France': 'Paris', 'Italy': 'Rome', 'Spain': 'Madrid'}
     ```

4. **集合（Set）**
   - **特点**：集合是无序的，元素唯一，自动去除重复项。
   - **用途**：适用于去重、集合运算（如并集、交集）等。
   - **示例**：
     ```python
     # 创建和使用集合
     my_set = {1, 2, 3, 3, 4}
     print(my_set)  # 输出: {1, 2, 3, 4}
     ```

5. **范围（Range）**
   - **特点**：范围是一个不可变的序列类型，通常用于循环。
   - **用途**：适用于需要执行固定次数循环的场合。
   - **示例**：
     ```python
     # 使用范围
     for i in range(5):
         print(i)  # 依次打印 0, 1, 2, 3, 4
     ```

### 如何选择合适的数据结构

选择合适的数据结构依赖于具体的应用需求：
- **访问模式**：需要频繁访问、搜索还是修改数据？
- **数据唯一性**：数据是否需要保持唯一性？
- **内存效率**：是否需要优化数据结构的内存使用？
- **操作效率**：哪些操作（插入、删除、访问）最为频繁？

理解和掌握这些数据结构对于编写高效、易于维护的Python程序至关重要。通过选择适合特定需求的数据结构，可以显著提高程序的性能和可用性。
In Python, the terms "list" and "array" refer to two distinct types of data structures that serve different purposes and are used in different contexts. Understanding the differences between these two can help you choose the right structure for your data and optimize your code for specific tasks.

### Python List

**Definition:**
A Python list is a versatile, dynamic data structure provided by Python as a built-in option. It can store elements of different types and sizes.

**Characteristics:**
- **Dynamic Type**: Lists can store any type of object: numbers, strings, other lists, etc.
- **Dynamic Size**: Lists can grow or shrink dynamically as items are added or removed.
- **Memory Overhead**: Lists consume more memory due to the flexibility they provide in storing any type of object.

**Usage:**
Lists are used for general-purpose storage where the flexibility of the data type and size is important. They are especially useful when you don't know the size of the data in advance or when you need to store heterogeneous data.

**Example:**
```python
my_list = [1, "Hello", 3.14, [1, 2, 3]]
my_list.append("Python")
print(my_list)  # Output: [1, "Hello", 3.14, [1, 2, 3], "Python"]
```

### Python Array (array module)

**Definition:**
Arrays in Python, provided by the `array` module, are a compact, more performance-oriented container that stores items of the same type and size.

**Characteristics:**
- **Homogeneous Type**: All elements in an array must be of the same type.
- **Efficiency**: Arrays are more memory efficient than lists because they tightly pack their elements.
- **Less Flexibility**: Arrays can only hold elements of specified data types (like `int`, `float`).

**Usage:**
Arrays are preferred when you need to store large amounts of data of the same type, such as numerical data in scientific computing or when performing operations that benefit from compact, homogeneous storage for efficiency.

**Example:**
```python
import array
my_array = array.array('i', [1, 2, 3, 4])
my_array.append(5)
print(my_array)  # Output: array('i', [1, 2, 3, 4, 5])
```

### NumPy Array

**Definition:**
The NumPy array, provided by the NumPy library, is an even more optimized version of an array with powerful capabilities for scientific computing.

**Characteristics:**
- **High Performance**: Optimized for numerical computations and capable of handling multi-dimensional data efficiently.
- **Advanced Functionality**: Supports a wide range of mathematical and statistical operations directly on arrays.

**Usage:**
NumPy arrays are the backbone of data manipulation and scientific computing in Python. They are essential for handling vectorized operations, matrix manipulations, and advanced data analyses.

**Example:**
```python
import numpy as np
my_numpy_array = np.array([1, 2, 3, 4, 5])
print(my_numpy_array + 10)  # Output: [11, 12, 13, 14, 15]
```

### Conclusion

The choice between lists, arrays from the `array` module, and NumPy arrays should be based on your specific needs:
- Use **lists** for general-purpose data storage when data type and size flexibility are important.
- Use **arrays from the `array` module** when you need efficient compact storage for large quantities of homogeneous data.
- Use **NumPy arrays** for high-performance, scientific, and numerical computations.

选择列表、`array` 模块中的数组或 NumPy 数组应基于您的具体需求：
- 当数据类型和大小的灵活性很重要时，使用 **列表** 进行通用数据存储。
- 当您需要为大量同质数据提供高效紧凑的存储时，使用 **`array` 模块中的数组**。
- 对于高性能、科学和数值计算，使用 **NumPy 数组**。

In Python, sets are a collection type that store unordered and unique elements. They are particularly useful for performing mathematical set operations like unions, intersections, and differences. You can create sets using either curly braces `{}` or the `set()` function. However, to create an empty set, you must use `set()` since using `{}` by itself creates an empty dictionary, not a set.

在 Python 中，集合是一种存储无序且唯一元素的集合类型。它们特别适用于执行数学集合操作，如并集、交集和差集。您可以使用花括号 `{}` 或 `set()` 函数创建集合。然而，要创建一个空集合，您必须使用 `set()`，因为单独使用 `{}` 会创建一个空字典，而不是集合。

### Creating Sets with Braces and `set()` | 使用花括号和 `set()` 创建集合

#### English
- **Using Curly Braces `{}`**: This method is straightforward for creating sets with initial elements. Simply place the elements inside curly braces, separated by commas.
- **Using `set()` Function**: This method is versatile and can be used to create both empty sets and to convert other iterable types (like lists or tuples) into a set, thus removing any duplicate elements.

#### 中文
- **使用花括号 `{}`**：这种方法用于创建具有初始元素的集合非常简单。只需将元素放入花括号中，用逗号分隔。
- **使用 `set()` 函数**：这种方法非常灵活，可用于创建空集合和将其他可迭代类型（如列表或元组）转换为集合，从而去除任何重复元素。

### Examples | 示例

#### Creating a Non-empty Set | 创建非空集合

```python
# Using curly braces
fruits = {'apple', 'banana', 'cherry'}
print(fruits)  # Output might be in any order: {'banana', 'cherry', 'apple'}

# Converting a list to a set
fruit_list = ['apple', 'banana', 'cherry', 'apple']
fruit_set = set(fruit_list)
print(fruit_set)  # Outputs: {'banana', 'cherry', 'apple'}
```

#### Creating an Empty Set | 创建空集合

```python
# Correct way to create an empty set
empty_set = set()
print(empty_set)  # Output: set()

# Incorrect way using curly braces results in an empty dictionary
not_a_set = {}
print(type(not_a_set))  # Output: <class 'dict'>
```

### Conclusion | 结论

It's important to distinguish between the use of curly braces and the `set()` function in Python. While both can create populated sets, only the `set()` function can create an empty set. This distinction helps prevent bugs and misunderstandings, especially when transitioning between different types of collections in Python.

区分 Python 中使用花括号和 `set()` 函数的方式非常重要。虽然两者都可以创建有元素的集合，但只有 `set()` 函数可以创建空集合。这种区别有助于防止错误和误解，特别是在 Python 中不同类型的集合之间进行转换时。

In programming, lists in Python can be adapted to simulate more complex data structures such as stacks and queues. Understanding how to implement these structures using Python lists is crucial for solving various computational problems efficiently.

在编程中，Python 的列表可以被适配来模拟更复杂的数据结构，如堆栈和队列。理解如何使用 Python 列表实现这些结构对于有效解决各种计算问题至关重要。

### Using a List to Implement a Stack | 用列表实现堆栈

#### English
A stack is a Last In First Out (LIFO) data structure. It can be easily implemented with a Python list since lists provide native support for adding and removing elements from the end with `append()` and `pop()` methods, which operate in constant time.

#### 中文
堆栈是一种后进先出（LIFO）的数据结构。它可以很容易地用 Python 列表实现，因为列表天然支持使用 `append()` 和 `pop()` 方法从末端添加和移除元素，这些操作是常数时间的。

**Example | 示例:**

```python
stack = []
stack.append('a')  # Push 'a' onto the stack
stack.append('b')  # Push 'b' onto the stack
stack.append('c')  # Push 'c' onto the stack
print(stack.pop())  # Pop 'c' from the stack
print(stack)        # Output: ['a', 'b']
```

### Using a List to Implement a Queue | 用列表实现队列

#### English
A queue is a First In First Out (FIFO) data structure. While lists can be used to implement a queue, the operations are not efficient as removing elements from the beginning of a list is a linear time operation. However, Python’s `collections.deque` is optimized for fast fixed-time appending and popping from both ends, making it more suitable for queues.

#### 中文
队列是一种先进先出（FIFO）的数据结构。虽然列表可以用来实现队列，但操作效率不高，因为从列表开始处移除元素是一个线性时间操作。然而，Python 的 `collections.deque` 为从两端快速固定时间的附加和弹出进行了优化，使其更适合队列。

**Example (using `list`, not recommended for large data) | 示例（使用 `list`，不推荐用于大数据）:**

```python
queue = []
queue.append('a')  # Enqueue 'a'
queue.append('b')  # Enqueue 'b'
queue.append('c')  # Enqueue 'c'
print(queue.pop(0))  # Dequeue 'a'
print(queue)         # Output: ['b', 'c']
```

**Better Example (using `deque`) | 更好的示例（使用 `deque`）:**

```python
from collections import deque
queue = deque()
queue.append('a')  # Enqueue 'a'
queue.append('b')  # Enqueue 'b'
queue.append('c')  # Enqueue 'c'
print(queue.popleft())  # Dequeue 'a'
print(queue)            # Output: deque(['b', 'c'])
```

### Conclusion | 结论

Using Python lists to implement stacks is straightforward and efficient. However, for queues, it's better to use `collections.deque` due to its performance benefits, especially when dealing with large datasets or operations that require frequent insertions and deletions from both ends of the data structure.

使用 Python 列表实现堆栈是直接和高效的。然而，对于队列，由于其性能优势，最好使用 `collections.deque`，特别是在处理大型数据集或需要频繁在数据结构的两端插入和删除的操作时。

In Python, dictionaries are fundamental data structures that map immutable keys to corresponding values. This makes dictionaries incredibly versatile and useful for various applications where quick lookup and data organization are needed. Understanding the types of objects that can be used as keys in dictionaries is crucial for effective Python programming.

在 Python 中，字典是基本的数据结构，用于将不可变键映射到相应的值。这使得字典在需要快速查找和数据组织的各种应用中非常灵活和有用。了解可以作为字典键的对象类型对于有效的 Python 编程至关重要。

### Dictionary Keys | 字典键

#### English
Dictionaries use keys for indexing; these keys can be any immutable type. Strings and numbers can always be used as keys because of their immutable nature. If a tuple contains only strings, numbers, or other tuples, then it can also serve as a key. However, if a tuple contains any mutable object, either directly or indirectly, it cannot be used as a key. Lists cannot be used as keys because they can be modified in place using methods like `append()`, `extend()`, indexing assignments, or slicing.

#### 中文
字典使用键进行索引；这些键可以是任何不可变类型。由于字符串和数字的不可变性，它们总是可以作为键使用。如果一个元组只包含字符串、数字或其他元组，那么它也可以作为键。然而，如果一个元组直接或间接地包含任何可变对象，则不能用作键。列表不能用作键，因为它们可以使用 `append()`、`extend()`、索引赋值或切片等方法进行原地修改。

### Why Immutability Matters | 为什么不变性很重要

#### English
The requirement for keys to be immutable in dictionaries stems from the need to have a consistent hash value for each key. A hash value is used internally by the dictionary to quickly locate the key-value pair. If a key’s value can change, its hash value can also change, which would compromise the integrity of the dictionary’s structure, leading to errors or incorrect data retrieval.

#### 中文
字典中键必须是不可变的要求源于每个键需要具有一致的哈希值的需求。哈希值在字典内部用于快速定位键值对。如果键的值可以改变，它的哈希值也可以改变，这将破坏字典结构的完整性，导致错误或不正确的数据检索。

### Examples of Valid and Invalid Dictionary Keys | 有效和无效字典键的示例

#### English
Here are some examples to illustrate valid and invalid keys in Python dictionaries:

```python
# Valid dictionary keys
valid_dict = {
    "name": "Alice",
    42: "The answer",
    (1, 2, 3): "Tuple with immutable elements"
}

# Invalid dictionary key example (because it includes a list)
try:
    invalid_dict = {
        (1, 2, [3, 4]): "Tuple with a list"
    }
except TypeError as e:
    print(f"Error: {e}")
```

#### 中文
这里有一些示例来说明 Python 字典中有效和无效的键：

```python
# 有效的字典键
valid_dict = {
    "name": "Alice",
    42: "答案",
    (1, 2, 3): "包含不可变元素的元组"
}

# 无效的字典键示例（因为它包含了一个列表）
try:
    invalid_dict = {
        (1, 2, [3, 4]): "包含列表的元组"
    }
except TypeError as e:
    print(f"错误：{e}")
```

### Conclusion | 结论

Using appropriate types as dictionary keys is essential for maintaining the functionality and reliability of dictionary operations in Python. Always ensure that keys are immutable to avoid unexpected behaviors and errors in your programs.

在 Python 中，使用适当的类型作为字典键对于保持字典操作的功能性和可靠性至关重要。始终确保键是不可变的，以避免程序中出现意外行为和错误。
