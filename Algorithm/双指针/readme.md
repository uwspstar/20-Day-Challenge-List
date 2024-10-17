# 双指针

### 双指针 (Two Pointers)

#### Definition  
双指针是一种非常常用的算法技巧，通常用于遍历数组、字符串或链表。通过两个指针分别从数组的不同位置开始，逐步向中间或某个方向移动，双指针可以高效地解决一些涉及到子数组、子串或特定条件的问题。

#### Key Concepts  
1. **左指针与右指针 (Left and Right Pointers)**: 双指针可以一头一尾分别从数组的左边界和右边界开始，逐步收缩或扩展。
2. **快慢指针 (Fast and Slow Pointers)**: 通过一个指针移动快，一个指针移动慢来解决问题，通常用于检测链表中的环。
3. **条件判断 (Condition Check)**: 双指针的操作通常会基于某些条件，例如值的大小、重复元素等来调整指针的移动方向。

#### 双指针的步骤  
1. **初始化指针**：设置两个指针分别指向数组、字符串或链表的不同位置，通常是头尾或开始位置。
2. **移动指针**：根据条件，调整其中一个或两个指针的移动方向，直到满足条件。
3. **结束判断**：在特定条件下结束循环，比如指针相遇或者遍历结束。

#### 双指针的适用场景  
- 数组中查找和为某个值的两数
- 链表中查找环
- 反转数组或字符串
- 有序数组去重

#### Python 双指针模板

```python
def two_pointer_algorithm(arr):
    left, right = 0, len(arr) - 1  # 初始化两个指针
    while left < right:  # 当左指针小于右指针时继续
        # 执行一些操作，例如求和、查找、比较等
        if 满足条件:
            return result
        left += 1  # 或者移动右指针
        right -= 1
```

好的，我们从 LeetCode 双指针题目开始详细讲解，包括逐行中文注释代码及时间和空间复杂度分析。以下是前五道题目的详细解释。

---

### [1. LeetCode 167: Two Sum II - Input Array Is Sorted（两数之和 II - 输入有序数组）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E5%8F%8C%E6%8C%87%E9%92%88/LeetCode%20167%3A%20%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C%20II%20-%20%E8%BE%93%E5%85%A5%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84.md)


**题目描述**：
给定一个升序排列的整数数组 `numbers` 和一个目标值 `target`，找到两个数，使它们的和等于目标值 `target`。返回这两个数的下标（从 1 开始计数）。

**题目分析**：
可以使用双指针法来解决该问题。由于数组是有序的，因此可以将指针分别放置在数组的起点和终点，计算它们对应的数之和。如果和等于目标值，则返回结果；如果和小于目标值，则移动左指针以增大和；如果和大于目标值，则移动右指针以减小和。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找两数之和的函数
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # 初始化左右指针
        left, right = 0, len(numbers) - 1

        # 使用双指针法查找目标值
        while left < right:
            # 计算当前左右指针对应的和
            current_sum = numbers[left] + numbers[right]
            if current_sum == target:
                # 如果和等于目标值，返回下标（从 1 开始计数）
                return [left + 1, right + 1]
            elif current_sum < target:
                # 如果和小于目标值，移动左指针
                left += 1
            else:
                # 如果和大于目标值，移动右指针
                right -= 1

        return []  # 返回空列表，表示没有找到结果

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次即可找到目标值。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### [2. LeetCode 344: Reverse String（反转字符串）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E5%8F%8C%E6%8C%87%E9%92%88/LeetCode%20344%3A%20%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%20(Reverse%20String).md)

**题目描述**：
编写一个函数，其作用是将输入的字符串数组 `s` 原地反转，不能使用额外的空间，必须使用 O(1) 的额外空间复杂度。

**题目分析**：
可以使用双指针法来解决该问题。将指针分别放置在字符串数组的起点和终点，交换它们指向的元素，然后向中间移动指针，直到指针相遇为止。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义反转字符串的函数
    def reverseString(self, s: List[str]) -> None:
        # 初始化左右指针
        left, right = 0, len(s) - 1

        # 使用双指针法交换字符串数组中的元素
        while left < right:
            # 交换左右指针对应的元素
            s[left], s[right] = s[right], s[left]
            # 移动左右指针
            left += 1
            right -= 1

# 时间复杂度：O(n) - 最多遍历数组的一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组的一半。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### [3. LeetCode 345: Reverse Vowels of a String（反转字符串中的元音字母）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E5%8F%8C%E6%8C%87%E9%92%88/LeetCode%20345%3A%20%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E5%85%83%E9%9F%B3%E5%AD%97%E6%AF%8D%20(Reverse%20Vowels%20of%20a%20String).md)

**题目描述**：
编写一个函数，其作用是将输入字符串 `s` 中的元音字母反转，只反转元音字母，其他字符保持不变。

