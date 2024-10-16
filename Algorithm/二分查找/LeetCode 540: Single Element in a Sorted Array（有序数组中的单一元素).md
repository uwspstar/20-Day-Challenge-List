### LeetCode 540: Single Element in a Sorted Array（有序数组中的单一元素）

https://leetcode.com/problems/single-element-in-a-sorted-array/description/

**题目描述**：
给定一个只包含整数的有序数组，其中每个元素都会出现两次，只有一个元素只会出现一次。请你找出并返回这个单一的元素。

你必须设计一个时间复杂度为 O(log n) 的算法来解决这个问题。

**代码实现**：
```python
class Solution:
    def singleNonDuplicate(self, nums: List[int]) -> int:
        # 初始化左右指针
        left, right = 0, len(nums) - 1
        
        # 二分查找
        while left < right:
            mid = (left + right) // 2
            # 确保 mid 为偶数
            if mid % 2 == 1:
                mid -= 1
            
            # 检查 mid 和 mid + 1 是否成对
            if nums[mid] == nums[mid + 1]:
                # 如果成对，说明单一元素在右侧
                left = mid + 2
            else:
                # 如果不成对，说明单一元素在左侧或是 mid
                right = mid
        
        # 当 left == right 时，即找到单一元素
        return nums[left]

# 时间复杂度：O(log n) - 二分查找的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
我们要求用 O(log n) 的时间复杂度找到有序数组中的单一元素。由于数组是有序的，并且每个元素都成对出现，我们可以利用二分查找来缩小查找范围，最终找到那个只出现一次的元素。

**解决方案详解**：

- **初始化条件**：
  - 左边界 `left` 初始化为 0，右边界 `right` 初始化为数组的最后一个索引 `len(nums) - 1`，用于二分查找整个数组。
  
- **二分查找的过程**：
  - 每次计算中间索引 `mid`，为了确保我们每次都能正确地找到成对的元素，我们将 `mid` 向下取偶数（`mid -= 1` 如果 `mid` 是奇数）。
  - 然后检查 `nums[mid]` 是否等于 `nums[mid + 1]`：
    - 如果它们成对出现，说明单一元素在右侧，因此移动左边界 `left = mid + 2`。
    - 如果它们不成对，说明单一元素在左侧或是 `mid` 本身，因此移动右边界 `right = mid`。
  
- **结束条件**：
  - 当 `left == right` 时，左右指针相遇，说明此时 `left` 指向的就是那个只出现一次的单一元素。

**复杂度分析**：
- **时间复杂度**：O(log n)，我们使用二分查找，每次将查找范围缩小一半，因此时间复杂度为 O(log n)。
- **空间复杂度**：O(1)，只使用了常量空间来存储指针和中间变量。

**示例讲解**：

#### 示例 1:
```
输入: nums = [1,1,2,3,3,4,4,8,8]
输出: 2
```
- 初始状态：`left = 0`, `right = 8`，`mid = (0 + 8) // 2 = 4`，检查 `nums[4] == nums[5]`，因为 `nums[4] = 4`，`nums[5] = 4`，移动左指针 `left = 6`。
- 第二次迭代：`mid = (6 + 8) // 2 = 6`，检查 `nums[6] == nums[7]`，因为 `nums[6] = 8`，`nums[7] = 8`，移动左指针 `left = 8`。
- 此时 `left == right`，返回 `nums[8] = 2`。

#### 示例 2:
```
输入: nums = [3,3,7,7,10,11,11]
输出: 10
```
- 初始状态：`left = 0`, `right = 6`，`mid = (0 + 6) // 2 = 3`，检查 `nums[2] == nums[3]`，因为 `nums[2] = 7`，`nums[3] = 7`，移动左指针 `left = 4`。
- 第二次迭代：`mid = (4 + 6) // 2 = 5`，检查 `nums[4] == nums[5]`，因为 `nums[4] = 10`，`nums[5] = 11`，移动右指针 `right = 4`。
- 此时 `left == right`，返回 `nums[4] = 10`。

**总结**：
利用二分查找的特性，通过缩小查找范围，能够在 O(log n) 时间内找到有序数组中的单一元素。
