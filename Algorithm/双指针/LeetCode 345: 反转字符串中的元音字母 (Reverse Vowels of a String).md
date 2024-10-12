## Title: [LeetCode 345: 反转字符串中的元音字母 (Reverse Vowels of a String)](https://leetcode.com/problems/reverse-vowels-of-a-string/)

---

## 问题

编写一个函数，其作用是将输入字符串中的**元音字母**反转。元音字母包括 `'a', 'e', 'i', 'o', 'u'` 以及它们的大写形式。

### 示例 1:

```
输入: s = "hello"
输出: "holle"
```

### 示例 2:

```
输入: s = "leetcode"
输出: "leotcede"
```

---

## 解题思路

这道题要求我们反转字符串中的**元音字母**，其他字符保持不变。可以使用 **双指针** 技巧来高效完成这个任务。

### 关键步骤：

1. **双指针法**：
   - 初始化两个指针：一个 `left` 从字符串的起始位置开始，另一个 `right` 从字符串的末尾开始。
   - 双指针分别向中间移动，当 `left` 和 `right` 都指向元音字母时，交换它们。
   - 继续移动 `left` 和 `right`，直到两者相遇。

2. **元音字母集合**：
   - 创建一个集合来存储所有元音字母（包括大写和小写），方便快速查找。
   
3. **原地反转**：
   - 在不需要额外空间的情况下直接在原字符串的字符数组上交换元音字母。

---

### 代码实现：

```python
class Solution:
    def reverseVowels(self, s: str) -> str:
        vowels = set("aeiouAEIOU")  # 创建包含元音字母的集合
        s = list(s)  # 将字符串转为列表以便修改字符
        left, right = 0, len(s) - 1

        while left < right:
            # 左指针寻找元音
            while left < right and s[left] not in vowels:
                left += 1
            # 右指针寻找元音
            while left < right and s[right] not in vowels:
                right -= 1
            # 交换左指针和右指针的元音
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

        return ''.join(s)  # 将列表重新转换为字符串
```

---

### 代码解释：

1. **创建元音集合**：
   - 使用 `set("aeiouAEIOU")` 来存储所有的元音字母，包括大小写，这样查找元音字母的时间复杂度是 O(1)。

2. **双指针遍历**：
   - 我们使用 `left` 从字符串的开始位置遍历，`right` 从末尾开始遍历。
   - 当 `left` 和 `right` 都指向元音字母时，我们交换它们。
   - 如果 `left` 不是元音，则 `left` 右移；如果 `right` 不是元音，则 `right` 左移。

3. **交换元音字母**：
   - 当 `left` 和 `right` 指向的字符都是元音时，交换它们。
   - 交换后继续移动指针，直到 `left` 和 `right` 相遇。

4. **返回结果**：
   - 将列表转换回字符串并返回结果。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 `n` 是字符串的长度。每个字符最多被访问两次（一次通过 `left`，一次通过 `right`），因此时间复杂度为 O(n)。
  
- **空间复杂度**：O(n)，因为我们将字符串转换为字符数组来进行修改，并在最后将其重新转换为字符串。

---

### 示例讲解：

#### 示例 1:

```
输入: s = "hello"
```

- 初始状态：`left = 0`, `right = 4`。
- `'h'` 不是元音，`left` 右移到 `1`。
- `'o'` 是元音，`right` 左移到 `3`。
- `'e'` 和 `'o'` 都是元音，交换它们，结果为 `["h","o","l","l","e"]`。
- 指针继续移动，`left` 到达 `2`，`right` 到达 `2`，反转完成。

结果：`"holle"`。

#### 示例 2:

```
输入: s = "leetcode"
```

- 初始状态：`left = 0`, `right = 7`。
- `'l'` 不是元音，`left` 右移到 `1`。
- `'e'` 是元音，`right` 左移到 `6`。
- `'e'` 和 `'e'` 是元音，交换后不变。
- 继续处理，`left` 到 `2`，`right` 到 `5`。
- 交换 `'o'` 和 `'e'`，最后结果为 `["l","e","o","t","c","e","d","e"]`。

结果：`"leotcede"`。

---

### 总结

- **中文**：通过双指针法，我们可以高效地找到字符串中的元音字母并进行反转操作。此方法只使用 O(n) 的时间和 O(n) 的空间来处理。

---

### 推荐相似问题：

1. [LeetCode 344: 反转字符串](https://leetcode.com/problems/reverse-string/)
2. [LeetCode 541: 反转字符串 II](https://leetcode.com/problems/reverse-string-ii/)
3. [LeetCode 557: 反转字符串中的单词 III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)
4. [LeetCode 151: 翻转字符串里的单词](https://leetcode.com/problems/reverse-words-in-a-string/)
