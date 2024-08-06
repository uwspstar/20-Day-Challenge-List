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

------

### lambda
The `lambda` keyword in Python is used to create small, anonymous functions. It's a way to define a function on the fly, without having to formally define a function using `def`. Lambda functions are syntactically restricted to a single expression.

#### 1. What is a lambda function in Python?
[English]
A lambda function in Python is a small anonymous function defined using the `lambda` keyword. It can have any number of arguments but only one expression. The result of the expression is returned automatically.

```python
# Traditional function
def add(x, y):
    return x + y

# Lambda function
add_lambda = lambda x, y: x + y

print(add(3, 5))          # Output: 8
print(add_lambda(3, 5))   # Output: 8
```

**What Happens:**
The `add` function and `add_lambda` lambda function both take two arguments and return their sum. They behave identically in this context.

**Behind the Scenes:**
The `lambda` keyword creates an anonymous function on the fly, which is then assigned to `add_lambda`. This function can be called just like any other function.

[Chinese]
Python 中的 lambda 函数是使用 `lambda` 关键字定义的小型匿名函数。它可以有任意数量的参数，但只有一个表达式。表达式的结果会自动返回。

```python
# 传统函数
def add(x, y):
    return x + y

# Lambda 函数
add_lambda = lambda x, y: x + y

print(add(3, 5))          # 输出: 8
print(add_lambda(3, 5))   # 输出: 8
```

**What Happens:**
`add` 函数和 `add_lambda` lambda 函数都接受两个参数并返回它们的和。在这种情况下，它们的行为是一样的。

**Behind the Scenes:**
`lambda` 关键字即时创建了一个匿名函数，然后将其赋值给 `add_lambda`。这个函数可以像其他函数一样调用。

#### 2. How do you use lambda functions with higher-order functions?
[English]
Lambda functions are often used with higher-order functions like `map()`, `filter()`, and `reduce()` to perform operations on sequences.

```python
# Using lambda with map
squared = list(map(lambda x: x**2, [1, 2, 3, 4]))
print(squared)  # Output: [1, 4, 9, 16]

# Using lambda with filter
evens = list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))
print(evens)  # Output: [2, 4]
```

**What Happens:**
- `map` applies the lambda function to each element of the list, returning a new list with squared values.
- `filter` applies the lambda function to each element and returns a list of elements that satisfy the condition.

**Behind the Scenes:**
`map` and `filter` functions internally iterate over the list, applying the lambda function to each element and collecting the results.

[Chinese]
Lambda 函数通常与 `map()`、`filter()` 和 `reduce()` 等高阶函数一起使用，以对序列执行操作。

```python
# 将 lambda 与 map 一起使用
squared = list(map(lambda x: x**2, [1, 2, 3, 4]))
print(squared)  # 输出: [1, 4, 9, 16]

# 将 lambda 与 filter 一起使用
evens = list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))
print(evens)  # 输出: [2, 4]
```

**What Happens:**
- `map` 将 lambda 函数应用于列表的每个元素，返回一个包含平方值的新列表。
- `filter` 将 lambda 函数应用于每个元素，并返回满足条件的元素列表。

**Behind the Scenes:**
`map` 和 `filter` 函数在内部迭代列表，将 lambda 函数应用于每个元素并收集结果。

#### 3. What are some common use cases for lambda functions?
[English]
Common use cases for lambda functions include:
1. **Sorting**: Using custom sort keys.
2. **Event Handling**: In GUI applications.
3. **Data Processing**: In conjunction with functional programming tools.

```python
# Sorting with lambda
points = [(1, 2), (4, 1), (5, 3), (2, 2)]
sorted_points = sorted(points, key=lambda point: point[1])
print(sorted_points)  # Output: [(4, 1), (1, 2), (2, 2), (5, 3)]
```

**What Happens:**
The `sorted` function sorts `points` based on the second element of each tuple using the lambda function as the key.

