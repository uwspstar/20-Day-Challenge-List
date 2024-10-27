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

        return root
```

### 代码解释
1. **递归基线条件**：
   - 如果当前节点为空，直接返回，表示到达了叶子节点的下一层。

2. **递归翻转左右子树**：
   - 调用 `invertTree` 对当前节点的左子树和右子树进行翻转。

3. **交换左右子树**：
   - 交换当前节点的左右子树，使得左子树变为右子树，右子树变为左子树。

4. **返回翻转后的根节点**：
   - 返回根节点，完成二叉树的镜像翻转。

### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。每个节点访问一次。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。递归调用栈的深度最多为 h，在最坏情况下可能是 O(n)（完全倾斜的二叉树）。

### 示例运行分析
#### 示例 1
- **输入**：
  ```
      4
     / \
    2   7
   / \ / \
  1  3 6  9
  ```
- **逐步执行**：
  1. 从根节点 `4` 开始调用 `invertTree(4)`。
  2. 递归到节点 `2` 和节点 `7`，分别调用 `invertTree(2)` 和 `invertTree(7)`。
  3. 对每个子树递归翻转，交换左右子树。
  4. 最终输出：
     ```
         4
        / \
       7   2
      / \ / \
     9  6 3  1
     ```
- **输出**：
  ```
      4
     / \
    7   2
   / \ / \
  9  6 3  1
  ```

### 总结
- 这是一种经典的递归问题，通过遍历整棵树并交换左右子树来实现二叉树的镜像翻转。
- 递归方式简洁直观，符合树结构的特性。
