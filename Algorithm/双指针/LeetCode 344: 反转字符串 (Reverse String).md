## Title: [LeetCode 344: 反转字符串 (Reverse String)](https://leetcode.com/problems/reverse-string/)

---

## 问题

编写一个函数，其功能是将输入的字符串中的字符反转。

你必须原地修改输入数组，使用 O(1) 的额外空间。

### 示例 1:

```
输入: s = ["h","e","l","l","o"]
输出: ["o","l","l","e","h"]
```

### 示例 2:

```
输入: s = ["H","a","n","n","a","h"]
输出: ["h","a","n","n","a","H"]
```

---

## 解题思路

这道题要求我们将字符串反转，并且必须**原地**完成操作，使用**O(1)** 的额外空间。

我们可以使用 **双指针** 技巧解决这个问题：

- 初始化两个指针，`left` 指向字符串的开头，`right` 指向字符串的末尾。
- 交换 `left` 和 `right` 指针所指的字符。
- 然后 `left` 向右移动，`right` 向左移动，直到 `left` 大于或等于 `right`。

---

### 步骤：

1. 初始化两个指针：
   - `left` 指向字符串的第一个字符，索引为 `0`。
   - `right` 指向字符串的最后一个字符，索引为 `len(s) - 1`。
   
2. 使用一个循环，当 `left` 小于 `right` 时：
   - 交换 `left` 和 `right` 位置的字符。
   - 然后将 `left` 向右移动 (`left += 1`)，`right` 向左移动 (`right -= 1`)。

3. 重复这个过程直到 `left >= right`。

---

### 代码实现：

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        left, right = 0, len(s) - 1

        while left < right:
            # 交换 s[left] 和 s[right]
            s[left], s[right] = s[right], s[left]
            # 移动指针
            left += 1
            right -= 1
```

---

### 代码解释：

1. **初始化双指针**：
   - `left` 指向数组的第一个元素 (`索引 0`)，`right` 指向数组的最后一个元素 (`索引 len(s) - 1`)。

2. **交换字符**：
   - 当 `left` 小于 `right` 时，交换 `s[left]` 和 `s[right]`，然后移动指针以继续交换下一对字符。

3. **指针移动**：
   - 交换后，`left` 指针右移一位，`right` 指针左移一位。直到两者相遇或交错（即 `left >= right`）。

4. **原地操作**：
   - 我们不需要额外空间，所有操作都在输入数组上直接进行，因此满足题目的 O(1) 空间要求。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 `n` 是输入数组的长度。我们只遍历数组的一半，即每次交换一对字符。
  
- **空间复杂度**：O(1)，因为我们只使用了常量的额外空间（用于存储指针和临时变量）。

---

### 示例讲解：

#### 示例 1:

```
输入: s = ["h","e","l","l","o"]
```

- 初始状态：`left = 0, right = 4`，交换 `s[0]` 和 `s[4]`，结果为 `["o","e","l","l","h"]`。
- `left` 移到 1，`right` 移到 3，交换 `s[1]` 和 `s[3]`，结果为 `["o","l","l","e","h"]`。
- 此时 `left = 2, right = 2`，指针相遇，反转完成，最终结果为 `["o","l","l","e","h"]`。

#### 示例 2:

```
输入: s = ["H","a","n","n","a","h"]
```

- 初始状态：`left = 0, right = 5`，交换 `s[0]` 和 `s[5]`，结果为 `["h","a","n","n","a","H"]`。
- `left` 移到 1，`right` 移到 4，交换 `s[1]` 和 `s[4]`，结果为 `["h","a","n","n","a","H"]`（位置相同不变）。
- `left` 移到 2，`right` 移到 3，交换 `s[2]` 和 `s[3]`，结果为 `["h","a","n","n","a","H"]`。
- 指针相遇，反转完成。

---

### 总结

- **中文**：该问题可以通过双指针法高效解决。通过交换左右两边的字符，可以在 O(n) 的时间复杂度下完成字符串反转，并且只使用 O(1) 的额外空间。

---

### 推荐相似问题：

1. [LeetCode 541: 反转字符串 II](https://leetcode.com/problems/reverse-string-ii/)
2. [LeetCode 557: 反转字符串中的单词 III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)
3. [LeetCode 345: 反转字符串中的元音字母](https://leetcode.com/problems/reverse-vowels-of-a-string/)
4. [LeetCode 151: 翻转字符串里的单词](https://leetcode.com/problems/reverse-words-in-a-string/)
