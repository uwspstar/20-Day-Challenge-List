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


#### 以下是关于 Python 多重赋值的 5 个面试问题及其答案

### 1. What is multiple assignment in Python? 在Python中什么是多重赋值？

 
Multiple assignment allows you to assign multiple variables at the same time in a single line of code. For example:

```python
a, b, c = 1, 2, 3
```
 
多重赋值允许你在一行代码中同时给多个变量赋值。例如：

```python
a, b, c = 1, 2, 3
```

### 2. How does multiple assignment make code cleaner and more efficient? 多重赋值如何使代码更简洁、更高效？

 
Multiple assignment reduces the number of lines of code and makes it easier to read. It also ensures that related variables are initialized together, reducing the chance of errors.

```python
# Without multiple assignment
x = 5
y = 10
z = 15

# With multiple assignment
x, y, z = 5, 10, 15
```
 
多重赋值减少了代码行数，使其更易读。它还确保相关变量一起初始化，减少了出错的机会。

```python
# 没有多重赋值
x = 5
y = 10
z = 15

# 使用多重赋值
x, y, z = 5, 10, 15
```

### 3. Can multiple assignment be used to swap variable values? How? 多重赋值可以用来交换变量值吗？如何实现？


Yes, multiple assignment can be used to swap variable values without needing a temporary variable. For example:

```python
a, b = 1, 2
a, b = b, a
print(a, b)  # Output: 2 1
```
 
是的，多重赋值可以用来交换变量值而不需要临时变量。例如：

```python
a, b = 1, 2
a, b = b, a
print(a, b)  # 输出: 2 1
```

### 4. How does unpacking work in multiple assignment? 在多重赋值中，解包是如何工作的？

 
Unpacking in multiple assignment allows you to assign values from a collection (like a list or tuple) to variables. For example:

```python
numbers = [1, 2, 3]
a, b, c = numbers
print(a, b, c)  # Output: 1 2 3
```

 
在多重赋值中，解包允许你将集合（如列表或元组）中的值赋给变量。例如：

```python
numbers = [1, 2, 3]
a, b, c = numbers
print(a, b, c)  # 输出: 1 2 3
```

### 5. What happens if the number of variables and values don't match in multiple assignment? 如果多重赋值中变量和值的数量不匹配会怎样？

 
If the number of variables and values don't match, Python will raise a `ValueError`. For example:

```python
a, b = 1, 2, 3  # Raises ValueError: too many values to unpack
```
 
如果变量和值的数量不匹配，Python 会引发 `ValueError`。例如：

```python
a, b = 1, 2, 3  # 引发 ValueError: too many values to unpack
```

