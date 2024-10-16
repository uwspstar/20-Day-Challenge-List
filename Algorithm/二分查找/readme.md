# 二分查找

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

---

#### 适用于各种场景的二分查找模板

### 代码解析：

```python
def binary_search(arr: List[int], target: int) -> int:  # 定义二分查找函数，输入为数组和目标值
    left, right = 0, len(arr) - 1  # 初始化左右指针
    first_true_index = -1  # 初始化结果变量为 -1，表示未找到
    while left <= right:  # 当左指针小于等于右指针时，继续二分查找
        mid = (left + right) // 2  # 计算中间索引
        if feasible(mid):  # 判断中间索引是否满足条件
            first_true_index = mid  # 如果满足条件，更新结果
            right = mid - 1  # 继续向左半部分搜索，寻找第一个满足条件的值
        else:  # 如果不满足条件
            left = mid + 1  # 继续向右半部分搜索
    return first_true_index  # 返回结果索引
```

---

### 代码解释逐行：

1. **函数定义**：
   - `binary_search` 接受一个整数数组 `arr` 和一个目标值 `target`。
   - 这里我们寻找满足某种条件的元素，模板会根据不同问题的 `feasible` 函数来变化。

2. **初始化左右指针**：
   - 左指针 `left` 从数组开头 `0` 位置开始，右指针 `right` 从数组结尾 `len(arr) - 1` 开始。
   - `first_true_index` 初始化为 -1，表示如果没有找到满足条件的值，将返回 -1。

3. **二分查找核心逻辑**：
   - `mid = (left + right) // 2`：通过取左右指针的中间值来分割数组。
   - `feasible(mid)`：这是关键的一步，用于检查 `mid` 位置是否满足条件。如果满足条件，则更新 `first_true_index` 并继续向左半部分搜索，否则向右半部分搜索。

4. **返回结果**：
   - 最终返回满足条件的第一个位置。如果未找到，返回 `-1`。

---

### `feasible` 函数详解：

- `feasible` 函数是模板的核心部分，它根据问题的不同定义。通常，`feasible` 函数判断 `arr[mid]` 是否满足某个特定条件。以布尔数组为例，`feasible(mid)` 可以是 `arr[mid] == True`。
  
- 其他问题中，`feasible` 函数的定义可能会更复杂。例如：
   1. **寻找第一个大于等于目标值的元素**：`feasible(mid)` 可以定义为 `arr[mid] >= target`。
   2. **寻找符合某个区间条件的元素**：`feasible(mid)` 可以定义为 `min_value <= arr[mid] <= max_value`。

---

### 复杂度分析：

- **时间复杂度**：O(log n)。由于每次循环将搜索范围缩小一半，所以二分查找的时间复杂度是对数级别的。
- **空间复杂度**：O(1)。只需要常量级别的额外空间来存储指针和中间值。

---

### 关键点 & 提示：
- 在二分查找中，`feasible` 函数是决定结果的关键，需要根据不同问题进行适配。
- 通常，`feasible` 函数的设计依赖于判断 `arr[mid]` 是否满足某个条件。

---

### 对比：

| 场景                   | feasible 函数定义           | 时间复杂度    |
| ---------------------- | --------------------------- | ------------- |
| 寻找布尔数组中的第一个 True | `arr[mid] == True`           | O(log n)      |
| 寻找第一个大于等于 target 的值 | `arr[mid] >= target`         | O(log n)      |
| 寻找满足某个区间条件的元素   | `min_value <= arr[mid] <= max_value` | O(log n)      |

---

### 面试问题解答：

#### 1. 如何根据不同场景来定义 `feasible` 函数？

- **问题描述**：
  在不同的二分查找问题中，`feasible` 函数负责判断给定的 `mid` 索引是否满足某个条件。根据问题的不同，`feasible` 函数的定义也需要变化。一般来说，`feasible` 函数的设计需要根据目标问题的条件来判断当前值是否符合查找要求。

- **解答**：
  - **寻找布尔数组中第一个 `True`**：`feasible(mid)` 可以定义为 `arr[mid] == True`。这意味着如果当前值是 `True`，则满足条件，更新边界。
  - **寻找第一个大于等于目标值的元素**：`feasible(mid)` 可以定义为 `arr[mid] >= target`。如果当前值大于或等于目标值，那么它可能是解，也可能要继续查找前面部分。
  - **寻找满足某个区间条件的元素**：`feasible(mid)` 可以定义为 `min_value <= arr[mid] <= max_value`，表示当前元素在一个范围内。

  总的来说，`feasible` 函数是用于检查 `arr[mid]` 是否符合问题给定的条件。关键是找到可以缩小搜索空间的逻辑，让二分查找有明确的停止条件。

---

#### 2. 在一个严格递增的数组中，如何找到第一个大于某个目标值的元素？

- **问题描述**：
  给定一个严格递增的数组，要求找到数组中第一个大于目标值 `target` 的元素，返回其索引。如果不存在这样的元素，返回 -1。

