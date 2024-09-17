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

### 10 道 LeetCode 双指针题目及详细解释

---

#### 1. LeetCode 167: 两数之和 II - 输入有序数组 (Two Sum II - Input Array Is Sorted)

##### Problem Description  
给定一个已按升序排列的数组，找到两个数，使得它们的和等于目标数。返回这两个数的索引，注意数组的索引从 1 开始。

##### 解法：双指针  
使用两个指针分别从数组的两端向中间移动，根据当前和与目标的关系调整指针。

##### Python 代码：

```python
def twoSum(numbers, target):
    left, right = 0, len(numbers) - 1  # 初始化左指针和右指针
    while left < right:  # 当左指针小于右指针时继续
        current_sum = numbers[left] + numbers[right]  # 计算当前两数之和
        if current_sum == target:  # 如果找到目标和，返回索引
            return [left + 1, right + 1]  # 索引从 1 开始
        elif current_sum < target:  # 如果当前和小于目标，左指针右移
            left += 1
        else:  # 如果当前和大于目标，右指针左移
            right -= 1
```

##### 解释：
- 左指针从数组左端开始，右指针从数组右端开始。
- 根据当前和与目标值的大小关系，决定移动哪个指针，直到找到目标和。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 2. LeetCode 344: 反转字符串 (Reverse String)

##### Problem Description  
编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组的形式给出。

##### 解法：双指针  
使用双指针从字符串的两端开始交换字符，直到指针相遇。

##### Python 代码：

```python
def reverseString(s):
    left, right = 0, len(s) - 1  # 初始化左指针和右指针
    while left < right:  # 当左指针小于右指针时继续
        s[left], s[right] = s[right], s[left]  # 交换左指针和右指针的字符
        left += 1  # 左指针右移
        right -= 1  # 右指针左移
```

##### 解释：
- 双指针分别指向字符串的头尾，交换两端的字符，然后逐步向中间移动指针。
- 当左指针和右指针相遇时，字符串已经完全反转。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 3. LeetCode 19: 删除链表的倒数第 N 个结点 (Remove Nth Node From End of List)

##### Problem Description  
给定一个链表，删除链表的倒数第 `n` 个结点，并返回链表的头节点。

##### 解法：双指针  
使用快慢指针，快指针先移动 `n` 步，然后快慢指针同时移动，直到快指针到达链表末尾，慢指针指向要删除的结点的前一个结点。

##### Python 代码：

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def removeNthFromEnd(head, n):
    dummy = ListNode(0, head)  # 哑节点，指向链表头部
    slow = fast = dummy  # 快慢指针初始化为哑节点
    for _ in range(n):  # 快指针先移动 n 步
        fast = fast.next
    while fast.next:  # 快慢指针同时移动，直到快指针到达链表末尾
        slow = slow.next
        fast = fast.next
    slow.next = slow.next.next  # 删除倒数第 n 个结点
    return dummy.next
```

##### 解释：
- 使用哑节点避免边界条件问题。
- 快指针先移动 `n` 步，然后快慢指针同时移动，直到快指针到达链表末尾，慢指针指向要删除结点的前一个结点。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 4. LeetCode 26: 删除有序数组中的重复项 (Remove Duplicates from Sorted Array)

##### Problem Description  
给定一个有序数组，原地删除重复出现的元素，使得每个元素只出现一次，返回删除后数组的新长度。

##### 解法：双指针  
使用双指针，左指针指向要保留的位置，右指针遍历数组，跳过重复项。

##### Python 代码：

```python
def removeDuplicates(nums):
    if not nums:
        return 0
    left = 1  # 左指针从第二个元素开始
    for right in range(1, len(nums)):  # 右指针遍历数组
        if nums[right] != nums[right - 1]:  # 如果当前元素不等于前一个元素
            nums[left] = nums[right]  # 保留该元素
            left += 1  # 左指针右移
    return left  # 返回新的数组长度
```

##### 解释：
- 右指针遍历数组，遇到不重复的元素时，将其移到左指针指向的位置。
- 左指针记录下一个不重复元素的位置，最终左指针指向的就是新数组的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 5. LeetCode 88: 合并两个有序数组 (Merge Sorted Array)

##### Problem Description  
给定两个有序整数数组 `nums1` 和 `nums2`，将 `nums2` 合并到 `nums1` 中，使得 `nums1` 成为一个有序数组。

##### 解法：双指针  
使用双指针分别指向两个数组的末尾，从大到小比较，将较大的元素放到 `nums1` 的末尾。

##### Python 代码：

```python
def merge(nums1, m, nums2, n):
    p1, p2, p = m - 1, n - 1, m + n - 1  # 初始化指针，分别指向 nums1 和 nums2 的末尾
    while p1 >= 0 and p2 >= 0:  # 当两个数组都有元素时继续
        if nums1[p1] > nums2[p2]:  # 如果 nums1 的元素更大
            nums1[p] = nums1[p1]  # 将 nums1 的元素放到最后
            p1 -= 1  # 移动 nums1 的指针
        else:  # 如果 nums2 的元素更大
            nums1[p] = nums2[p2]  # 将 nums2 的元素放到最后
            p

2 -= 1  # 移动 nums2 的指针
        p -= 1  # 移动合并后的数组的指针
    nums1[:p2 + 1] = nums2[:p2 + 1]  # 如果 nums2 还有剩余元素，直接拷贝
