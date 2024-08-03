## `range()` function

- [Understanding the Python `range()` Function](https://codebitwave.com/python-101-understanding-the-python-range-function/)

The `range()` function in Python is a versatile built-in function used to generate sequences of numbers. It is particularly useful for looping a specific number of times in `for` loops.

`range()`函数是Python中一个多功能的内置函数，用于生成数字序列。它特别适用于在`for`循环中循环特定次数。

Here's a detailed explanation and code examples to illustrate its use:

以下是详细解释和代码示例，以说明其用法：

1. **Basic Usage**:
    - **Description**: Generates a sequence from 0 up to but not including the specified end value.
    - **Code Example**:

```python
for i in range(10):
    print(i, end=' ')  # Outputs: 0 1 2 3 4 5 6 7 8 9
```

**基本用法**：
- **描述**：生成从0开始到指定终止值但不包括终止值的序列。
- **代码示例**：

```python
for i in range(10):
    print(i, end=' ')  # 输出：0 1 2 3 4 5 6 7 8 9
```

2. **Starting from a Non-Zero Value**:
    - **Description**: Specifies a start value, end value, and optionally, a step value.
    - **Code Example**:

```python
for i in range(5, 15):
    print(i, end=' ')  # Outputs: 5 6 7 8 9 10 11 12 13 14
```

**从非零值开始**：
- **描述**：指定一个起始值、终止值和可选的步长值。
- **代码示例**：

```python
for i in range(5, 15):
    print(i, end=' ')  # 输出：5 6 7 8 9 10 11 12 13 14
```

3. **Using a Step Value**:
    - **Description**: Allows for increments other than 1, which can be positive or negative.
    - **Code Example**:

```python
for i in range(0, 20, 3):
    print(i, end=' ')  # Outputs: 0 3 6 9 12 15 18
```

**使用步长值**：
- **描述**：允许除1以外的增量，可以是正数或负数。
- **代码示例**：

```python
for i in range(0, 20, 3):
    print(i, end=' ')  # 输出：0 3 6 9 12 15 18
```

4. **Negative Step Value**:
    - **Description**: Generates a sequence in reverse order using a negative step.
    - **Code Example**:

```python
for i in range(10, 0, -2):
    print(i, end=' ')  # Outputs: 10 8 6 4 2
```

**负步长值**：
- **描述**：使用负步长生成倒序序列。
- **代码示例**：

```python
for i in range(10, 0, -2):
    print(i, end=' ')  # 输出：10 8 6 4 2
```

The `range()` function is highly efficient because it generates the required numbers on the fly without storing the entire sequence in memory, making it suitable for large ranges.

`range()`函数非常高效，因为它即时生成所需的数字，而不是在内存中存储整个序列，这使它适用于大范围。
