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

### 10 道 LeetCode 滑动窗口题目及详细解释

---

#### 1. LeetCode 3: 无重复字符的最长子串 (Longest Substring Without Repeating Characters)

##### Problem Description  
给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。

##### 解法：滑动窗口  
使用滑动窗口记录当前窗口内的所有字符，当遇到重复字符时，收缩左指针，直到窗口内无重复字符为止。

##### Python 代码：

```python
def lengthOfLongestSubstring(s):
    char_set = set()  # 记录当前窗口内的字符
    left = 0  # 初始化左指针
    max_length = 0  # 初始化最大长度
    for right in range(len(s)):  # 右指针逐步遍历字符串
        while s[right] in char_set:  # 如果当前字符已经在窗口内
            char_set.remove(s[left])  # 移除左指针指向的字符
            left += 1  # 左指针右移
        char_set.add(s[right])  # 将当前字符加入窗口
        max_length = max(max_length, right - left + 1)  # 更新最大长度
    return max_length
```

##### 代码行解释：
```python
    char_set = set()  # 使用集合记录窗口内的字符，避免重复
    left = 0  # 初始化左指针
    max_length = 0  # 初始化最长子串的长度
    for right in range(len(s)):  # 遍历字符串，每次移动右指针
        while s[right] in char_set:  # 如果当前字符已经在集合中
            char_set.remove(s[left])  # 从集合中移除左指针指向的字符
            left += 1  # 左指针右移
        char_set.add(s[right])  # 将当前字符加入集合
        max_length = max(max_length, right - left + 1)  # 更新最长子串长度
```

##### 解释：
- 使用 `char_set` 集合记录窗口内的字符，确保窗口内无重复字符。
- 当遇到重复字符时，左指针右移，直到窗口内无重复字符。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(min(n, m))，其中 `m` 是字符集的大小。

---

#### 2. LeetCode 76: 最小覆盖子串 (Minimum Window Substring)

##### Problem Description  
给定一个字符串 `s` 和一个字符串 `t`，在 `s` 中找到最小的包含 `t` 中所有字符的子串。

##### 解法：滑动窗口 + 哈希表  
使用滑动窗口和两个哈希表，一个记录 `t` 中字符的频率，一个记录当前窗口内字符的频率。当窗口内的字符频率满足 `t` 时，尝试收缩窗口找到最小子串。

##### Python 代码：

```python
from collections import Counter

def minWindow(s, t):
    if not t or not s:
        return ""
    
    dict_t = Counter(t)  # 统计 t 中字符的频率
    required = len(dict_t)  # t 中不同字符的数量
    left, right = 0, 0  # 初始化窗口指针
    formed = 0  # 记录窗口内满足条件的字符数量
    window_counts = {}  # 记录窗口内字符的频率
    min_length = float("inf")  # 初始化最小长度
    min_left, min_right = 0, 0  # 初始化最小子串的左右边界

    while right < len(s):
        char = s[right]  # 获取右指针指向的字符
        window_counts[char] = window_counts.get(char, 0) + 1  # 更新窗口字符频率
        
        if char in dict_t and window_counts[char] == dict_t[char]:  # 如果当前字符满足 t 中的频率
            formed += 1  # 满足条件的字符数量加 1

        while left <= right and formed == required:  # 当所有字符都满足时，尝试收缩窗口
            if right - left + 1 < min_length:  # 更新最小子串长度
                min_length = right - left + 1
                min_left, min_right = left, right

            window_counts[s[left]] -= 1  # 移除左指针指向的字符
            if s[left] in dict_t and window_counts[s[left]] < dict_t[s[left]]:  # 如果移除后不再满足条件
                formed -= 1  # 满足条件的字符数量减 1
            left += 1  # 左指针右移

        right += 1  # 右指针右移

    return "" if min_length == float("inf") else s[min_left:min_right + 1]  # 返回最小子串
```