**题目分析**：
可以使用双指针法来解决该问题。将指针分别放置在字符串的起点和终点，移动指针直到遇到元音字母，然后交换它们。继续移动指针直到指针相遇为止。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义反转字符串中元音字母的函数
    def reverseVowels(self, s: str) -> str:
        # 将字符串转换为列表以便交换字符
        s = list(s)
        # 定义元音字母集合
        vowels = set("aeiouAEIOU")
        # 初始化左右指针
        left, right = 0, len(s) - 1

        # 使用双指针法交换字符串中的元音字母
        while left < right:
            # 移动左指针直到遇到元音字母
            while left < right and s[left] not in vowels:
                left += 1
            # 移动右指针直到遇到元音字母
            while left < right and s[right] not in vowels:
                right -= 1
            # 交换左右指针对应的元音字母
            s[left], s[right] = s[right], s[left]
            # 移动左右指针
            left += 1
            right -= 1

        # 将列表转换为字符串并返回
        return "".join(s)

# 时间复杂度：O(n) - 最多遍历字符串一次
# 空间复杂度：O(n) - 使用了一个列表来存储字符串
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，最多遍历字符串一次。
- **空间复杂度**：O(n)，由于字符串是不可变的，转换为列表的操作占用了额外的空间。

---

### [4. LeetCode 11: Container With Most Water（盛最多水的容器）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E5%8F%8C%E6%8C%87%E9%92%88/LeetCode%2011%3A%20%E7%9B%9B%E6%9C%80%E5%A4%9A%E6%B0%B4%E7%9A%84%E5%AE%B9%E5%99%A8%20(Container%20With%20Most%20Water).md)

**题目描述**：
给定一个长度为 `n` 的整数数组 `height`，数组中的每个元素代表柱子的高度。找出能够盛水最多的两个柱子，返回它们能够盛水的最大面积。

**题目分析**：
可以使用双指针法来解决该问题。将指针分别放置在数组的起点和终点，计算它们之间能够盛水的面积。然后移动指向较矮柱子的指针，因为移动较高的柱子不会增加面积。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算盛最多水容器的函数
    def maxArea(self, height: List[int]) -> int:
        # 初始化左右指针和最大面积
        left, right = 0, len(height) - 1
        max_area = 0

        # 使用双指针法查找最大面积
        while left < right:
            # 计算当前左右指针能够盛水的面积
            current_area = (right - left) * min(height[left], height[right])
            # 更新最大面积
            max_area = max(max_area, current_area)
            # 移动较矮柱子的指针
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### [5. LeetCode 26: Remove Duplicates from Sorted Array（删除有序数组中的重复项）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E5%8F%8C%E6%8C%87%E9%92%88/LeetCode%2026%3A%20%E5%88%A0%E9%99%A4%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E9%87%8D%E5%A4%8D%E9%A1%B9%20(Remove%20Duplicates%20from%20Sorted%20Array).md)

**题目描述**：
给定一个升序排列的整数数组 `nums`，删除其中的重复元素，使每个元素只出现一次，并返回新的长度。不要使用额外的数组空间，必须在原地修改数组并使用 O(1) 额外空间。

**题目分析**：
可以使用双指针法来解决该问题。第一个指针 `slow` 指向结果数组的末尾，第二个指针 `fast` 用于遍历整个数组。当 `fast` 指向的元素与 `slow` 指向的元素不同时，更新 `slow` 指向的位置，并将 `fast` 指向的元素复制到 `slow` 指向的位置。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除有序数组中重复项的函数
    def removeDuplicates(self, nums: List[int]) -> int:
        # 如果数组为空，直接返回 0


        if not nums:
            return 0

        # 初始化慢指针
        slow = 0

        # 使用快指针遍历数组
        for fast in range(1, len(nums)):
            # 当快指针与慢指针指向的元素不同时，更新慢指针的位置
            if nums[fast] != nums[slow]:
                slow += 1
                nums[slow] = nums[fast]

        # 返回新的数组长度
        return slow + 1

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

好的，我们继续讲解接下来的五道 LeetCode 双指针题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 6. LeetCode 27: Remove Element（移除元素）

**题目描述**：
给定一个数组 `nums` 和一个值 `val`，你需要原地移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。不要使用额外的数组空间，必须在原地修改输入数组，并使用 O(1) 的额外空间。

**题目分析**：
可以使用双指针法来解决该问题。一个指针 `slow` 用于记录结果数组的末尾，另一个指针 `fast` 用于遍历整个数组。当 `fast` 指向的元素不等于 `val` 时，将其复制到 `slow` 指向的位置，然后移动 `slow` 指针。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义移除元素的函数
    def removeElement(self, nums: List[int], val: int) -> int:
        # 初始化慢指针
        slow = 0

        # 使用快指针遍历数组
        for fast in range(len(nums)):
            # 当快指针指向的元素不等于 val 时，将其放到慢指针位置
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1

        # 返回新的数组长度
        return slow

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 7. LeetCode 283: Move Zeroes（移动零）

**题目描述**：
给定一个数组 `nums`，将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序不变。

