# 列表是可变序列

Python supports a variety of compound data types that allow the combination of different values. Among these, the most commonly used is the **list**.

Python 支持多种复合数据类型，可以将不同的值组合在一起。其中，最常用的是**列表**。

### Lists in Python

Lists are mutable sequences, which means they can be modified after their creation. They can contain items of different types, including other lists, allowing for the creation of nested structures.

### Python 中的列表

列表是可变序列，这意味着它们可以在创建后被修改。它们可以包含不同类型的项，包括其他列表，允许创建嵌套结构。

Here's an overview of some fundamental operations and characteristics of lists:

以下是列表的一些基本操作和特征的概述：

- **Creating a list**: You can create a list by placing comma-separated values inside square brackets `[]`.

  **创建列表**：你可以通过在方括号 `[]` 中放置逗号分隔的值来创建列表。

- **Accessing elements**: You can access elements of a list by indexing, starting from 0 for the first element.

  **访问元素**：你可以通过索引来访问列表的元素，从第一个元素的 0 开始。

- **Modifying elements**: Since lists are mutable, you can modify their content by assigning new values to specific indices.

  **修改元素**：由于列表是可变的，你可以通过为特定索引分配新值来修改其内容。

- **Adding elements**: You can add elements to a list using methods like `append()` (adds to the end) and `insert()` (adds at a specific position).

  **添加元素**：你可以使用 `append()`（在末尾添加）和 `insert()`（在特定位置添加）等方法向列表添加元素。

- **Removing elements**: Methods like `remove()` (removes the first matching element) and `pop()` (removes an element at a specific index) are used for removing items.

  **删除元素**：使用 `remove()`（删除第一个匹配的元素）和 `pop()`（在特定索引处删除元素）等方法来删除项。

Here's a simple example to demonstrate some of these operations:

这里有一个简单的例子来演示其中的一些操作：

```python
# Creating a list
my_list = [1, "hello", 3.14, [1, 2, 3]]

# Accessing elements
print("First element:", my_list[0])  # Outputs 1

# Modifying elements
my_list[1] = "world"

# Adding elements
my_list.append("new item")

# Removing elements
my_list.pop(3)  # Removes the sublist [1, 2, 3]

print("Modified list:", my_list)
```

Output:

输出：

```
First element: 1
Modified list: [1, 'world', 3.14, 'new item']
```

Lists are highly versatile and are widely used in Python for various applications, from data processing to machine learning algorithms, due to their dynamic and mutable nature.

列表非常通用，在 Python 中广泛用于各种应用，从数据处理到机器学习算法，这归功于它们的动态和可变性。
