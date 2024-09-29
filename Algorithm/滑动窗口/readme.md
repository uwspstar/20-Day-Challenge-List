# 滑动窗口
### 滑动窗口 (Sliding Window)

#### Definition  
滑动窗口是一种优化技术，通常用于处理连续子数组或子串的问题。通过移动窗口的左右边界，我们能够在线性时间内解决一些复杂度较高的问题，如寻找最长子串、满足条件的子数组等。滑动窗口可以动态调整窗口的大小，从而高效处理大规模数据。

#### Key Concepts  
1. **窗口左边界 (Left Boundary)**: 定义窗口的起始位置，当需要缩小窗口时，左边界向右移动。
2. **窗口右边界 (Right Boundary)**: 定义窗口的结束位置，右边界通常用于扩展窗口。
3. **条件判断 (Condition Check)**: 滑动窗口在扩展或收缩时会检查窗口内是否满足问题给定的条件。
4. **动态调整 (Dynamic Adjustment)**: 窗口的大小会根据不同情况进行动态调整，当满足条件时缩小窗口，不满足时扩大窗口。

#### 滑动窗口的步骤  
1. **定义左右边界**：使用两个指针，分别表示窗口的左右边界。
2. **扩展右边界**：移动右指针，增加窗口的大小，直到窗口满足某些条件。
3. **收缩左边界**：在满足条件的情况下，移动左指针，尝试缩小窗口，直到不再满足条件。
4. **记录结果**：每次窗口满足条件时，记录当前结果。

#### 滑动窗口的适用场景  
- 求最大或最小子数组
- 求满足条件的最短或最长子数组
- 查找满足条件的子串
- 统计字符频率、数值和

#### Python 滑动窗口模板

```python
def sliding_window(arr, target):
    left = 0  # 初始化窗口的左边界
    current_sum = 0  # 当前窗口内的和
    for right in range(len(arr)):  # 移动右边界
        current_sum += arr[right]  # 增加当前窗口内的和
        while current_sum >= target:  # 当窗口满足条件时
            # 执行需要的操作，比如记录结果
            current_sum -= arr[left]  # 缩小窗口
            left += 1  # 移动左边界
```

### 5 道 LeetCode 滑动窗口题目及详细解释

---

#### 1. LeetCode 3: 无重复字符的最长子串 (Longest Substring Without Repeating Characters)

##### Problem Description  
给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。

##### 解法：滑动窗口  
我们通过左右两个指针维护一个滑动窗口，记录当前窗口中的字符。每当发现重复字符时，缩小窗口，直到窗口内没有重复字符。

##### Python 代码：

```python
def lengthOfLongestSubstring(s):
    char_set = set()  # 记录窗口内的字符
    left = 0  # 初始化左边界
    max_len = 0  # 记录最长长度
    for right in range(len(s)):  # 移动右边界
        while s[right] in char_set:  # 如果出现重复字符，缩小窗口
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])  # 加入新字符
        max_len = max(max_len, right - left + 1)  # 更新最长长度
    return max_len
```

##### 解释：
- 通过使用集合 `char_set` 来记录窗口中的字符。
- 每次发现重复字符时，缩小窗口直到没有重复字符。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(min(n, m))，其中 n 是字符串的长度，m 是字符集的大小。

---

#### 2. LeetCode 209: 长度最小的子数组 (Minimum Size Subarray Sum)

##### Problem Description  
给定一个含有正整数的数组和一个正整数 `target`，找出该数组中满足其和大于等于 `target` 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。

##### 解法：滑动窗口  
我们通过滑动窗口计算子数组的和，找到和大于等于 `target` 的最小子数组长度。

##### Python 代码：

```python
def minSubArrayLen(target, nums):
    left = 0  # 初始化左边界
    current_sum = 0  # 当前窗口内的和
    min_len = float('inf')  # 初始化最小长度为无穷大
    for right in range(len(nums)):  # 移动右边界
        current_sum += nums[right]  # 增加当前窗口的和
        while current_sum >= target:  # 当窗口内的和大于等于 target
            min_len = min(min_len, right - left + 1)  # 更新最小长度
            current_sum -= nums[left]  # 缩小窗口
            left += 1
    return 0 if min_len == float('inf') else min_len
```

##### 解释：
- 使用滑动窗口动态调整窗口的大小，当窗口内的和大于等于 `target` 时，尽量缩小窗口。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 3. LeetCode 76: 最小覆盖子串 (Minimum Window Substring)