**题目分析**：
可以使用双指针法来解决该问题。一个指针 `slow` 用于记录结果数组的末尾（即非零元素的末尾），另一个指针 `fast` 用于遍历整个数组。当 `fast` 指向的元素不为 `0` 时，将其复制到 `slow` 指向的位置，然后移动 `slow` 指针。最后将 `slow` 后面的元素全部设置为 `0`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义移动零的函数
    def moveZeroes(self, nums: List[int]) -> None:
        # 初始化慢指针
        slow = 0

        # 使用快指针遍历数组
        for fast in range(len(nums)):
            # 当快指针指向的元素不为 0 时，将其放到慢指针位置
            if nums[fast] != 0:
                nums[slow] = nums[fast]
                slow += 1

        # 将慢指针后面的所有元素设置为 0
        for i in range(slow, len(nums)):
            nums[i] = 0

# 时间复杂度：O(n) - 最多遍历数组两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组两次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 8. LeetCode 88: Merge Sorted Array（合并两个有序数组）

**题目描述**：
给定两个有序整数数组 `nums1` 和 `nums2`，将 `nums2` 合并到 `nums1` 中，使 `nums1` 成为一个有序数组。`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示 `nums1` 的初始内容，后 `n` 个元素为 `0`，代表空位，`nums2` 的长度为 `n`。

**题目分析**：
可以使用双指针法从数组的末尾开始合并（逆向合并）。定义三个指针：`p1` 指向 `nums1` 的有效元素末尾，`p2` 指向 `nums2` 的末尾，`p` 指向 `nums1` 的末尾。当 `p1` 和 `p2` 都未越界时，比较 `p1` 和 `p2` 指向的元素，将较大的元素放入 `p` 位置。最后处理 `p2` 未合并完的情况。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义合并两个有序数组的函数
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        # 初始化指针
        p1, p2, p = m - 1, n - 1, m + n - 1

        # 从后向前合并两个数组
        while p1 >= 0 and p2 >= 0:
            # 将较大的元素放入 p 位置
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            p -= 1

        # 将 nums2 中剩余的元素放入 nums1
        nums1[:p2 + 1] = nums2[:p2 + 1]

# 时间复杂度：O(m + n) - 最多遍历两个数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(m + n)，其中 m 和 n 分别是两个数组的长度，最多遍历两个数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 9. LeetCode 524: Longest Word in Dictionary through Deleting（通过删除字母匹配到字典里最长单词）

**题目描述**：
给定一个字符串 `s` 和一个字符串数组 `dictionary`，找出并返回 `dictionary` 中最长的字符串，该字符串可以通过删除 `s` 中的一些字符得到。如果有多个符合条件的字符串，返回字典序最小的那个字符串。

**题目分析**：
可以使用双指针法来判断 `dictionary` 中的每个字符串是否可以通过删除 `s` 中的一些字符得到。将两个指针分别放置在 `s` 和目标字符串的起点，遍历 `s`，判断是否能够顺序匹配目标字符串中的所有字符。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最长字符串的函数
    def findLongestWord(self, s: str, dictionary: List[str]) -> str:
        # 定义判断 s 是否包含目标字符串的函数
        def is_subsequence(s, target):
            it = iter(s)
            return all(char in it for char in target)

        # 遍历字典中的每个字符串，找到最长且字典序最小的字符串
        result = ""
        for word in dictionary:
            # 如果 word 是 s 的子序列，且长度更长或字典序更小，则更新结果
            if is_subsequence(s, word):
                if len(word) > len(result) or (len(word) == len(result) and word < result):
                    result = word

        return result

# 时间复杂度：O(n * m) - n 是字典中字符串的数量，m 是 s 的长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * m)，其中 n 是字典中字符串的数量，m 是 `s` 的长度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 10. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由一些**闭区间**组成的列表 `firstList` 和 `secondList`，返回这两个区间列表的交集。每个列表中的区间均按升序排列。

**题目分析**：
可以使用双指针法来解决该问题。将两个指针分别放置在 `firstList` 和 `secondList` 的起点，找到两个区间的交集，如果有交

集则加入结果列表。然后移动指向右边界较小的区间的指针。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找区间交集的函数
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        # 初始化两个指针
        i, j = 0, 0
        # 初始化结果列表
        result = []

        # 使用双指针法查找区间交集
        while i < len(firstList) and j < len(secondList):
            # 取两个区间的最大起点和最小终点
            start = max(firstList[i][0], secondList[j][0])
            end = min(firstList[i][1], secondList[j][1])

            # 如果有交集，加入结果列表
            if start <= end:
                result.append([start, end])

            # 移动指向右边界较小的区间的指针
            if firstList[i][1] < secondList[j][1]:
                i += 1
            else:
                j += 1

        return result

# 时间复杂度：O(m + n) - 最多遍历两个列表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(m + n)，其中 m 和 n 分别是两个区间列表的长度，最多遍历两个列表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

好的，我们继续讲解接下来的五道 LeetCode 双指针题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 11. LeetCode 42: Trapping Rain Water（接雨水）

**题目描述**：
给定一个非负整数数组 `height`，表示每个柱子的高度，计算数组中的柱子能够接住多少雨水。

**题目分析**：
可以使用双指针法来解决该问题。初始化左右指针分别指向数组的起点和终点，以及两个变量 `left_max` 和 `right_max` 记录当前指针位置的最大高度。移动左右指针并更新最大高度，如果当前高度小于最大高度，则将差值加入总雨水量中。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义接雨水的函数
    def trap(self, height: List[int]) -> int:
        # 初始化左右指针和最大高度
        left, right = 0, len(height) - 1
        left_max, right_max = 0, 0
        total_water = 0

        # 使用双指针法计算接雨水量
        while left < right:
            if height[left] < height[right]:
                # 更新左侧最大高度
                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    # 计算当前接水量
                    total_water += left_max - height[left]
                left += 1
            else:
                # 更新右侧最大高度
                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    # 计算当前接水量
                    total_water += right_max - height[right]
                right -= 1

        return total_water

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和高度的记录）。

---

### 12. LeetCode 680: Valid Palindrome II（验证回文字符串 II）

**题目描述**：
给定一个字符串 `s`，你可以最多删除一个字符。判断是否能成为回文字符串。

**题目分析**：
可以使用双指针法来解决该问题。初始化左右指针分别指向字符串的起点和终点，判断当前字符是否相等。如果不相等，则可以尝试删除左指针或右指针指向的字符，并检查是否形成回文字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义验证回文字符串的函数
    def validPalindrome(self, s: str) -> bool:
        # 定义检查是否为回文字符串的辅助函数
        def is_palindrome(low, high):
            while low < high:
                if s[low] != s[high]:
                    return False
                low += 1
                high -= 1
            return True

        # 初始化左右指针
        left, right = 0, len(s) - 1

        # 使用双指针法判断是否可以成为回文字符串
        while left < right:
            if s[left] != s[right]:
                # 尝试删除左指针或右指针指向的字符
                return is_palindrome(left + 1, right) or is_palindrome(left, right - 1)
            left += 1
            right -= 1

        return True

# 时间复杂度：O(n) - 最多遍历字符串一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，最多遍历字符串一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 13. LeetCode 209: Minimum Size Subarray Sum（长度最小的子数组）

**题目描述**：
给定一个含有正整数的数组 `nums` 和一个正整数 `target`，找出该数组中和大于或等于 `target` 的最小子数组长度。如果不存在符合条件的子数组，返回 `0`。

**题目分析**：
可以使用滑动窗口（双指针）法来解决该问题。初始化左右指针指向数组的起点，并维护一个滑动窗口的和 `current_sum`。移动右指针扩大窗口，直到窗口和大于或等于 `target`，然后移动左指针缩小窗口，更新最小子数组长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找长度最小的子数组的函数
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        # 初始化左右指针、当前和和最小长度
        left, current_sum = 0, 0
        min_length = float('inf')

        # 使用滑动窗口法查找最小子数组长度
        for right in range(len(nums)):
            current_sum += nums[right]
            # 当当前和大于或等于目标值时，尝试缩小窗口
            while current_sum >= target:
                min_length = min(min_length, right - left + 1)
                current_sum -= nums[left]
                left += 1

        return 0 if min_length == float('inf') else min_length

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和滑动窗口的和）。

---

### 14. LeetCode 3: Longest Substring Without Repeating Characters（无重复字符的最长子串）

**题目描述**：
给定一个字符串 `s`，找出其中不含有重复字符的最长子串的长度。

**题目分析**：
可以使用滑动窗口（双指针）法来解决该问题。初始化左右指针指向字符串的起点，并维护一个哈希集合 `seen` 记录当前窗口内的字符。移动右指针扩大窗口，直到遇到重复字符，然后移动左指针缩小窗口，更新最长子串的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找无重复字符最长子串长度的函数
    def lengthOfLongestSubstring(self, s: str) -> int:
        # 初始化左右指针、哈希集合和最长长度
        left, max_length = 0, 0
        seen = set()

        # 使用滑动窗口法查找最长子串长度
        for right in range(len(s)):
            # 当右指针指向的字符已在集合中时，移动左指针
            while s[right] in seen:
                seen.remove(s[left])
                left += 1
            # 将右指针指向的字符加入集合
            seen.add(s[right])
            # 更新最长长度
            max_length = max(max_length, right - left + 1)

        return max_length

# 时间复杂度：O(n) - 最多遍历字符串一次
# 空间复杂度：O(min(n, m)) - n 为字符串长度，m 为字符集大小（即 26）
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，最多遍历字符串一次。
- **空间复杂度**：O(min(n, m))，其中 n 是字符串的长度，m 为字符集大小（即 26），用于存储集合中的字符。

---

### 15. LeetCode 75: Sort Colors（颜色分类）

**题目描述**：
给定一个包含红色、白色和蓝色的数组 `nums`（分别用整数 `0`、`1` 和 `2` 表示），请对数组进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排序。

**题目分析**：
可以使用三指针法来解决该问题。定义三个指针：`left` 指向红色的末尾，`right` 指向蓝色的开头，`i` 用于遍历数组。遍历过程中将 `0` 交换到 `left` 指针位置，将 `2` 交换到 `right` 指针位置。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义颜色分类的函数
    def sortColors(self, nums: List[int]) -> None:
       

 # 初始化左右指针和遍历指针
        left, i, right = 0, 0, len(nums) - 1

        # 使用三指针法对数组进行排序
        while i <= right:
            if nums[i] == 0:
                # 将 0 交换到 left 指针位置
                nums[i], nums[left] = nums[left], nums[i]
                left += 1
                i += 1
            elif nums[i] == 2:
                # 将 2 交换到 right 指针位置
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
            else:
                # 1 的情况不需要交换，直接移动 i 指针
                i += 1

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

好的，我们继续讲解接下来的五道 LeetCode 双指针题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 16. LeetCode 925: Long Pressed Name（长按键入）

**题目描述**：
你的朋友正在使用键盘输入他的名字 `name`。偶尔，在键入字符时可能会被长按键入。例如，当输入字符 'a' 时，可能会输入 `aa`，而且字符仍然会按顺序出现。你会检查键入的字符 `typed` 是否可能是你的朋友的名字 `name` 的长按键入（即 `typed` 的字符可以多于 `name`，但不能少于 `name`）。

**题目分析**：
可以使用双指针法来解决该问题。一个指针 `i` 用于遍历 `name`，另一个指针 `j` 用于遍历 `typed`。如果两个指针指向的字符相同，则同时移动两个指针；如果 `typed` 中当前字符与 `name` 的前一个字符相同，则只移动 `j` 指针；否则返回 `False`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否为长按键入的函数
    def isLongPressedName(self, name: str, typed: str) -> bool:
        # 初始化两个指针
        i, j = 0, 0

        # 使用双指针法遍历 name 和 typed
        while j < len(typed):
            if i < len(name) and name[i] == typed[j]:
                # 当两个指针指向的字符相同时，同时移动两个指针
                i += 1
            elif j > 0 and typed[j] == typed[j - 1]:
                # 当 typed 当前字符与前一个字符相同时，移动 j 指针
                j += 1
            else:
                # 不能匹配，返回 False
                return False
            j += 1

        # 判断是否所有 name 中的字符都被匹配
        return i == len(name)

# 时间复杂度：O(n + m) - n 和 m 分别是 name 和 typed 的长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是 `name` 和 `typed` 的长度，最多遍历两个字符串一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 17. LeetCode 283: Move Zeroes（移动零）

**题目描述**：
给定一个数组 `nums`，将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序不变。

**题目分析**：
可以使用双指针法来解决该问题。一个指针 `slow` 用于记录结果数组的末尾（即非零元素的末尾），另一个指针 `fast` 用于遍历整个数组。当 `fast` 指向的元素不为 `0` 时，将其复制到 `slow` 指向的位置，然后移动 `slow` 指针。最后将 `slow` 后面的元素全部设置为 `0`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义移动零的函数
    def moveZeroes(self, nums: List[int]) -> None:
        # 初始化慢指针
        slow = 0

        # 使用快指针遍历数组
        for fast in range(len(nums)):
            # 当快指针指向的元素不为 0 时，将其放到慢指针位置
            if nums[fast] != 0:
                nums[slow] = nums[fast]
                slow += 1

        # 将慢指针后面的所有元素设置为 0
        for i in range(slow, len(nums)):
            nums[i] = 0

# 时间复杂度：O(n) - 最多遍历数组两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组两次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 18. LeetCode 977: Squares of a Sorted Array（有序数组的平方）

**题目描述**：
给定一个按非递减顺序排列的整数数组 `nums`，返回每个数字的平方组成的新数组，要求新数组也按非递减顺序排列。

**题目分析**：
可以使用双指针法来解决该问题。初始化两个指针分别指向数组的起点和终点，比较两个指针指向的元素的平方值，将较大的平方值加入结果数组，然后移动相应的指针。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算有序数组的平方的函数
    def sortedSquares(self, nums: List[int]) -> List[int]:
        # 初始化左右指针和结果数组
        left, right = 0, len(nums) - 1
        result = [0] * len(nums)
        # 填充结果数组的指针
        pos = len(nums) - 1

        # 使用双指针法计算平方并填充结果数组
        while left <= right:
            if abs(nums[left]) > abs(nums[right]):
                result[pos] = nums[left] ** 2
                left += 1
            else:
                result[pos] = nums[right] ** 2
                right -= 1
            pos -= 1

        return result

# 时间复杂度：O(n) - 最多遍历数组一次
# 空间复杂度：O(n) - 用于存储结果数组的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组一次。
- **空间复杂度**：O(n)，用于存储结果数组的额外空间。

---

### 19. LeetCode 876: Middle of the Linked List（链表的中间节点)

**题目描述**：
给定一个单链表，找到链表的中间节点。如果链表的节点个数为偶数，则返回中间两个节点的第二个节点。

**题目分析**：
可以使用快慢指针法来解决该问题。定义两个指针 `slow` 和 `fast`，`slow` 每次移动一步，`fast` 每次移动两步。当 `fast` 指向链表的末尾时，`slow` 就指向链表的中间节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义查找链表中间节点的函数
    def middleNode(self, head: ListNode) -> ListNode:
        # 初始化快慢指针
        slow, fast = head, head

        # 使用快慢指针法查找链表中间节点
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        return slow

# 时间复杂度：O(n) - 最多遍历链表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 20. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由一些**闭区间**组成的列表 `firstList` 和 `secondList`，返回这两个区间列表的交集。每个列表中的区间均按升序排列。

**题目分析**：
可以使用双指针法来解决该问题。将两个指针分别放置在 `firstList` 和 `secondList` 的起点，找到两个区间的交集，如果有交集则加入结果列表。然后移动指向右边界较小的区间的指针。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找区间交集的函数
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        # 初始化两个指针
        i, j = 0, 0
        # 初始化结果列表
        result = []

        # 使用双指针法查找区间交集


        while i < len(firstList) and j < len(secondList):
            # 取两个区间的最大起点和最小终点
            start = max(firstList[i][0], secondList[j][0])
            end = min(firstList[i][1], secondList[j][1])

            # 如果有交集，加入结果列表
            if start <= end:
                result.append([start, end])

            # 移动指向右边界较小的区间的指针
            if firstList[i][1] < secondList[j][1]:
                i += 1
            else:
                j += 1

        return result

# 时间复杂度：O(m + n) - 最多遍历两个列表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(m + n)，其中 m 和 n 分别是两个区间列表的长度，最多遍历两个列表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

好的，我们继续讲解接下来的五道 LeetCode 双指针题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 21. LeetCode 15: 3Sum（三数之和）

**题目描述**：
给定一个包含 `n` 个整数的数组 `nums`，判断是否存在三个元素 `a, b, c` 使得 `a + b + c = 0`。找出所有满足条件且不重复的三元组。

**题目分析**：
可以使用双指针法来解决该问题。首先将数组进行排序，然后固定一个元素 `nums[i]`，再使用左右双指针寻找剩余两个元素 `nums[left]` 和 `nums[right]`，使得三者之和为 0。通过移动指针和去重策略，可以高效地找到所有不重复的三元组。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找三数之和的函数
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # 初始化结果列表
        res = []
        # 将数组排序
        nums.sort()

        # 遍历数组，固定一个元素 nums[i]
        for i in range(len(nums)):
            # 跳过重复的元素
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            # 初始化左右指针
            left, right = i + 1, len(nums) - 1

            # 使用双指针查找剩余两个元素
            while left < right:
                total = nums[i] + nums[left] + nums[right]
                if total == 0:
                    # 找到满足条件的三元组，加入结果列表
                    res.append([nums[i], nums[left], nums[right]])
                    # 跳过重复的元素
                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1
                    # 移动左右指针
                    left += 1
                    right -= 1
                elif total < 0:
                    # 和小于 0，移动左指针
                    left += 1
                else:
                    # 和大于 0，移动右指针
                    right -= 1

        return res

# 时间复杂度：O(n^2) - 遍历数组和使用双指针查找的复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，其中 n 是数组的长度。排序的复杂度为 O(n log n)，双指针查找的复杂度为 O(n^2)。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 22. LeetCode 16: 3Sum Closest（最接近的三数之和）

**题目描述**：
给定一个包含 `n` 个整数的数组 `nums` 和一个目标值 `target`，找出 `nums` 中的三个整数，使得它们的和与 `target` 最接近。返回这三个数的和。

**题目分析**：
可以使用双指针法来解决该问题。首先将数组进行排序，然后固定一个元素 `nums[i]`，再使用左右双指针寻找剩余两个元素 `nums[left]` 和 `nums[right]`，计算三者之和并与目标值进行比较，更新最接近的和。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最接近的三数之和的函数
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        # 将数组排序
        nums.sort()
        # 初始化最接近的和为数组前三个元素的和
        closest_sum = nums[0] + nums[1] + nums[2]

        # 遍历数组，固定一个元素 nums[i]
        for i in range(len(nums) - 2):
            # 初始化左右指针
            left, right = i + 1, len(nums) - 1

            # 使用双指针查找剩余两个元素
            while left < right:
                current_sum = nums[i] + nums[left] + nums[right]
                # 更新最接近的和
                if abs(current_sum - target) < abs(closest_sum - target):
                    closest_sum = current_sum

                # 根据当前和与目标值的大小关系移动指针
                if current_sum < target:
                    left += 1
                elif current_sum > target:
                    right -= 1
                else:
                    # 如果当前和等于目标值，直接返回
                    return current_sum

        return closest_sum

# 时间复杂度：O(n^2) - 遍历数组和使用双指针查找的复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，其中 n 是数组的长度。排序的复杂度为 O(n log n)，双指针查找的复杂度为 O(n^2)。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 23. LeetCode 18: 4Sum（四数之和）

**题目描述**：
给定一个包含 `n` 个整数的数组 `nums` 和一个目标值 `target`，判断 `nums` 中是否存在四个元素 `a, b, c, d` 使得 `a + b + c + d = target`。找出所有满足条件且不重复的四元组。

**题目分析**：
可以使用双指针法来解决该问题。首先将数组进行排序，然后固定两个元素 `nums[i]` 和 `nums[j]`，再使用左右双指针寻找剩余两个元素 `nums[left]` 和 `nums[right]`，使得四者之和等于目标值。通过移动指针和去重策略，可以高效地找到所有不重复的四元组。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找四数之和的函数
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        # 初始化结果列表
        res = []
        # 将数组排序
        nums.sort()

        # 遍历数组，固定两个元素 nums[i] 和 nums[j]
        for i in range(len(nums) - 3):
            # 跳过重复的元素
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, len(nums) - 2):
                # 跳过重复的元素
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue

                # 初始化左右指针
                left, right = j + 1, len(nums) - 1

                # 使用双指针查找剩余两个元素
                while left < right:
                    total = nums[i] + nums[j] + nums[left] + nums[right]
                    if total == target:
                        # 找到满足条件的四元组，加入结果列表
                        res.append([nums[i], nums[j], nums[left], nums[right]])
                        # 跳过重复的元素
                        while left < right and nums[left] == nums[left + 1]:
                            left += 1
                        while left < right and nums[right] == nums[right - 1]:
                            right -= 1
                        # 移动左右指针
                        left += 1
                        right -= 1
                    elif total < target:
                        # 和小于目标值，移动左指针
                        left += 1
                    else:
                        # 和大于目标值，移动右指针
                        right -= 1

        return res

# 时间复杂度：O(n^3) - 遍历数组和使用双指针查找的复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^3)，其中 n 是数组的长度。排序的复杂度为 O(n log n)，双指针查找的复杂度为 O(n^3)。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 24. LeetCode 844: Backspace String Compare（比较含退格的字符串）

**题目描述**：
给定两个字符串 `s` 和 `t`，分别表示输入的两个字符串。每个字符串中可能包含 `#`，表示退格字符。请判断两字符串经过退格处理后是否相等。

