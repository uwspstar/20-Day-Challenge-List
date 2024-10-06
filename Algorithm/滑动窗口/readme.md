# 滑动窗口 (Sliding Window)

### Definition
滑动窗口是一种用于处理数组或字符串中连续子序列的高效算法。它通过定义一个窗口范围，在该范围内执行操作或计算，然后根据需要动态调整窗口的起始和结束位置。滑动窗口技术通常用于解决最小/最大子数组问题、子串查找等。

### Key Concepts
- **窗口 (Window)**: 当前处理的子数组或子串的范围，通常由两个指针表示（左指针和右指针）。
- **动态调整 (Dynamic Adjustment)**: 根据条件变化来移动窗口的起始或结束位置，以满足特定要求。
- **时间复杂度优化 (Time Complexity Optimization)**: 通过滑动窗口，避免重复计算，从而降低时间复杂度。

### 滑动窗口的步骤
1. **初始化窗口**: 设置左右指针，通常左指针为 0，右指针用于遍历数组或字符串。
2. **扩展窗口**: 通过移动右指针扩大窗口，增加当前元素。
3. **收缩窗口**: 当满足某种条件时，移动左指针以收缩窗口，移除不再需要的元素。
4. **处理结果**: 根据窗口的大小或内容进行处理，更新结果。

### 滑动窗口的适用场景
- 查找最大或最小子数组/子串
- 字符串匹配问题
- 固定大小窗口的移动计算

### 时间复杂度分析
- **时间复杂度**: O(n)，其中 n 是数组或字符串的长度。每个元素最多被访问两次（一次被加入窗口，一次被移出窗口）。
- **空间复杂度**: O(1) 或 O(k)，具体取决于存储窗口中元素的方式。

### Python 滑动窗口模板
```python
def sliding_window(arr, k):
    n = len(arr)
    if n < k:
        return []  # 如果数组长度小于窗口大小，返回空数组

    max_sum = float('-inf')  # 初始化最大和
    current_sum = 0

    # 计算初始窗口的和
    for i in range(k):
        current_sum += arr[i]

    max_sum = current_sum  # 更新最大和

    # 移动窗口
    for i in range(k, n):
        current_sum += arr[i] - arr[i - k]  # 加入新元素并移除旧元素
        max_sum = max(max_sum, current_sum)  # 更新最大和

    return max_sum  # 返回最大和
```

---

#### Python 滑动窗口模板

```python
def sliding_window_example(arr, target):
    left = 0  # 初始化左指针
    window_sum = 0  # 初始化窗口的累加和
    for right in range(len(arr)):  # 右指针逐步遍历数组
        window_sum += arr[right]  # 更新窗口累加和
        while window_sum > target:  # 如果窗口内的和大于目标值
            window_sum -= arr[left]  # 移除左指针指向的值
            left += 1  # 左指针右移
        # 此时窗口内的元素满足某种条件，可以进行记录或处理
```

---

以下是对两种滑动窗口模板的比较，评估其结构、清晰度和功能性。

### 原始滑动窗口模板
```python
def sliding_window(arr, k):
    n = len(arr)
    if n < k:
        return []  # 如果数组长度小于窗口大小，返回空数组

    max_sum = float('-inf')  # 初始化最大和
    current_sum = 0

    # 计算初始窗口的和
    for i in range(k):
        current_sum += arr[i]

    max_sum = current_sum  # 更新最大和

    # 移动窗口
    for i in range(k, n):
        current_sum += arr[i] - arr[i - k]  # 加入新元素并移除旧元素
        max_sum = max(max_sum, current_sum)  # 更新最大和

    return max_sum  # 返回最大和
```

### 新的滑动窗口模板
```python
def sliding_window_example(arr, target):
    left = 0  # 初始化左指针
    window_sum = 0  # 初始化窗口的累加和
    for right in range(len(arr)):  # 右指针逐步遍历数组
        window_sum += arr[right]  # 更新窗口累加和
        while window_sum > target:  # 如果窗口内的和大于目标值
            window_sum -= arr[left]  # 移除左指针指向的值
            left += 1  # 左指针右移
        # 此时窗口内的元素满足某种条件，可以进行记录或处理
```

### 比较

1. **清晰度和结构**:
   - **原始模板**: 该模板对于特定问题（找到大小为 `k` 的子数组的最大和）结构良好。它清晰地初始化变量并处理数组大小的边界情况。注释有助于指导用户理解每一步。
   - **新模板**: 该模板同样清晰，专注于不同的问题（根据目标和调整窗口）。它有效地使用注释来解释每一行的目的，特别是 `while` 循环，这对理解滑动窗口的调整至关重要。

2. **功能性**:
   - **原始模板**: 该实现直接计算固定大小 `k` 的子数组的最大和，适用于问题陈述中要求特定子数组大小的情况。
   - **新模板**: 该实现更灵活，根据目标和动态调整窗口大小。它可以适应各种问题，例如查找满足特定条件的子数组。

3. **适用场景**:
   - **原始模板**: 最适合那些问题陈述中指定固定窗口大小的情况。
   - **新模板**: 更加多功能，允许处理涉及动态窗口内求和的更广泛问题。

### 结论
- **哪个更好？** 这取决于你要解决的具体问题：
  - 如果你需要固定大小窗口的求和问题，**原始模板**更好。
  - 如果你需要根据条件（如目标和）动态调整窗口，**新模板**更优秀。

总体而言，两种模板各有优点，适用于不同类型的滑动窗口问题。你可以根据当前需求选择其中一种，或者结合两者的优点来构建更强大的解决方案库。


---

好的，我们将逐步讲解 30 道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。以下是前五道滑动窗口题目的详细解析和代码实现。

---

### 1. LeetCode 3: Longest Substring Without Repeating Characters（无重复字符的最长子串）

**题目描述**：
给定一个字符串 `s`，找到其中不含有重复字符的最长子串的长度。