##### 代码行解释：
```python
    dict_t = Counter(t)  # 使用 Counter 统计 t 中字符的频率
    required = len(dict_t)  # 统计 t 中不同字符的数量
    left, right = 0, 0  # 初始化窗口的左右指针
    formed = 0  # 记录窗口内满足 t 中字符条件的数量
    window_counts = {}  # 记录当前窗口内字符的频率
    min_length = float("inf")  # 初始化最小子串的长度
    min_left, min_right = 0, 0  # 初始化最小子串的左右边界

    while right < len(s):  # 遍历 s 中的每个字符
        char = s[right]  # 获取当前字符
        window_counts[char] = window_counts.get(char, 0) + 1  # 更新当前窗口内字符的频率

        if char in dict_t and window_counts[char] == dict_t[char]:  # 如果当前字符满足 t 中的频率要求
            formed += 1  # 满足条件的字符数量加 1

        while left <= right and formed == required:  # 如果所有字符都满足条件
            if right - left + 1 < min_length:  # 更新最小子串的长度
                min_length = right - left + 1
                min_left, min_right = left, right

            window_counts[s[left]] -= 1  # 移除左指针

指向的字符
            if s[left] in dict_t and window_counts[s[left]] < dict_t[s[left]]:  # 如果移除后不再满足条件
                formed -= 1  # 满足条件的字符数量减 1
            left += 1  # 左指针右移

        right += 1  # 右指针右移

    return "" if min_length == float("inf") else s[min_left:min_right + 1]  # 返回最小子串
```

##### 解释：
- 使用两个哈希表记录 `t` 中字符频率和当前窗口内字符频率。
- 当窗口内所有字符频率都满足 `t` 时，尝试收缩窗口找到最小子串。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(n)

---

#### 3. LeetCode 438: 找到字符串中所有字母异位词 (Find All Anagrams in a String)

##### Problem Description  
给定一个字符串 `s` 和一个非空字符串 `p`，找到 `s` 中所有是 `p` 的字母异位词的子串，返回这些子串的起始索引。

##### 解法：滑动窗口 + 哈希表  
使用滑动窗口记录当前窗口内的字符频率，并与 `p` 中字符的频率进行比较。

##### Python 代码：

```python
from collections import Counter

def findAnagrams(s, p):
    result = []  # 存储结果
    p_count = Counter(p)  # 统计 p 中字符的频率
    s_count = Counter()  # 记录窗口内字符的频率

    left = 0  # 初始化左指针
    for right in range(len(s)):
        s_count[s[right]] += 1  # 更新右指针指向的字符频率

        if right >= len(p):  # 当窗口大小超过 p 的长度时
            if s_count[s[left]] == 1:  # 如果左指针指向的字符只出现一次，直接移除
                del s_count[s[left]]
            else:
                s_count[s[left]] -= 1  # 否则字符频率减 1
            left += 1  # 左指针右移

        if s_count == p_count:  # 如果窗口内字符频率与 p 中字符频率一致
            result.append(left)  # 记录当前左指针的位置

    return result
```

##### 代码行解释：
```python
    p_count = Counter(p)  # 使用 Counter 统计 p 中字符的频率
    s_count = Counter()  # 初始化窗口内字符频率的计数器
    left = 0  # 初始化左指针
    for right in range(len(s)):  # 遍历 s 中的每个字符
        s_count[s[right]] += 1  # 更新窗口内字符频率

        if right >= len(p):  # 如果当前窗口大小超过 p 的长度
            if s_count[s[left]] == 1:  # 如果左指针指向的字符只出现一次，直接删除
                del s_count[s[left]]
            else:
                s_count[s[left]] -= 1  # 否则字符频率减 1
            left += 1  # 左指针右移

        if s_count == p_count:  # 如果窗口内字符频率与 p 中字符频率一致
            result.append(left)  # 记录当前左指针的位置
```

