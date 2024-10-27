### LeetCode 110: 平衡二叉树
[LeetCode 110: Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

#### 题目描述
一个二叉树被认为是平衡的，如果对于树中的每个节点，左右子树的高度（或深度）之差最多为 1。换句话说，树中每个节点的两个子树的深度差不超过 1。

树的高度定义：二叉树中某个节点的高度是从该节点到叶子节点的最长路径上的边数。

给定一个二叉树，判断它是否是平衡的。

#### 参数
- **root**: 二叉树的根节点。

#### 返回结果
- 一个布尔值，表示给定的树是否是平衡的。

#### 示例
##### 示例 1
```
      1
     / \
    2   3
   / 
  4   
```

对应的输入表示为：
```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
```

**输出**：`True`

**解释**：根据定义，这是一个平衡的二叉树。

##### 示例 2
```
      1
     / \
    2   2
   / \
  3   3
 / \
4   4
```

对应的输入表示为：
```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(2)
root.left.left = TreeNode(3)
root.left.right = TreeNode(3)
root.left.left.left = TreeNode(4)
root.left.left.right = TreeNode(4)
```

**输出**：`False`

**解释**：节点 2 的左右子树的高度差为 2，故树不平衡。

### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 解决方案类
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(root):
            # 如果当前节点为空，返回平衡状态为 True，高度为 0
            if root is None:
                return [True, 0]
            
            # 递归计算左右子树的平衡状态和高度
            left = dfs(root.left)   # 计算左子树的平衡状态和高度
            right = dfs(root.right) # 计算右子树的平衡状态和高度
            
            # 当前节点是否平衡：
            # 1. 左子树和右子树都要平衡
            # 2. 左右子树的高度差不超过 1
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
            
            # 计算当前节点的高度：
            # 树的高度定义：二叉树中某个节点的高度是从该节点到叶子节点的最长路径上的边数。
            # 递归逻辑：当前节点的高度是左右子树的最大高度加 1
            current_height = 1 + max(left[1], right[1])
            
            return [balanced, current_height] # 返回平衡状态和当前高度
        
        # 返回根节点的平衡状态
        return dfs(root)[0]
```

### 逐步执行示例分析
我们以以下二叉树为例进行逐步分析：

```
      1
     / \
    2   3
   / 
  4   
```

#### 初始调用
- 从根节点 `1` 开始调用 `dfs(1)`。

#### 递归过程
1. **节点 1** (`dfs(1)`)
   - 调用 `dfs(1.left)`，即节点 2。

2. **节点 2** (`dfs(2)`)
   - 调用 `dfs(2.left)`，即节点 4。

3. **节点 4** (`dfs(4)`)
   - 调用 `dfs(4.left)`，为空，返回 `[True, 0]`，表示左子树平衡，高度为 0。
   - 调用 `dfs(4.right)`，也为空，返回 `[True, 0]`，表示右子树平衡，高度为 0。
   - 当前节点 `4` 左右子树的高度差为 `0`，平衡。当前高度为 `1 + max(0, 0) = 1`。
   - 返回 `[True, 1]`。

4. **节点 2** 回溯到 (`dfs(2)`)
   - 接下来调用 `dfs(2.right)`，为空，返回 `[True, 0]`，表示右子树平衡，高度为 0。
   - 当前节点 `2` 左右子树分别为 `[True, 1]`（左）和 `[True, 0]`（右），平衡，高度差为 `1`。
   - 当前高度为 `1 + max(1, 0) = 2`。
   - 返回 `[True, 2]`。

5. **节点 1** 回溯到 (`dfs(1)`)
   - 调用 `dfs(1.right)`，即节点 3。

6. **节点 3** (`dfs(3)`)
   - 调用 `dfs(3.left)`，为空，返回 `[True, 0]`。
   - 调用 `dfs(3.right)`，也为空，返回 `[True, 0]`。
   - 当前节点 `3` 左右子树平衡，高度差为 `0`。
   - 当前高度为 `1 + max(0, 0) = 1`。
   - 返回 `[True, 1]`。

7. **节点 1** 最后一步 (`dfs(1)`)
   - 左子树为 `[True, 2]`，右子树为 `[True, 1]`，平衡，高度差为 `1`。
   - 当前高度为 `1 + max(2, 1) = 3`。
   - 返回 `[True, 3]`。

### 最终结果
- 根节点返回 `[True, 3]`，表示树是平衡的。
- `isBalanced(root)` 返回 `True`。

### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是树中节点的数量。每个节点仅被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度。递归调用栈的深度为 h，在最坏情况下可能是 O(n)（完全倾斜的二叉树）。

### 总结
- 此解法通过后序遍历递归地检查树的平衡状态，同时计算每个节点的高度。
- `max(left[1], right[1])` 用于确保当前节点的高度是左右子树的最大高度加 1。
