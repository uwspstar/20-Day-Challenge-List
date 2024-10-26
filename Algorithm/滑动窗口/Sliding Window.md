# 灵活滑动窗口 (Flexible Sliding Window)

## Definition
灵活滑动窗口是一种处理动态变化的窗口大小的技术，通过在数组或序列中维护一个有效的窗口，以实现特定条件的搜索或计算。该技术能够处理最长或最短子数组等问题，通常用于字符串、数组等数据结构。

## Key Concepts
- **动态窗口 (Dynamic Window)**: 窗口的大小和位置会根据条件的变化而变化。
- **条件验证 (Condition Validation)**: 通过检查当前窗口的有效性，决定是否需要移动窗口的边界。

## 灵活滑动窗口的步骤
1. 初始化窗口和结果变量。
2. 通过扩展右边界，逐步将新元素加入窗口。
3. 根据条件的有效性，动态调整左边界，确保窗口有效。
4. 更新结果变量，记录当前窗口满足条件时的最长或最短长度。

## 适用场景
- 查找满足特定条件的最长或最短子数组。
- 处理不固定大小的滑动窗口问题，如查找子字符串、子数组等。

## Python 灵活滑动窗口模板 - 最长子数组
```python
def sliding_window_flexible_longest(input):
    window = []  # 初始化窗口
    ans = 0
    left = 0
    
    for right in range(len(input)):
        window.append(input[right])  # 扩展右边界
        while invalid(window):  # 确保窗口有效
            window.remove(input[left])  # 移除左侧元素
            left += 1
        ans = max(ans, len(window))  # 更新最长子数组长度
    
    return ans  # 返回满足条件的最长子数组长度
```

## Python 灵活滑动窗口模板 - 最短子数组
```python
def sliding_window_flexible_shortest(input):
    window = []  # 初始化窗口
    ans = float("inf")  # 初始化为正无穷
    left = 0
    
    for right in range(len(input)):
        window.append(input[right])  # 扩展右边界
        while valid(window):  # 确保窗口有效
            ans = min(ans, len(window))  # 更新最短子数组长度
            window.remove(input[left])  # 移除左侧元素
            left += 1
    
    return ans if ans != float("inf") else 0  # 返回满足条件的最短子数组长度
```

## Python 固定大小滑动窗口模板
```python
def sliding_window_fixed(input, window_size):
    ans = input[0:window_size]  # 初始化窗口
    for right in range(window_size, len(input)):
        left = right - window_size  # 计算左边界
        window = input[left:right + 1]  # 更新窗口
        ans = optimal(ans, window)  # 更新最优解
    return ans  # 返回最优解
```

## Tips
- 确保在每次窗口更新时，及时检查窗口的有效性。
- 根据具体问题定义 `valid` 和 `invalid` 函数，以确保窗口符合条件。

## Warning
- 当处理大型数据时，使用 `list.remove()` 可能会导致性能问题，考虑使用 `collections.deque` 进行优化。

## Complexity Analysis
- **时间复杂度**: O(n)，每个元素最多被处理两次。
- **空间复杂度**: O(n)，存储窗口内容所需的空间。

---

That's a comprehensive list of sliding window problems! I’ll provide detailed solutions with inline comments in Chinese, starting with the first few problems.

