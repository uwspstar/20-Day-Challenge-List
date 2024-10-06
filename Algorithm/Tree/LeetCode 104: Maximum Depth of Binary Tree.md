### LeetCode 题目：104. 二叉树的最大深度

https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

#### 问题描述：
给定一个二叉树，返回其最大深度。最大深度是指从根节点到最远叶子节点的最长路径上的节点数。

#### 示例 1：
```python
输入：
    3
   / \
  9  20
    /  \
   15   7
输出：3
```

#### 示例 2：
```python
输入：root = [1,null,2]
输出：2
```

### 原始代码（递归方法）：

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:  # 如果当前节点为空，返回深度 0
            return 0
            
        left_depth = self.maxDepth(root.left)  # 递归计算左子树的深度
        right_depth = self.maxDepth(root.right)  # 递归计算右子树的深度

        return 1 + max(left_depth, right_depth)  # 返回当前节点的深度
```

### 逐行解释：

1. **`def maxDepth(self, root: Optional[TreeNode]) -> int:`**：
   - 定义主函数 `maxDepth`，接受二叉树的根节点 `root`，返回树的最大深度。

2. **`if not root:`**：
   - 检查当前节点是否为空。如果为空，说明没有节点，返回深度 0。

3. **`left_depth = self.maxDepth(root.left)`**：
   - 递归调用 `maxDepth`，计算左子树的深度，并将结果存储在 `left_depth` 中。

4. **`right_depth = self.maxDepth(root.right)`**：
   - 递归调用 `maxDepth`，计算右子树的深度，并将结果存储在 `right_depth` 中。

5. **`return 1 + max(left_depth, right_depth)`**：
   - 返回当前节点的深度。当前节点的深度是左子树深度和右子树深度的最大值加上 1。

### 时间复杂度分析：

- **时间复杂度**：O(n)
  - 每个节点都会被访问一次，因此时间复杂度为 O(n)，其中 n 是树中节点的数量。

- **空间复杂度**：O(h)
  - 递归调用栈的深度为树的高度 h，最坏情况下为 O(n)，而最好的情况下为 O(log n)。

### 总结：

- **递归方法**：通过递归有效地计算二叉树的最大深度，使用简单明了的逻辑。
- **高效性**：该算法在处理各种树结构时都能保持高效，适用于大规模的二叉树。

如果你有其他问题或需要进一步讨论，请随时告诉我！
