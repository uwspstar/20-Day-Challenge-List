### LeetCode 235: 二叉搜索树的最近公共祖先
[LeetCode 235: Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

#### 题目描述
给定一个二叉搜索树（BST）的根节点、以及两个节点 `p` 和 `q`，找到这两个节点的最近公共祖先（Lowest Common Ancestor, LCA）。

- **最近公共祖先的定义**：
  - 对于两个节点 p 和 q，在树中找到的公共祖先节点的深度应是最深的，即距离根节点最远。
- **二叉搜索树的特性**：
  - 左子树的所有节点的值均小于根节点的值。
  - 右子树的所有节点的值均大于根节点的值。

#### 示例
##### 示例 1
```
输入: root = [6, 2, 8, 0, 4, 7, 9], p = 2, q = 8
输出: 6
解释: 节点 6 是节点 2 和 8 的最近公共祖先。
```

##### 示例 2
```
输入: root = [6, 2, 8, 0, 4, 7, 9], p = 2, q = 4
输出: 2
解释: 节点 2 是节点 2 和 4 的最近公共祖先。
```

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
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        # 如果当前节点为空，返回空节点
        if not root:
            return root
        
        # 如果当前节点的值小于 p 和 q 的值，则 LCA 在右子树
        if root.val < p.val and root.val < q.val:
            return self.lowestCommonAncestor(root.right, p, q)
        
        # 如果当前节点的值大于 p 和 q 的值，则 LCA 在左子树
        if root.val > p.val and root.val > q.val:
            return self.lowestCommonAncestor(root.left, p, q)

        # 如果当前节点介于 p 和 q 之间，或等于其中之一，则当前节点即为 LCA
        return root
```

### 代码解释
1. **递归查找最近公共祖先**：
   - 对于二叉搜索树，我们可以利用其性质来查找最近公共祖先：
     - **如果当前节点的值小于 p 和 q 的值**，说明 p 和 q 都在当前节点的右子树中，LCA 也必定在右子树中。我们递归地在右子树中查找。
     - **如果当前节点的值大于 p 和 q 的值**，说明 p 和 q 都在当前节点的左子树中，LCA 也必定在左子树中。我们递归地在左子树中查找。
     - **否则**，当前节点即为最近公共祖先，因为 p 和 q 位于当前节点的两侧，或者当前节点是 p 或 q 之一。

2. **返回最近公共祖先**：
   - 当找到满足条件的节点时，返回该节点作为最近公共祖先。

### 通过示例来解释

#### 示例 1
- **输入**：
  ```
  root = [6, 2, 8, 0, 4, 7, 9], p = 2, q = 8
  ```
- **执行过程**：
  1. 当前节点为 `6`，`p = 2`，`q = 8`。
  2. `6` 介于 `2` 和 `8` 之间，不满足两个条件之一。
  3. 这意味着 `6` 是 p 和 q 的最近公共祖先。
- **输出**：`6`

#### 示例 2
- **输入**：
  ```
  root = [6, 2, 8, 0, 4, 7, 9], p = 2, q = 4
  ```
- **执行过程**：
  1. 当前节点为 `6`，`p = 2`，`q = 4`。
  2. `root.val = 6` 大于 `p.val = 2` 和 `q.val = 4`，满足第二个条件。
  3. 根据代码，进入左子树，继续递归。
  4. 当前节点变为 `2`，`p = 2`，`q = 4`。
  5. `root.val = 2` 介于 `2` 和 `4` 之间，不满足两个条件之一。
  6. 返回当前节点 `2`，即为 LCA。
- **输出**：`2`

#### 示例 3
- **输入**：
  ```
  root = [6, 2, 8, 0, 4, 7, 9], p = 7, q = 9
  ```
- **执行过程**：
  1. 当前节点为 `6`，`p = 7`，`q = 9`。
  2. `root.val = 6` 小于 `p.val = 7` 和 `q.val = 9`，满足第一个条件。
  3. 根据代码，进入右子树，继续递归。
  4. 当前节点变为 `8`，`p = 7`，`q = 9`。
  5. `root.val = 8` 介于 `7` 和 `9` 之间，不满足两个条件之一。
  6. 返回当前节点 `8`，即为 LCA。
- **输出**：`8`

### 复杂度分析
- **时间复杂度**：O(h)，其中 h 是二叉搜索树的高度。
  - 在最坏情况下（完全不平衡的树），时间复杂度为 O(n)，其中 n 是节点数。
- **空间复杂度**：O(h)，由于递归调用栈的深度为树的高度。

### 总结
- 该解法利用了二叉搜索树的特性，通过递归或迭代查找节点，实现了高效的最近公共祖先查找。
- 对于二叉搜索树，LCA 的查找过程相对高效，因为我们可以利用 BST 的有序性，减少不必要的遍历操作。