##### 解释：
- 使用 `p_count` 和 `s_count` 分别记录 `p` 中字符频率和当前窗口内字符频率。
- 当窗口大小大于 `p` 时，移动左指针使窗口大小始终保持与 `p` 一致。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 4. LeetCode 567: 字符串的排列 (Permutation in String)

##### Problem Description  
给定两个字符串 `s1` 和 `s2`，判断 `s2` 中是否存在 `s1` 的排列。换句话说，判断 `s2` 中是否包含 `s1` 的某个排列的子串。

##### 解法：滑动窗口 + 哈希表  
使用滑动窗口记录当前窗口内的字符频率，并与 `s1` 中字符的频率进行比较。当窗口大小与 `s1` 一致且频率相同时，即找到排列。

##### Python 代码：

```python
from collections import Counter

def checkInclusion(s1, s2):
    s1_count = Counter(s1)  # 统计 s1 中字符的频率
    s2_count = Counter()  # 初始化窗口内字符的频率
    left = 0  # 初始化左指针

    for right in range(len(s2)):  # 遍历 s2 中的字符
        s2_count[s2[right]] += 1  # 更新右指针指向字符的频率

        # 如果当前窗口的大小超过 s1 的长度，移除左边的字符
        if right - left + 1 > len(s1):
            if s2_count[s2[left]] == 1:  # 如果左指针指向字符只出现一次，删除该字符
                del s2_count[s2[left]]
            else:  # 否则减少该字符的频率
                s2_count[s2[left]] -= 1
            left += 1  # 左指针右移

        # 如果当前窗口内的字符频率与 s1 的频率一致，则找到排列
        if s1_count == s2_count:
            return True

    return False
```

##### 代码行解释：
```python
    s1_count = Counter(s1)  # 使用 Counter 统计 s1 中字符的频率
    s2_count = Counter()  # 初始化窗口内字符频率的计数器
    left = 0  # 初始化左指针

    for right in range(len(s2)):  # 遍历 s2 中的每个字符
        s2_count[s2[right]] += 1  # 更新右指针指向的字符频率

        if right - left + 1 > len(s1):  # 如果当前窗口大小超过 s1 的长度
            if s2_count[s2[left]] == 1:  # 如果左指针指向字符只出现一次，直接删除
                del s2_count[s2[left]]
            else:
                s2_count[s2[left]] -= 1  # 否则字符频率减 1
            left += 1  # 左指针右移

        if s1_count == s2_count:  # 如果窗口内字符频率与 s1 中字符频率一致
            return True  # 返回 True，表示找到 s1 的排列

    return False  # 如果未找到，返回 False
```

##### 解释：
- 使用 `s1_count` 和 `s2_count` 分别记录 `s1` 中字符频率和当前窗口内字符频率。
- 当窗口大小大于 `s1` 时，移动左指针使窗口大小始终保持与 `s1` 一致。
- 当窗口内字符频率与 `s1` 中字符频率一致时，说明找到了 `s1` 的排列。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 5. LeetCode 643: 子数组最大平均数 I (Maximum Average Subarray I)

##### Problem Description  
给定一个整数数组 `nums` 和一个整数 `k`，找出 `nums` 中平均值最大的连续 `k` 个子数组，并输出该最大平均值。

##### 解法：滑动窗口  
使用固定大小的滑动窗口，维护当前 `k` 个元素的和。每次移动窗口时更新当前和，并计算平均值。

##### Python 代码：

```python
def findMaxAverage(nums, k):
    window_sum = sum(nums[:k])  # 初始化窗口的和，初始窗口为前 k 个元素
    max_sum = window_sum  # 初始化最大和
    for i in range(k, len(nums)):  # 遍历数组，从第 k 个元素开始
        window_sum += nums[i] - nums[i - k]  # 移动窗口时，更新窗口的和
        max_sum = max(max_sum, window_sum)  # 更新最大和
    return max_sum / k  # 返回最大平均值
```