**解题思路**：
使用滑动窗口法解决此问题。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用一个哈希集合 `set` 记录窗口中已经出现的字符。在每次迭代中，右指针向右移动，如果当前字符不在集合中，则将其加入集合，并更新最长子串长度。否则，将左指针右移，直到删除重复字符为止。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算无重复字符最长子串长度的函数
    def lengthOfLongestSubstring(self, s: str) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        max_length = 0
        # 使用集合记录窗口中出现的字符
        char_set = set()

        # 右指针遍历整个字符串
        for right in range(len(s)):
            # 如果当前字符在集合中，说明有重复字符
            while s[right] in char_set:
                # 从左边移除字符，直到没有重复字符
                char_set.remove(s[left])
                left += 1

            # 将当前字符加入集合
            char_set.add(s[right])
            # 更新最长子串长度
            max_length = max(max_length, right - left + 1)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(min(n, m)) - 其中 n 是字符串的长度，m 是字符集的大小（取决于字符串的字符类型）。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(min(n, m))，其中 n 是字符串的长度，m 是字符集的大小（取决于字符串的字符类型）。

---

### 2. LeetCode 76: Minimum Window Substring（最小覆盖子串）

**题目描述**：
给定一个字符串 `s` 和一个字符串 `t`，找到 `s` 中包含 `t` 所有字符的最小子串。如果 `s` 中不存在这样的子串，则返回空字符串 `""`。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用两个哈希表 `need` 和 `window` 记录目标字符和当前窗口中字符的个数。移动右指针扩大窗口，直到窗口中包含了 `t` 中所有字符，然后移动左指针缩小窗口，直到窗口不再包含所有字符为止。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找最小覆盖子串的函数
    def minWindow(self, s: str, t: str) -> str:
        # 如果目标字符串为空，直接返回空字符串
        if not t or not s:
            return ""

        # 记录目标字符串 t 中每个字符的个数
        need = defaultdict(int)
        for c in t:
            need[c] += 1

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录满足条件的字符个数和最小子串的起始位置及长度
        valid = 0
        start = 0
        min_len = float("inf")

        # 记录当前窗口中每个字符的个数
        window = defaultdict(int)

        # 右指针遍历整个字符串 s
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1

            # 更新窗口中的数据
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    valid += 1

            # 当窗口中的字符包含目标字符串所有字符时，尝试缩小窗口
            while valid == len(need):
                # 更新最小覆盖子串
                if right - left < min_len:
                    start = left
                    min_len = right - left

                # 当前字符将要移出窗口
                d = s[left]
                left += 1

                # 更新窗口中的数据
                if d in need:
                    if window[d] == need[d]:
                        valid -= 1
                    window[d] -= 1

        # 返回最小覆盖子串
        return "" if min_len == float("inf") else s[start:start + min_len]

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(m) - 哈希表存储目标字符串中每个字符的个数，其中 m 是目标字符串 t 的长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储目标字符串中每个字符的个数，其中 m 是目标字符串 t 的长度。

---

### 3. LeetCode 567: Permutation in String（字符串的排列）

**题目描述**：
给定两个字符串 `s1` 和 `s2`，写一个函数判断 `s2` 中是否包含 `s1` 的排列。如果是，返回 `true`；否则，返回 `false`。

**解题思路**：
使用滑动窗口法。在 `s2` 中查找 `s1` 的排列，使用两个哈希表 `need` 和 `window` 记录 `s1` 中每个字符的个数和当前窗口中字符的个数。移动右指针扩大窗口，直到窗口中包含了 `s1` 中所有字符，返回 `true`，否则返回 `false`。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义判断字符串的排列是否存在的函数
    def checkInclusion(self, s1: str, s2: str) -> bool:
        # 记录 s1 中每个字符的个数
        need = defaultdict(int)
        for c in s1:
            need[c] += 1

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录满足条件的字符个数
        valid = 0

        # 记录当前窗口中每个字符的个数
        window = defaultdict(int)

        # 右指针遍历整个字符串 s2
        while right < len(s2):
            # 当前字符进入窗口
            c = s2[right]
            right += 1

            # 更新窗口中的数据
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    valid += 1

            # 当窗口的长度等于 s1 的长度时，尝试判断是否为排列
            while right - left >= len(s1):
                if valid == len(need):
                    return True

                # 当前字符将要移出窗口
                d = s2[left]
                left += 1

                # 更新窗口中的数据
                if d in need:
                    if window[d] == need[d]:
                        valid -= 1
                    window[d] -= 1

        # 未找到符合条件的排列
        return False

# 时间复杂度：O(n) - 遍历字符串 s2 的时间复杂度，其中 n 是 s2 的长度。
# 空间复杂度：O(m) - 哈希表存储字符串 s1 中每个字符的个数，其中 m 是 s1 的长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历字符串 s2 的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储字符串 s1 中每个字符的个数，其中 m 是 s1 的长度。

---

### 4. LeetCode 438: Find All Anagrams in a String（找到字符串中所有字母异位词）

**题目描述**：
给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的字母异位词，返回它们的起始索引。

**解题思路**：
使用滑动窗口法。在 `s` 中查找 `p` 的字母异位词，使用两个哈希表 `need` 和 `window` 记录 `p` 中每个字符的个数和当前窗口中字符的个数。移动右指

针扩大窗口，直到窗口中包含了 `p` 中所有字符，记录起始索引，并移动左指针继续查找下一个异位词。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找字母异位词的函数
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # 记录 p 中每个字符的个数
        need = defaultdict(int)
        for c in p:
            need[c] += 1

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录满足条件的字符个数和结果列表
        valid = 0
        result = []

        # 记录当前窗口中每个字符的个数
        window = defaultdict(int)

        # 右指针遍历整个字符串 s
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1

            # 更新窗口中的数据
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    valid += 1

            # 当窗口的长度等于 p 的长度时，判断是否为异位词
            while right - left >= len(p):
                if valid == len(need):
                    result.append(left)

                # 当前字符将要移出窗口
                d = s[left]
                left += 1

                # 更新窗口中的数据
                if d in need:
                    if window[d] == need[d]:
                        valid -= 1
                    window[d] -= 1

        return result

