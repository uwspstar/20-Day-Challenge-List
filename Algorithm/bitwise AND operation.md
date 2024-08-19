## Concept Explanation

- [Algorithms 101: Using Bitwise AND to Check the Least Significant Bit](https://codebitwave.com/algorithms-101-using-bitwise-and-to-check-the-least-significant-bit/)

### English
The bitwise AND operation `n & 1` is a quick and efficient way to determine whether a number is odd or even. In binary, the least significant bit (LSB) of an integer determines its parity: 
- If the LSB is `1`, the number is odd.
- If the LSB is `0`, the number is even.

For example:
- `5` in binary is `101`. The LSB is `1`, so `5` is odd.
- `4` in binary is `100`. The LSB is `0`, so `4` is even.

The operation `n & 1` directly checks this LSB:
- If `n & 1` equals `1`, the number is odd.
- If `n & 1` equals `0`, the number is even.

This method has a time complexity of O(1) because it only involves a single bitwise operation, and it requires no additional memory. Therefore, it is widely used in performance-sensitive applications, such as competitive programming or real-time systems.

### Chinese
按位与操作 `n & 1` 是一种快速且高效的方法来确定一个数字是奇数还是偶数。在二进制中，整数的最低有效位（LSB）决定了其奇偶性：
- 如果 LSB 是 `1`，则该数字是奇数。
- 如果 LSB 是 `0`，则该数字是偶数。

例如：
- `5` 的二进制表示是 `101`。最低有效位是 `1`，因此 `5` 是奇数。
- `4` 的二进制表示是 `100`。最低有效位是 `0`，因此 `4` 是偶数。

操作 `n & 1` 直接检查这个最低有效位：
- 如果 `n & 1` 等于 `1`，则该数字是奇数。
- 如果 `n & 1` 等于 `0`，则该数字是偶数。

这种方法的时间复杂度为 O(1)，因为它只涉及一个按位操作，并且不需要额外的内存。因此，它在性能敏感的应用中被广泛使用，如竞赛编程或实时系统。

## Code Example

### English

Here’s a simple Python function that uses `n & 1` to determine if a number is odd or even:

```python
def is_odd(n: int) -> bool:
    return n & 1 == 1

def is_even(n: int) -> bool:
    return n & 1 == 0
```

Explanation:
- **is_odd(n)**: Returns `True` if `n` is odd, otherwise returns `False`.
- **is_even(n)**: Returns `True` if `n` is even, otherwise returns `False`.

### Chinese

以下是一个使用 `n & 1` 来判断数字是奇数还是偶数的简单 Python 函数：

```python
def is_odd(n: int) -> bool:
    return n & 1 == 1

def is_even(n: int) -> bool:
    return n & 1 == 0
```

解释：
- **is_odd(n)**: 如果 `n` 是奇数，则返回 `True`，否则返回 `False`。
- **is_even(n)**: 如果 `n` 是偶数，则返回 `True`，否则返回 `False`。

## Usage in Applications

### English
This bitwise operation is particularly useful in scenarios where performance is critical:
1. **Competitive Programming**: Quick checks for odd/even numbers without the overhead of division or modulo operations.
2. **Real-time Systems**: Efficient bit-level manipulations where every clock cycle counts.
3. **Low-level Programming**: Embedded systems where minimizing memory usage and execution time is crucial.

### Chinese
这种按位操作在性能关键的场景中特别有用：
1. **竞赛编程**：快速检查奇数/偶数，而无需除法或取模操作的开销。
2. **实时系统**：高效的比特级操作，每一个时钟周期都至关重要。
3. **低级编程**：嵌入式系统中，减少内存使用和执行时间至关重要。

### Summary / 总结

- **English**: The bitwise AND operation `n & 1` is a powerful tool for determining the parity of a number with O(1) time complexity and no additional memory usage. Its efficiency makes it a valuable tool in performance-sensitive applications.
- **Chinese**: 按位与操作 `n & 1` 是一种强大的工具，可以在 O(1) 时间复杂度下确定数字的奇偶性，并且不需要额外的内存。其效率使其成为性能敏感应用中的一个有价值的工具。