- **解答**：
  在这个问题中，我们可以通过二分查找来解决，并使用以下 `feasible` 函数：

  ```python
  def feasible(mid):
      return arr[mid] > target
  ```

  - **步骤**：
    1. 初始化左右指针 `left = 0, right = len(arr) - 1`。
    2. 进行二分查找，通过 `feasible(mid)` 函数判断 `arr[mid]` 是否大于目标值 `target`。
    3. 如果 `arr[mid] > target`，则更新边界，继续向左侧查找，直到找到第一个大于 `target` 的元素。
    4. 如果不存在满足条件的元素，返回 `-1`。

  - **代码示例**：

  ```python
  def find_first_greater(arr: List[int], target: int) -> int:
      left, right = 0, len(arr) - 1
      result = -1
      while left <= right:
          mid = (left + right) // 2
          if arr[mid] > target:
              result = mid  # 找到符合条件的值，更新结果
              right = mid - 1  # 继续向左查找
          else:
              left = mid + 1  # 继续向右查找
      return result
  ```

---

#### 3. 如何修改二分查找来寻找最后一个满足条件的值？

- **问题描述**：
  二分查找通常用于寻找第一个满足条件的值。如果我们需要找到最后一个满足条件的值，如何修改二分查找的逻辑？

- **解答**：
  要找到最后一个满足条件的值，我们需要在满足条件时，不是向左继续查找，而是向右继续查找。通过这种方式，我们可以确保查找的范围缩小到最后一个满足条件的值。

  - **步骤**：
    1. 初始化左右指针 `left = 0, right = len(arr) - 1`。
    2. 进行二分查找，如果 `feasible(mid)` 返回 `True`，说明当前值满足条件，但为了找到最后一个满足条件的值，需要将左指针向右移动，继续查找右侧。
    3. 直到左指针与右指针相遇，返回找到的最后一个满足条件的值的索引。

  - **代码示例**：

  ```python
  def find_last_feasible(arr: List[int], feasible: Callable[[int], bool]) -> int:
      left, right = 0, len(arr) - 1
      result = -1
      while left <= right:
          mid = (left + right) // 2
          if feasible(mid):
              result = mid  # 记录满足条件的结果
              left = mid + 1  # 继续向右查找，寻找最后一个满足条件的值
          else:
              right = mid - 1  # 向左继续查找
      return result
  ```

  这里，`feasible` 函数决定当前 `mid` 是否满足条件，通过继续向右查找，我们可以找到最后一个符合条件的元素。



---

这段代码展示了一个二分查找的通用模板，其中 `feasible` 函数可以根据具体问题进行调整。这种方法可以应用于多种查找问题，特别是在数组有序的情况下，能大大提高查找效率。

---

好的，以下是30道LeetCode中常见的二分查找相关题目，包括详细解释、逐行中文注释代码以及时间和空间复杂度分析。

---

### [1. LeetCode 704: Binary Search（二分查找）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%20704%3A%20Binary%20Search%EF%BC%88%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE%EF%BC%89.md)

**题目描述**：
给定一个排序数组 `nums` 和一个目标值 `target`，在数组中查找目标值，返回目标值所在的索引位置。如果目标值不存在于数组中，返回 -1。

**代码实现**：
```python
def search(nums: List[int], target: int) -> int:
    # 定义左右指针，left 指向数组起始位置，right 指向数组末尾位置
    left, right = 0, len(nums) - 1
    # 当 left 指针小于等于 right 指针时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值等于目标值，返回该索引
        if nums[mid] == target:
            return mid
        # 如果中间值小于目标值，说明目标值在右半部分，将左指针移动到 mid + 1
        elif nums[mid] < target:
            left = mid + 1
        # 如果中间值大于目标值，说明目标值在左半部分，将右指针移动到 mid - 1
        else:
            right = mid - 1
    # 若未找到目标值，返回 -1
    return -1

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题是经典的二分查找题目，通过逐步缩小搜索范围来寻找目标值，时间复杂度是 O(log n)，适合用于排序数组中查找元素。

---

### [2. LeetCode 33: Search in Rotated Sorted Array（搜索旋转排序数组）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%2033%3A%20%E6%90%9C%E7%B4%A2%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%20(Search%20in%20Rotated%20Sorted%20Array).md)

**题目描述**：
假设按照升序排序的数组在预先未知的某个点上进行了旋转（例如：数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]`），请在其中搜索目标值，返回其索引位置。如果目标值不存在，返回 -1。

**代码实现**：
```python
def search(nums: List[int], target: int) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于等于 right 指针时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值等于目标值，直接返回该索引
        if nums[mid] == target:
            return mid
        # 判断左半部分是否有序
        if nums[left] <= nums[mid]:
            # 如果目标值在左半部分，移动右指针
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # 否则右半部分有序
        else:
            # 如果目标值在右半部分，移动左指针
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    # 若未找到目标值，返回 -1
    return -1

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
旋转排序数组的特点是将某个点的前后部分进行了互换，所以搜索时需要判断哪个半部分是有序的，再决定搜索范围。

---

### 3. LeetCode 81: Search in Rotated Sorted Array II（搜索旋转排序数组 II）

**题目描述**：
这是旋转排序数组的延伸版本，但数组中允许存在重复元素。请在其中搜索目标值，返回目标值是否存在（存在返回 True，不存在返回 False）。

**代码实现**：
```python
def search(nums: List[int], target: int) -> bool:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于等于 right 指针时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值等于目标值，返回 True
        if nums[mid] == target:
            return True
        # 处理重复元素
        if nums[left] == nums[mid] == nums[right]:
            left += 1
            right -= 1
        # 判断左半部分是否有序
        elif nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # 否则右半部分有序
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    # 若未找到目标值，返回 False
    return False

