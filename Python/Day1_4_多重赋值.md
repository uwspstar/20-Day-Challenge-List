# 多重赋值

In Python, multiple assignment allows you to assign multiple variables at the same time in a single line of code. This feature can make your code cleaner and more efficient.

在Python中，多重赋值允许你在一行代码中同时给多个变量赋值。这个特性可以使你的代码更简洁、更高效。

Here’s how you can use multiple assignment in Python:

以下是如何在Python中使用多重赋值：

```python
a, b = 5, 10
print("a =", a)
print("b =", b)
```

This code will output:

这段代码的输出将是：

```
a = 5
b = 10
```

Multiple assignment can also be used with list or tuple unpacking:

多重赋值还可以与列表或元组解包一起使用：

```python
coordinates = (1, 2, 3)
x, y, z = coordinates
print("x =", x)
print("y =", y)
print("z =", z)
```

This code will output:

这段代码的输出将是：

```
x = 1
y = 2
z = 3
```

The comparison of multiple assignment methods is shown in the table below:

多重赋值方法的比较如下表所示：

| Method | Description in English | Description in Chinese |
|--------|------------------------|------------------------|
| Direct Assignment | Directly assigns values to multiple variables. | 直接为多个变量赋值。 |
| Tuple Unpacking | Unpacks values from a tuple into variables. | 从元组中解包值到变量。 |
| List Unpacking | Unpacks values from a list into variables. | 从列表中解包值到变量。 |

Multiple assignment is very useful for swapping values or when you need to distribute values from collections like lists or tuples to individual variables.

多重赋值在交换值或需要从列表或元组等集合中分配值给单个变量时非常有用。
