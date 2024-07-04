# 存储数据集合

Set 是 Python 中用于存储数据集合的四种内置数据类型之一，另外三种是 List（列表）、Tuple（元组）和 Dictionary（字典），每种类型都有不同的特性和用途。

A set is an unordered, unchangeable*, and unindexed collection.

集合是一个无序的、不可变的*、无索引的集合。

*Note: While set items are unchangeable, you can remove items and add new items.

*注意：虽然集合项是不可变的，但你可以删除项或添加新项。

### Comparison of Python Collections

Here's a comparison table showing the main differences between List, Tuple, Set, and Dictionary:

| Type      | Ordered | Changeable | Indexed | Syntax   |
|-----------|---------|------------|---------|----------|
| List      | Yes     | Yes        | Yes     | [ ]      |
| Tuple     | Yes     | No         | Yes     | ( )      |
| Set       | No      | Items No*, Set Yes | No      | { }      |
| Dictionary| Yes     | Yes        | Yes     | {key: value} |

### 理解背后的原理

在 Python 集合中，集合的无序性意味着集合中的元素没有固定的顺序。不可变的特性指的是集合中的元素一旦定义就不能被修改，但你可以增加或删除元素。这种设计允许集合在检查成员、删除重复项时提供更高的效率。

In Python sets, the unordered nature means there is no fixed order to the elements in the set. The unchangeable characteristic refers to the fact that once elements are defined in a set, they cannot be altered, though you can add or remove elements. This design allows sets to be more efficient in membership checks and eliminating duplicates.