##### Problem Description  
给定两个字符串 `s` 和 `t`，找到 `s` 中最小的包含 `t` 中所有字符的子串。如果不存在这样的子串，返回空字符串。

##### 解法：滑动窗口  
我们通过滑动窗口检查是否包含 `t` 中所有字符，并在找到满足条件时尽量缩小窗口。

##### Python 代码：

```python
from collections import Counter

def minWindow(s, t):
    if not s or not t:
        return ""

    t_count = Counter(t)  # 统计 t 中每个字符的出现次数
    window_count = {}  # 记录窗口中的字符
    left = 0  # 初始化左边界
    min_len = float('inf')  # 最小子串长度
    result = ""  # 最终结果
    formed = 0  # 满足条件的字符个数

    for right in range(len(s)):  # 移动右边界
        char = s[right]
        window_count[char] = window_count.get(char, 0) + 1

        if char in t_count and window_count[char] == t_count[char]:
            formed += 1

        while left <= right and formed == len(t_count):
            char = s[left]
            if right - left + 1 < min_len:
                min_len = right - left + 1
                result = s[left:right + 1]
            window_count[char] -= 1
            if char in t_count and window_count[char] < t_count[char]:
                formed -= 1
            left += 1

    return result if min_len != float('inf') else ""
```

##### 解释：
- 使用 `Counter` 统计目标字符串 `t` 中字符的频率，并用滑动窗口动态匹配。
- 当窗口中包含所有 `t` 的字符时，尽量缩小窗口。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(t + s)，其中 t 和 s 分别为两个字符串的长度。

---

#### 4. LeetCode 567: 字符串的排列 (Permutation in String)

##### Problem Description  
给定两个字符串 `s1` 和 `s2`，写一个函数来判断 `s2` 是否包含 `s1` 的排列。换句话说，第一个字符串的排列之一是第二个字符串的子串。

##### 解法：滑动窗口 + 字符计数  
通过滑动窗口比较当前窗口内的字符频率是否与目标字符串 `s1` 的字符频率相同。

##### Python 代码：

```python
from collections import Counter

def checkInclusion(s1, s2):
    s1_count = Counter(s1)  # 统计 s1 中字符的频率
    window_count = Counter()  # 滑动窗口中字符的频率
    left = 0

    for right in range(len(s2)):  # 移动右边界
        window_count[s2[right]] += 1
        if right - left + 1 > len(s1):  # 窗口大小超出 s1 长度时，缩小窗口
            if window_count[s2[left]] == 1:
                del window_count[s2[left]]
            else:
                window_count[s2[left]] -= 1
            left += 1

        if window_count == s1_count:  # 如果窗口内的字符频率与 s1 的一致
            return True

    return False
```

##### 解释：
- 通过滑动窗口动态调整当前窗口内的字符频率，检查是否与 `s1` 的字符频率一致。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 5. LeetCode 438:

 找到字符串中所有字母异位词 (Find All Anagrams in a String)

##### Problem Description  
给定两个字符串 `s` 和 `p`，找到 `s` 中所有是 `p` 异位词的子串，返回这些子串的起始索引。

##### 解法：滑动窗口 + 字符计数  
我们通过滑动窗口动态调整窗口内字符的频率，找到所有异位词。

##### Python 代码：

```python
from collections import Counter

def findAnagrams(s, p):
    p_count = Counter(p)  # 统计 p 中字符的频率
    window_count = Counter()  # 窗口内的字符频率
    result = []  # 存储结果
    left = 0

    for right in range(len(s)):  # 移动右边界
        window_count[s[right]] += 1

        if right - left + 1 > len(p):  # 窗口大小超出 p 长度时，缩小窗口
            if window_count[s[left]] == 1:
                del window_count[s[left]]
            else:
                window_count[s[left]] -= 1
            left += 1

        if window_count == p_count:  # 如果窗口内字符频率与 p 一致
            result.append(left)

    return result
```

##### 解释：
- 通过滑动窗口检查每个子串是否是 `p` 的异位词，并返回所有起始索引。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(p + s)

---

### Conclusion  
滑动窗口是一种非常有效的技术，特别适合处理子数组和子串的问题。通过调整窗口的大小，可以在不增加复杂度的情况下，找到符合条件的结果。掌握滑动窗口可以显著提高算法效率，尤其是涉及到字符串匹配、子数组求和等问题时。

---


[![滑动窗口技巧与相关题目](https://img.youtube.com/vi/Rk1mEiEuNqs/0.jpg)](https://www.youtube.com/watch?v=Rk1mEiEuNqs)