**题目分析**：


可以使用双指针法从后向前遍历两个字符串。当遇到 `#` 时，跳过对应的字符，并处理多余的退格字符，直到找到有效字符进行比较。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义比较含退格的字符串的函数
    def backspaceCompare(self, s: str, t: str) -> bool:
        # 定义从后向前遍历字符串的辅助函数
        def process_string(string):
            skip = 0
            for char in reversed(string):
                if char == '#':
                    skip += 1
                elif skip:
                    skip -= 1
                else:
                    yield char

        # 使用双指针从后向前遍历两个字符串，比较它们的字符
        return all(x == y for x, y in zip(process_string(s), process_string(t)))

# 时间复杂度：O(n + m) - n 和 m 分别是 s 和 t 的长度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是 `s` 和 `t` 的长度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和字符的处理）。

---

### 25. LeetCode 31: Next Permutation（下一个排列）

**题目描述**：
实现获取下一个排列的函数，给定一个排列的整数数组 `nums`，将其重新排列为下一个字典序更大的排列（即找到比当前数组更大的排列）。如果不存在这样的排列，则将其重新排列为最小的排列（即升序排列）。

**题目分析**：
可以使用双指针法来解决该问题。首先从后向前找到第一个递减元素的位置 `i`，再从后向前找到第一个大于 `nums[i]` 的元素 `j`，交换它们，然后将 `i` 后面的元素进行翻转。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义获取下一个排列的函数
    def nextPermutation(self, nums: List[int]) -> None:
        # 初始化指针
        i = len(nums) - 2

        # 从后向前找到第一个递减的元素
        while i >= 0 and nums[i] >= nums[i + 1]:
            i -= 1

        # 如果存在递减元素，则找到第一个大于 nums[i] 的元素进行交换
        if i >= 0:
            j = len(nums) - 1
            while j >= 0 and nums[j] <= nums[i]:
                j -= 1
            # 交换 nums[i] 和 nums[j]
            nums[i], nums[j] = nums[j], nums[i]

        # 将 i 之后的元素翻转，使其成为最小的排列
        nums[i + 1:] = reversed(nums[i + 1:])

