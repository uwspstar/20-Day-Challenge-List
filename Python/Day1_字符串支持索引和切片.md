# 字符串支持索引和切片
In Python, strings support indexing and slicing. This can be conceptualized by understanding that indices point to the spaces between characters, with the left side of the first character labeled as 0 and the right side of the last character labeled as the length of the string, `n`. For instance, in the string `"Python"`:

在 Python 中，字符串支持索引和切片。可以这样理解：索引指向字符之间的空间，第一个字符的左侧标为 0，最后一个字符的右侧标为字符串长度 `n`。例如，在字符串 `"Python"` 中：

```
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

Here's how indexing and slicing work based on this diagram:

这里展示了根据此图表索引和切片的工作方式：

1. **Indexing**: Accessing a single character by its position.
   - Positive indices start from 0 (leftmost).
   - Negative indices start from -1 (rightmost).
   
   **索引**：通过其位置访问单个字符。
   - 正索引从 0（最左边）开始。
   - 负索引从 -1（最右边）开始。

2. **Slicing**: Accessing a subset of the string by specifying a start and end point.
   - The slice starts at the start index and goes up to but does not include the end index.

   **切片**：通过指定起始点和终点来访问字符串的子集。
   - 切片从起始索引开始，一直到终索引，但不包括终索引。

Here’s a practical example to illustrate these concepts:

以下是一个实际的例子来说明这些概念：

```python
s = "Python"

# Indexing
first_letter = s[0]   # 'P'
last_letter = s[-1]   # 'n'

# Slicing
subset = s[1:4]       # 'yth'
reverse = s[::-1]     # 'nohtyP'

print("First letter:", first_letter)
print("Last letter:", last_letter)
print("Subset of string:", subset)
print("Reverse of string:", reverse)
```

In the Python string slicing notation, `s[::-1]` is a commonly used idiom for reversing a string. Let's break down what each part of the slice notation means:

在 Python 字符串切片符号中，`s[::-1]` 是一种常用的用于反转字符串的习语。让我们分解切片符号的每个部分的含义：

- **`s`**: This is the string variable we are working with.

  **`s`**：这是我们正在处理的字符串变量。

- **`[ ]`**: The square brackets denote a slicing operation.

  **`[ ]`**：方括号表示切片操作。

- **`:`**: The colon inside the brackets is used to separate the start index, end index, and the step.

  **`:`**：括号内的冒号用于分隔起始索引、终止索引和步长。

- **First empty space before the first `:`**: This indicates the start index. When it's empty, it defaults to the start of the string.

  **第一个 `:` 之前的空位**：这表示起始索引。当它为空时，默认为字符串的开始。

- **Second empty space after the first `:` and before the second `:`**: This indicates the end index. When it's empty, it defaults to the end of the string.

  **第一个 `:` 之后和第二个 `:` 之前的空位**：这表示终止索引。当它为空时，默认为字符串的结尾。

- **`-1` after the second `:`**: This is the step. A step of `-1` tells Python to go backwards through the string. Essentially, it decrements the current index on each iteration.

  **第二个 `:` 之后的 `-1`**：这是步长。步长为 `-1` 告诉 Python 向后通过字符串。本质上，它在每次迭代时减少当前索引。

Putting it all together, `s[::-1]` starts at the end of the string (since no start is specified, it starts from the default end), ends at the beginning (since no end is specified, it stops at the default start), and moves with a step of `-1`, effectively reversing the string.

综合起来，`s[::-1]` 从字符串的末尾开始（因为没有指定开始，所以从默认的末尾开始），结束在开始（因为没有指定结束，所以在默认的开始处停止），并以 `-1` 的步长移动，有效地反转了字符串。