# 时间复杂度：O(log n) - 平均情况下，每次查找将搜索范围缩小一半（最坏情况为 O(n)）
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
在处理旋转排序数组时，若数组中存在重复元素，需要先去除两边的重复元素，避免因重复元素造成的干扰。

---

### [4. LeetCode 153: Find Minimum in Rotated Sorted Array（寻找旋转排序数组中的最小值）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%20153%3A%20Find%20Minimum%20in%20Rotated%20Sorted%20Array%EF%BC%88%E5%AF%BB%E6%89%BE%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9C%80%E5%B0%8F%E5%80%BC).md)

**题目描述**：
假设按照升序排序的数组在预先未知的某个点上进行了旋转，请找出其中最小的元素。

**代码实现**：
```python
def findMin(nums: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于 right 指针时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值大于右边界值，说明最小值在右半部分
        if nums[mid] > nums[right]:
            left = mid + 1
        # 否则最小值在左半部分或为当前 mid
        else:
            right = mid
    # 返回最小值
    return nums[left]

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
旋转排序数组的最小值一定在无序的一半中，通过判断中间值与右边界值的关系可以有效缩小搜索范围。

---

### 5. LeetCode 154: Find Minimum in Rotated Sorted Array II（寻找旋转排序数组中的最小值 II）

**题目描述**：
这是旋转排序数组的延伸版本，但数组中允许存在重复元素。请找出其中最小的元素。

**代码实现**：
```python
def findMin(nums: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于 right 指针时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值大于右边界值，说明最小值在右半部分
        if nums[mid] > nums[right]:
            left = mid + 1
        # 如果中间值小于右边界值，最小值在左半部分
        elif nums[mid] < nums[right]:
            right = mid
        # 如果中间值等于右边界值，无法判断最小值在哪个半部分，缩小搜索范围
        else:
            right -= 1
    # 返回最小值
    return nums[left]

# 时间复杂度：O(log n) - 平均情况下，每次查找将搜索范围缩小一半（最坏情况为 O(n)）
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
当旋转排序数组中存在重复元素时，需特别注意元素相等的情况，在这种情况下通过缩小右边界来去除重复元素。

---

好的，我们先继续介绍接下来的五道二分查找相关题目。每个题目将包含详细的题目描述、中文注释代码以及时间复杂度和空间复杂度分析。

---

### 6. LeetCode 162: Find Peak Element（寻找峰值）

**题目描述**：
给定一个数组 `nums`，其中 `nums[i] != nums[i+1]`，找到一个峰值元素并返回其索引。数组可能包含多个峰值元素，你可以返回任意一个峰值元素的索引。

**代码实现**：
```python
def findPeakElement(nums: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于 right 指针时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值比下一个值小，说明峰值在右半部分
        if nums[mid] < nums[mid + 1]:
            left = mid + 1
        # 否则峰值在左半部分（包括当前 mid）
        else:
            right = mid
    # 返回峰值元素的索引
    return left

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
峰值元素是指比相邻元素都大的元素。由于相邻元素不相等，所以峰值元素必定存在，可以通过二分查找逐步缩小搜索范围。

---

### [7. LeetCode 34: Find First and Last Position of Element in Sorted Array（在排序数组中查找元素的第一个和最后一个位置）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%2034:%20%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE%20(Find%20First%20and%20Last%20Position%20of%20Element%20in%20Sorted%20Array).md)

**题目描述**：
给定一个按照升序排列的整数数组 `nums` 和一个目标值 `target`，找出目标值在数组中出现的第一个和最后一个位置。如果目标值不存在于数组中，返回 `[-1, -1]`。

**代码实现**：
```python
def searchRange(nums: List[int], target: int) -> List[int]:
    # 定义一个辅助函数，用来找到目标值的边界索引
    def findBoundary(nums, target, findFirst):
        # 定义左右指针
        left, right = 0, len(nums) - 1
        # 初始化结果索引为 -1
        boundaryIndex = -1
        # 当 left 指针小于等于 right 指针时继续循环
        while left <= right:
            # 计算中间位置索引
            mid = (left + right) // 2
            # 如果中间值等于目标值，更新边界索引
            if nums[mid] == target:
                boundaryIndex = mid
                # 查找第一个位置时，将右指针左移
                if findFirst:
                    right = mid - 1
                # 查找最后一个位置时，将左指针右移
                else:
                    left = mid + 1
            # 如果中间值小于目标值，移动左指针
            elif nums[mid] < target:
                left = mid + 1
            # 如果中间值大于目标值，移动右指针
            else:
                right = mid - 1
        # 返回边界索引
        return boundaryIndex

    # 查找目标值的第一个位置和最后一个位置
    firstPosition = findBoundary(nums, target, True)
    lastPosition = findBoundary(nums, target, False)
    # 返回结果
    return [firstPosition, lastPosition]

# 时间复杂度：O(log n) - 使用二分查找法分别查找目标值的第一个和最后一个位置
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
这道题的关键是用二分查找找到目标值的边界位置。通过分别查找第一个和最后一个出现位置，可以有效地减少时间复杂度。

---

### 8. LeetCode 374: Guess Number Higher or Lower（猜数字大小）

**题目描述**：
猜数字游戏的规则如下：我从 1 到 n 选择一个数字。你需要猜我选择的数字。每次你猜错时，我会告诉你这个数字是大了还是小了。使用二分查找来优化你的猜测次数。

**代码实现**：
```python
def guessNumber(n: int) -> int:
    # 定义左右指针
    left, right = 1, n
    # 当 left 指针小于等于 right 指针时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 调用 guess() 函数判断结果（假设此函数已定义）
        result = guess(mid)
        # 如果猜测正确，返回该数字
        if result == 0:
            return mid
        # 如果猜测小了，将左指针右移
        elif result == -1:
            right = mid - 1
        # 如果猜测大了，将右指针左移
        else:
            left = mid + 1

# 时间复杂度：O(log n) - 每次猜测将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
在猜数字问题中，使用二分查找法可以有效地减少猜测次数，从而达到 O(log n) 的时间复杂度。

---

### 9. LeetCode 658: Find K Closest Elements（找到 K 个最接近的元素）

**题目描述**：
给定一个排序数组 `arr` 和两个整数 `k` 和 `x`，请从数组中找到 `k` 个最接近 `x` 的元素。返回这 `k` 个元素并按升序排序。

**代码实现**：
```python
def findClosestElements(arr: List[int], k: int, x: int) -> List[int]:
    # 定义左右指针
    left, right = 0, len(arr) - k
    # 当 left 指针小于 right 指针时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 比较 x 与 arr[mid] 和 arr[mid+k] 的差距
        if x - arr[mid] > arr[mid + k] - x:
            # 说明最接近 x 的 k 个元素在右半部分
            left = mid + 1
        else:
            # 说明最接近 x 的 k 个元素在左半部分
            right = mid
    # 返回从 left 开始的 k 个元素
    return arr[left:left + k]

# 时间复杂度：O(log(n-k)) - 二分查找来确定起始位置
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题通过二分查找法找到最接近目标值的起始索引，再返回连续的 k 个元素。该方法有效地减少了时间复杂度。

---

### 10. LeetCode 658: Find Peak Element II（寻找峰值 II）

**题目描述**：
该题是寻找二维数组中的峰值。峰值元素是指大于四个方向的相邻元素。找到其中一个峰值元素并返回其索引。

**代码实现**：
```python
def findPeakGrid(mat: List[List[int]]) -> List[int]:
    # 定义左右指针
    left, right = 0, len(mat[0]) - 1
    # 当 left 指针小于等于 right 指针时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 寻找当前列中最大值的索引
        max_row = max(range(len(mat)), key=lambda i: mat[i][mid])
        # 判断是否为峰值
        if (mid == 0 or mat[max_row][mid] > mat[max_row][mid - 1]) and (mid == len(mat[0]) - 1 or mat[max_row][mid] > mat[max_row][mid + 1]):
            return [max_row, mid]
        # 如果中间值小于左边值，说明峰值在左半部分
        elif mid > 0 and mat[max_row][mid] < mat[max_row][mid - 1]:
            right = mid - 1
        # 否则峰值在右半部分
        else:
            left = mid + 1

# 时间复杂度：O(log n) - 每次查找将列数减半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
在二维数组中寻找峰值的关键在于通过列的二分查找来逐

步缩小范围，找到满足条件的峰值。

---

好的，我们继续讲解接下来的五道二分查找相关题目，每个题目将包含详细的题目描述、中文注释代码以及时间复杂度和空间复杂度分析。

---

### 11. LeetCode 300: Longest Increasing Subsequence（最长递增子序列）

**题目描述**：
给定一个无序的整数数组 `nums`，找到其中最长递增子序列的长度。

**代码实现**：
```python
def lengthOfLIS(nums: List[int]) -> int:
    # 定义一个数组 dp 来保存以每个元素结尾的最长递增子序列长度
    dp = []
    # 遍历每个元素
    for num in nums:
        # 使用二分查找找到当前元素在 dp 中的插入位置（如果存在相等值则替换）
        left, right = 0, len(dp)
        while left < right:
            mid = (left + right) // 2
            if dp[mid] < num:
                left = mid + 1
            else:
                right = mid
        # 如果 left 等于 dp 的长度，说明当前元素比 dp 中所有元素都大，追加到 dp
        if left >= len(dp):
            dp.append(num)
        else:
            # 否则用当前元素替换 dp 中比它大的最小元素
            dp[left] = num
    # dp 的长度即为最长递增子序列的长度
    return len(dp)

# 时间复杂度：O(n log n) - 遍历每个元素时，使用二分查找法确定其插入位置
# 空间复杂度：O(n) - 使用了一个 dp 数组来保存递增子序列
```

**题目分析**：
该题利用了二分查找来优化动态规划的解法，通过在递增序列中使用二分查找找到插入位置，可以将时间复杂度降低到 O(n log n)。

---

### 12. LeetCode 74: Search a 2D Matrix（搜索二维矩阵）

**题目描述**：
编写一个高效的算法来判断 `m x n` 矩阵中，是否存在一个目标值 `target`。该矩阵具有以下特性：
- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。

**代码实现**：
```python
def searchMatrix(matrix: List[List[int]], target: int) -> bool:
    # 矩阵为空时返回 False
    if not matrix or not matrix[0]:
        return False
    # 获取矩阵的行数和列数
    rows, cols = len(matrix), len(matrix[0])
    # 定义左指针为 0，右指针为矩阵元素总数减一
    left, right = 0, rows * cols - 1
    # 当 left 小于等于 right 时继续循环
    while left <= right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 将一维索引转换为二维索引
        mid_value = matrix[mid // cols][mid % cols]
        # 如果中间值等于目标值，返回 True
        if mid_value == target:
            return True
        # 如果中间值小于目标值，移动左指针
        elif mid_value < target:
            left = mid + 1
        # 如果中间值大于目标值，移动右指针
        else:
            right = mid - 1
    # 若未找到目标值，返回 False
    return False

# 时间复杂度：O(log(m * n)) - 相当于对一维数组进行二分查找
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
二维矩阵的二分查找可以将矩阵看作是一个一维数组，利用二分查找逐步缩小搜索范围，提升查找效率。

---

### 13. LeetCode 240: Search a 2D Matrix II（搜索二维矩阵 II）

**题目描述**：
编写一个高效的算法来搜索 `m x n` 矩阵 `matrix` 中的目标值 `target`。该矩阵具有以下特性：
- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

**代码实现**：
```python
def searchMatrix(matrix: List[List[int]], target: int) -> bool:
    # 矩阵为空时返回 False
    if not matrix or not matrix[0]:
        return False
    # 获取矩阵的行数和列数
    rows, cols = len(matrix), len(matrix[0])
    # 定义起始点在矩阵的右上角
    row, col = 0, cols - 1
    # 当 row 小于行数且 col 大于等于 0 时继续循环
    while row < rows and col >= 0:
        # 如果当前值等于目标值，返回 True
        if matrix[row][col] == target:
            return True
        # 如果当前值小于目标值，移动到下一行
        elif matrix[row][col] < target:
            row += 1
        # 如果当前值大于目标值，移动到上一列
        else:
            col -= 1
    # 若未找到目标值，返回 False
    return False

# 时间复杂度：O(m + n) - 每次移动都会排除一行或一列的元素
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题通过从右上角开始搜索，可以在每次比较中排除一整行或一整列的元素，从而有效地减少查找次数。

---

### [14. LeetCode 852: Peak Index in a Mountain Array（山脉数组的峰顶索引）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%20852%3A%20Peak%20Index%20in%20a%20Mountain%20Array%EF%BC%88%E5%B1%B1%E8%84%89%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E5%B3%B0%E5%80%BC%E7%B4%A2%E5%BC%95%EF%BC%89.md)

**题目描述**：
符合山脉数组定义的数组 `arr` 中，找出峰顶元素的索引。

**代码实现**：
```python
def peakIndexInMountainArray(arr: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(arr) - 1
    # 当 left 小于 right 时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值小于右边值，说明峰值在右半部分
        if arr[mid] < arr[mid + 1]:
            left = mid + 1
        # 否则峰值在左半部分
        else:
            right = mid
    # 返回峰值元素的索引
    return left

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
山脉数组的峰值元素是指数组中的最大值，利用二分查找法逐步缩小范围，可以高效地找到峰值元素。

---

### 15. LeetCode 374: Guess Number Higher or Lower II（猜数字大小 II）

**题目描述**：
给定一个整数 `n`，你需要找到从 `1` 到 `n` 的所有猜测中所需的最小猜测次数，使用动态规划和二分查找优化。

**代码实现**：
```python
def getMoneyAmount(n: int) -> int:
    # 定义一个二维 dp 数组
    dp = [[0] * (n + 1) for _ in range(n + 1)]
    # 遍历所有区间长度
    for length in range(2, n + 1):
        # 遍历所有起始位置
        for start in range(1, n - length + 2):
            end = start + length - 1
            dp[start][end] = float('inf')
            # 在区间 [start, end] 内猜测每个数字
            for k in range(start, end):
                # 计算最大代价
                cost = k + max(dp[start][k - 1], dp[k + 1][end])
                # 更新最小代价
                dp[start][end] = min(dp[start][end], cost)
    # 返回从 1 到 n 的最小猜测次数
    return dp[1][n]

# 时间复杂度：O(n^3) - 三重循环遍历所有区间
# 空间复杂度：O(n^2) - 使用了一个二维 dp 数组来保存每个区间的最小代价
```

**题目分析**：
该题通过动态规划和二分查找结合，优化了猜数字游戏的最小代价计算。需要遍历所有可能的区间长度，并在每个区间内进行最优选择。

---

好的，我们继续完成剩余的二分查找相关题目。以下是接下来的15道二分查找题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 16. LeetCode 275: H-Index II

**题目描述**：
给定一个排序的数组 `citations`，其中 `citations[i]` 表示某个研究者的第 `i` 篇论文的引用次数（按照引用次数从小到大排序）。计算并返回该研究者的 H-指数。

H-指数的定义是：某人的 H-指数是指其发表的 `N` 篇论文中有 `h` 篇至少被引用 `h` 次，其余 `N-h` 篇论文每篇被引用次数不超过 `h` 次。

**代码实现**：
```python
def hIndex(citations: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(citations) - 1
    # 记录论文数量
    n = len(citations)
    # 当左指针小于等于右指针时继续循环
    while left <= right:
        # 计算中间位置
        mid = (left + right) // 2
        # 如果满足 H 指数条件（即剩余论文数量大于等于引用次数）
        if citations[mid] >= n - mid:
            right = mid - 1
        else:
            left = mid + 1
    # 返回 H 指数
    return n - left

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
H-指数是衡量学术影响力的标准之一，利用二分查找法可以有效地判断某个引用次数是否满足 H-指数的条件，从而快速找到符合条件的 H-指数值。

---

### 17. LeetCode 658: Find K Closest Elements（找到 K 个最接近的元素）

**题目描述**：
给定一个排序数组 `arr` 和两个整数 `k` 和 `x`，从数组中找到 `k` 个最接近 `x` 的元素。返回这 `k` 个元素并按升序排序。

**代码实现**：
```python
def findClosestElements(arr: List[int], k: int, x: int) -> List[int]:
    # 定义左右指针
    left, right = 0, len(arr) - k
    # 当 left 小于 right 时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 比较目标值 x 与 arr[mid] 和 arr[mid+k] 的距离
        if x - arr[mid] > arr[mid + k] - x:
            left = mid + 1
        else:
            right = mid
    # 返回从 left 开始的 k 个最接近元素
    return arr[left:left + k]

# 时间复杂度：O(log(n-k)) - 二分查找起始位置
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
通过二分查找找到与 `x` 最接近的起始位置，然后返回从起始位置开始的 `k` 个元素，从而确保输出是连续的最接近目标值的子数组。

---

### 18. LeetCode 410: Split Array Largest Sum（分割数组的最大值）

**题目描述**：
给定一个非负整数数组 `nums` 和一个整数 `m`，将该数组分成 `m` 个非空的连续子数组。设计一个算法使得这 `m` 个子数组中和的最大值最小。

**代码实现**：
```python
def splitArray(nums: List[int], m: int) -> int:
    # 定义初始左右边界，左边界为数组最大值，右边界为数组总和
    left, right = max(nums), sum(nums)
    # 当 left 小于 right 时继续循环
    while left < right:
        # 计算中间值
        mid = (left + right) // 2
        # 记录当前子数组的个数和当前子数组的和
        count, curr_sum = 1, 0
        for num in nums:
            # 如果当前子数组和加上 num 大于 mid，则划分一个新子数组
            if curr_sum + num > mid:
                count += 1
                curr_sum = num
            else:
                curr_sum += num
        # 如果子数组个数超过 m 个，说明 mid 值太小
        if count > m:
            left = mid + 1
        # 否则 mid 值满足要求
        else:
            right = mid
    # 返回分割后的最大子数组和
    return left

# 时间复杂度：O(n log(sum(nums) - max(nums))) - 二分查找法寻找最优解
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题通过二分查找来找到分割数组的最优解，时间复杂度较低，适合处理较大的数组数据。

---

### 19. LeetCode 33: Search in Rotated Sorted Array（搜索旋转排序数组）

**题目描述**：
假设按照升序排列的数组在预先未知的某个点上进行了旋转（例如：数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]`）。请在其中搜索目标值，返回其索引。如果目标值不存在，返回 -1。

**代码实现**：
```python
def search(nums: List[int], target: int) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 小于等于 right 时继续循环
    while left <= right:
        # 计算中间位置
        mid = (left + right) // 2
        # 如果中间值等于目标值，直接返回该索引
        if nums[mid] == target:
            return mid
        # 判断左半部分是否有序
        if nums[left] <= nums[mid]:
            # 如果目标值在左半部分，移动右指针
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            # 否则目标值在右半部分
            else:
                left = mid + 1
        # 判断右半部分是否有序
        else:
            # 如果目标值在右半部分，移动左指针
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            # 否则目标值在左半部分
            else:
                right = mid - 1
    # 若未找到目标值，返回 -1
    return -1

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
旋转排序数组的特点是将某个点的前后部分进行了互换，所以搜索时需要判断哪个半部分是有序的，再决定搜索范围。

---

### 20. LeetCode 378: Kth Smallest Element in a Sorted Matrix（有序矩阵中第 K 小的元素）

**题目描述**：
给定一个 `n x n` 矩阵 `matrix`，其中每行和每列元素均按升序排列，请找到矩阵中第 `k` 小的元素。

**代码实现**：
```python
def kthSmallest(matrix: List[List[int]], k: int) -> int:
    # 定义初始的左边界和右边界
    left, right = matrix[0][0], matrix[-1][-1]
    # 当 left 小于 right 时继续循环
    while left < right:
        # 计算中间值
        mid = (left + right) // 2
        # 统计矩阵中小于等于 mid 的元素个数
        count = sum(bisect.bisect_right(row, mid) for row in matrix)
        # 如果元素个数小于 k，则说明第 k 小元素在右半部分
        if count < k:
            left = mid + 1
        # 否则在左半部分
        else:
            right = mid
    # 返回第 k 小元素
    return left

# 时间复杂度：O(n log(max-min)) - 二分查找法寻找第 k 小元素
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
利用二分查找法确定目标元素的范围，通过统计小于等于中间值的元素个数来判断第 k 小元素的位置。



---

好的，我们继续完成剩余的10道二分查找题目。以下是每道题目的详细解析，包括题目描述、中文注释代码及时间和空间复杂度分析。

---

### 21. LeetCode 744: Find Smallest Letter Greater Than Target（寻找比目标字母大的最小字母）

**题目描述**：
给定一个排序后的字符数组 `letters` 和一个目标字母 `target`，返回数组中比目标字母大的最小字母。如果不存在比目标字母大的字母，则返回数组的第一个字母。

**代码实现**：
```python
def nextGreatestLetter(letters: List[str], target: str) -> str:
    # 定义左右指针
    left, right = 0, len(letters) - 1
    # 当左指针小于等于右指针时继续循环
    while left <= right:
        # 计算中间位置
        mid = (left + right) // 2
        # 如果中间值小于等于目标值，说明目标值比当前中间值大
        if letters[mid] <= target:
            left = mid + 1
        # 如果中间值大于目标值，则移动右指针
        else:
            right = mid - 1
    # 返回左指针位置的字母（取模处理越界情况）
    return letters[left % len(letters)]

# 时间复杂度：O(log n) - 二分查找法搜索比目标值大的最小字母
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题通过二分查找法快速找到比目标字母大的最小字母。如果目标字母比所有字母都大，则返回数组的第一个字母。

---

### 22. LeetCode 1351: Count Negative Numbers in a Sorted Matrix（统计有序矩阵中的负数）

**题目描述**：
给定一个 `m x n` 的矩阵 `grid`，其中每一行的元素按升序排列，每一列的元素也按升序排列。统计并返回矩阵中所有负数的数量。

**代码实现**：
```python
def countNegatives(grid: List[List[int]]) -> int:
    # 初始化计数器
    count = 0
    # 遍历每一行
    for row in grid:
        # 使用二分查找找到负数的起始位置
        left, right = 0, len(row) - 1
        while left <= right:
            mid = (left + right) // 2
            # 如果中间值小于 0，说明负数在左半部分
            if row[mid] < 0:
                right = mid - 1
            # 如果中间值大于等于 0，说明负数在右半部分
            else:
                left = mid + 1
        # left 指针指向第一个负数的位置，累加负数数量
        count += len(row) - left
    # 返回负数总数
    return count

# 时间复杂度：O(m log n) - 每行使用二分查找法查找负数起始位置
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
在每一行中使用二分查找法找到第一个负数的位置，然后累加所有行的负数数量。该方法比直接遍历更高效。

---

### 23. LeetCode 1011: Capacity To Ship Packages Within D Days（在 D 天内送达包裹的能力）

**题目描述**：
给定一个整数数组 `weights`，表示每个包裹的重量，以及一个整数 `days`，表示需要在 `days` 天内将所有包裹送达。设计一个算法找到能够在 `days` 天内送达包裹的最小运载能力。

**代码实现**：
```python
def shipWithinDays(weights: List[int], days: int) -> int:
    # 定义左右边界，左边界为最大单个包裹重量，右边界为所有包裹重量之和
    left, right = max(weights), sum(weights)
    # 当左边界小于右边界时继续循环
    while left < right:
        # 计算中间值
        mid = (left + right) // 2
        # 计算需要的天数
        need, curr = 1, 0
        for weight in weights:
            # 如果当前包裹重量加上当前运载量超过 mid，说明需要多一天
            if curr + weight > mid:
                need += 1
                curr = 0
            curr += weight
        # 如果需要的天数超过限制，说明运载能力不够，增加运载能力
        if need > days:
            left = mid + 1
        # 否则减小运载能力
        else:
            right = mid
    # 返回最小运载能力
    return left

# 时间复杂度：O(n log(sum(weights) - max(weights))) - 二分查找法寻找最小运载能力
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
通过二分查找法确定最小运载能力，在每次查找中判断是否能够在 `days` 天内将所有包裹送达，从而找到最优解。

---

### 24. LeetCode 275: H-Index II

**题目描述**：
给定一个升序排序的数组 `citations`，其中 `citations[i]` 表示某个研究者的第 `i` 篇论文的引用次数。计算并返回该研究者的 H 指数。

**代码实现**：
```python
def hIndex(citations: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(citations) - 1
    n = len(citations)
    # 当左指针小于等于右指针时继续循环
    while left <= right:
        mid = (left + right) // 2
        # 如果满足 H 指数条件
        if citations[mid] >= n - mid:
            right = mid - 1
        else:
            left = mid + 1
    # 返回 H 指数
    return n - left

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
H-指数是衡量学术影响力的标准之一，利用二分查找法可以有效地判断某个引用次数是否满足 H 指数的条件，从而快速找到符合条件的 H 指数值。

---

### 25. LeetCode 153: Find Minimum in Rotated Sorted Array（寻找旋转排序数组中的最小值）

**题目描述**：
假设按照升序排列的数组在预先未知的某个点上进行了旋转，请找出其中最小的元素。

**代码实现**：
```python
def findMin(nums: List[int]) -> int:
    # 定义左右指针
    left, right = 0, len(nums) - 1
    # 当 left 指针小于 right 指针时继续循环
    while left < right:
        # 计算中间位置索引
        mid = (left + right) // 2
        # 如果中间值大于右边界值，说明最小值在右半部分
        if nums[mid] > nums[right]:
            left = mid + 1
        # 否则最小值在左半部分（包括当前 mid）
        else:
            right = mid
    # 返回最小值
    return nums[left]

# 时间复杂度：O(log n) - 每次查找将搜索范围缩小一半
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
旋转排序数组的最小值一定在无序的一半中，通过判断中间值与右边界值的关系可以有效缩小搜索范围。

---

### 26. LeetCode 34: Find First and Last Position of Element in Sorted Array（在排序数组中查找元素的第一个和最后一个位置）

**题目描述**：
给定一个按照升序排列的整数数组 `nums` 和一个目标值 `target`，找出目标值在数组中出现的第一个和最后一个位置。如果目标值不存在于数组中，返回 `[-1, -1]`。

**代码实现**：
```python
def searchRange(nums: List[int], target: int) -> List[int]:
    # 辅助函数：查找边界
    def findBoundary(nums, target, findFirst):
        left, right = 0, len(nums) - 1
        boundaryIndex = -1
        # 当左指针小于等于右指针时继续循环


        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                boundaryIndex = mid
                # 查找第一个位置时，缩小右边界
                if findFirst:
                    right = mid - 1
                # 查找最后一个位置时，缩小左边界
                else:
                    left = mid + 1
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return boundaryIndex

    # 查找第一个和最后一个位置
    firstPosition = findBoundary(nums, target, True)
    lastPosition = findBoundary(nums, target, False)
    return [firstPosition, lastPosition]

# 时间复杂度：O(log n) - 两次二分查找
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该题的关键是用二分查找找到目标值的边界位置。通过分别查找第一个和最后一个出现位置，可以有效地减少时间复杂度。

---

### [27. LeetCode 69: Sqrt(x)（求平方根）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%2069%3A%20%E8%AE%A1%E7%AE%97%E5%B9%B3%E6%96%B9%E6%A0%B9%20(Calculate%20Square%20Root).md)

**题目描述**：
给定一个非负整数 `x`，计算并返回 `x` 的平方根，结果只保留整数部分，向下取整。

**代码实现**：
```python
class Solution:
    def mySqrt(self, x: int) -> int:
        # 边界处理：如果 x 是 0，直接返回 0
        if x == 0:
            return 0
        
        # 初始化左右指针
        left, right = 1, x
        
        # 当左指针小于等于右指针时继续二分查找
        while left <= right:
            mid = (left + right) // 2
            # 如果 mid 的平方等于 x，直接返回 mid
            if mid * mid == x:
                return mid
            # 如果 mid 的平方小于 x，说明平方根在 mid 的右边
            elif mid * mid < x:
                left = mid + 1
            # 如果 mid 的平方大于 x，说明平方根在 mid 的左边
            else:
                right = mid - 1
        
        # 返回右指针，因为当循环结束时，right 指向的就是小于等于平方根的整数部分
        return right

# 时间复杂度：O(log x) - 二分查找的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
这道题可以用二分查找来解决。由于平方函数是单调递增的，我们可以通过不断缩小搜索范围，找到一个整数 `y`，使得 `y^2 <= x` 且 `(y + 1)^2 > x`。最终，右指针 `r` 会指向满足条件的整数平方根。

---

### [28. LeetCode 278: First Bad Version（第一个错误的版本）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE/LeetCode%20278%3A%20First%20Bad%20Version%EF%BC%88%E7%AC%AC%E4%B8%80%E4%B8%AA%E9%94%99%E8%AF%AF%E7%9A%84%E7%89%88%E6%9C%AC%EF%BC%89.md)

### LeetCode 278: First Bad Version（第一个错误的版本）

**题目描述**：
你是产品经理，目前正在带领一个团队开发一个新产品。然而，某一天你发现产品的某个版本存在问题，导致后续的所有版本都出错。假设你有 `n` 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误版本。你可以通过调用 `isBadVersion(version)` API 来判断版本是否出错。请你实现一个函数来查找第一个错误的版本。

你应该尽量减少对 `isBadVersion` API 的调用次数。

**代码实现**：
```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        # 初始化左右指针
        l, r = 1, n
        idx = -1  # 用于记录第一个错误版本的索引
        
        # 二分查找第一个错误版本
        while l <= r:
            mid = (l + r) // 2
            # 如果当前版本是错误版本，可能是第一个错误版本
            if isBadVersion(mid):
                idx = mid  # 更新第一个错误版本的索引
                r = mid - 1  # 错误版本可能在左侧
            else:
                # 如果当前版本是正确的，错误版本在右侧
                l = mid + 1
        
        # 返回第一个错误版本的索引
        return idx

# 时间复杂度：O(log n) - 二分查找的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**题目分析**：
该问题可以使用二分查找来高效解决。因为版本数组是有序的，从某个版本开始都是错误版本，因此我们可以利用二分查找缩小查找范围，直到找到第一个错误的版本。

**解决方案详解**：

- **初始化条件**：
  - 左边界 `l` 初始化为 1，右边界 `r` 初始化为 `n`，即所有版本的范围。
  - 使用 `idx` 记录第一个错误版本的索引。

- **二分查找的过程**：
  - 每次计算中间值 `mid`，调用 `isBadVersion(mid)`：
    - 如果 `isBadVersion(mid)` 返回 `True`，说明当前版本以及之后的版本都是错误的，可能第一个错误版本在左侧，因此将右边界 `r` 移动到 `mid - 1`，同时更新 `idx` 为 `mid`。
    - 如果 `isBadVersion(mid)` 返回 `False`，说明当前版本是正确的，错误版本在右侧，因此将左边界 `l` 移动到 `mid + 1`。

- **结束条件**：
  - 当左右指针交错时，循环结束，`idx` 就是第一个错误版本的索引。

**复杂度分析**：
- **时间复杂度**：O(log n)，我们每次迭代都将查找范围缩小一半，因此时间复杂度为 O(log n)。
- **空间复杂度**：O(1)，只使用了常量空间来存储指针和中间变量.