##### 代码行解释：
```python
    window_sum = sum(nums[:k])  # 计算前 k 个元素的和，初始化窗口的和
    max_sum = window_sum  # 初始化最大和为当前窗口的和

    for i in range(k, len(nums)):  # 遍历数组，从第 k 个元素开始
        window_sum += nums[i] - nums[i - k]  # 移动窗口时，更新窗口的和：加上新元素，减去旧元素
        max_sum = max(max_sum, window_sum)  # 更新最大和

    return max_sum / k  # 返回最大平均值，最大和除以 k
```

##### 解释：
- 初始化 `window_sum` 为前 `k` 个元素的和。
- 每次移动窗口时，更新窗口的和：`window_sum += nums[i] - nums[i - k]`。
- 通过更新 `max_sum`，找到 `k` 个连续元素的最大和，再计算平均值。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 6. LeetCode 209: 长度最小的子数组 (Minimum Size Subarray Sum)

##### Problem Description  
给定一个含有 `n` 个正整数的数组和一个正整数 `target`，找出该数组中满足其和大于等于 `target` 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的子数组，返回 `0`。

##### 解法：滑动窗口  
使用滑动窗口维护一个当前和，当当前和大于等于 `target` 时，尝试收缩窗口以找到最小长度。

##### Python 代码：

```python
def minSubArrayLen(target, nums):
    left = 0  # 初始化左指针
    current_sum = 0  # 当前窗口内的和
    min_length = float('inf')  # 初始化最小长度为无穷大

    for right in range(len(nums)):  # 右指针遍历数组
        current_sum += nums[right]  # 更新当前窗口的和

        # 当当前和大于等于目标值时，收缩窗口
        while current_sum >= target:
            min_length = min(min_length, right - left + 1)  # 更新最小长度
            current_sum -= nums[left]  # 移除左指针指向的元素
            left += 1  # 左指针右移

    return min_length if min_length != float('inf') else 0  # 如果最小长度未更新，返回 0
```

##### 代码行解释：
```python
    left = 0  # 初始化左指针
    current_sum = 0  # 当前窗口内的和
    min_length = float('inf')  # 初始化最小长度为无穷大

    for right in range(len(nums)):  # 右指针遍历数组
        current_sum += nums[right]  # 更新当前窗口的和

        while current_sum >= target:  # 当当前和大于等于目标值时
            min_length = min(min_length, right - left + 1)  # 更新最小长度
            current_sum -= nums[left]  # 移除左指针指向的元素
            left += 1  # 左指针右移

    return min_length if min_length != float('inf') else 0  # 返回最小长度，如果未更新，返回 0
```

##### 解释：
- 通过右指针遍历数组，不断更新当前窗口的和。
- 当窗口内的和大于等于 `target` 时，移动左指针收缩窗口，直到窗口内的和小于 `target`。
- 更新 `min_length` 以记录最小的符合条件的子数组长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 7. LeetCode 424: 替换后的最长重复字符 (Longest Repeating Character Replacement)

##### Problem Description  
给定一个字符串 `s` 和一个整数 `k`，可以将 `s` 中最多 `k` 个字符替换为其他字符，求替换后的字符串中最长的连续重复字符的长度。

##### 解法：滑动窗口 + 哈希表  
使用滑动窗口和哈希表记录当前窗口内字符的频率。每次移动右指针扩展窗口，并在当前窗口满足替换条件时收缩左指针。

##### Python 代码：

```python
def characterReplacement(s, k):
    char_count = {}  # 记录当前窗口内字符的频率
    left = 

0  # 初始化左指针
    max_count = 0  # 当前窗口内最多字符的个数
    max_length = 0  # 初始化最长长度

    for right in range(len(s)):  # 右指针遍历字符串
        char_count[s[right]] = char_count.get(s[right], 0) + 1  # 更新当前字符的频率
        max_count = max(max_count, char_count[s[right]])  # 更新当前窗口内最多字符的个数

        # 如果窗口内非最多字符的数量大于 k，收缩窗口
        while (right - left + 1) - max_count > k:
            char_count[s[left]] -= 1  # 移除左指针指向的字符
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长长度

    return max_length
```

