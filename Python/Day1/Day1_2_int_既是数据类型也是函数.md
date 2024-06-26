# int 既是数据类型也是函数

In Python, `int` serves both as a data type and a function, performing different roles in each capacity.

在 Python 中，`int` 既是数据类型也是函数，在每个容量中执行不同的角色。

1. **As a Data Type**: `int` is one of Python's built-in primitive data types. It represents integers, which are whole numbers without a fractional component, and can be positive, negative, or zero.

   **作为数据类型**：`int` 是 Python 内置的基本数据类型之一。它表示整数，即没有小数部分的整数，可以是正数、负数或零。

2. **As a Function**: The `int()` function is used to convert other data types into an integer. This includes converting floating-point numbers (by truncating the decimal part without rounding), strings (if the string represents a valid integer), and other objects that support conversion to integers (through special methods like `__int__`).

   **作为函数**：`int()` 函数用于将其他数据类型转换为整数。这包括转换浮点数（通过截断小数部分而不进行四舍五入）、字符串（如果字符串表示有效的整数）以及支持转换为整数的其他对象（通过诸如 `__int__` 这样的特殊方法）。

Here are some examples illustrating `int` as both a data type and a function:

```python
# int as a data type
a = 123
print("Data type of 'a':", type(a))  # Outputs: <class 'int'>

# int as a function
b = int("456")  # Converts string to integer
c = int(789.123)  # Converts float to integer by truncating
d = int(True)  # Converts boolean True to integer (True becomes 1)

print("Converted string to int:", b)
print("Converted float to int by truncating:", c)
print("Converted boolean to int:", d)
```

These examples demonstrate the versatility of `int` in Python, both as a fundamental data type for storing whole numbers and as a utility function for type conversion.

这些示例展示了 Python 中 `int` 的多功能性，既作为存储整数的基本数据类型，也作为类型转换的实用函数。