```

##### 解释：
- 从两个数组的末尾开始比较，逐步将较大的元素放入 `nums1` 的末尾。
- 如果 `nums2` 有剩余元素，直接将其放入 `nums1`。

##### 时间复杂度：O(m + n)  
##### 空间复杂度：O(1)

---

#### 6. LeetCode 524: 通过删除字母匹配到字典里最长单词 (Longest Word in Dictionary through Deleting)

##### Problem Description  
给定一个字符串和一个字符串字典，找到字典中最长的字符串，该字符串可以通过删除给定字符串的某些字符得到。

##### 解法：双指针  
使用双指针遍历给定字符串和字典中的每个单词，判断字典中的单词是否是给定字符串的子序列。

##### Python 代码：

```python
def findLongestWord(s, d):
    def isSubsequence(x):  # 辅助函数判断 x 是否为 s 的子序列
        it = iter(s)
        return all(c in it for c in x)
    
    d.sort(key=lambda x: (-len(x), x))  # 按长度降序，字典序升序排序
    for word in d:
        if isSubsequence(word):  # 如果是子序列
            return word  # 返回最长单词
    return ""  # 如果没有找到，返回空字符串
```

##### 解释：
- 使用双指针判断字典中的单词是否是字符串的子序列。
- 按长度和字典序排序，返回符合条件的最长单词。

##### 时间复杂度：O(n * m)，其中 `n` 是字典的长度，`m` 是字符串的长度。  
##### 空间复杂度：O(1)

---

#### 7. LeetCode 3: 无重复字符的最长子串 (Longest Substring Without Repeating Characters)

##### Problem Description  
给定一个字符串，请你找出其中不含有重复字符的最长子串的长度。

##### 解法：双指针 + 滑动窗口  
使用双指针维护一个滑动窗口，通过移动指针保证窗口内无重复字符。

##### Python 代码：

```python
def lengthOfLongestSubstring(s):
    char_set = set()  # 记录窗口中的字符
    left = 0  # 初始化左指针
    max_len = 0  # 记录最长长度
    for right in range(len(s)):  # 右指针遍历字符串
        while s[right] in char_set:  # 如果有重复字符，左指针右移
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])  # 将新字符加入窗口
        max_len = max(max_len, right - left + 1)  # 更新最长长度
    return max_len
```

##### 解释：
- 使用集合记录当前窗口中的字符，当出现重复字符时，移动左指针。
- 每次更新窗口的最大长度，返回结果。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(min(n, m))，其中 `m` 是字符集的大小。

---

#### 8. LeetCode 27: 移除元素 (Remove Element)

##### Problem Description  
给定一个数组和一个值，原地移除所有等于这个值的元素，返回移除后数组的长度。

##### 解法：双指针  
使用双指针，一个指针遍历数组，另一个指针记录下一个不等于目标值的位置。

##### Python 代码：

```python
def removeElement(nums, val):
    left = 0  # 初始化左指针
    for right in range(len(nums)):  # 右指针遍历数组
        if nums[right] != val:  # 如果当前元素不等于目标值
            nums[left] = nums[right]  # 将该元素移到左指针位置
            left += 1  # 左指针右移
    return left  # 返回新的数组长度
```

##### 解释：
- 右指针遍历数组，遇到不等于目标值的元素时，将其移动到左指针位置。
- 最终左指针指向的就是新数组的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 9. LeetCode 80: 删除有序数组中的重复项 II (Remove Duplicates from Sorted Array II)

##### Problem Description  
给定一个有序数组，原地删除重复出现次数超过两次的元素，使得每个元素最多保留两个。

##### 解法：双指针  
使用双指针，一个指针遍历数组，另一个指针记录要保留的位置。

##### Python 代码：

```python
def removeDuplicates(nums):
    if len(nums) <= 2:
        return len(nums)
    left = 2  # 初始化左指针，最多保留两个
    for right in range(2, len(nums)):  # 右指针遍历数组
        if nums[right] != nums[left - 2]:  # 如果当前元素不等于保留元素
            nums[left] = nums[right]  # 将该元素移到左指针位置
            left += 1  # 左指针右移
    return left  # 返回新的数组长度
```

##### 解释：
- 使用左指针记录要保留的位置，右指针遍历数组。
- 当遇到超过两次重复时，跳过该元素，否则将其移到左指针位置。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 10. LeetCode 125: 验证回文串 (Valid Palindrome)

##### Problem Description  
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

##### 解法：双指针  
使用双指针分别从字符串的两端开始，逐步向中间移动，比较字符是否相同。

##### Python 代码：

```python
def isPalindrome(s):
    left, right = 0, len(s) - 1  # 初始化左指针和右指针
    while left < right:  # 当左指针小于右指针时继续
        while left < right and not s[left].isalnum():  # 跳过非字母数字字符
            left += 1
        while left < right and not s[right].isalnum():  # 跳过非字母数字字符
            right -= 1
        if s[left].lower() != s[right].lower():  # 比较字符是否相同
            return False
        left += 1  # 左指针右移
        right -= 1  # 右指针左移
    return True  # 如果所有字符都相同，返回 True
```

##### 解释：
- 左右指针分别从字符串两端开始，跳过非字母数字字符，并忽略大小写进行比较。
- 如果字符不相同，返回 `False`；如果遍历结束，返回 `True`。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

### Conclusion  
双指针是一种灵活且高效的算法技巧，常用于数组、字符串、链表等数据结构的遍历和处理。通过合理地移动两个指针，能够高效解决许多问题。
