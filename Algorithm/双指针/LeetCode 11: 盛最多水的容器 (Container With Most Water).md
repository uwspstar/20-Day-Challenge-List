## Title: [LeetCode 11: 盛最多水的容器 (Container With Most Water)](https://leetcode.com/problems/container-with-most-water/)

---

## 问题

给定一个长度为 `n` 的整数数组 `height`，每个元素代表一个竖直的线段，其两端分别位于坐标 `(i, 0)` 和 `(i, height[i])`。找出两条线段，使得它们与 `x` 轴共同构成的容器可以容纳最多的水。

返回容器可以存储的最大水量。

**注意**：你不能倾斜容器，且 `n` 至少为 2。

### 示例 1:

```
输入: height = [1,8,6,2,5,4,8,3,7]
输出: 49
解释: 选取的线段位于索引 1 (高度 = 8) 和索引 8 (高度 = 7)。此容器可以容纳的水量为 (8 - 1) * min(8, 7) = 49。
```

### 示例 2:

```
输入: height = [1,1]
输出: 1
```

---

## 解题思路

我们可以使用 **双指针** 技巧来高效地解决这个问题。

1. **双指针法**：
   - 初始化两个指针：`left` 指向数组的最左边，`right` 指向数组的最右边。
   - 计算当前由两条线段与 `x` 轴形成的容器的容量，并记录最大容量。
   - 每次选择较短的那条线段并移动对应的指针，因为短线段会限制容器的高度。移动短线段可以尝试找到更高的线段来容纳更多的水。

2. **面积计算**：
   - 容器的容量由两条线段之间的距离和它们的最小高度决定。面积计算公式为：
$$

     \[
     \text{Area} = (\text{right} - \text{left}) \times \min(\text{height[left]}, \text{height[right]})
     \]
$$


3. **如何移动指针**：
   - 移动较短的那根线段，因为较短的线段限制了当前容器的容量。移动它可能会找到一根更高的线段来增加容器的容量。

---

### 代码实现：

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1  # 初始化左右指针
        max_area = 0  # 记录最大水量

        while left < right:
            # 计算当前容器的面积
            current_area = (right - left) * min(height[left], height[right])
            max_area = max(max_area, current_area)

            # 移动较短的那根线段
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area
```

---

### 代码解释：

1. **初始化指针**：
   - `left` 指针从数组的最左侧开始，`right` 指针从数组的最右侧开始。
   - `max_area` 用来存储当前计算的最大面积。

2. **计算容器面积**：
   - 容器的面积由两条线段的最小高度和它们之间的距离决定。
   - 每次比较 `height[left]` 和 `height[right]`，并计算容器的容量。

3. **移动指针**：
   - 如果 `height[left]` 小于 `height[right]`，我们移动 `left` 指针，因为较短的线段限制了容器的容量。
   - 如果 `height[right]` 小于或等于 `height[left]`，我们移动 `right` 指针。

4. **返回结果**：
   - 循环结束时，`max_area` 保存的是可以盛水的最大容量。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 `n` 是数组的长度。我们使用双指针遍历数组一次。
  
- **空间复杂度**：O(1)，我们只使用了常量的额外空间来存储指针和结果。

---

### 示例讲解：

#### 示例 1:

```
输入: height = [1,8,6,2,5,4,8,3,7]
```

- 初始状态：`left = 0`, `right = 8`，计算面积为 `(8 - 0) * min(1, 7) = 8`，`max_area = 8`。
- 移动 `left` 指针到 `1`，计算面积为 `(8 - 1) * min(8, 7) = 49`，`max_area = 49`。
- 移动 `right` 指针到 `7`，继续比较，最终得到 `max_area = 49`。

#### 示例 2:

```
输入: height = [1,1]
```

- `left` 和 `right` 分别在两端，计算面积为 `(1 - 0) * min(1, 1) = 1`。
- 因为两根线段相同，移动任一指针，循环结束，结果为 `1`。

---

### 总结

- **中文**：通过双指针法，我们可以高效地找到两个线段，它们与 `x` 轴形成的容器可以盛最多的水。每次移动较短的线段以尝试找到更大的面积。

---

### 推荐相似问题：

1. [LeetCode 42: 接雨水](https://leetcode.com/problems/trapping-rain-water/)
2. [LeetCode 16: 最接近的三数之和](https://leetcode.com/problems/3sum-closest/)
3. [LeetCode 485: 最大连续1的个数](https://leetcode.com/problems/max-consecutive-ones/)
4. [LeetCode 121: 买卖股票的最佳时机](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
