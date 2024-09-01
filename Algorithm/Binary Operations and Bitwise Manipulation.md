### Binary Operations and Bitwise Manipulation in Programming

[20天学 Algorithm](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/README.md)

## MORE

- [Practical Applications of Bitwise Operations](https://codebitwave.com/algorithms-101-practical-applications-of-bitwise-operations/)
- [`>>` vs `>>>`](https://codebitwave.com/algorithms-101-vs/)

## Introduction
Understanding binary operations and bitwise manipulation is fundamental for low-level programming, performance optimization, and solving various algorithmic problems. This blog post will break down the key concepts and techniques related to binary operations and bitwise manipulation, providing examples and practical insights.

理解二进制运算和位操作是低级编程、性能优化以及解决各种算法问题的基础。在这篇博客文章中，我们将分解与二进制运算和位操作相关的关键概念和技术，并提供示例和实用见解。

## Binary and Bit Concepts

### Understanding Binary Numbers and Bits
Binary is a base-2 number system that uses only two digits, `0` and `1`. Each digit in a binary number is called a bit (binary digit). The binary number system is the foundation of all computing systems.

二进制是一个使用仅有的两个数字`0`和`1`的基数为2的数字系统。二进制数中的每一位称为一个比特（二进制数字）。二进制数系统是所有计算机系统的基础。

## Representation of Numbers in Binary

### Representation of Positive Numbers
Positive integers are represented in binary form by converting the decimal number to a base-2 format. For example, the decimal number `5` is represented as `101` in binary.

正整数通过将十进制数转换为基数2的格式来表示。例如，十进制数字 `5` 在二进制中表示为 `101`。

### Representation of Negative Numbers
Negative integers are typically represented using two's complement in binary. This method allows for easy binary arithmetic operations such as addition and subtraction. To get the two's complement of a number, invert all the bits and add one to the result.

负整数通常使用二进制的二进制补码来表示。这种方法允许轻松进行二进制算术运算，例如加法和减法。要获得一个数的二进制补码，反转所有位并在结果上加一。

## Printing Binary

### Printing Binary Representations
To print the binary representation of a number, you can use built-in functions in many programming languages. For example, in Python, the `bin()` function returns the binary string of an integer.

```python
print(bin(5))  # Output: 0b101
```

要打印一个数字的二进制表示，可以使用许多编程语言中的内置函数。例如，在Python中，`bin()`函数返回一个整数的二进制字符串。

```python
print(bin(5))  # 输出: 0b101
```

### Defining Binary and Hexadecimal Variables
In many programming languages, binary literals can be defined by prefixing the number with `0b`, and hexadecimal literals with `0x`.

在许多编程语言中，二进制文字可以通过在数字前加上 `0b` 前缀来定义，十六进制文字可以通过 `0x` 来定义。

```python
binary_number = 0b101
hex_number = 0x1A
```

## Common Bitwise Operations

### Bitwise OR (|)
The bitwise OR operation compares each bit of two numbers and returns `1` if either bit is `1`.

位或运算比较两个数字的每个位，如果任意一个位是 `1`，则返回 `1`。

```python
a = 5  # 101 in binary
b = 3  # 011 in binary
result = a | b  # 111 in binary (7 in decimal)
```

### Bitwise AND (&)
The bitwise AND operation compares each bit of two numbers and returns `1` only if both bits are `1`.

位与运算比较两个数字的每个位，只有当两个位都为 `1` 时才返回 `1`。

```python
result = a & b  # 001 in binary (1 in decimal)
```

### Bitwise XOR (^)
The bitwise XOR operation compares each bit of two numbers and returns `1` if the bits are different.

位异或运算比较两个数字的每个位，如果位不同则返回 `1`。

```python
result = a ^ b  # 110 in binary (6 in decimal)
```

### Bitwise NOT (~)
The bitwise NOT operation inverts all the bits of a number, effectively finding the one's complement of the number.

位非运算反转数字的所有位，有效地找到数字的反码。

```python
result = ~a  # 010 in binary (2 in decimal when considering 3 bits)
```

### Bit Shifts (<<, >>, >>>)
Bit shifting operations move the bits of a number to the left or right. Left shifts (<<) add zeros to the right, effectively multiplying the number by 2. Right shifts (>>) remove bits from the right, effectively dividing the number by 2.

位移操作将一个数字的位向左或向右移动。左移（<<）在右边添加零，有效地将数字乘以2。右移（>>）从右边移除位，有效地将数字除以2。

```python
result = a << 1  # 1010 in binary (10 in decimal)
result = a >> 1  # 010 in binary (2 in decimal)
```

## Difference Between Bitwise and Logical Operators

### Bitwise vs. Logical Operators
Bitwise operators work at the bit level, manipulating each bit of the operands. Logical operators, on the other hand, work with entire boolean values and are used in control flow statements.

位运算符在位级别工作，操作操作数的每个位。逻辑运算符则处理整个布尔值，并用于控制流语句中。

```python
bitwise_or = a | b  # Bitwise OR
logical_or = True or False  # Logical OR
```

## Negation/Two's Complement

### Two's Complement
Two's complement is a method for representing negative numbers in binary. It is obtained by inverting all the bits of the number (finding the one's complement) and adding one. This representation simplifies binary subtraction and allows for consistent arithmetic operations.

二进制补码是一种用二进制表示负数的方法。它通过反转数字的所有位（找到反码）并加1来获得。这种表示法简化了二进制减法，并允许一致的算术运算。

```python
# For a number -x, two's complement is found as follows:
x = 5  # Binary: 101
neg_x = ~x + 1  # Two's complement: 011 (3 in decimal for 3-bit representation)
```

## Special Case of the Smallest Integer

### Uniqueness of the Smallest Integer
In a fixed-width binary system (like 32-bit integers), the smallest integer is unique because its absolute value cannot be represented as a positive number within the same bit width.

在固定宽度的二进制系统（如32位整数）中，最小的整数是唯一的，因为它的绝对值无法在相同的位宽内表示为正数。

```python
min_int = -128  # In 8-bit binary, this is represented as 10000000
```

## Why Binary is Designed This Way

### Consistency in Addition Logic
Binary design, particularly the two's complement system, allows for consistent addition and subtraction logic without needing special conditions or branching, making it efficient for hardware implementations.

二进制设计，特别是二进制补码系统，允许一致的加法和减法逻辑，无需特殊条件或分支，使其对硬件实现更加高效。

## Overflow Considerations

### Handling Overflow
Overflow occurs when a calculation exceeds the maximum value that can be stored in a given data type. In binary arithmetic, this needs to be managed carefully to avoid incorrect results.

溢出发生在计算结果超过给定数据类型所能存储的最大值时。在二进制算术中，这需要小心处理以避免错误结果。

```python
# Example: Adding two large 8-bit numbers
a = 127  # 01111111
b = 1    # 00000001
result = a + b  # Overflow! Result is 10000000 in binary (-128 in signed 8-bit)
```

## Advanced Bitwise Techniques

### Advanced Uses of XOR
The XOR operation is particularly powerful for solving specific problems, such as finding the unique element in an array where every other element appears twice.

XOR运算对于解决特定问题尤其强大，例如在每个元素出现两次的数组中找到唯一的元素。

```python
# Example: Finding the unique element
arr = [2, 3, 5, 4, 5, 3, 4]
unique = 0
for num in arr:
    unique ^= num
print(unique)  # Output: 2
```

### Implementing Arithmetic with Bitwise Operations
You can implement arithmetic operations like addition and subtraction using only bitwise logic. This is often used in low-level programming and hardware design.

你可以仅使用位操作来实现算术运算，如加法和减法。这通常用于低级编程和硬件设计中。

```python
# Example: Addition using bitwise operators
def add(x, y):
    while y != 0:
        carry = x & y
        x = x ^ y
        y = carry << 1
    return x
```

## Conclusion

Binary operations and

 bitwise manipulation are essential tools for optimizing code, especially in systems programming and algorithm design. By mastering these techniques, you'll be able to tackle a wide range of problems more efficiently.

二进制运算和位操作是优化代码的重要工具，特别是在系统编程和算法设计中。通过掌握这些技术，你将能够更高效地解决各种问题。

By following the concepts and examples outlined in this blog post, you'll gain a deeper understanding of how to use bitwise operations to your advantage in programming.

------

### 1. **What are Binary Operations?**

[English] Binary operations involve performing operations on binary numbers, which are base-2 numbers consisting of only `0`s and `1`s. These operations are fundamental in computing and are widely used in algorithms, cryptography, and data processing.

**Types of Binary Operations:**
- **AND (`&`)**: Returns `1` if both bits are `1`; otherwise, returns `0`.
- **OR (`|`)**: Returns `1` if at least one of the bits is `1`; otherwise, returns `0`.
- **XOR (`^`)**: Returns `1` if the bits are different; otherwise, returns `0`.
- **NOT (`~`)**: Inverts the bits, turning `1` into `0` and vice versa.
- **Left Shift (`<<`)**: Shifts the bits to the left by a specified number of positions.
- **Right Shift (`>>`)**: Shifts the bits to the right by a specified number of positions.

**Example:**
```python
a = 0b1101  # 13 in binary
b = 0b1011  # 11 in binary

# AND operation
print(bin(a & b))  # 0b1001 -> 9 in decimal

# OR operation
print(bin(a | b))  # 0b1111 -> 15 in decimal

# XOR operation
print(bin(a ^ b))  # 0b0110 -> 6 in decimal

# NOT operation
print(bin(~a))  # -0b1110 -> -14 in decimal

# Left Shift operation
print(bin(a << 2))  # 0b110100 -> 52 in decimal

# Right Shift operation
print(bin(a >> 2))  # 0b11 -> 3 in decimal
```
**What Happens:** The code demonstrates various binary operations between two numbers `a` and `b`.

**Behind the Scenes:** Each operation processes the binary digits (bits) of the numbers to produce a new binary result according to the operation’s rules.

[Chinese] 二进制运算涉及对二进制数执行操作，二进制数是仅由 `0` 和 `1` 组成的基数为 2 的数字。这些操作在计算中是基础，并广泛用于算法、密码学和数据处理。

**二进制运算类型:**
- **与 (`&`)**: 如果两个位都为 `1`，则返回 `1`; 否则，返回 `0`。
- **或 (`|`)**: 如果至少有一个位为 `1`，则返回 `1`; 否则，返回 `0`。
- **异或 (`^`)**: 如果两个位不同，则返回 `1`; 否则，返回 `0`。
- **非 (`~`)**: 颠倒位，将 `1` 变为 `0`，反之亦然。
- **左移 (`<<`)**: 将位向左移动指定的位数。
- **右移 (`>>`)**: 将位向右移动指定的位数。

**示例:**
```python
a = 0b1101  # 二进制 13
b = 0b1011  # 二进制 11

# 与运算
print(bin(a & b))  # 0b1001 -> 十进制 9

# 或运算
print(bin(a | b))  # 0b1111 -> 十进制 15

# 异或运算
print(bin(a ^ b))  # 0b0110 -> 十进制 6

# 非运算
print(bin(~a))  # -0b1110 -> 十进制 -14

# 左移运算
print(bin(a << 2))  # 0b110100 -> 十进制 52

# 右移运算
print(bin(a >> 2))  # 0b11 -> 十进制 3
```
**What Happens:** 代码展示了两个数字 `a` 和 `b` 之间的各种二进制运算。

**Behind the Scenes:** 每个操作根据运算规则处理数字的二进制数字（位）以生成新的二进制结果。

### 2. **What is Bitwise Manipulation and Why is it Important?**

[English] Bitwise manipulation refers to the modification of individual bits within a binary number. This technique is essential for tasks like setting, clearing, or toggling specific bits, which is often required in low-level programming, cryptography, and performance optimization.

**Common Bitwise Operations:**
- **Setting a Bit:** Turning a specific bit to `1`.
- **Clearing a Bit:** Turning a specific bit to `0`.
- **Toggling a Bit:** Flipping the value of a specific bit (from `0` to `1` or `1` to `0`).
- **Checking a Bit:** Determining if a specific bit is `1` or `0`.

**Example:**
```python
n = 0b1010  # 10 in binary

# Set the 1st bit (0-indexed)
n |= (1 << 1)
print(bin(n))  # 0b1010 -> 0b1010 (already set, so no change)

# Clear the 3rd bit (0-indexed)
n &= ~(1 << 3)
print(bin(n))  # 0b1010 -> 0b0010 -> 2 in decimal

# Toggle the 2nd bit (0-indexed)
n ^= (1 << 2)
print(bin(n))  # 0b0010 -> 0b0110 -> 6 in decimal

# Check if the 1st bit is set
is_set = (n & (1 << 1)) != 0
print(is_set)  # True
```
**What Happens:** The code demonstrates setting, clearing, toggling, and checking specific bits in the binary number `n`.

**Behind the Scenes:** Bitwise operations directly manipulate the bits, allowing precise control over individual bits in a number.

[Chinese] 位操作是指修改二进制数中的单个位。这项技术对于设置、清除或切换特定位非常重要，这通常是低级编程、密码学和性能优化所需的。

**常见的位操作:**
- **设置位:** 将特定位设置为 `1`。
- **清除位:** 将特定位设置为 `0`。
- **切换位:** 翻转特定位的值（从 `0` 到 `1` 或从 `1` 到 `0`）。
- **检查位:** 判断特定位是 `1` 还是 `0`。

**示例:**
```python
n = 0b1010  # 二进制 10

# 设置第 1 位（从 0 开始）
n |= (1 << 1)
print(bin(n))  # 0b1010 -> 0b1010（已设置，所以没有变化）

# 清除第 3 位（从 0 开始）
n &= ~(1 << 3)
print(bin(n))  # 0b1010 -> 0b0010 -> 十进制 2

# 切换第 2 位（从 0 开始）
n ^= (1 << 2)
print(bin(n))  # 0b0010 -> 0b0110 -> 十进制 6

# 检查第 1 位是否设置
is_set = (n & (1 << 1)) != 0
print(is_set)  # True
```
**What Happens:** 代码展示了在二进制数字 `n` 中设置、清除、切换和检查特定位。

**Behind the Scenes:** 位操作直接操作位，使得可以精确控制数字中的单个位。

### 3. **What are Some Practical Applications of Bitwise Operations?**

[English] Bitwise operations have numerous practical applications in programming, particularly in areas requiring high performance and low-level data manipulation.

**Applications:**
- **Performance Optimization:** Bitwise operations are faster than arithmetic operations, making them ideal for optimizing performance in critical sections of code.
- **Masking:** Bitwise AND operations can be used to extract specific bits from a number.
- **Encryption:** Bitwise XOR is commonly used in encryption algorithms due to its ability to obscure data.
- **Flag Management:** Bitwise operations are used to set, clear, and check flags in systems programming and embedded systems.

**Example:**
```python
# Masking example
data = 0b11001100  # Some data
mask = 0b11110000  # Mask to extract the upper 4 bits

masked_data = data & mask
print(bin(masked_data))  # 0b11000000 -> 192 in decimal
```
**What Happens:** The code uses a mask to extract the upper 4 bits from

 the binary number `data`.

**Behind the Scenes:** Masking is a common technique in data processing, allowing selective extraction or modification of bits within a binary number.

[Chinese] 位操作在编程中有许多实际应用，特别是在需要高性能和低级数据操作的领域。

**应用:**
- **性能优化:** 位操作比算术操作更快，因此非常适合在代码的关键部分进行性能优化。
- **掩码:** 位与运算可用于从数字中提取特定位。
- **加密:** 位异或在加密算法中常用，因为它能够隐藏数据。
- **标志管理:** 位操作用于在系统编程和嵌入式系统中设置、清除和检查标志。

**示例:**
```python
# 掩码示例
data = 0b11001100  # 一些数据
mask = 0b11110000  # 提取高 4 位的掩码

masked_data = data & mask
print(bin(masked_data))  # 0b11000000 -> 十进制 192
```
**What Happens:** 代码使用掩码从二进制数 `data` 中提取高 4 位。

**Behind the Scenes:** 掩码是一种常见的数据处理技术，允许选择性地提取或修改二进制数字中的位。

### 4. **How do Bitwise Shifts Work and When Should You Use Them?**

[English] Bitwise shifts move bits to the left or right, effectively multiplying or dividing the number by powers of two. Shifts are useful for efficient mathematical operations, particularly in performance-critical code.

**Types of Shifts:**
- **Left Shift (`<<`)**: Moves bits to the left, multiplying the number by 2 for each shift.
- **Right Shift (`>>`)**: Moves bits to the right, dividing the number by 2 for each shift.

**Example:**
```python
x = 0b0001  # 1 in binary

# Left shift by 2 positions
x = x << 2
print(bin(x))  # 0b0100 -> 4 in decimal

# Right shift by 1 position
x = x >> 1
print(bin(x))  # 0b0010 -> 2 in decimal
```
**What Happens:** The code demonstrates shifting bits left and right, effectively multiplying and dividing the number.

**Behind the Scenes:** Bitwise shifts are faster than multiplication and division operations, making them a preferred choice in performance-sensitive applications.

[Chinese] 位移操作将位向左或向右移动，有效地将数字乘以或除以二的幂。位移在性能关键代码中特别有用，用于高效的数学运算。

**位移类型:**
- **左移 (`<<`)**: 将位向左移动，每移动一位，将数字乘以 2。
- **右移 (`>>`)**: 将位向右移动，每移动一位，将数字除以 2。

**示例:**
```python
x = 0b0001  # 二进制 1

# 向左移动 2 位
x = x << 2
print(bin(x))  # 0b0100 -> 十进制 4

# 向右移动 1 位
x = x >> 1
print(bin(x))  # 0b0010 -> 十进制 2
```
**What Happens:** 代码演示了位向左和向右移动，有效地乘以和除以数字。

**Behind the Scenes:** 位移操作比乘法和除法运算更快，因此在性能敏感的应用中更受青睐。

### 5. **What are Some Common Bitwise Tricks Used in Algorithms?**

[English] Bitwise tricks are clever uses of bitwise operations to solve algorithmic problems more efficiently. These tricks are often used in competitive programming, cryptography, and systems programming.

**Common Tricks:**
- **Swapping Two Numbers:** Using XOR to swap values without a temporary variable.
- **Checking Even/Odd:** Using AND with `1` to check if a number is even or odd.
- **Power of Two Check:** Using AND to check if a number is a power of two.
- **Counting Set Bits:** Using bitwise operations to count the number of `1`s in a binary number.

**Example:**
```python
# Swapping two numbers using XOR
a = 5  # 0b0101
b = 9  # 0b1001

a = a ^ b
b = a ^ b
a = a ^ b
print(a, b)  # a = 9, b = 5

# Checking if a number is even
n = 4  # 0b0100
is_even = (n & 1) == 0
print(is_even)  # True
```
**What Happens:** The code demonstrates swapping two numbers using XOR and checking if a number is even.

**Behind the Scenes:** These tricks exploit the properties of binary numbers and bitwise operations to perform tasks efficiently.

[Chinese] 位操作技巧是巧妙地使用位操作更有效地解决算法问题。这些技巧常用于竞赛编程、密码学和系统编程。

**常见技巧:**
- **交换两个数:** 使用异或交换值，而无需临时变量。
- **检查奇偶性:** 使用与 `1` 进行与运算检查一个数是偶数还是奇数。
- **检查二的幂:** 使用与运算检查一个数是否是二的幂。
- **计数设置位:** 使用位操作计数二进制数中的 `1` 的数量。

**示例:**
```python
# 使用异或交换两个数
a = 5  # 0b0105
b = 9  # 0b1001

a = a ^ b
b = a ^ b
a = a ^ b
print(a, b)  # a = 9, b = 5

# 检查一个数是否为偶数
n = 4  # 0b0100
is_even = (n & 1) == 0
print(is_even)  # True
```
**What Happens:** 代码展示了使用异或交换两个数字和检查一个数字是否为偶数。

**Behind the Scenes:** 这些技巧利用二进制数字和位操作的特性来高效地执行任务。


------

通过遵循本文中概述的概念和示例，你将更深入地理解如何在编程中利用位操作。

### Recommend Resources:
[![算法讲解003_入门_二进制和位运算_by_左程云](https://img.youtube.com/vi/snb1cumIaKA/maxresdefault.jpg)](https://youtu.be/snb1cumIaKA)