# 时间复杂度：O(n) - 最多遍历数组两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，最多遍历数组两次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和数组的翻转）。

---

好的，我们继续讲解接下来的五道 LeetCode 双指针题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 26. LeetCode 141: Linked List Cycle（环形链表）

**题目描述**：
给定一个链表，判断链表中是否有环。如果链表中存在环，则返回 `True`，否则返回 `False`。

**题目分析**：
可以使用快慢指针法来解决该问题。定义两个指针 `slow` 和 `fast`，`slow` 每次移动一步，`fast` 每次移动两步。如果 `slow` 和 `fast` 相遇，则说明链表中存在环；否则当 `fast` 或 `fast.next` 为空时，说明链表中不存在环。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义判断链表是否有环的函数
    def hasCycle(self, head: ListNode) -> bool:
        # 初始化快慢指针
        slow, fast = head, head

        # 使用快慢指针法判断链表是否有环
        while fast and fast.next:
            slow = slow.next          # 慢指针移动一步
            fast = fast.next.next     # 快指针移动两步
            if slow == fast:          # 快慢指针相遇，说明有环
                return True

        return False  # 快指针到达链表末尾，说明没有环

# 时间复杂度：O(n) - 最多遍历链表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 27. LeetCode 19: Remove Nth Node From End of List（删除链表的倒数第 N 个节点）

