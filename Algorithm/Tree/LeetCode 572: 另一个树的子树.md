### LeetCode 572: 另一个树的子树
[LeetCode 572: Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)

#### 题目描述
给定两棵二叉树 `root` 和 `subRoot`，判断 `subRoot` 是否是 `root` 的一个子树。

- 一个子树是指由 `root` 中的某个节点及其所有后代组成的树，该子树的结构和 `subRoot` 完全相同。

#### 示例
##### 示例 1
```
root:       3
          /   \
         4     5
        / \
       1   2

subRoot:   4
          / \
         1   2
```

**输出**：`True`  
**解释**：`subRoot` 是 `root` 的一个子树。

##### 示例 2
```
root:       3
          /   \
         4     5
        / \
       1   2
            \
             0

subRoot:   4
          / \
         1   2
```

**输出**：`False`  
**解释**：`subRoot` 不是 `root` 的一个子树，因为节点 `2` 有一个额外的子节点 `0`。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        # 如果 root 为空，则 subRoot 无法是其子树
        if not root:
            return False
        
        # 检查当前节点及其左右子树是否与 subRoot 相同
        return self.is_same_tree(root, subRoot) or \
               self.isSubtree(root.left, subRoot) or \
               self.isSubtree(root.right, subRoot)

    def is_same_tree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # 如果两棵树都为空，则它们相同
        if not p and not q:
            return True
        # 如果其中一棵树为空，或者值不同，则它们不相同
        if not p or not q or p.val != q.val:
            return False
        # 递归检查左右子树
        return self.is_same_tree(p.left, q.left) and self.is_same_tree(p.right, q.right)
```

### 代码解释
1. **函数 `isSubtree`**：
   - 这个函数用于判断 `subRoot` 是否是 `root` 的子树。
   - 如果 `root` 为空，返回 `False`，因为 `subRoot` 无法是空树的子树。
   - 使用递归调用来检查当前节点的子树是否与 `subRoot` 相同，或者继续在左、右子树中递归查找。
  
2. **函数 `is_same_tree`**：
   - 该函数用于判断两棵二叉树是否完全相同。
   - 如果两棵树都为空，返回 `True`。
   - 如果仅有一棵树为空，或当前节点值不相同，则返回 `False`。
   - 递归调用检查左右子树是否相同。

### 复杂度分析
- **时间复杂度**：O(m * n)，其中 m 和 n 分别是 `root` 和 `subRoot` 的节点数。
  - 对于每个节点，都需要调用 `is_same_tree` 进行比较，在最坏情况下是 O(m * n)。
- **空间复杂度**：O(h)，其中 h 是 `root` 的高度。
  - 这是递归调用栈的深度，在最坏情况下可能是 O(n)（完全倾斜的二叉树）。

### 示例运行分析
#### 示例 1
- **输入**：
  ```
  root: 3 4 1 x x 2 x x 5 x x
  subRoot: 4 1 x x 2 x x
  ```
- **逐步执行**：
  1. 从根节点 `3` 开始调用 `isSubtree(3, 4)`，当前节点值不同，继续递归。
  2. 递归到节点 `4`，调用 `is_same_tree(4, 4)`，发现左右子树完全相同，返回 `True`。
- **输出**：`True`

#### 示例 2
- **输入**：
  ```
  root: 3 4 1 x x 2 x 0 x x 5 x x
  subRoot: 4 1 x x 2 x x
  ```
- **逐步执行**：
  1. 从根节点 `3` 开始调用 `isSubtree(3, 4)`，当前节点值不同，继续递归。
  2. 递归到节点 `4`，调用 `is_same_tree(4, 4)`，发现右子树不完全相同，继续递归。
  3. 递归到其他节点，无法找到匹配的子树。
- **输出**：`False`

### 总结
- 此解法通过递归遍历 `root`，在每个节点上调用 `is_same_tree` 来判断 `subRoot` 是否是其子树。
- 该方法使用了递归的特性，有效地判断了子树关系。
