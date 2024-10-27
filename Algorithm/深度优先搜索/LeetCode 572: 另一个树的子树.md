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
- 该方法使用了递归的特性，有效地判断了子树关系。
