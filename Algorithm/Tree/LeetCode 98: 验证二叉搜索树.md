### LeetCode 98: 验证二叉搜索树
[LeetCode 98: Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

#### 题目描述
给定一个二叉树，编写一个函数来检查它是否是一个**有效的二叉搜索树**（Binary Search Tree, BST）。

- **二叉搜索树的定义**：
  - 左子树中所有节点的值均小于其根节点的值。
  - 右子树中所有节点的值均大于其根节点的值。
  - 左右子树也必须分别是二叉搜索树。

#### 示例
##### 示例 1
```
输入:
    2
   / \
  1   3

输出: true
```

##### 示例 2
```
输入:
    5
   / \
  1   4
     / \
    3   6

输出: false
解释: 节点值 4 的右子树中包含了一个值为 3 的节点，违反了二叉搜索树的定义。
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
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        # 辅助函数，用于递归验证每个节点是否满足二叉搜索树的性质
        def isValid(node, minVal, maxVal):
            # 如果当前节点为空，则满足条件
            if not node:
                return True
            
            # 如果当前节点值不在 minVal 和 maxVal 范围内，则不是二叉搜索树
            if not (minVal < node.val < maxVal):
                return False
            
            # 递归检查左子树和右子树
            # 左子树：所有节点必须小于当前节点值
            # 右子树：所有节点必须大于当前节点值
            return isValid(node.left, minVal, node.val) and isValid(node.right, node.val, maxVal)
        
        # 初始调用，最小值设为负无穷大，最大值设为正无穷大
        return isValid(root, float('-inf'), float('inf'))
```

### 代码解释
1. **辅助函数 `isValid`**：
   - 递归地验证每个节点是否满足二叉搜索树的性质。
   - 传递三个参数：
     - `node`: 当前节点。
     - `minVal`: 当前节点的最小允许值。
     - `maxVal`: 当前节点的最大允许值。
   - 对于每个节点，要求值在 `(minVal, maxVal)` 范围内，否则返回 `False`。
   - 递归调用检查左右子树：
     - **左子树**：节点值必须小于当前节点值，更新最大值为当前节点值。
     - **右子树**：节点值必须大于当前节点值，更新最小值为当前节点值。

2. **主函数 `isValidBST`**：
   - 初始化调用 `isValid` 函数，最小值为负无穷大，最大值为正无穷大。

### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树中的节点数。
  - 每个节点访问一次，因此时间复杂度是线性的。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。
  - 递归调用栈的深度为树的高度，最坏情况下为 O(n)（完全不平衡的树）。

### 示例运行分析
#### 示例 1
- **输入**：
  ```
      2
     / \
    1   3
  ```
- **执行过程**：
  1. 根节点 `2` 满足条件，左子树检查范围为 `(-inf, 2)`，右子树检查范围为 `(2, inf)`。
  2. 左子树节点 `1` 满足 `-inf < 1 < 2`，递归继续。
  3. 右子树节点 `3` 满足 `2 < 3 < inf`，递归继续。
  4. 整棵树满足二叉搜索树的定义。
- **输出**：`True`

#### 示例 2
- **输入**：
  ```
      5
     / \
    1   4
       / \
      3   6
  ```
- **执行过程**：
  1. 根节点 `5` 满足条件，左子树检查范围为 `(-inf, 5)`，右子树检查范围为 `(5, inf)`。
  2. 左子树节点 `1` 满足 `-inf < 1 < 5`，递归继续。
  3. 右子树节点 `4` 不满足 `5 < 4 < inf`，违反二叉搜索树的定义。
- **输出**：`False`

### 总结
- 该解法通过递归遍历二叉树并在每次递归中使用区间限制节点值，来确保二叉搜索树的定义被满足。
- 递归的实现方式符合树结构问题的典型解法。
