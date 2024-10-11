## Title: [LeetCode 167: 两数之和 II - 输入有序数组](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

### 问题

给定一个 **按非递减顺序排序** 的 1 索引整数数组 `numbers` 和一个整数 `target`，找出两个数使它们相加之和等于目标数 `target`。请返回这两个数的索引 `index1` 和 `index2`，其中 `1 <= index1 < index2 <= numbers.length`。

返回的答案是以长度为 2 的整数数组 `[index1, index2]`，其中 `index1` 和 `index2` 是从 1 开始的索引。

**解决方案必须仅使用恒定的额外空间。**

### 示例 1:

```
输入: numbers = [2,7,11,15], target = 9
输出: [1,2]
解释: 数字 2 和 7 相加之和为 9，因此 index1 = 1, index2 = 2。我们返回 [1, 2]。
```

### 示例 2:

```
输入: numbers = [2,3,4], target = 6
输出: [1,3]
```

### 示例 3:

```
输入: numbers = [-1,0], target = -1
输出: [1,2]
```

---

### 解题思路

因为数组已经是排序好的，我们可以使用 **双指针** 技巧来高效地解决这个问题。

### 步骤：

1. 初始化两个指针：
   - `left` 指针指向数组的起始位置（索引为 `0`）。
   - `right` 指针指向数组的末尾位置（索引为 `numbers.length - 1`）。
   
2. 当 `left` 指针小于 `right` 指针时，执行以下步骤：
   - 计算当前 `left` 和 `right` 指向的元素之和。
   - 如果当前和等于 `target`，则返回 `[left + 1, right + 1]`，因为题目要求返回 1 索引的结果。
   - 如果当前和小于 `target`，则将 `left` 指针右移以尝试增加和。
   - 如果当前和大于 `target`，则将 `right` 指针左移以尝试减小和。

---

### 代码实现：

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers) - 1

        while left < right:
            current_sum = numbers[left] + numbers[right]
            if current_sum == target:
                return [left + 1, right + 1]  # 返回 1 索引的结果
            elif current_sum < target:
                left += 1  # 当前和小于目标，移动 left 指针
            else:
                right -= 1  # 当前和大于目标，移动 right 指针
```

---

### 代码解释：

1. **初始化双指针**：
   - 我们从 `left` 指针指向数组的开头（索引为 `0`），`right` 指针指向数组的末尾（索引为 `len(numbers) - 1`）。

2. **循环直到满足条件**：
   - 当 `left` 小于 `right` 时，计算 `numbers[left]` 和 `numbers[right]` 的和。
   - 如果和等于目标值 `target`，我们返回 `[left + 1, right + 1]`，因为题目要求返回 1 索引的结果。
   - 如果当前和小于目标值，则将 `left` 指针右移以增加和。
   - 如果当前和大于目标值，则将 `right` 指针左移以减小和。

3. **返回索引**：
   - 一旦找到满足条件的两个数，返回它们的 1 索引形式 `[left + 1, right + 1]`。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 `n` 是数组 `numbers` 的长度。我们使用双指针遍历数组，每个元素最多被访问一次。
  
- **空间复杂度**：O(1)，因为我们只使用了两个指针作为额外空间，没有使用额外的存储空间。

---

### 示例讲解：

#### 示例 1:

```
numbers = [2,7,11,15], target = 9
```

- 从 `left = 0` 和 `right = 3` 开始。
- 当前和为 `numbers[0] + numbers[3] = 2 + 15 = 17`，大于目标值，因此将 `right` 左移到 `right = 2`。
- 当前和为 `numbers[0] + numbers[2] = 2 + 11 = 13`，仍然大于目标值，因此将 `right` 左移到 `right = 1`。
- 当前和为 `numbers[0] + numbers[1] = 2 + 7 = 9`，等于目标值，因此返回 `[1, 2]`（1 索引）。

#### 示例 2:

```
numbers = [2,3,4], target = 6
```

- 从 `left = 0` 和 `right = 2` 开始。
- 当前和为 `numbers[0] + numbers[2] = 2 + 4 = 6`，等于目标值，因此返回 `[1, 3]`。

---

### 总结

- **中文**：利用数组已经排序的性质，使用双指针的方法，可以高效地找到两数之和等于目标值的元素对。通过移动左右指针，可以调整和来满足要求。

---

### 推荐相似问题：

1. [LeetCode 1: 两数之和](https://leetcode.com/problems/two-sum/)
2. [LeetCode 15: 三数之和](https://leetcode.com/problems/3sum/)
3. [LeetCode 653: 两数之和 IV - 输入是 BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)
4. [LeetCode 16: 最接近的三数之和](https://leetcode.com/problems/3sum-closest/)
