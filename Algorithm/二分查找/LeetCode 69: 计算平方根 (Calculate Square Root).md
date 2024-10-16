# 计算平方根 (Calculate Square Root)

https://leetcode.com/problems/sqrtx/description/

## Definition
给定一个非负整数 `x`，计算并返回 `x` 的平方根，结果向下取整（即不使用小数部分）。本算法使用二分查找来高效地找到平方根。

## Key Concepts
- **二分查找 (Binary Search)**: 通过每次将搜索范围缩小一半来寻找目标值。在这里，目标值是 `x` 的平方根。
- **上下边界 (Bounds)**: 使用左右指针 `l` 和 `r` 来限制查找的范围。

## 主要步骤 (Main Steps)
1. **特例处理**: 如果 `x` 等于 0，直接返回 0。
2. **初始化边界**: 设置左指针 `l` 为 1，右指针 `r` 为 `x`。
3. **进行二分查找**:
   - 计算中点 `mid`。
   - 检查 `mid` 的平方是否等于 `x`，如果相等，返回 `mid`。
   - 如果 `mid` 的平方小于 `x`，将左边界 `l` 移动到 `mid + 1`。
   - 如果 `mid` 的平方大于 `x`，将右边界 `r` 移动到 `mid - 1`。
4. **返回结果**: 返回右边界 `r`，这是平方根向下取整的结果。

## Python 实现模板 (Python Implementation Template)
```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0:  # 处理特例
            return 0
        
        l, r = 1, x  # 初始化左右边界
        
        while l <= r:  # 进行二分查找
            mid = (l + r) // 2  # 计算中点
            if mid * mid == x:  # 如果找到平方根
                return mid
            elif mid * mid < x:  # 如果 mid 的平方小于 x
                l = mid + 1  # 移动左边界
            else:  # 如果 mid 的平方大于 x
                r = mid - 1  # 移动右边界
        
        return r  # 返回平方根向下取整的结果
```

## Tips
- 使用二分查找可以显著提高计算效率，尤其是在 `x` 较大时。
- 确保考虑到 `x` 为 0 的特例，以避免错误。

## Complexity Analysis
- **时间复杂度 (Time Complexity)**: O(log x)，每次迭代都将搜索范围缩小一半。
- **空间复杂度 (Space Complexity)**: O(1)，只使用了常量级的空间来存储变量。

---

### Example
**使用示例**:
```python
sol = Solution()
print(sol.mySqrt(4))  # 输出 2
print(sol.mySqrt(8))  # 输出 2
```

---

This format provides a comprehensive understanding of the `mySqrt` function. If you need any adjustments or additional information, feel free to ask!
