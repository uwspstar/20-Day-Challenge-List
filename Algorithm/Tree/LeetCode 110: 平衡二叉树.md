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
- `max(left[1], right[1])` 用于确保当前节点的高度是左右子树的最大高度加 1。
