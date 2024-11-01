### LeetCode 543: 二叉树的直径 (Diameter of Binary Tree)

**题目描述**：  
给定一棵二叉树，找到树的直径。  
树的直径是指树中任意两个节点路径中最长的一条，该路径可能经过也可能不经过根节点。

[LeetCode 543: Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

**优化后的代码实现**：
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

# 定义解决方案的类
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        # 初始化直径为 0
        self.diameter = 0

        # 定义用于计算高度的递归函数，并在过程中更新直径
        def maxHeight(node: Optional[TreeNode]) -> int:
            if not node:
                return 0

            # 递归计算左、右子树的高度
            left_height = maxHeight(node.left)
            right_height = maxHeight(node.right)

            # 更新直径，直径等于左子树高度 + 右子树高度
            self.diameter = max(self.diameter, left_height + right_height)

            # 返回当前节点的高度
            return 1 + max(left_height, right_height)

        # 调用递归函数计算高度，并更新直径
        maxHeight(root)
        return self.diameter

# 时间复杂度：O(n) - 每个节点只遍历一次，其中 n 是节点数量。
# 空间复杂度：O(h) - 递归栈的深度，其中 h 是树的高度。
```

**题目分析**：
这道题可以通过深度优先搜索（DFS）来解决。在遍历过程中，同时计算子树的高度并更新直径。树的直径可以通过左右子树的高度之和得到。

**解决方案详解**：

- **初始化**：
  - 使用 `self.diameter` 存储当前计算出的最大直径。

- **递归逻辑**：
  - 如果当前节点为空，返回高度 0。
  - 递归计算当前节点的左、右子树高度。
  - 计算通过当前节点的路径长度（左子树高度 + 右子树高度）并更新 `self.diameter`。
  - 返回当前节点的高度，即 `1 + max(left_height, right_height)`。

- **返回结果**：
  - 返回存储在 `self.diameter` 中的最大直径。

**复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是二叉树节点的数量。每个节点仅访问一次。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。递归调用栈的深度等于树的高度。

---

### 示例讲解：逐步解析示例步骤（中文）

假设输入的树结构如下：

```
      1
     / \
    2   3
   / \
  4   5
```

我们需要找出树的直径，即从一个节点到另一个节点的最长路径。

#### 逐步计算过程：

1. **初始化**：
   - `self.diameter` 设置为 `0`。

2. **计算 `maxHeight(1)`**（即从根节点开始的最大高度）：
   - 进入节点 `1`，开始计算其左、右子树高度。

3. **计算 `maxHeight(2)`**（节点 `1` 的左子树高度）：
   - 进入节点 `2`，继续递归其左、右子树高度。

4. **计算 `maxHeight(4)`**（节点 `2` 的左子树高度）：
   - 进入节点 `4`，发现其左、右子树均为空，因此返回高度 `0`。
   - 当前节点 `4` 的高度为 `1 + max(0, 0) = 1`。

5. **计算 `maxHeight(5)`**（节点 `2` 的右子树高度）：
   - 进入节点 `5`，同样发现其左、右子树均为空，返回高度 `0`。
   - 当前节点 `5` 的高度为 `1 + max(0, 0) = 1`。

6. **回到节点 `2`**：
   - 左子树高度为 `1`（来自节点 `4`），右子树高度为 `1`（来自节点 `5`）。
   - 更新直径：`self.diameter = max(self.diameter, 1 + 1) = 2`。
   - 当前节点 `2` 的高度为 `1 + max(1, 1) = 2`。

7. **计算 `maxHeight(3)`**（节点 `1` 的右子树高度）：
   - 进入节点 `3`，发现其左、右子树均为空，返回高度 `0`。
   - 当前节点 `3` 的高度为 `1 + max(0, 0) = 1`。

8. **回到节点 `1`**：
   - 左子树高度为 `2`（来自节点 `2`），右子树高度为 `1`（来自节点 `3`）。
   - 更新直径：`self.diameter = max(self.diameter, 2 + 1) = 3`。
   - 当前节点 `1` 的高度为 `1 + max(2, 1) = 3`。

9. **最终结果**：
   - 直径 `self.diameter` 已更新为 `3`，即树的最长路径为 `3`，对应路径 `4 -> 2 -> 1 -> 3`。

最终结果为 `3`。
