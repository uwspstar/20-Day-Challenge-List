### LeetCode 226: 翻转二叉树
[LeetCode 226: Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

#### 题目描述
给定一个二叉树的根节点 `root`，将该二叉树翻转（镜像化）。即将每个节点的左右子树进行交换。

#### 示例
##### 示例 1
```
输入：
    4
   / \
  2   7
 / \ / \
1  3 6  9

输出：
    4
   / \
  7   2
 / \ / \
9  6 3  1
```

##### 示例 2
```
输入：
  2
 / \
1   3

输出：
  2
 / \
3   1
```

##### 示例 3
```
输入：[]
输出：[]
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
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        # 如果当前节点为空，直接返回
        if not root:
            return root
        
        # 递归翻转左子树和右子树
        left = self.invertTree(root.left)
        right = self.invertTree(root.right)

        # 交换当前节点的左右子树
        root.left, root.right = right, left

- 递归方式简洁直观，符合树结构的特性。