**题目描述**：
给定一个链表，删除链表的倒数第 `n` 个节点，并返回链表的头节点。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `first` 和 `second`，首先将 `first` 指针向前移动 `n` 步，然后同时移动 `first` 和 `second` 指针，当 `first` 指针到达链表末尾时，`second` 指针指向倒数第 `n+1` 个节点，删除其下一个节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义删除倒数第 n 个节点的函数
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        # 定义虚拟头节点，方便处理边界情况
        dummy = ListNode(0, head)
        # 初始化两个指针
        first, second = dummy, dummy

        # 将第一个指针向前移动 n 步
        for _ in range(n):
            first = first.next

        # 同时移动两个指针，直到第一个指针到达链表末尾
        while first.next:
            first = first.next
            second = second.next

        # 删除第二个指针的下一个节点
        second.next = second.next.next

        # 返回链表头节点
        return dummy.next

# 时间复杂度：O(n) - 最多遍历链表两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表两次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 28. LeetCode 876: Middle of the Linked List（链表的中间节点）

**题目描述**：
给定一个单链表，找到链表的中间节点。如果链表的节点个数为偶数，则返回中间两个节点的第二个节点。

**题目分析**：
可以使用快慢指针法来解决该问题。定义两个指针 `slow` 和 `fast`，`slow` 每次移动一步，`fast` 每次移动两步。当 `fast` 指向链表的末尾时，`slow` 就指向链表的中间节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义查找链表中间节点的函数
    def middleNode(self, head: ListNode) -> ListNode:
        # 初始化快慢指针
        slow, fast = head, head

        # 使用快慢指针法查找链表中间节点
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        return slow

