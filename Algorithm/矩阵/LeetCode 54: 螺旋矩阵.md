### **LeetCode 54: 螺旋矩阵 (Spiral Matrix)**

https://leetcode.com/problems/spiral-matrix/

这段代码用于从左上角开始，按照顺时针方向提取矩阵的所有元素。代码采用边界变量 (`left, right, top, bottom`) 来逐步收缩矩阵的范围。

---

### **代码解释**

1. **初始化边界**：
   - `left` 和 `right` 表示当前矩阵的左右边界。
   - `top` 和 `bottom` 表示当前矩阵的上下边界。

2. **螺旋顺序提取元素**：
   - **从左到右**：遍历 `top` 行，从 `left` 到 `right - 1`。
   - **从上到下**：遍历 `right - 1` 列，从 `top` 到 `bottom - 1`。
   - **从右到左**：遍历 `bottom - 1` 行，从 `right - 1` 到 `left`，在更新 `bottom` 前检查边界条件。
   - **从下到上**：遍历 `left` 列，从 `bottom - 1` 到 `top`，在更新 `left` 前检查边界条件。

3. **退出条件**：
   - 在每次完成四个方向的遍历后，收缩边界。
   - 如果 `left >= right` 或 `top >= bottom`，停止遍历。

---

### **优化后的代码**

```python
from typing import List

class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        # 初始化结果数组和边界变量
        res = []
        left, right = 0, len(matrix[0])  # 左右边界
        top, bottom = 0, len(matrix)    # 上下边界

        # 按螺旋顺序提取矩阵元素
        while left < right and top < bottom:
            # 从左到右
            for i in range(left, right):
                res.append(matrix[top][i])
            top += 1

            # 从上到下
            for i in range(top, bottom):
                res.append(matrix[i][right - 1])
            right -= 1

            # 如果超出边界，退出循环
            if not (left < right and top < bottom):
                break

            # 从右到左
            for i in range(right - 1, left - 1, -1):
                res.append(matrix[bottom - 1][i])
            bottom -= 1

            # 从下到上
            for i in range(bottom - 1, top - 1, -1):
                res.append(matrix[i][left])
            left += 1

        return res
```

---

### **示例运行**

假设输入 `matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]`：

1. 初始状态：
   - `left = 0`, `right = 3`
   - `top = 0`, `bottom = 3`

2. **第一轮循环**：
   - 从左到右：`[1, 2, 3]`
   - 从上到下：`[6, 9]`
   - 从右到左：`[8, 7]`
   - 从下到上：`[4]`

3. **第二轮循环**：
   - 从左到右：`[5]`

4. **结束**：
   - 输出结果：`[1, 2, 3, 6, 9, 8, 7, 4, 5]`

---

### **复杂度分析**

- **时间复杂度**：O(m * n)，遍历矩阵中的所有元素。
- **空间复杂度**：O(1)，除了返回的结果数组外，使用了常量级的额外空间。

---

### **总结**

这段代码高效地处理了二维矩阵的螺旋提取问题，通过边界条件的逐步收缩来实现矩阵遍历。边界检查和退出条件的设计确保了对非正方形矩阵的兼容性。
