# 二分查找
### 二分查找 (Binary Search)

#### Definition  
二分查找是一种在**有序数组**中查找特定元素的高效算法。通过每次将搜索范围缩小一半，二分查找可以在对数时间内找到目标元素的位置或判断目标元素是否存在。该算法的核心思想是比较目标值与数组中间元素的大小，并据此决定继续在左半部分或右半部分进行搜索。

#### Key Concepts  
1. **有序数组 (Sorted Array)**: 二分查找仅适用于已经排序的数组。
2. **中点 (Midpoint)**: 每次查找的过程中计算数组的中间位置，并将目标值与中间元素进行比较。
3. **左右边界 (Left and Right Boundaries)**: 通过调整搜索的左右边界逐步缩小搜索范围。

#### 二分查找的步骤  
1. **初始化左右边界**：设定初始的左右边界，通常左边界为 `0`，右边界为 `len(arr) - 1`。
2. **计算中点**：根据左右边界计算中点 `mid = (left + right) // 2`。
3. **比较中点元素**：将目标值与中点元素比较，决定向左或向右缩小搜索范围。
4. **更新边界**：根据比较结果调整左右边界，继续下一轮搜索，直到找到目标值或边界相遇。

#### 二分查找的适用场景  
- 查找有序数组中的元素
- 查找某个范围内的第一个或最后一个满足条件的元素
- 查找插入位置

#### Python 二分查找模板

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1  # 初始化左右边界
    while left <= right:  # 当左边界小于等于右边界时继续
        mid = (left + right) // 2  # 计算中点
        if arr[mid] == target:  # 找到目标值
            return mid
        elif arr[mid] < target:  # 目标值在右半部分
            left = mid + 1
        else:  # 目标值在左半部分
            right = mid - 1
    return -1  # 未找到目标值
```

### 10 道 LeetCode 二分查找题目及详细解释

---

#### 1. LeetCode 704: 二分查找 (Binary Search)

##### Problem Description  
给定一个 `n` 个元素的有序数组，编写一个函数来搜索目标值。如果目标值存在，返回其索引；否则，返回 `-1`。

##### 解法：二分查找  
使用经典的二分查找算法，通过每次计算中点，缩小搜索范围。

##### Python 代码：

```python
def search(nums, target):
    left, right = 0, len(nums) - 1  # 初始化左右边界
    while left <= right:  # 当左边界小于等于右边界时继续
        mid = (left + right) // 2  # 计算中点
        if nums[mid] == target:  # 如果找到目标值
            return mid
        elif nums[mid] < target:  # 目标值在右半部分
            left = mid + 1
        else:  # 目标值在左半部分
            right = mid - 1
    return -1  # 未找到目标值
