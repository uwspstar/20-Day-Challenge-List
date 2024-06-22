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

These operations allow you to manipulate strings efficiently, whether you're accessing individual characters or extracting parts of the string.

这些操作允许你高效地操作字符串，无论是访问单个字符还是提取字符串的部分。
