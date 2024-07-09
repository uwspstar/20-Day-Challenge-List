# 内置类型
- https://docs.python.org/zh-cn/3/library/stdtypes.html
### 存储数据集合

Set 是 Python 中用于存储数据集合的四种内置数据类型之一，另外三种是 List（列表）、Tuple（元组）和 Dictionary（字典），每种类型都有不同的特性和用途。

A set is an unordered, unchangeable*, and unindexed collection.

集合是一个无序的、不可变的*、无索引的集合。

*Note: While set items are unchangeable, you can remove items and add new items.

*注意：虽然集合项是不可变的，但你可以删除项或添加新项。

### Comparison of Python Collections

Here's a comparison table showing the main differences between List, Tuple, Set, and Dictionary:

| Type      | Ordered | Changeable | Indexed | Syntax   |
|-----------|---------|------------|---------|----------|
| List   [ ]   | Yes     | Yes        | Yes     | [ ]      |
| Tuple  ( )   | Yes     | No         | Yes     | ( )      |
| Set    { }   | No      | Items No*, Set Yes | No      | { }      |
| Dictionary {key: value} | Yes     | Yes        | Yes     | {key: value} |

### 理解背后的原理

在 Python 集合中，集合的无序性意味着集合中的元素没有固定的顺序。不可变的特性指的是集合中的元素一旦定义就不能被修改，但你可以增加或删除元素。这种设计允许集合在检查成员、删除重复项时提供更高的效率。

In Python sets, the unordered nature means there is no fixed order to the elements in the set. The unchangeable characteristic refers to the fact that once elements are defined in a set, they cannot be altered, though you can add or remove elements. This design allows sets to be more efficient in membership checks and eliminating duplicates.

Python provides a variety of collection data types that are suitable for different purposes. Here’s a detailed explanation of each type:

### List
列表

- **Description**: A list is an ordered collection that can be changed or modified. It allows duplicate elements, making it suitable for scenarios where items can repeat and order matters.
- **描述**：列表是一种有序的集合，可以被修改或更改。它允许元素重复，适用于项目可能重复且顺序重要的场景。

### Tuple
元组

- **Description**: A tuple is similar to a list in that it is ordered. However, tuples are immutable, meaning once they are created, their elements cannot be changed. This is suitable for fixed data.
- **描述**：元组与列表相似，即它们是有序的。但是，元组是不可变的，一旦创建，其元素就不能更改。这适用于固定数据。

### Set
集合

- **Description**: A set is an unordered collection of items where each item is unique. Sets are ideal for membership testing and eliminating duplicate entries.
- **描述**：集合是一个无序的元素集，每个元素都是唯一的。集合非常适合进行成员测试和消除重复条目。

### Dictionary
字典

- **Description**: A dictionary is a collection which is ordered (as of Python 3.7) and consists of a key-value pair. Each key-value pair maps the key to its associated value. Dictionaries are optimal for fast lookups and can be changed or updated.
- **描述**：字典是一个有序的集合（从Python 3.7开始）并且由键值对组成。每个键值对将键映射到其关联的值。字典非常适合快速查找，并且可以更改或更新。

Here’s a comparison table summarizing the properties of each collection type:

| Type       | Ordered | Changeable | Indexed | Allows Duplicates | Use-case Example                |
|------------|---------|------------|---------|-------------------|---------------------------------|
| List       | Yes     | Yes        | Yes     | Yes               | Handling a sequence of items    |
| Tuple      | Yes     | No         | Yes     | Yes               | Storing fixed data              |
| Set        | No      | Partially  | No      | No                | Removing duplicates, membership testing |
| Dictionary | Yes (3.7+)| Yes      | Yes     | No (in keys)      | Fast lookups by key             |

The table helps in understanding the fundamental differences and practical use-cases for each collection type. Each serves a unique purpose in Python programming depending on the requirements of data management and operations you intend to perform.