##### 代码行解释：
```python
    char_count = {}  # 初始化记录窗口内字符频率的字典
    left = 0  # 初始化左指针
    max_count = 0  # 当前窗口内出现最多字符的个数
    max_length = 0  # 初始化最长长度

    for right in range(len(s)):  # 右指针遍历字符串
        char_count[s[right]] = char_count.get(s[right], 0) + 1  # 更新当前字符的频率
        max_count = max(max_count, char_count[s[right]])  # 更新当前窗口内最多字符的个数

        while (right - left + 1) - max_count > k:  # 如果当前窗口内非最多字符的数量大于 k，收缩窗口
            char_count[s[left]] -= 1  # 移除左指针指向的字符
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长长度

    return max_length
```

##### 解释：
- 使用 `char_count` 记录当前窗口内每个字符的频率。
- 当窗口内非最多字符的数量大于 `k` 时，移动左指针收缩窗口。
- 更新 `max_length` 以记录替换后的最长连续重复字符的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 8. LeetCode 713: 乘积小于 K 的子数组 (Subarray Product Less Than K)

##### Problem Description  
给定一个正整数数组 `nums` 和一个正整数 `k`，请你找出该数组中乘积小于 `k` 的连续子数组的个数。

##### 解法：滑动窗口  
使用滑动窗口维护当前窗口内的乘积，当乘积大于或等于 `k` 时，移动左指针收缩窗口。每次移动右指针扩展窗口时，记录当前窗口内所有子数组的个数。

##### Python 代码：

```python
def numSubarrayProductLessThanK(nums, k):
    if k <= 1:  # 如果 k 小于等于 1，则不可能有乘积小于 k 的子数组
        return 0
    product = 1  # 初始化乘积为 1
    left = 0  # 初始化左指针
    count = 0  # 记录子数组的个数

    for right in range(len(nums)):  # 遍历数组
        product *= nums[right]  # 更新乘积
        while product >= k:  # 当乘积大于或等于 k 时，收缩窗口
            product /= nums[left]  # 移除左指针指向的元素
            left += 1  # 左指针右移
        count += right - left + 1  # 当前窗口内的所有子数组的个数为 (right - left + 1)
    return count
```

##### 代码行解释：
```python
    if k <= 1:  # 如果 k 小于等于 1，则返回 0，因为不可能有乘积小于 k 的子数组
        return 0
    product = 1  # 初始化乘积为 1
    left = 0  # 初始化左指针
    count = 0  # 初始化子数组个数为 0

    for right in range(len(nums)):  # 遍历数组中的每个元素
        product *= nums[right]  # 更新当前窗口内的乘积

        while product >= k:  # 如果当前乘积大于或等于 k，则移动左指针收缩窗口
            product /= nums[left]  # 移除左指针指向的元素，更新乘积
            left += 1  # 左指针右移

        count += right - left + 1  # 当前窗口内的所有子数组个数为 (right - left + 1)
    return count  # 返回所有子数组的个数
```

##### 解释：
- 通过右指针遍历数组，不断更新当前窗口的乘积。
- 当窗口内的乘积大于或等于 `k` 时，移动左指针收缩窗口，直到窗口内的乘积小于 `k`。
- 当前窗口内所有子数组的个数为 `right - left + 1`，将其累加到结果中。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 9. LeetCode 1004: 最大连续 1 的个数 III (Max Consecutive Ones III)

##### Problem Description  
给定一个二进制数组 `nums` 和一个整数 `k`，可以将数组中的最多 `k` 个 `0` 变为 `1`，求包含 `1` 的最长连续子数组的长度。

##### 解法：滑动窗口  
使用滑动窗口记录当前窗口内 `0` 的个数。当 `0` 的数量大于 `k` 时，移动左指针收缩窗口，直到 `0` 的数量小于等于 `k`。

##### Python 代码：