# 时间复杂度：O(n) - 最多遍历链表一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表一次。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动）。

---

### 29. LeetCode 143: Reorder List（重排链表）

**题目描述**：
给定一个单链表 `L`：`L0 → L1 → … → Ln-1 → Ln`，将其重新排列为：`L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …`，要求使用原地算法，不使用额外空间。

**题目分析**：
可以使用双指针法结合链表操作来解决该问题：
1. 使用快慢指针找到链表的中间节点，将链表分为两半。
2. 反转后半部分链表。
3. 合并前半部分和后半部分的链表节点。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义重排链表的函数
    def reorderList(self, head: ListNode) -> None:
        # 如果链表为空或只有一个节点，直接返回
        if not head or not head.next:
            return

        # 步骤 1：使用快慢指针找到链表的中间节点
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 步骤 2：将链表分为两部分，并反转后半部分链表
        second = slow.next
        slow.next = None
        prev = None
        while second:
            temp = second.next
            second.next = prev
            prev = second
            second = temp

        # 步骤 3：将前半部分与反转后的后半部分合并
        first, second = head, prev
        while second:
            temp1, temp2 = first.next, second.next
            first.next = second
            second.next = temp1
            first, second = temp1, temp2

# 时间复杂度：O(n) - 最多遍历链表三次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表三次：一次找到中间节点，一次反转后半部分链表，一次合并链表。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。

---

### 30. LeetCode 234: Palindrome Linked List（回文链表）

**题目描述**：
给定一个链表，判断链表是否为回文结构。

**题目分析**：
可以使用双指针法结合链表操作来解决该问题：
1. 使用快慢指针找到链表的中间节点。
2. 反转后半部分链表。
3. 比较前半部分和

反转后的后半部分是否相等。

**代码实现**：
```python
# 定义链表节点类
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义判断回文链表的函数
    def isPalindrome(self, head: ListNode) -> bool:
        # 步骤 1：使用快慢指针找到链表的中间节点
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # 步骤 2：反转后半部分链表
        prev = None
        while slow:
            temp = slow.next
            slow.next = prev
            prev = slow
            slow = temp

        # 步骤 3：比较前半部分和反转后的后半部分链表
        left, right = head, prev
        while right:  # 注意：只需比较后半部分的长度
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True

# 时间复杂度：O(n) - 最多遍历链表两次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是链表的长度，最多遍历链表两次：一次找到中间节点，一次比较链表的前后部分。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和链表操作）。