# 时间复杂度：O(n) - 遍历字符串 s 的时间复杂度，其中 n 是 s 的长度。
# 空间复杂度：O(m) - 哈希表存储字符串 p 中每个字符的个数，其中 m 是 p 的长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历字符串 s 的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储字符串 p 中每个字符的个数，其中 m 是 p 的长度。

---

### 5. LeetCode 159: Longest Substring with At Most Two Distinct Characters（至多包含两个不同字符的最长子串）

**题目描述**：
给定一个字符串 `s`，找到至多包含两个不同字符的最长子串。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用一个哈希表 `window` 记录窗口中每个字符的个数。移动右指针扩大窗口，直到窗口中包含的不同字符超过两个，然后移动左指针缩小窗口，直到窗口中包含的不同字符不超过两个为止，并更新最长子串长度。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找至多包含两个不同字符的最长子串的函数
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        # 如果字符串为空，直接返回 0
        if not s:
            return 0

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每个字符的个数和最长子串长度
        window = defaultdict(int)
        max_length = 0

        # 右指针遍历整个字符串
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1
            window[c] += 1

            # 当窗口中不同字符的个数超过两个时，移动左指针缩小窗口
            while len(window) > 2:
                d = s[left]
                left += 1
                window[d] -= 1
                if window[d] == 0:
                    del window[d]

            # 更新最长子串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(1) - 最多存储两个不同字符及其个数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(1)，最多存储两个不同字符及其个数。

---

好的，我们继续讲解接下来的五道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 6. LeetCode 992: Subarrays with K Different Integers（K 个不同整数的子数组）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，返回 `nums` 中包含恰好 `k` 个不同整数的子数组的个数。

**解题思路**：
使用滑动窗口法。定义两个滑动窗口，分别用于计算最多包含 `k` 个不同整数的子数组和最多包含 `k-1` 个不同整数的子数组的个数，二者之差即为恰好包含 `k` 个不同整数的子数组个数。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算恰好包含 k 个不同整数的子数组个数的函数
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        # 定义辅助函数：计算最多包含 K 个不同整数的子数组个数
        def atMostK(nums, k):
            left = 0
            count = 0
            window = defaultdict(int)  # 存储窗口中每个数字的出现次数

            for right in range(len(nums)):
                # 当前数字进入窗口
                if window[nums[right]] == 0:
                    k -= 1
                window[nums[right]] += 1

                # 当窗口中的不同数字超过 K 个时，移动左指针缩小窗口
                while k < 0:
                    window[nums[left]] -= 1
                    if window[nums[left]] == 0:
                        k += 1
                    left += 1

                # 计算当前窗口中所有子数组的个数
                count += right - left + 1

            return count

        # 返回最多包含 K 个不同整数的子数组个数 - 最多包含 K-1 个不同整数的子数组个数
        return atMostK(nums, k) - atMostK(nums, k - 1)

# 时间复杂度：O(n) - 遍历数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(k) - 存储滑动窗口中每个数字的出现次数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历数组的时间复杂度。
- **空间复杂度**：O(k)，存储滑动窗口中每个数字的出现次数。

---

### 7. LeetCode 424: Longest Repeating Character Replacement（替换后的最长重复字符）

**题目描述**：
给定一个字符串 `s` 和一个整数 `k`，你可以将字符串中任意字符替换为任何其他字符，最多替换 `k` 次。返回替换后包含相同字符的最长子串的长度。