```python
def longestOnes(nums, k):
    left = 0  # 初始化左指针
    max_length = 0  # 记录最长连续 1 的个数
    zero_count = 0  # 当前窗口内 0 的数量

    for right in range(len(nums)):  # 遍历数组
        if nums[right] == 0:  # 如果当前元素为 0，更新 0 的数量
            zero_count += 1

        while zero_count > k:  # 如果窗口内 0 的数量大于 k，收缩窗口
            if nums[left] == 0:  # 如果左指针指向的元素为 0，更新 0 的数量
                zero_count -= 1
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长连续 1 的个数

    return max_length
```

##### 代码行解释：
```python
    left = 0  # 初始化左指针
    max_length = 0  # 初始化最长连续 1 的个数
    zero_count = 0  # 初始化当前窗口内 0 的数量

    for right in range(len(nums)):  # 遍历数组中的每个元素
        if nums[right] == 0:  # 如果当前元素为 0，则更新 0 的数量
            zero_count += 1

        while zero_count > k:  # 如果窗口内 0 的数量大于 k，收缩窗口
            if nums[left] == 0:  # 如果左指针指向的元素为 0，更新 0 的数量
                zero_count -= 1
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长连续 1 的个数
```

##### 解释：
- 当窗口内 `0` 的数量大于 `k` 时，移动左指针收缩窗口。
- 通过更新 `max_length` 来记录可以替换 `k` 个 `0` 的最长连续子数组的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 10. LeetCode 1208: 尽可能使字符串相等 (Get Equal Substrings Within Budget)

##### Problem Description  
给定两个长度相同的字符串 `s` 和 `t`，以及一个整数 `maxCost`。每次可以将 `s` 中的一个字符变为 `t` 中对应位置的字符，代价是两个字符的 ASCII 值差的绝对值。求能够在预算 `maxCost` 内的最长相等子字符串的长度。

##### 解法：滑动窗口  
使用滑动窗口维护当前窗口内的转换代价和。当代价和大于 `maxCost` 时，移动左指针收缩窗口，直到代价和小于等于 `maxCost`。

##### Python 代码：

```python
def equalSubstring(s, t, maxCost):
    left = 0  # 初始化左指针
    max_length = 0  # 记录最长相等子字符串的长度
    current_cost = 0  # 当前窗口内的转换代价和

    for right in range(len(s)):  # 遍历字符串
        current_cost += abs(ord(s[right]) - ord(t[right]))  # 更新当前窗口的转换代价

        # 当当前转换代价和大于预算时，收缩窗口
        while current_cost > maxCost:
            current_cost -= abs(ord(s[left]) - ord(t[left]))  # 移除左指针指向的字符代价
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长相等子字符串的长度

    return max_length
```

##### 代码行解释：
```python
    left = 0  # 初始化左指针
    max_length = 0  # 初始化最长相等子字符串的长度
    current_cost = 0  # 初始化当前窗口内的转换代价和

    for right in range(len(s)):  # 遍历字符串中的每个字符
        current_cost += abs(ord(s[right]) - ord(t[right]))  # 更新当前窗口的转换代价：两个字符的 ASCII 值差的绝对值

        while current_cost > maxCost:  # 如果当前转换代价和大于预算时
            current_cost -= abs(ord(s[left]) - ord(t[left]))  # 移除左指针指向的字符代价
            left += 1  # 左指针右移

        max_length = max(max_length, right - left + 1)  # 更新最长相等子字符串的长度
```

##### 解释：
- 当窗口内的转换代价和大于 `maxCost` 时，移动左指针收缩窗口，直到代价和小于等于 `maxCost`。
- 通过更新 `max_length` 来记录能够在预算内的最长相等子字符串的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

### Conclusion  
滑动窗口是一种高效的算法技巧，特别适合用于解决字符串和数组中子数组或子串的问题。通过维护一个动态窗口并调整窗口的边界，可以在一次遍历中快速找到符合条件的解，从而大大提高算法的效率。常见的滑动窗口问题包括最长子串、最

