### LeetCode 34: 在排序数组中查找元素的第一个和最后一个位置 (Find First and Last Position of Element in Sorted Array)

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
  
---

## 问题

给定一个按照非递减顺序排列的整数数组 `nums` 和一个目标值 `target`，请你找出目标值在数组中的**第一个**和**最后一个**位置。

如果数组中不存在目标值，返回 `[-1, -1]`。

你必须设计并实现时间复杂度为 `O(log n)` 的算法。

### 示例 1:

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

### 示例 2:

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1, -1]
```

### 示例 3:

```
输入: nums = [], target = 0
输出: [-1, -1]
```

---

## 解题思路

这道题要求我们找到目标值的第一个和最后一个出现的位置，并且时间复杂度必须是 `O(log n)`。这是一个典型的**二分查找**问题。

我们可以通过两次二分查找来分别找到目标值的第一个位置和最后一个位置：

1. **找第一个位置**：
   - 当 `nums[mid] == target` 时，我们将 `right` 移动到 `mid - 1`，以继续在左边寻找第一个出现的位置。

2. **找最后一个位置**：
   - 当 `nums[mid] == target` 时，我们将 `left` 移动到 `mid + 1`，以继续在右边寻找最后一个出现的位置。

---

### 代码实现：

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]: 
        # 查找目标值第一次出现的位置
        def find_first(nums, target):
            l, r = 0, len(nums) - 1 
            idx = -1
            while l <= r: 
                mid = (l + r) // 2
                if nums[mid] >= target:  # 继续向左寻找
                    r = mid - 1
                    if nums[mid] == target:
                        idx = mid  # 更新idx，可能是第一次出现的位置
                else:
                    l = mid + 1
            return idx
        
        # 查找目标值最后一次出现的位置
        def find_last(nums, target):
            l, r = 0, len(nums) - 1 
            idx = -1
            while l <= r: 
                mid = (l + r) // 2
                if nums[mid] <= target:  # 继续向右寻找
                    l = mid + 1
                    if nums[mid] == target:
                        idx = mid  # 更新idx，可能是最后一次出现的位置
                else:
                    r = mid - 1
            return idx
        
        first = find_first(nums, target)

        if first == -1:  # 如果没有找到目标值
            return [-1, -1]

        last = find_last(nums, target)

        return [first, last]
```

---

### 代码解释：

1. **找第一个出现的位置** (`find_first`)：
   - 使用二分查找，如果 `nums[mid] >= target`，则说明目标值可能在 `mid` 左侧，因此将 `right` 移到 `mid - 1`。
   - 如果 `nums[mid] == target`，记录当前 `mid` 为可能的第一个位置，同时继续向左寻找，直到无法再缩小范围。

2. **找最后一个出现的位置** (`find_last`)：
   - 同样使用二分查找，但这次如果 `nums[mid] <= target`，则将 `left` 移到 `mid + 1`，继续向右寻找目标值的最后一个出现位置。
   - 每当找到目标值时，记录当前的 `mid` 为最后一个可能的位置。

3. **组合结果**：
   - 首先调用 `find_first` 查找第一个出现的位置，如果返回 `-1` 说明没有找到目标值，直接返回 `[-1, -1]`。
   - 然后调用 `find_last` 查找最后一个出现的位置，并返回 `[first, last]`。

---

### 复杂度分析：

- **时间复杂度**：O(log n)，因为我们对数组进行了两次二分查找，每次的时间复杂度都是 O(log n)。
  
- **空间复杂度**：O(1)，我们只使用了常量级别的额外空间来存储指针和结果。

---

### 示例讲解：

#### 示例 1:

```
输入: nums = [5,7,7,8,8,10], target = 8
```

- 第一次二分查找 `find_first`：
  - 第一次 `mid = 2`，`nums[2] = 7`，小于目标值，移动 `left` 到 `3`。
  - 第二次 `mid = 4`，`nums[4] = 8`，等于目标值，更新 `idx = 4`，继续向左查找，`right = 3`。
  - 第三次 `mid = 3`，`nums[3] = 8`，更新 `idx = 3`，继续向左，`right = 2`，结束查找。
  - 结果为 `first = 3`。

- 第二次二分查找 `find_last`：
  - 第一次 `mid = 2`，`nums[2] = 7`，小于目标值，移动 `left` 到 `3`。
  - 第二次 `mid = 4`，`nums[4] = 8`，更新 `idx = 4`，继续向右查找，`left = 5`，结束查找。
  - 结果为 `last = 4`。

最终返回 `[3, 4]`。

#### 示例 2:

```
输入: nums = [5,7,7,8,8,10], target = 6
```

- 第一次二分查找 `find_first`：
  - 找不到目标值，直接返回 `-1`。
  
结果为 `[-1, -1]`。

---

### 总结

- **中文**：这道题通过二分查找的方式，高效地找到了目标值的第一个和最后一个出现的位置。通过分别查找第一个和最后一个位置，我们可以在 O(log n) 的时间复杂度下完成任务。

---

### 关键提示 (Key Tips)：

1. **二分查找的应用**：通过分别查找第一个和最后一个位置，可以高效地找到目标值在数组中的范围。
2. **判断条件**：
   - `find_first`：当 `nums[mid] >= target` 时，将右指针 `right` 移动，确保找到第一个位置。
   - `find_last`：当 `nums[mid] <= target` 时，将左指针 `left` 移动，确保找到最后一个位置。
3. **边界处理**：如果 `first` 为 `-1`，说明目标值不存在，直接返回 `[-1, -1]`。

---

### 推荐相似问题：

1. [LeetCode 704: 二分查找](https://leetcode.com/problems/binary-search/)
2. [LeetCode 153: 寻找旋转排序数组中的最小值](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
3. [LeetCode 162: 寻找峰值](https://leetcode.com/problems/find-peak-element/)