**解题思路**：
使用滑动窗口法。在每次迭代中，右指针向右移动，并更新窗口中字符出现的最大频率 `max_freq`。当窗口的长度减去 `max_freq` 大于 `k` 时，说明窗口中有太多字符需要被替换，此时移动左指针缩小窗口。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义计算替换后的最长重复字符的长度的函数
    def characterReplacement(self, s: str, k: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每个字符的个数和最长子串长度
        window = defaultdict(int)
        max_length = 0
        max_freq = 0  # 记录窗口中出现次数最多的字符的频率

        # 右指针遍历整个字符串
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1
            window[c] += 1
            # 更新最大频率
            max_freq = max(max_freq, window[c])

            # 当窗口长度减去最大频率大于 k 时，说明需要缩小窗口
            while right - left - max_freq > k:
                d = s[left]
                left += 1
                window[d] -= 1

            # 更新最长子串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(1) - 存储滑动窗口中每个字符的个数，最多 26 个字符。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(1)，存储滑动窗口中每个字符的个数，最多 26 个字符。

---

### 8. LeetCode 340: Longest Substring with At Most K Distinct Characters（至多包含 K 个不同字符的最长子串）

**题目描述**：
给定一个字符串 `s` 和一个整数 `k`，找到至多包含 `k` 个不同字符的最长子串。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用一个哈希表 `window` 记录窗口中每个字符的个数。移动右指针扩大窗口，直到窗口中包含的不同字符超过 `k`，然后移动左指针缩小窗口，直到窗口中包含的不同字符不超过 `k` 为止，并更新最长子串长度。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找至多包含 K 个不同字符的最长子串的函数
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        # 如果字符串为空或 K 为 0，直接返回 0
        if not s or k == 0:
            return 0

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每个字符的个数和最长子串长度
        window = defaultdict(int)
        max_length = 0

        # 右指针遍历整个字符串
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1
            window[c] += 1

            # 当窗口中不同字符的个数超过 K 个时，移动左指针缩小窗口
            while len(window) > k:
                d = s[left]
                left += 1
                window[d] -= 1
                if window[d] == 0:
                    del window[d]

            # 更新最长子串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(k) - 存储 K 个不同字符及其个数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(k)，存储 K 个不同字符及其个数。

---

### 9. LeetCode 1004: Max Consecutive Ones III（最大连续 1 的个数 III）

**题目描述**：
给定一个二进制数组 `nums` 和一个整数 `k`，如果最多可以将 `k` 个 0 变为 1，返回数组中包含 1 的最长子数组的长度。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并记录当前窗口中 0 的个数。当窗口中 0 的个数大于 `k` 时，移动左指针缩小窗口。每次更新最长子数组的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最大连续 1 的个数的函数
    def longestOnes(self, nums: List[int], k: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中 0 的个数和最长子数组长度
        zero_count = 0
        max_length = 0

        # 右指针遍历整个数组
        while right < len(nums):
            # 当前数字进入窗口
            if nums[right] == 0:
                zero_count += 1
            right += 1

            # 当窗口中 0 的个数大于 k 时，移动左指针

缩小窗口
            while zero_count > k:
                if nums[left] == 0:
                    zero_count -= 1
                left += 1

            # 更新最长子数组长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 10. LeetCode 1052: Grumpy Bookstore Owner（易怒书店老板）

**题目描述**：
有一位易怒的书店老板，他会在一些时段对顾客态度不佳。给定一个整数数组 `customers` 表示每个时段光顾书店的顾客数量，以及一个二进制数组 `grumpy` 表示每个时段老板的态度，1 表示易怒，0 表示态度良好。你有 `X` 分钟的时间来使老板的态度良好，返回在这段时间内书店接待的最大顾客数量。

**解题思路**：
使用滑动窗口法。在每个时段，计算基础的顾客数量（不被老板易怒影响的顾客）。使用滑动窗口找到最大长度为 `X` 的窗口，使得这个窗口内被老板易怒影响的顾客数量最多，最后将其加入基础顾客数量中。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最大顾客数量的函数
    def maxSatisfied(self, customers: List[int], grumpy: List[int], X: int) -> int:
        # 计算基础顾客数量（不被老板易怒影响的顾客）
        base_satisfied = sum(customers[i] for i in range(len(customers)) if grumpy[i] == 0)
        # 计算初始滑动窗口中被老板影响的顾客数量
        additional_satisfied = sum(customers[i] for i in range(X) if grumpy[i] == 1)

        # 初始化最大额外顾客数量
        max_additional = additional_satisfied

        # 滑动窗口从左向右移动
        for i in range(X, len(customers)):
            # 移动滑动窗口，更新被影响的顾客数量
            if grumpy[i] == 1:
                additional_satisfied += customers[i]
            if grumpy[i - X] == 1:
                additional_satisfied -= customers[i - X]

            # 更新最大额外顾客数量
            max_additional = max(max_additional, additional_satisfied)

        # 返回基础顾客数量加上最大额外顾客数量
        return base_satisfied + max_additional

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

好的，我们继续讲解接下来的五道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 11. LeetCode 239: Sliding Window Maximum（滑动窗口最大值）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，在 `nums` 中找出长度为 `k` 的所有子数组的最大值，返回这些最大值组成的列表。

**解题思路**：
使用双端队列来维护当前滑动窗口的最大值。在每次滑动窗口向右移动时，移除队列中超出窗口的元素，并将当前元素加入队列中。队列的第一个元素始终是窗口中的最大值。

**代码实现**：
```python
# 导入 collections 模块
from collections import deque

# 定义解决方案的类
class Solution:
    # 定义查找滑动窗口最大值的函数
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # 初始化结果列表和双端队列
        result = []
        deq = deque()  # 存储当前滑动窗口中元素的索引

        # 遍历整个数组
        for i in range(len(nums)):
            # 如果队列的首个元素超出当前窗口，移除它
            if deq and deq[0] < i - k + 1:
                deq.popleft()

            # 移除队列中所有比当前元素小的元素（这些元素不可能成为最大值）
            while deq and nums[deq[-1]] < nums[i]:
                deq.pop()

            # 将当前元素的索引加入队列
            deq.append(i)

            # 当窗口大小达到 k 时，记录当前窗口的最大值
            if i >= k - 1:
                result.append(nums[deq[0]])

        return result

# 时间复杂度：O(n) - 每个元素最多被加入和移除队列一次。
# 空间复杂度：O(k) - 存储滑动窗口中最多 k 个元素的索引。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，每个元素最多被加入和移除队列一次。
- **空间复杂度**：O(k)，存储滑动窗口中最多 k 个元素的索引。

---

### 12. LeetCode 424: Longest Repeating Character Replacement（替换后的最长重复字符）

**题目描述**：
给定一个字符串 `s` 和一个整数 `k`，你可以将字符串中任意字符替换为任何其他字符，最多替换 `k` 次。返回替换后包含相同字符的最长子串的长度。

**解题思路**：
使用滑动窗口法。在每次迭代中，右指针向右移动，并更新窗口中字符出现的最大频率 `max_freq`。当窗口的长度减去 `max_freq` 大于 `k` 时，说明窗口中有太多字符需要被替换，此时移动左指针缩小窗口。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义计算替换后的最长重复字符的长度的函数
    def characterReplacement(self, s: str, k: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每个字符的个数和最长子串长度
        window = defaultdict(int)
        max_length = 0
        max_freq = 0  # 记录窗口中出现次数最多的字符的频率

        # 右指针遍历整个字符串
        while right < len(s)):
            # 当前字符进入窗口
            c = s[right]
            right += 1
            window[c] += 1
            # 更新最大频率
            max_freq = max(max_freq, window[c])

            # 当窗口长度减去最大频率大于 k 时，说明需要缩小窗口
            while right - left - max_freq > k:
                d = s[left]
                left += 1
                window[d] -= 1

            # 更新最长子串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(1) - 存储滑动窗口中每个字符的个数，最多 26 个字符。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(1)，存储滑动窗口中每个字符的个数，最多 26 个字符。

---

### 13. LeetCode 643: Maximum Average Subarray I（最大平均子数组 I）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，找到长度为 `k` 的子数组的最大平均值。

**解题思路**：
使用滑动窗口法。在遍历数组时，维护一个长度为 `k` 的滑动窗口，每次更新窗口中的元素和，计算当前窗口的平均值并更新最大平均值。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最大平均子数组的函数
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        # 计算初始窗口的元素和
        current_sum = sum(nums[:k])
        max_sum = current_sum

        # 滑动窗口从左向右移动
        for i in range(k, len(nums)):
            # 更新当前窗口的元素和
            current_sum += nums[i] - nums[i - k]
            max_sum = max(max_sum, current_sum)

        # 返回最大平均值
        return max_sum / k

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 14. LeetCode 239: Sliding Window Maximum（滑动窗口最大值）

**题目描述**：
给定一个整数数组 `nums` 和一个整数 `k`，在 `nums` 中找出长度为 `k` 的所有子数组的最大值，返回这些最大值组成的列表。

**解题思路**：
使用双端队列来维护当前滑动窗口的最大值。在每次滑动窗口向右移动时，移除队列中超出窗口的元素，并将当前元素加入队列中。队列的第一个元素始终是窗口中的最大值。

**代码实现**：
```python
# 导入 collections 模块
from collections import deque

# 定义解决方案的类
class Solution:
    # 定义查找滑动窗口最大值的函数
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # 初始化结果列表和双端队列
        result = []
        deq = deque()  # 存储当前滑动窗口中元素的索引

        # 遍历整个数组
        for i in range(len(nums)):
            # 如果队列的首个元素超出当前窗口，移除它
            if deq and deq[0] < i - k + 1:
                deq.popleft()

            # 移除队列中所有比当前元素小的元素（这些元素不可能成为最大值）
            while deq and nums[deq[-1]] < nums[i]:
                deq.pop()

            # 将当前元素的索引加入队列
            deq.append(i)

            # 当窗口大小达到 k 时，记录当前窗口的最大值
            if i >= k - 1:
                result.append(nums[deq[0]])

        return result

# 时间复杂度：O(n) - 每个元素最多被加入和移除队列一次。
# 空间复杂度：O(k) - 存储滑动窗口中最多 k 个元素的索引。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，每个元素最多被加入和移除队列一次。
- **空间复杂度**：O(k)，存储滑动窗口中最多 k 个元素的索引。

---

### 15. LeetCode 1208: Get Equal Substrings Within Budget（预算内均衡子字符串）

**题目描述**：
给定两个长度相同的字符串 `s` 和 `t` 以及一个整数 `maxCost`，你可以将 `s` 中的任意字符替换为 `t` 中对应位置的字符，替换的成本

是两字符的 ASCII 值差的绝对值，返回在预算 `maxCost` 内能得到的最长均衡子字符串的长度。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并计算窗口中字符替换的总成本。当总成本大于 `maxCost` 时，移动左指针缩小窗口，直到总成本小于等于 `maxCost`，然后更新最长均衡子字符串长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算预算内最长均衡子字符串的长度的函数
    def equalSubstring(self, s: str, t: str, maxCost: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中的总成本和最长子字符串长度
        total_cost = 0
        max_length = 0

        # 右指针遍历整个字符串
        while right < len(s):
            # 计算当前字符替换的成本，并更新总成本
            total_cost += abs(ord(s[right]) - ord(t[right]))
            right += 1

            # 当总成本大于 maxCost 时，移动左指针缩小窗口
            while total_cost > maxCost:
                total_cost -= abs(ord(s[left]) - ord(t[left]))
                left += 1

            # 更新最长子字符串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

好的，我们继续讲解接下来的五道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 16. LeetCode 930: Binary Subarrays With Sum（二进制子数组的和）

**题目描述**：
给定一个二进制数组 `nums` 和一个目标和 `goal`，返回和为 `goal` 的非空子数组的个数。

**解题思路**：
使用前缀和+滑动窗口法来解决。定义一个 `prefix_sum` 记录当前窗口的前缀和，使用一个字典 `count_map` 记录前缀和出现的次数。每次遇到新的前缀和时，检查 `prefix_sum - goal` 是否存在于字典中，如果存在，则说明存在一个子数组和为 `goal`，将其计数加到结果中。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义计算二进制子数组和为 goal 的个数的函数
    def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:
        # 初始化前缀和和结果计数器
        prefix_sum = 0
        result = 0
        # 使用字典记录前缀和出现的次数
        count_map = defaultdict(int)
        count_map[0] = 1  # 初始化前缀和为 0 的计数

        # 遍历整个数组
        for num in nums:
            # 更新当前前缀和
            prefix_sum += num
            # 如果前缀和减去目标和在字典中，说明存在一个子数组和为 goal
            if prefix_sum - goal in count_map:
                result += count_map[prefix_sum - goal]
            # 更新前缀和在字典中的计数
            count_map[prefix_sum] += 1

        return result

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(n) - 字典存储前缀和出现次数的空间复杂度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(n)，字典存储前缀和出现次数的空间复杂度。

---

### 17. LeetCode 904: Fruit Into Baskets（放入篮子的水果）

**题目描述**：
在一条街上，你有两个篮子，可以装任意数量的水果，但每个篮子只能装一种类型的水果。给定一个整数数组 `fruits`，其中 `fruits[i]` 表示第 `i` 个水果的类型，找到两个篮子能够装下的水果的最长子数组长度。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用一个字典 `basket` 记录窗口中每种水果的个数。当窗口中不同水果的种类超过两种时，移动左指针缩小窗口，直到窗口中只剩下两种水果为止，并更新最长子数组长度。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找两个篮子能够装下的最长子数组的长度的函数
    def totalFruit(self, fruits: List[int]) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每种水果的个数和最长子数组长度
        basket = defaultdict(int)
        max_length = 0

        # 右指针遍历整个数组
        while right < len(fruits):
            # 当前水果进入窗口
            basket[fruits[right]] += 1
            right += 1

            # 当窗口中不同水果的种类超过两种时，移动左指针缩小窗口
            while len(basket) > 2:
                basket[fruits[left]] -= 1
                if basket[fruits[left]] == 0:
                    del basket[fruits[left]]
                left += 1

            # 更新最长子数组长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 最多存储两种不同类型的水果及其个数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，最多存储两种不同类型的水果及其个数。

---

### 18. LeetCode 1208: Get Equal Substrings Within Budget（预算内均衡子字符串）

**题目描述**：
给定两个长度相同的字符串 `s` 和 `t` 以及一个整数 `maxCost`，你可以将 `s` 中的任意字符替换为 `t` 中对应位置的字符，替换的成本是两字符的 ASCII 值差的绝对值，返回在预算 `maxCost` 内能得到的最长均衡子字符串的长度。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并计算窗口中字符替换的总成本。当总成本大于 `maxCost` 时，移动左指针缩小窗口，直到总成本小于等于 `maxCost`，然后更新最长均衡子字符串长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算预算内最长均衡子字符串的长度的函数
    def equalSubstring(self, s: str, t: str, maxCost: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中的总成本和最长子字符串长度
        total_cost = 0
        max_length = 0

        # 右指针遍历整个字符串
        while right < len(s):
            # 计算当前字符替换的成本，并更新总成本
            total_cost += abs(ord(s[right]) - ord(t[right]))
            right += 1

            # 当总成本大于 maxCost 时，移动左指针缩小窗口
            while total_cost > maxCost:
                total_cost -= abs(ord(s[left]) - ord(t[left]))
                left += 1

            # 更新最长子字符串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 19. LeetCode 485: Max Consecutive Ones（最大连续 1 的个数）

**题目描述**：
给定一个二进制数组 `nums`，找到最长的连续 1 的个数。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界。当右指针遇到 0 时，重置左指针位置。每次更新最大连续 1 的个数。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最大连续 1 的个数的函数
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录最长连续 1 的个数
        max_length = 0

        # 右指针遍历整个数组
        while right < len(nums):
            # 当遇到 0 时，左指针移动到右指针的下一个位置
            if nums[right] == 0:
                left = right + 1
            right += 1

            # 更新最大连续 1 的个数
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用

了常量级别的额外空间。

---

### 20. LeetCode 485: Max Consecutive Ones（最大连续 1 的个数）

**题目描述**：
给定一个二进制数组 `nums`，找到最长的连续 1 的个数。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界。当右指针遇到 0 时，重置左指针位置。每次更新最大连续 1 的个数。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最大连续 1 的个数的函数
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录最长连续 1 的个数
        max_length = 0

        # 右指针遍历整个数组
        while right < len(nums):
            # 当遇到 0 时，左指针移动到右指针的下一个位置
            if nums[right] == 0:
                left = right + 1
            right += 1

            # 更新最大连续 1 的个数
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

好的，我们继续讲解接下来的五道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 21. LeetCode 1209: Remove All Adjacent Duplicates in String II（删除字符串中的所有相邻重复项 II）

**题目描述**：
给定一个字符串 `s` 和一个整数 `k`，你需要对 `s` 中的相邻 `k` 个重复字符进行删除，直到字符串中不再含有 `k` 个连续的相同字符。返回最终的字符串。

**解题思路**：
使用滑动窗口法和栈的结合。定义一个栈 `stack`，存储字符和该字符的连续次数。当遍历字符串时，如果当前字符与栈顶字符相同，则将其次数加 1；否则，将当前字符和次数压入栈中。当某个字符的连续次数等于 `k` 时，从栈中移除该字符。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除所有相邻重复项的函数
    def removeDuplicates(self, s: str, k: int) -> str:
        # 定义栈，存储字符及其连续出现的次数
        stack = []

        # 遍历整个字符串
        for char in s:
            # 如果栈不为空，且当前字符与栈顶字符相同，则增加栈顶字符的计数
            if stack and stack[-1][0] == char:
                stack[-1][1] += 1
                # 如果栈顶字符的计数等于 k，则将其移除
                if stack[-1][1] == k:
                    stack.pop()
            else:
                # 否则，将当前字符及其计数（1）加入栈中
                stack.append([char, 1])

        # 生成最终结果字符串
        result = "".join(char * count for char, count in stack)
        return result

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(n) - 栈的最大空间复杂度取决于字符串长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(n)，栈的最大空间复杂度取决于字符串长度。

---

### 22. LeetCode 1004: Max Consecutive Ones III（最大连续 1 的个数 III）

**题目描述**：
给定一个二进制数组 `nums` 和一个整数 `k`，如果最多可以将 `k` 个 0 变为 1，返回数组中包含 1 的最长子数组的长度。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并记录当前窗口中 0 的个数。当窗口中 0 的个数大于 `k` 时，移动左指针缩小窗口。每次更新最长子数组的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最大连续 1 的个数的函数
    def longestOnes(self, nums: List[int], k: int) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中 0 的个数和最长子数组长度
        zero_count = 0
        max_length = 0

        # 右指针遍历整个数组
        while right < len(nums)):
            # 当前数字进入窗口
            if nums[right] == 0:
                zero_count += 1
            right += 1

            # 当窗口中 0 的个数大于 k 时，移动左指针缩小窗口
            while zero_count > k:
                if nums[left] == 0:
                    zero_count -= 1
                left += 1

            # 更新最长子数组长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 23. LeetCode 713: Subarray Product Less Than K（乘积小于 K 的子数组）

**题目描述**：
给定一个正整数数组 `nums` 和一个整数 `k`，返回数组中所有乘积小于 `k` 的连续子数组的个数。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并记录当前窗口中所有元素的乘积。当窗口中乘积大于或等于 `k` 时，移动左指针缩小窗口。每次移动右指针时，累加当前窗口中子数组的个数。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算乘积小于 K 的子数组的个数的函数
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        # 如果 k 小于等于 1，则不存在乘积小于 k 的子数组
        if k <= 1:
            return 0

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中所有元素的乘积和子数组个数
        product = 1
        count = 0

        # 右指针遍历整个数组
        while right < len(nums):
            # 更新当前窗口中所有元素的乘积
            product *= nums[right]
            right += 1

            # 当乘积大于等于 k 时，移动左指针缩小窗口
            while product >= k:
                product //= nums[left]
                left += 1

            # 计算当前窗口中子数组的个数
            count += right - left

        return count

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 24. LeetCode 209: Minimum Size Subarray Sum（长度最小的子数组）

**题目描述**：
给定一个包含正整数的数组 `nums` 和一个正整数 `target`，找到一个长度最小的连续子数组，使得该子数组的元素之和大于等于 `target`，返回该子数组的长度。如果不存在这样的子数组，返回 `0`。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并记录当前窗口中所有元素的和。当窗口中元素的和大于等于 `target` 时，记录最小子数组长度，并移动左指针缩小窗口，直到元素和小于 `target`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找长度最小的子数组的函数
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中所有元素的和和最小子数组长度
        current_sum = 0
        min_length = float("inf")

        # 右指针遍历整个数组
        while right < len(nums):
            # 更新当前窗口中所有元素的和
            current_sum += nums[right]
            right += 1

            # 当当前窗口中所有元素的和大于等于 target 时，尝试缩小窗口
            while current_sum >= target:
                min_length = min(min_length, right - left)
                current_sum -= nums[left]
                left += 1

        # 如果最小子数组长度仍然为初始值，说明不存在满足条件的子数组
        return 0 if min_length == float("inf") else min_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度

**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 25. LeetCode 30: Substring with Concatenation of All Words（连接所有单词的子串）

**题目描述**：
给定一个字符串 `s` 和一个字符串数组 `words`，所有字符串的长度相同。找出 `s` 中所有 `words` 连接成的子串的起始索引，返回这些起始索引组成的列表。

**解题思路**：
使用滑动窗口法。在 `s` 中查找由 `words` 中所有字符串连接而成的子串，使用两个哈希表 `need` 和 `window` 分别记录目标字符串和当前窗口中每个字符串的个数。当窗口中字符串的个数与目标字符串个数相等时，记录当前起始索引。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找连接所有单词的子串的函数
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        # 如果输入为空或 words 为空，直接返回空列表
        if not s or not words:
            return []

        # 初始化变量
        word_length = len(words[0])
        word_count = len(words)
        total_length = word_length * word_count
        need = defaultdict(int)
        for word in words:
            need[word] += 1

        # 定义结果列表
        result = []

        # 遍历每个可能的起始位置
        for i in range(word_length):
            left = i
            right = i
            window = defaultdict(int)

            # 右指针遍历整个字符串
            while right + word_length <= len(s):
                # 当前单词进入窗口
                word = s[right:right + word_length]
                right += word_length
                # 如果当前单词是目标单词之一
                if word in need:
                    window[word] += 1
                    # 如果当前单词的个数超过目标数量，移动左指针缩小窗口
                    while window[word] > need[word]:
                        left_word = s[left:left + word_length]
                        window[left_word] -= 1
                        left += word_length

                    # 如果窗口中所有单词的个数与目标数量相等，记录起始索引
                    if right - left == total_length:
                        result.append(left)
                else:
                    # 如果当前单词不在目标单词中，重置窗口
                    window.clear()
                    left = right

        return result

# 时间复杂度：O(n * m) - 遍历整个字符串的时间复杂度，其中 n 是 s 的长度，m 是 words 的长度。
# 空间复杂度：O(m) - 哈希表存储目标字符串中每个单词的个数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * m)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储目标字符串中每个单词的个数。

---

好的，我们继续讲解接下来的五道 LeetCode 滑动窗口题目，包括详细的题目分析、解题思路、逐行代码注释以及时间复杂度和空间复杂度分析。

---

### 26. LeetCode 567: Permutation in String（字符串的排列）

**题目描述**：
给定两个字符串 `s1` 和 `s2`，写一个函数判断 `s2` 中是否包含 `s1` 的排列。如果是，返回 `true`；否则，返回 `false`。

**解题思路**：
使用滑动窗口法。在 `s2` 中查找 `s1` 的排列，使用两个哈希表 `need` 和 `window` 记录 `s1` 中每个字符的个数和当前窗口中字符的个数。移动右指针扩大窗口，直到窗口中包含了 `s1` 中所有字符，返回 `true`，否则返回 `false`。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义判断字符串的排列是否存在的函数
    def checkInclusion(self, s1: str, s2: str) -> bool:
        # 记录 s1 中每个字符的个数
        need = defaultdict(int)
        for c in s1:
            need[c] += 1

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录满足条件的字符个数
        valid = 0

        # 记录当前窗口中每个字符的个数
        window = defaultdict(int)

        # 右指针遍历整个字符串 s2
        while right < len(s2):
            # 当前字符进入窗口
            c = s2[right]
            right += 1

            # 更新窗口中的数据
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    valid += 1

            # 当窗口的长度等于 s1 的长度时，判断是否为排列
            while right - left >= len(s1):
                if valid == len(need):
                    return True

                # 当前字符将要移出窗口
                d = s2[left]
                left += 1

                # 更新窗口中的数据
                if d in need:
                    if window[d] == need[d]:
                        valid -= 1
                    window[d] -= 1

        # 未找到符合条件的排列
        return False

# 时间复杂度：O(n) - 遍历字符串 s2 的时间复杂度，其中 n 是 s2 的长度。
# 空间复杂度：O(m) - 哈希表存储字符串 s1 中每个字符的个数，其中 m 是 s1 的长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历字符串 s2 的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储字符串 s1 中每个字符的个数，其中 m 是 s1 的长度。

---

### 27. LeetCode 340: Longest Substring with At Most K Distinct Characters（至多包含 K 个不同字符的最长子串）

**题目描述**：
给定一个字符串 `s` 和一个整数 `k`，找到至多包含 `k` 个不同字符的最长子串。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并使用一个哈希表 `window` 记录窗口中每个字符的个数。移动右指针扩大窗口，直到窗口中包含的不同字符超过 `k`，然后移动左指针缩小窗口，直到窗口中包含的不同字符不超过 `k` 为止，并更新最长子串长度。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找至多包含 K 个不同字符的最长子串的函数
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        # 如果字符串为空或 K 为 0，直接返回 0
        if not s or k == 0:
            return 0

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中每个字符的个数和最长子串长度
        window = defaultdict(int)
        max_length = 0

        # 右指针遍历整个字符串
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1
            window[c] += 1

            # 当窗口中不同字符的个数超过 K 个时，移动左指针缩小窗口
            while len(window) > k:
                d = s[left]
                left += 1
                window[d] -= 1
                if window[d] == 0:
                    del window[d]

            # 更新最长子串长度
            max_length = max(max_length, right - left)

        return max_length

# 时间复杂度：O(n) - 遍历整个字符串的时间复杂度，其中 n 是字符串的长度。
# 空间复杂度：O(k) - 存储 K 个不同字符及其个数。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个字符串的时间复杂度。
- **空间复杂度**：O(k)，存储 K 个不同字符及其个数。

---

### 28. LeetCode 438: Find All Anagrams in a String（找到字符串中所有字母异位词）

**题目描述**：
给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的字母异位词，返回它们的起始索引。

**解题思路**：
使用滑动窗口法。在 `s` 中查找 `p` 的字母异位词，使用两个哈希表 `need` 和 `window` 记录 `p` 中每个字符的个数和当前窗口中字符的个数。移动右指针扩大窗口，直到窗口中包含了 `p` 中所有字符，记录起始索引，并移动左指针继续查找下一个异位词。

**代码实现**：
```python
# 导入 collections 模块
from collections import defaultdict

# 定义解决方案的类
class Solution:
    # 定义查找字母异位词的函数
    def findAnagrams(self, s: str, p: str) -> List[int]:
        # 记录 p 中每个字符的个数
        need = defaultdict(int)
        for c in p:
            need[c] += 1

        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录满足条件的字符个数和结果列表
        valid = 0
        result = []

        # 记录当前窗口中每个字符的个数
        window = defaultdict(int)

        # 右指针遍历整个字符串 s
        while right < len(s):
            # 当前字符进入窗口
            c = s[right]
            right += 1

            # 更新窗口中的数据
            if c in need:
                window[c] += 1
                if window[c] == need[c]:
                    valid += 1

            # 当窗口的长度等于 p 的长度时，判断是否为异位词
            while right - left >= len(p):
                if valid == len(need):
                    result.append(left)

                # 当前字符将要移出窗口
                d = s[left]
                left += 1

                # 更新窗口中的数据
                if d in need:
                    if window[d] == need[d]:
                        valid -= 1
                    window[d] -= 1

        return result

# 时间复杂度：O(n) - 遍历字符串 s 的时间复杂度，其中 n 是 s 的长度。
# 空间复杂度：O(m) - 哈希表存储字符串 p 中每个字符的个数，其中 m 是 p 的长度。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历字符串 s 的时间复杂度。
- **空间复杂度**：O(m)，哈希表存储字符串 p 中每个字符的个数，其中 m 是 p 的长度。

---

### 29. LeetCode 209: Minimum Size Subarray Sum（长度最小的子数组）

**题目描述**：
给定一个包含正整数的数组 `nums` 和一个正整数 `target`，找到一个长度最小的连续子数组，使得该子数组的元素之和大于等于 `target`，返回该子数组的长度。如果不存在这样的子数组，返回 `0`。

**解题思路**：
使用滑动窗口法。定义两个指针 `left` 和 `right` 分别指向窗口的左右边界，并记录当前窗口中所有元素的和。当窗口中元素的和大于等于 `target` 时，记录最小子数组长度，并移动左指针缩小窗口，

直到元素和小于 `target`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找长度最小的子数组的函数
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        # 初始化滑动窗口的左右边界指针
        left = 0
        right = 0
        # 记录当前窗口中所有元素的和和最小子数组长度
        current_sum = 0
        min_length = float("inf")

        # 右指针遍历整个数组
        while right < len(nums):
            # 更新当前窗口中所有元素的和
            current_sum += nums[right]
            right += 1

            # 当当前窗口中所有元素的和大于等于 target 时，尝试缩小窗口
            while current_sum >= target:
                min_length = min(min_length, right - left)
                current_sum -= nums[left]
                left += 1

        # 如果最小子数组长度仍然为初始值，说明不存在满足条件的子数组
        return 0 if min_length == float("inf") else min_length

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 30. LeetCode 1423: Maximum Points You Can Obtain from Cards（你可以获得的最大点数）

**题目描述**：
给定一个整数组 `cardPoints`，其中第 `i` 个元素表示从第 `i` 张卡片获得的点数。每次从卡片的开头或末尾抽取一张卡片，总共可以抽 `k` 张，返回可以获得的最大点数。

**解题思路**：
使用滑动窗口法。在整个 `cardPoints` 中，选择一个长度为 `n-k` 的子数组，使得其元素和最小。总和减去该子数组的和即为最大点数。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最大点数的函数
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        # 计算所有卡片的总和
        total_points = sum(cardPoints)
        n = len(cardPoints)
        # 计算初始窗口（n-k 个元素）的和
        current_sum = sum(cardPoints[:n - k])
        min_subarray_sum = current_sum

        # 滑动窗口从左向右移动
        for i in range(n - k, n):
            current_sum += cardPoints[i] - cardPoints[i - (n - k)]
            min_subarray_sum = min(min_subarray_sum, current_sum)

        # 最大点数 = 总和 - 最小子数组和
        return total_points - min_subarray_sum

# 时间复杂度：O(n) - 遍历整个数组的时间复杂度，其中 n 是数组的长度。
# 空间复杂度：O(1) - 只使用了常量级别的额外空间。
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历整个数组的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。
