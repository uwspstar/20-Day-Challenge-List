### LeetCode 776: [Split BST](https://leetcode.com/problems/split-bst/)

---

## 题目描述

给定一棵二叉搜索树 (BST) 和一个值 `V`，将树分成两棵子树，其中一棵子树包含所有小于或等于 `V` 的节点，另一棵子树包含所有大于 `V` 的节点。返回这两棵树的根节点作为长度为 2 的列表。

---

### 示例 1:

```
输入: root = [4,2,6,1,3,5,7], V = 2
输出: [[2,1],[4,3,6,null,null,5,7]]
解释:
输入的二叉搜索树如下图所示：
       4
     /   \
    2     6
   / \   / \
  1   3 5   7

输出的两棵二叉搜索树分别是：
1. 小于等于 2 的子树:
       2
     /
    1

2. 大于 2 的子树:
       4
     /   \
    3     6
         / \
        5   7
```

---

### 解题思路

这是一个典型的递归问题。我们可以利用 BST 的特性来解决这个问题。给定节点的值 `root.val` 和给定的分界值 `V` 进行比较，并递归处理子树：

- **如果 `root.val <= V`**：表示当前节点及其左子树的所有节点都属于小于等于 `V` 的子树。那么我们递归地对 `root.right` 执行 `splitBST`，并将返回的左子树作为 `root.right`，表示 `V` 右侧部分应该分到新的子树中。
- **如果 `root.val > V`**：表示当前节点及其右子树的所有节点都属于大于 `V` 的子树。此时，我们递归地对 `root.left` 执行 `splitBST`，并将返回的右子树作为 `root.left`。

最终，我们返回分割后的两棵子树。

---

### 代码实现

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def splitBST(self, root: TreeNode, V: int):
        if not root:
            return [None, None]
        
        if root.val <= V:
            # 当前节点属于小于等于 V 的子树
            left_tree, right_tree = self.splitBST(root.right, V)
            root.right = left_tree  # 将左子树部分分配给 root 的右节点
            return [root, right_tree]  # root 和右子树分别返回
        
        else:
            # 当前节点属于大于 V 的子树
            left_tree, right_tree = self.splitBST(root.left, V)
            root.left = right_tree  # 将右子树部分分配给 root 的左节点
            return [left_tree, root]  # 左子树和 root 分别返回
```

---

### 代码解释

1. **基础情况**：
   - 当 `root` 为空时，返回 `[None, None]`，表示没有子树。
   
2. **递归判断**：
   - 如果当前节点的值小于等于 `V`，则当前节点及其左子树属于小于等于 `V` 的子树。我们递归地对 `root.right` 进行分割，返回的左子树将分配给 `root.right`。
   - 如果当前节点的值大于 `V`，则当前节点及其右子树属于大于 `V` 的子树。我们递归地对 `root.left` 进行分割，返回的右子树将分配给 `root.left`。

3. **返回值**：
   - 最终返回分割后的两棵子树。第一棵子树包含所有小于等于 `V` 的节点，第二棵子树包含所有大于 `V` 的节点。

---

### 复杂度分析

- **时间复杂度**：O(n)，其中 `n` 是树中的节点数。我们需要遍历所有节点一次来分割树。
- **空间复杂度**：O(n)，递归栈的深度最坏情况下可能是树的高度。

---

### 示例讲解

#### 示例 1:

```
输入: root = [4,2,6,1,3,5,7], V = 2
```

- 根节点 `root.val = 4`，`4 > V = 2`，所以递归分割 `root.left`。
- 在 `root.left = 2` 的子树上递归，`2 <= V`，所以我们递归分割 `root.right`，即节点 `3`。
- 最终返回结果为两棵子树：

```
1. 小于等于 2 的子树：
    2
   /
  1

2. 大于 2 的子树：
    4
   /   \
  3     6
       / \
      5   7
```