**Behind the Scenes:**
The lambda function is called for each element in `points`, returning the value to sort by, and `sorted` uses these values to arrange the elements.

[Chinese]
Lambda 函数的常见用例包括：
1. **排序**：使用自定义排序键。
2. **事件处理**：在 GUI 应用程序中。
3. **数据处理**：结合函数式编程工具。

```python
# 使用 lambda 排序
points = [(1, 2), (4, 1), (5, 3), (2, 2)]
sorted_points = sorted(points, key=lambda point: point[1])
print(sorted_points)  # 输出: [(4, 1), (1, 2), (2, 2), (5, 3)]
```

**What Happens:**
`sorted` 函数根据每个元组的第二个元素使用 lambda 函数作为键对 `points` 进行排序。

**Behind the Scenes:**
对 `points` 中的每个元素调用 lambda 函数，返回用于排序的值，`sorted` 使用这些值来排列元素。

#### 4. How are lambda functions syntactically different from regular functions?
[English]
Lambda functions are defined using the `lambda` keyword and are limited to a single expression. They do not have a `return` statement, as the result of the expression is returned implicitly. Regular functions are defined using the `def` keyword and can contain multiple statements, including a `return` statement.

```python
# Regular function
def add(x, y):
    return x + y

# Lambda function
add_lambda = lambda x, y: x + y
```

**What Happens:**
Both functions add two numbers and return the result, but the lambda function is defined in a single line without the `def` keyword or `return` statement.

**Behind the Scenes:**
The `lambda` expression is a syntactic shortcut that defines a function inline, while the `def` keyword sets up a named function with more flexibility for multiple statements.

[Chinese]
Lambda 函数使用 `lambda` 关键字定义，仅限于单个表达式。它们没有 `return` 语句，因为表达式的结果会隐式返回。常规函数使用 `def` 关键字定义，可以包含多个语句，包括 `return` 语句。

```python
# 常规函数
def add(x, y):
    return x + y

# Lambda 函数
add_lambda = lambda x, y: x + y
```

**What Happens:**
这两个函数都将两个数字相加并返回结果，但 lambda 函数在一行中定义，没有 `def` 关键字或 `return` 语句。

**Behind the Scenes:**
`lambda` 表达式是定义内联函数的语法捷径，而 `def` 关键字设置了一个具有更多灵活性的命名函数，可以包含多个语句。

#### 5. What are the limitations of lambda functions in Python?
[English]
Lambda functions are limited in several ways:
1. **Single Expression**: They can only contain one expression.
2. **Readability**: Complex operations can make lambda functions hard to read.
3. **No Annotations**: They do not support annotations or documentation strings.

```python
# Complex lambda (hard to read)
complex_lambda = lambda x: (x**2 if x % 2 == 0 else x**3) + 10
print(complex_lambda(2))  # Output: 14
print(complex_lambda(3))  # Output: 37
```

**What Happens:**
The `complex_lambda` function performs a conditional operation and adds 10, but the logic is harder to read compared to a regular function.

**Behind the Scenes:**
The lambda function is a concise way to define logic inline, but it sacrifices readability and documentation, making it harder to understand and maintain.

[Chinese]
Lambda 函数在多个方面受到限制：
1. **单一表达式**：它们只能包含一个表达式。
2. **可读性**：复杂操作可能使 lambda 函数难以阅读。
3. **无注解**：它们不支持注解或文档字符串。

```python
# 复杂的 lambda（难以阅读）
complex_lambda = lambda x: (x**2 if x % 2 == 0 else x**3) + 10
print(complex_lambda(2))  # 输出: 14
print(complex_lambda

(3))  # 输出: 37
```

**What Happens:**
`complex_lambda` 函数执行一个条件操作并加上 10，但相比常规函数，其逻辑更难阅读。

**Behind the Scenes:**
Lambda 函数是一种简洁的内联定义逻辑的方式，但它牺牲了可读性和文档性，使其更难理解和维护。
