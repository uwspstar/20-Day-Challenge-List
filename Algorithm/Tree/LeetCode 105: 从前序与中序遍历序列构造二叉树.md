### LeetCode 105: 从前序与中序遍历序列构造二叉树
[LeetCode 105: Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

#### 题目描述
给定二叉树的**前序遍历**和**中序遍历**的序列，构造这棵二叉树。

- **前序遍历**：根节点 -> 左子树 -> 右子树
- **中序遍历**：左子树 -> 根节点 -> 右子树

#### 示例
##### 示例 1
```
前序遍历: [3, 9, 20, 15, 7]
中序遍历: [9, 3, 15, 20, 7]

输出:
    3
   / \
  9  20
     / \
    15  7
```

##### 示例 2
```
前序遍历: [-1]
中序遍历: [-1]

输出:
    -1
```

#### 代码实现与详细注释
```python
from typing import List, Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        # 如果前序或中序为空，返回空节点
        if not preorder or not inorder:
            return None

        # 根据前序遍历的第一个元素创建根节点
        root = TreeNode(preorder[0])
        
        # 找到根节点在中序遍历中的索引
        idx = inorder.index(preorder[0])

        # 递归构建左子树和右子树
        # 左子树：前序为 preorder[1: idx + 1]，中序为 inorder[:idx]
        # 右子树：前序为 preorder[idx + 1:]，中序为 inorder[idx + 1:]
        root.left = self.buildTree(preorder[1: idx + 1], inorder[:idx])
        root.right = self.buildTree(preorder[idx + 1:], inorder[idx + 1:])

        return root
```

### 代码解释
1. **基本条件**：
   - 如果前序遍历或中序遍历为空，返回 `None`，表示已到达叶子节点。
  
2. **创建根节点**：
   - 前序遍历的第一个元素是当前树的根节点。
   - 创建一个新节点 `root`，值为 `preorder[0]`。

3. **划分中序遍历**：
   - 在中序遍历中找到根节点的位置 `idx`，此位置将中序遍历分为两部分：
     - **左子树的中序遍历**：`inorder[:idx]`
     - **右子树的中序遍历**：`inorder[idx + 1:]`

4. **递归构建左右子树**：
   - 根据中序遍历的划分，从前序遍历中提取左子树和右子树的节点值：
     - **左子树**：`preorder[1: idx + 1]` 和 `inorder[:idx]`
     - **右子树**：`preorder[idx + 1:]` 和 `inorder[idx + 1:]`
   - 递归地构建左子树和右子树。

5. **返回根节点**：
   - 返回构建好的二叉树根节点。

### 复杂度分析
- **时间复杂度**：O(n²)，其中 n 是节点数。
  - 在最坏情况下，每次递归调用都需要在中序遍历中搜索根节点，导致 O(n) 的查找时间。
  - 总体时间复杂度为 O(n) * O(n) = O(n²)。
- **空间复杂度**：O(n)，其中 n 是递归调用栈的深度。
  - 在最坏情况下，树完全不平衡，递归调用栈深度可能达到 O(n)。

### 示例运行分析
#### 示例 1
- **输入**：
  ```
  前序遍历: [3, 9, 20, 15, 7]
  中序遍历: [9, 3, 15, 20, 7]
  ```
- **逐步执行**：
  1. 前序第一个元素 `3` 为根节点。
  2. 中序中 `3` 的索引为 `1`，左子树的中序为 `[9]`，右子树的中序为 `[15, 20, 7]`。
  3. 递归构建左子树和右子树：
     - 左子树：前序为 `[9]`，中序为 `[9]`。
     - 右子树：前序为 `[20, 15, 7]`，中序为 `[15, 20, 7]`。
  4. 按此方法递归构建完整的二叉树：
     ```
         3
        / \
       9  20
          / \
         15  7
     ```
- **输出**：
  ```
      3
     / \
    9  20
       / \
      15  7
  ```

### 总结
- 该解法利用了**前序遍历**和**中序遍历**的性质，通过递归划分子树并构建二叉树。
- 在每次递归中，根节点从前序遍历中获取，中序遍历用于划分左右子树。