### LeetCode 3: Longest Substring Without Repeating Characters（无重复字符的最长子串）
[LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_map = {}  # 用于存储字符最后出现的索引
        l = 0  # 左指针
        max_len = 0  # 最大长度

        for r in range(len(s)):  # 右指针遍历字符串
            if s[r] in char_map and char_map[s[r]] >= l:
                # 如果字符重复且索引在左指针右侧或等于左指针
                l = char_map[s[r]] + 1  # 移动左指针到重复字符的下一位置
            
            char_map[s[r]] = r  # 更新字符的最新索引
            max_len = max(max_len, r - l + 1)  # 计算最长子串长度
        
        return max_len
```

### LeetCode 76: Minimum Window Substring（最小覆盖子串）
[LeetCode 76](https://leetcode.com/problems/minimum-window-substring/)
```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        l = 0  # 左指针
        t_map, window = {}, {}  # 目标字符频率表和窗口字符频率表

        # 统计目标字符串 t 中字符的频率
        for c in t:
            t_map[c] = t_map.get(c, 0) + 1
        
        have, need = 0, len(t_map)  # 已满足条件的字符数和需要满足的字符种类数
        res, res_len = [-1, -1], float("inf")  # 最小窗口的起止索引和长度

        # 右指针遍历字符串 s
        for r in range(len(s)):
            c = s[r]
            window[c] = window.get(c, 0) + 1  # 增加当前字符的频率

            if c in t_map and window[c] == t_map[c]:
                have += 1  # 如果字符数量符合目标，增加已满足的条件数

            # 当已满足的字符数等于需要的字符种类数时，尝试收缩窗口
            while have == need:
                # 更新最小窗口
                if (r - l + 1) < res_len:
                    res = [l, r]
                    res_len = (r - l + 1)

                # 收缩窗口
                window[s[l]] -= 1
                if s[l] in t_map and window[s[l]] < t_map[s[l]]:
                    have -= 1  # 如果字符数量不再满足目标，减少已满足的条件数
                
                l += 1  # 移动左指针
        
        l, r = res
        return s[l: r+1] if res_len != float("inf") else ""
```

### LeetCode 567: Permutation in String（字符串的排列）
[LeetCode 567](https://leetcode.com/problems/permutation-in-string/)
```python
from collections import Counter

class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        n1, n2 = len(s1), len(s2)
        
        # 如果 s1 比 s2 长，不可能存在排列
        if n1 > n2:
            return False
        
        count_s1 = Counter(s1)  # s1 中字符的频率计数器
        window = Counter(s2[:n1])  # s2 初始窗口的频率计数器
        
        # 检查初始窗口是否与 s1 相同
        if count_s1 == window:
            return True
        
        # 滑动窗口遍历 s2
        for i in range(n1, n2):
            window[s2[i]] += 1  # 添加新字符
            window[s2[i - n1]] -= 1  # 移除旧字符
            
            # 如果字符计数为 0，从窗口中删除
            if window[s2[i - n1]] == 0:
                del window[s2[i - n1]]
            
            # 检查当前窗口是否匹配
            if count_s1 == window:
                return True
        
        return False
```

### LeetCode 438: Find All Anagrams in a String（找到字符串中所有字母异位词）
[LeetCode 438](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
```python
from collections import Counter

class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        n1, n2 = len(p), len(s)
        if n1 > n2:
            return []
        
        p_count = Counter(p)  # 目标字符串 p 的字符计数器
        window = Counter(s[:n1])  # 初始窗口的字符计数器
        res = []  # 存储结果

        # 检查初始窗口是否是异位词
        if p_count == window:
            res.append(0)

        # 滑动窗口遍历 s
        for i in range(n1, n2):
            window[s[i]] += 1  # 添加新字符
            window[s[i - n1]] -= 1  # 移除旧字符
            
            # 如果字符计数为 0，从窗口中删除
            if window[s[i - n1]] == 0:
                del window[s[i - n1]]
            
            # 检查当前窗口是否是异位词
            if p_count == window:
                res.append(i - n1 + 1)

        return res
```

### LeetCode 159: Longest Substring with At Most Two Distinct Characters（至多两个不同字符的最长子串）
[LeetCode 159](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
```python
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        l = 0  # 左指针
        char_map = {}  # 字符频率表
        max_len = 0  # 最长长度

        # 右指针遍历字符串 s
        for r in range(len(s)):
            char_map[s[r]] = char_map.get(s[r], 0) + 1  # 添加当前字符

            # 如果字符种类数超过 2，移动左指针
            while len(char_map) > 2:
                char_map[s[l]] -= 1  # 移除左指针字符
                if char_map[s[l]] == 0:
                    del char_map[s[l]]  # 如果频率为 0，删除字符
                l += 1  # 左指针右移
            
            max_len = max(max_len, r - l + 1)  # 更新最长长度
        
        return max_len
```

### LeetCode 992: Subarrays with K Different Integers（具有 K 个不同整数的子数组）
[LeetCode 992](https://leetcode.com/problems/subarrays-with-k-different-integers/)
```python
from collections import defaultdict

class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        # 计算最多包含 k 个不同整数的子数组数量
        def atMostK(nums, k):
            l = 0  # 左指针
            count = defaultdict(int)  # 频率表
            res = 0  # 结果计数
            
            # 右指针遍历 nums
            for r in range(len(nums)):
                if count[nums[r]] == 0:
                    k -= 1  # 如果是新整数，减少 k
                
                count[nums[r]] += 1  # 增加当前整数的频率

                # 当不同整数的数量超过 k 时，移动左指针
                while k < 0:
                    count[nums[l]] -= 1
                    if count[nums[l]] == 0:
                        k += 1  # 如果整数频率为 0，增加 k
                    l += 1
                
                res += r - l + 1  # 计算当前子数组数量
            
            return res
        
        # 使用最多包含 k 个不同整数的子数组数量减去最多包含 (k-1) 个的数量
        return atMostK(nums, k) - atMostK(nums, k - 1)
```

### LeetCode 424: Longest Repeating Character Replacement（替换后的最长重复字符）
[LeetCode 424](https://leetcode.com/problems/longest-repeating-character-replacement/)
```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        l = 0  # 左指针
        count = defaultdict(int)  # 频率表
        max_count = 0  # 当前窗口中出现最多次的字符频率
        res = 0  # 结果

        # 右指针遍历字符串 s
        for r in range(len(s)):
            count[s[r]] += 1  # 增加当前字符的频率
            max_count = max(max_count, count[s[r]])  # 更新最大字符频率

            # 如果需要替换的字符数量超过 k，则移动左指针
            while (r - l + 1) - max_count > k:
                count[s[l]] -= 1  # 减少左指针字符的频率
                l += 1  # 左指针右移
            
            res = max(res, r - l + 1)  # 更新最长子串长度
        
        return res
```

### LeetCode 340: Longest Substring with At Most K Distinct Characters（至多 K 个不同字符的最长子串）
[LeetCode 340](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
```python
from collections import defaultdict

class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        l = 0  # 左指针
        count = defaultdict(int)  # 字符频率表
        max_len = 0  # 最长长度

        # 右指针遍历字符串 s
        for r in range(len(s)):
            count[s[r]] += 1  # 增加当前字符的频率

            # 如果字符种类超过 k，移动左指针
            while len(count) > k:
                count[s[l]] -= 1  # 减少左指针字符的频率
                if count[s[l]] == 0:
                    del count[s[l]]  # 如果频率为 0，删除字符
                l += 1  # 左指针右移
            
            max_len = max(max_len, r - l + 1)  # 更新最长长度
        
        return max_len
```

### LeetCode 1004: Max Consecutive Ones III（最大连续 1 的个数 III）
[LeetCode 1004](https://leetcode.com/problems/max-consecutive-ones-iii/)
```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        l = 0  # 左指针
        max_len = 0  # 最长长度
        zero_count = 0  # 当前窗口中的 0 的个数

        # 右指针遍历 nums
        for r in range(len(nums)):
            if nums[r] == 0:
                zero_count += 1  # 增加 0 的个数

            # 如果 0 的个数超过 k，移动左指针
            while zero_count > k:
                if nums[l] == 0:
                    zero_count -= 1  # 减少 0 的个数
                l += 1  # 左指针右移
            
            max_len = max(max_len, r - l + 1)  # 更新最长长度
        
        return max_len
```

### LeetCode 1052: Grumpy Bookstore Owner（书店老板的情绪管理）
[LeetCode 1052](https://leetcode.com/problems/grumpy-bookstore-owner/)
```python
class Solution:
    def maxSatisfied(self, customers: List[int], grumpy: List[int], minutes: int) -> int:
        satisfied = 0  # 客户满意度计数

        # 计算不使用技巧时的满意顾客数量
        for i in range(len(customers)):
            if grumpy[i] == 0:
                satisfied += customers[i]

        # 滑动窗口计算技巧期间额外增加的满意顾客数量
        extra = 0  # 当前窗口的额外满意度
        max_extra = 0  # 最大额外满意度

        # 初始化窗口
        for i in range(minutes):
            if grumpy[i] == 1:
                extra += customers[i]
        max_extra = extra

        # 滑动窗口遍历剩余部分
        for i in range(minutes, len(customers)):
            if grumpy[i] == 1:
                extra += customers[i]
            if grumpy[i - minutes] == 1:
                extra -= customers[i - minutes]
            
            max_extra = max(max_extra, extra)  # 更新最大额外满意度
        
        return satisfied + max_extra
```

### LeetCode 239: Sliding Window Maximum（滑动窗口最大值）
[LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/)
```python
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res = []  # 结果列表
        q = deque()  # 存储窗口中可能成为最大值的索引

        for i in range(len(nums)):
            # 如果队列最左侧元素不在窗口内，移除它
            if q and q[0] < i - k + 1:
                q.popleft()

            # 如果当前元素大于队列中的元素，移除这些元素
            while q and nums[q[-1]] < nums[i]:
                q.pop()
            
            q.append(i)  # 将当前索引加入队列

            # 当窗口大小达到 k 时，将最大值加入结果
            if i >= k - 1:
                res.append(nums[q[0]])

        return res
```

### LeetCode 643: Maximum Average Subarray I（子数组最大平均数 I）
[LeetCode 643](https://leetcode.com/problems/maximum-average-subarray-i/)
```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        # 计算初始窗口的和
        current_sum = sum(nums[:k])
        max_sum = current_sum  # 最大和初始化为初始窗口和

        # 滑动窗口遍历剩余数组
        for i in range(k, len(nums)):
            # 移动窗口：加上新元素，减去离开的元素
            current_sum += nums[i] - nums[i - k]
            max_sum = max(max_sum, current_sum)  # 更新最大和
        
        # 返回最大平均数
        return max_sum / k
```

### LeetCode 1209: Remove All Adjacent Duplicates in String II（移除字符串中所有相邻重复项 II）
[LeetCode 1209](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)
```python
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        stack = []  # 用于存储字符和其计数

        # 遍历字符串 s
        for char in s:
            if stack and stack[-1][0] == char:
                stack[-1][1] += 1  # 如果当前字符与栈顶相同，增加计数
                if stack[-1][1] == k:
                    stack.pop()  # 如果计数等于 k，移除该字符
            else:
                stack.append([char, 1])  # 否则，将字符和计数 1 加入栈

        # 重构字符串
        return ''.join(char * count for char, count in stack)
```

### LeetCode 713: Subarray Product Less Than K（乘积小于 K 的子数组）
[LeetCode 713](https://leetcode.com/problems/subarray-product-less-than-k/)
```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1:
            return 0  # 如果 k <= 1，不可能有乘积小于 k 的子数组

        product = 1  # 当前窗口的乘积
        l = 0  # 左指针
        res = 0  # 结果计数

        # 右指针遍历 nums
        for r in range(len(nums)):
            product *= nums[r]  # 增加当前元素到乘积

            # 如果乘积不小于 k，移动左指针
            while product >= k:
                product //= nums[l]  # 除去左指针元素
                l += 1
            
            res += r - l + 1  # 计算当前窗口的子数组数量
        
        return res
```

### LeetCode 209: Minimum Size Subarray Sum（最小长度子数组和）
[LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/)
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = 0  # 左指针
        current_sum = 0  # 当前窗口的和
        min_len = float('inf')  # 最小长度

        # 右指针遍历 nums
        for r in range(len(nums)):
            current_sum += nums[r]  # 增加当前元素到和

            # 当和大于等于目标值时，尝试收缩窗口
            while current_sum >= target:
                min_len = min(min_len, r - l + 1)  # 更新最小长度
                current_sum -= nums[l]  # 减少左指针元素
                l += 1  # 移动左指针
        
        # 如果找不到满足条件的子数组，返回 0；否则返回最小长度
        return min_len if min_len != float('inf') else 0
```

### LeetCode 30: Substring with Concatenation of All Words（串联所有单词的子串）
[LeetCode 30](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)
```python
from collections import Counter

class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        if not s or not words:
            return []

        word_len = len(words[0])  # 单个单词的长度
        num_words = len(words)  # 单词的个数
        total_len = word_len * num_words  # 所有单词串联后的长度
        word_count = Counter(words)  # 统计目标单词频率
        res = []  # 存储结果的索引列表

        # 遍历字符串 s，每次移动一个单词长度
        for i in range(word_len):
            l = i  # 左指针
            current_count = Counter()  # 当前窗口的单词计数
            count = 0  # 当前窗口中匹配的单词数量

            # 右指针遍历字符串
            for r in range(i, len(s) - word_len + 1, word_len):
                word = s[r:r + word_len]  # 当前单词

                if word in word_count:
                    current_count[word] += 1
                    count += 1

                    # 如果当前单词频率超过目标频率，移动左指针
                    while current_count[word] > word_count[word]:
                        left_word = s[l:l + word_len]
                        current_count[left_word] -= 1
                        count -= 1
                        l += word_len

                    # 如果匹配的单词数量等于目标单词数量，记录结果
                    if count == num_words:
                        res.append(l)
                else:
                    current_count.clear()  # 如果不是目标单词，清空计数器
                    count = 0
                    l = r + word_len
        
        return res
```

### LeetCode 904: Fruit Into Baskets（水果成篮）
[LeetCode 904](https://leetcode.com/problems/fruit-into-baskets/)
```python
from collections import defaultdict

class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        l = 0  # 左指针
        fruit_count = defaultdict(int)  # 统计水果种类和数量
        max_fruits = 0  # 最大水果数量

        # 右指针遍历 fruits
        for r in range(len(fruits)):
            fruit_count[fruits[r]] += 1  # 增加当前水果数量

            # 如果水果种类超过 2，移动左指针
            while len(fruit_count) > 2:
                fruit_count[fruits[l]] -= 1
                if fruit_count[fruits[l]] == 0:
                    del fruit_count[fruits[l]]  # 如果数量为 0，移除该水果
                l += 1  # 左指针右移
            
            max_fruits = max(max_fruits, r - l + 1)  # 更新最大水果数量
        
        return max_fruits
```

### LeetCode 930: Binary Subarrays With Sum（和为 S 的二进制子数组）
[LeetCode 930](https://leetcode.com/problems/binary-subarrays-with-sum/)
```python
from collections import defaultdict

class Solution:
    def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:
        prefix_sum = 0  # 前缀和
        count = defaultdict(int)  # 前缀和计数器
        count[0] = 1  # 初始化前缀和为 0 的次数
        res = 0  # 结果计数

        # 遍历 nums 计算前缀和
        for num in nums:
            prefix_sum += num  # 更新前缀和

            # 如果存在 (prefix_sum - goal)，则找到一个符合的子数组
            res += count[prefix_sum - goal]

            # 更新前缀和计数器
            count[prefix_sum] += 1
        
        return res
```
### LeetCode 1423: Maximum Points You Can Obtain from Cards（从卡牌中获得的最大点数）
[LeetCode 1423](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)
```python
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        total = sum(cardPoints)  # 卡牌总和
        window_sum = sum(cardPoints[:n - k])  # 初始化窗口为前 n-k 个元素的和
        min_window_sum = window_sum  # 最小窗口和

        # 滑动窗口遍历剩余部分
        for i in range(n - k, n):
            window_sum += cardPoints[i] - cardPoints[i - (n - k)]  # 移动窗口
            min_window_sum = min(min_window_sum, window_sum)  # 更新最小窗口和
        
        # 最大得分等于总和减去最小窗口和
        return total - min_window_sum
```

### LeetCode 485: Max Consecutive Ones（最大连续 1 的个数）
[LeetCode 485](https://leetcode.com/problems/max-consecutive-ones/)
```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        max_count = 0  # 最大连续 1 的计数
        current_count = 0  # 当前连续 1 的计数

        # 遍历数组 nums
        for num in nums:
            if num == 1:
                current_count += 1  # 增加连续 1 的计数
                max_count = max(max_count, current_count)  # 更新最大计数
            else:
                current_count = 0  # 重置当前计数
        
        return max_count
```

### LeetCode 340: Longest Substring with K Distinct Characters（至多 K 个不同字符的最长子串）
[LeetCode 340](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
```python
from collections import defaultdict

class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        l = 0  # 左指针
        count = defaultdict(int)  # 字符频率表
        max_len = 0  # 最长长度

        # 右指针遍历字符串 s
        for r in range(len(s)):
            count[s[r]] += 1  # 增加当前字符的频率

            # 如果字符种类超过 k，移动左指针
            while len(count) > k:
                count[s[l]] -= 1  # 减少左指针字符的频率
                if count[s[l]] == 0:
                    del count[s[l]]  # 如果频率为 0，删除字符
                l += 1  # 左指针右移
            
            max_len = max(max_len, r - l + 1)  # 更新最长长度
        
        return max_len
```

### LeetCode 1208: Get Equal Substrings Within Budget（在预算内的等价子字符串）
[LeetCode 1208](https://leetcode.com/problems/get-equal-substrings-within-budget/)
```python
class Solution:
    def equalSubstring(self, s: str, t: str, maxCost: int) -> int:
        l = 0  # 左指针
        current_cost = 0  # 当前转换成本
        max_len = 0  # 最长子串长度

        # 右指针遍历字符串 s 和 t
        for r in range(len(s)):
            current_cost += abs(ord(s[r]) - ord(t[r]))  # 计算转换成本

            # 如果当前成本超过 maxCost，移动左指针
            while current_cost > maxCost:
                current_cost -= abs(ord(s[l]) - ord(t[l]))  # 减少左指针的成本
                l += 1  # 左指针右移
            
            max_len = max(max_len, r - l + 1)  # 更新最长子串长度
        
        return max_len
```

### LeetCode 713: Subarray Product Less Than K（乘积小于 K 的子数组）
[LeetCode 713](https://leetcode.com/problems/subarray-product-less-than-k/)
```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if k <= 1:
            return 0  # 如果 k <= 1，不可能有乘积小于 k 的子数组

        product = 1  # 当前窗口的乘积
        l = 0  # 左指针
        res = 0  # 结果计数

        # 右指针遍历 nums
        for r in range(len(nums)):
            product *= nums[r]  # 增加当前元素到乘积

            # 如果乘积不小于 k，移动左指针
            while product >= k:
                product //= nums[l]  # 除去左指针元素
                l += 1
            
            res += r - l + 1  # 计算当前窗口的子数组数量
        
        return res
```

### LeetCode 424: Longest Repeating Character Replacement（替换后的最长重复字符）
[LeetCode 424](https://leetcode.com/problems/longest-repeating-character-replacement/)
```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        l = 0  # 左指针
        count = defaultdict(int)  # 频率表
        max_count = 0  # 当前窗口中出现最多次的字符频率
        res = 0  # 结果

        # 右指针遍历字符串 s
        for r in range(len(s)):
            count[s[r]] += 1  # 增加当前字符的频率
            max_count = max(max_count, count[s[r]])  # 更新最大字符频率

            # 如果需要替换的字符数量超过 k，则移动左指针
            while (r - l + 1) - max_count > k:
                count[s[l]] -= 1  # 减少左指针字符的频率
                l += 1  # 左指针右移
            
            res = max(res, r - l + 1)  # 更新最长子串长度
        
        return res
```

### LeetCode 209: Minimum Size Subarray Sum（最小长度子数组和）
[LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/)
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l = 0  # 左指针
        current_sum = 0  # 当前窗口的和
        min_len = float('inf')  # 最小长度

        # 右指针遍历 nums
        for r in range(len(nums)):
            current_sum += nums[r]  # 增加当前元素到和

            # 当和大于等于目标值时，尝试收缩窗口
            while current_sum >= target:
                min_len = min(min_len, r - l + 1)  # 更新最小长度
                current_sum -= nums[l]  # 减少左指针元素
                l += 1  # 移动左指针
        
        return min_len if min_len != float('inf') else 0
```

### LeetCode 1423: Maximum Points You Can Obtain from Cards（从卡牌中获得的最大点数）
[LeetCode 1423](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)
```python
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        total = sum(cardPoints)  # 卡牌总和
        window_sum = sum(cardPoints[:n - k])  # 初始化窗口为前 n-k 个元素的和
        min_window_sum = window_sum  # 最小窗口和

        # 滑动窗口遍历剩余部分
        for i in range(n - k, n):
            window_sum += cardPoints[i] - cardPoints[i - (n - k)]  # 移动窗口
            min_window_sum = min(min_window_sum, window_sum)  # 更新最小窗口和
        
        return total - min_window_sum
```