```

##### 解释：
- 使用 `left` 和 `right` 来控制搜索范围，每次通过 `mid` 找到中间元素。
- 根据 `mid` 和 `target` 的比较结果，调整 `left` 或 `right` 的值，缩小搜索范围。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 2. LeetCode 34: 在排序数组中查找元素的第一个和最后一个位置 (Find First and Last Position of Element in Sorted Array)

##### Problem Description  
给定一个升序排列的整数数组，找到目标值的起始和结束位置。如果数组中不存在目标值，返回 `[-1, -1]`。

##### 解法：二分查找  
使用两次二分查找分别找到目标值的第一个和最后一个位置。

##### Python 代码：

```python
def searchRange(nums, target):
    def findLeft(nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return left

    def findRight(nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] <= target:
                left = mid + 1
            else:
                right = mid - 1
        return right

    left, right = findLeft(nums, target), findRight(nums, target)
    if left <= right and left < len(nums) and nums[left] == target:
        return [left, right]
    return [-1, -1]
```

##### 解释：
- 分别使用 `findLeft` 和 `findRight` 函数来找到目标值的左边界和右边界。
- 根据 `left` 和 `right` 的结果返回目标值的范围。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 3. LeetCode 33: 搜索旋转排序数组 (Search in Rotated Sorted Array)

##### Problem Description  
给定一个已按照升序排列的数组，但在某个未知的点上进行了旋转，请在数组中找到目标值并返回其索引。如果目标值不存在，返回 `-1`。

##### 解法：二分查找  
根据数组的旋转性质，调整左右边界进行二分查找。

##### Python 代码：

```python
def search(nums, target):
    left, right = 0, len(nums) - 1  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        if nums[left] <= nums[mid]:  # 判断左半部分是否有序
            if nums[left] <= target < nums[mid]:  # 目标值在左半部分
                right = mid - 1
            else:
                left = mid + 1
        else:  # 否则右半部分有序
            if nums[mid] < target <= nums[right]:  # 目标值在右半部分
                left = mid + 1
            else:
                right = mid - 1
    return -1
```

##### 解释：
- 判断数组的左半部分或右半部分是否有序，根据有序性调整左右边界。
- 当找到目标值时，返回其索引。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 4. LeetCode 81: 搜索旋转排序数组 II (Search in Rotated Sorted Array II)

##### Problem Description  
与题目 33 类似，但数组中可能包含重复元素。

##### 解法：二分查找  
由于可能存在重复元素，需要在处理时跳过重复元素。

##### Python 代码：

```python
def search(nums, target):
    left, right = 0, len(nums) - 1  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return True
        if nums[left] == nums[mid] == nums[right]:  # 处理重复元素
            left += 1
            right -= 1
        elif nums[left] <= nums[mid]:  # 左半部分有序
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # 右半部分有序
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    return False
```

##### 解释：
- 处理旋转数组中的重复元素，通过跳过相等的左右边界。
- 与题目 33 的方法类似，但在遇到重复元素时需要额外处理。

##### 时间复杂度：O(log n)（最坏情况 O(n)）  
##### 空间复杂度：O(1)

---

#### 5. LeetCode 69: x 的平方根 (Sqrt(x))

##### Problem Description  
给定一个非负整数 `x`，计算并返回 `x` 的平方根的整数部分。

##### 解法：二分查找  
通过二分查找在 `[0, x]` 的范围内找到平方小于或等于 `x` 的最大整数。

##### Python 代码：

```python
def mySqrt(x):
    if x < 2:
        return x
    left, right = 2

, x // 2  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        num = mid * mid
        if num == x:
            return mid
        elif num < x:  # 如果平方小于 x，向右查找
            left = mid + 1
        else:  # 如果平方大于 x，向左查找
            right = mid - 1
    return right  # 返回最大的整数平方小于等于 x
```

##### 解释：
- 使用二分查找寻找平方小于等于 `x` 的最大整数。
- 在每次比较时，根据 `mid * mid` 与 `x` 的比较结果调整边界。

##### 时间复杂度：O(log x)  
##### 空间复杂度：O(1)

---

#### 6. LeetCode 744: 寻找比目标字母大的最小字母 (Find Smallest Letter Greater Than Target)

##### Problem Description  
给定一个排序好的字符列表，找出列表中比目标字母大的最小字母。如果不存在比目标字母大的字母，则返回列表的第一个字母。

##### 解法：二分查找  
通过二分查找找到第一个比目标字母大的字母。

##### Python 代码：

```python
def nextGreatestLetter(letters, target):
    left, right = 0, len(letters) - 1  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        if letters[mid] <= target:  # 如果当前字母小于等于目标字母，向右查找
            left = mid + 1
        else:  # 否则向左查找
            right = mid - 1
    return letters[left % len(letters)]  # 如果越界，返回第一个字母
```

##### 解释：
- 二分查找找到第一个大于目标字母的位置，返回该位置的字母。
- 如果越界则返回列表的第一个字母。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 7. LeetCode 374: 猜数字大小 (Guess Number Higher or Lower)

##### Problem Description  
猜一个数字并返回其大小。数字范围在 `[1, n]` 之间，每次猜测后会告诉你答案是大了、小了还是猜对了。

##### 解法：二分查找  
通过二分查找逐步缩小猜测范围，直到找到目标数字。

##### Python 代码：

```python
def guessNumber(n):
    left, right = 1, n  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        res = guess(mid)  # 通过 guess 函数判断猜测结果
        if res == 0:  # 猜对了
            return mid
        elif res < 0:  # 猜大了，向左查找
            right = mid - 1
        else:  # 猜小了，向右查找
            left = mid + 1
```

##### 解释：
- 使用二分查找逐步缩小猜测范围，直到找到目标数字。
- `guess(mid)` 函数会告诉我们当前猜测是大了、小了还是猜对了。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 8. LeetCode 852: 山脉数组的峰顶索引 (Peak Index in a Mountain Array)

##### Problem Description  
给定一个山脉数组，找到其中的峰顶元素，并返回其索引。

##### 解法：二分查找  
通过二分查找，找到数组中第一个满足 `arr[mid] > arr[mid + 1]` 的位置，即为峰顶。

##### Python 代码：

```python
def peakIndexInMountainArray(arr):
    left, right = 0, len(arr) - 1  # 初始化左右边界
    while left < right:
        mid = (left + right) // 2
        if arr[mid] > arr[mid + 1]:  # 如果当前元素大于下一个元素，峰顶在左边
            right = mid
        else:  # 峰顶在右边
            left = mid + 1
    return left  # 返回峰顶的索引
```

##### 解释：
- 使用二分查找找到峰顶元素，即找到满足 `arr[mid] > arr[mid + 1]` 的位置。
- 根据比较结果调整搜索范围，最后返回峰顶索引。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 9. LeetCode 35: 搜索插入位置 (Search Insert Position)

##### Problem Description  
给定一个排序数组和一个目标值，返回目标值插入位置的索引。如果目标值已经存在，则返回其索引。

##### 解法：二分查找  
通过二分查找找到目标值，或返回插入位置。

##### Python 代码：

```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1  # 初始化左右边界
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:  # 目标值在右边
            left = mid + 1
        else:  # 目标值在左边
            right = mid - 1
    return left  # 返回插入位置
```

##### 解释：
- 使用二分查找，找到目标值的位置。
- 如果目标值不存在，则返回适合插入的位置。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

#### 10. LeetCode 278: 第一个错误的版本 (First Bad Version)

##### Problem Description  
给定一个产品，其中某个版本开始出错，找到第一个错误的版本。

##### 解法：二分查找  
通过二分查找找到第一个错误的版本。

##### Python 代码：

```python
def firstBadVersion(n):
    left, right = 1, n  # 初始化左右边界
    while left < right:
        mid = (left + right) // 2
        if isBadVersion(mid):  # 如果是错误版本
            right = mid  # 向左查找
        else:
            left = mid + 1  # 向右查找
    return left  # 返回第一个错误版本
```

##### 解释：
- 使用二分查找逐步缩小范围，找到第一个错误的版本。
- 每次通过 `isBadVersion(mid)` 判断当前版本是否错误，并调整边界。

##### 时间复杂度：O(log n)  
##### 空间复杂度：O(1)

---

### Conclusion  
二分查找是一种非常高效的搜索算法，特别适用于有序数组或问题。通过不断地将搜索范围缩小一半，可以在对数时间内找到目标元素或插入位置。掌握二分查找能够显著提高算法效率，尤其是在处理大量数据时。
