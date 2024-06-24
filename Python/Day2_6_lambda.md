# lambda 
The `lambda` keyword in Python is used to create small, anonymous functions. It's a way to define a function on the fly, without having to formally define a function using `def`. Lambda functions are syntactically restricted to a single expression.

Python 中的 `lambda` 关键字用于创建小巧的匿名函数。这是一种即时定义函数的方式，无需使用 `def` 正式定义函数。Lambda 函数在语法上限制为单个表达式。

### Key Characteristics of Lambda Functions

- **Simplicity**: Lambda functions are meant to be simple and concise, typically used for small operations where defining a full function would be an overkill.
- **Anonymity**: They are anonymous, meaning that they do not need a name.
- **Functionality**: They can be used anywhere a function is required.

### Lambda 函数的关键特性

- **简单性**：Lambda 函数旨在简单且简洁，通常用于定义完整函数过于繁琐的小型操作。
- **匿名性**：它们是匿名的，这意味着它们不需要名称。
- **功能性**：它们可以用在任何需要函数的地方。

### Examples | 示例

#### Example 1: Simple Addition

```python
# Using a lambda function to add two numbers
add = lambda a, b: a + b
print(add(3, 5))  # Outputs: 8
```

**示例 1：简单加法**

```python
# 使用 lambda 函数来加两个数字
add = lambda a, b: a + b
print(add(3, 5))  # 输出：8
```

#### Example 2: Sorting a List of Tuples

```python
# Using a lambda function to sort a list of tuples by the second item
tuples = [(1, 'one'), (3, 'three'), (2, 'two')]
tuples.sort(key=lambda x: x[1])
print(tuples)  # Outputs: [(3, 'three'), (1, 'one'), (2, 'two')]
```

**示例 2：排序元组列表**

```python
# 使用 lambda 函数按第二项对元组列表进行排序
tuples = [(1, 'one'), (3, 'three'), (2, 'two')]
tuples.sort(key=lambda x: x[1])
print(tuples)  # 输出：[(3, 'three'), (1, 'one'), (2, 'two')]
```

#### Example 3: Filtering a List

```python
# Using a lambda to filter out even numbers from a list
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Outputs: [2, 4, 6]
```

**示例 3：过滤列表**

```python
# 使用 lambda 过滤列表中的偶数
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # 输出：[2, 4, 6]
```

### Conclusion | 结论

Lambda functions are a powerful feature in Python, allowing for simplified function definition in a concise manner. They are useful in many situations where a simple expression-based function is needed temporarily.

Lambda 函数是 Python 中的一个强大功能，允许以简洁的方式简化函数定义。在需要临时简单的基于表达式的函数的许多情况下，它们非常有用。
