### LeetCode 333: [Largest BST Subtree](https://leetcode.com/problems/largest-bst-subtree/)（最大 BST 子树）
**题目描述**：  
给定一个二叉树，找到其中最大的二叉搜索子树（BST）并返回其节点数量。一个子树是二叉搜索树（BST），当且仅当它的所有节点都满足：左子树的所有节点小于根节点，右子树的所有节点大于根节点。

**题目分析**：  
这是一个树的递归问题。在遍历树的过程中，通过后序遍历判断每个子树是否满足二叉搜索树的特性，并记录满足条件的最大子树的节点数。对于每个节点，我们需要判断它的左右子树是否是 BST，并比较子树中的最大和最小值，以确保其符合 BST 条件。

**代码实现**：

```python
# 定义二叉树节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def largestBSTSubtree(self, root: TreeNode) -> int:
        self.max_size = 0  # 记录最大 BST 子树的大小

        def postorder(node):
            if not node:
                # 返回值依次为：是否是 BST，节点数，最小值，最大值
                return True, 0, float('inf'), float('-inf')
            
            left_is_bst, left_size, left_min, left_max = postorder(node.left)
            right_is_bst, right_size, right_min, right_max = postorder(node.right)

            # 当前子树为 BST 的条件
            if left_is_bst and right_is_bst and left_max < node.val < right_min:
                size = left_size + right_size + 1
                self.max_size = max(self.max_size, size)
                return True, size, min(left_min, node.val), max(right_max, node.val)
            else:
                return False, 0, 0, 0

        postorder(root)
        return self.max_size

# 时间复杂度：O(n) - 遍历每个节点一次
# 空间复杂度：O(h) - 递归栈的深度，其中 h 是树的高度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树中节点的数量。每个节点在后序遍历中仅访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度。在最坏情况下（链状树），递归栈的深度可以达到 O(n)。

下面我们用一个具体的例子逐步运行 LeetCode 333 的解法。假设我们有以下二叉树：

```
        10
       /  \
      5    15
     / \   / \
    1   8 12  20
```

这个树的最大 BST 子树是左子树 `(5, 1, 8)`，并且包含 3 个节点。我们将通过后序遍历一步步分析如何找到这个最大 BST 子树。

---

### 代码思路复习
1. 使用后序遍历（左 -> 右 -> 根），每次在递归中处理左右子树后，再判断当前节点的子树是否满足 BST 条件。
2. 对于每个节点，返回四个信息：
   - 是否为 BST 子树（True/False）
   - 子树的节点数
   - 子树中的最小值
   - 子树中的最大值

### 详细步骤

我们从根节点 10 开始后序遍历。

---

#### Step 1: 访问节点 `1`
- 左右子节点都为空，因此 `1` 是 BST。
- 返回值：`(True, 1, 1, 1)`  
  - `True` 表示是 BST
  - `1` 表示节点数量
  - `1` 和 `1` 分别是子树的最小和最大值

---

#### Step 2: 访问节点 `8`
- 左右子节点都为空，因此 `8` 是 BST。
- 返回值：`(True, 1, 8, 8)`

---

#### Step 3: 访问节点 `5`
- 左子树 `1` 是 BST 且 `1 < 5`
- 右子树 `8` 是 BST 且 `5 < 8`
- 因此 `5` 作为根节点的子树 `(5, 1, 8)` 满足 BST 条件
- 该子树的节点数为 `1 (左) + 1 (右) + 1 (根) = 3`，更新 `self.max_size = 3`
- 返回值：`(True, 3, 1, 8)`

---

#### Step 4: 访问节点 `12`
- 左右子节点都为空，因此 `12` 是 BST。
- 返回值：`(True, 1, 12, 12)`

---

#### Step 5: 访问节点 `20`
- 左右子节点都为空，因此 `20` 是 BST。
- 返回值：`(True, 1, 20, 20)`

---

#### Step 6: 访问节点 `15`
- 左子树 `12` 是 BST 且 `12 < 15`
- 右子树 `20` 是 BST 且 `15 < 20`
- 因此 `15` 作为根节点的子树 `(15, 12, 20)` 满足 BST 条件
- 该子树的节点数为 `1 (左) + 1 (右) + 1 (根) = 3`，`self.max_size` 保持为 3
- 返回值：`(True, 3, 12, 20)`

---

#### Step 7: 访问根节点 `10`
- 左子树 `(5, 1, 8)` 是 BST 且 `8 < 10`
- 右子树 `(15, 12, 20)` 是 BST 且 `10 < 12`
- 因此以 `10` 为根的整棵树是 BST
- 该树的节点数为 `3 (左) + 3 (右) + 1 (根) = 7`，更新 `self.max_size = 7`
- 返回值：`(True, 7, 1, 20)`

---

### 结果
遍历结束后，`self.max_size` 的值为 `7`，表示整棵树是最大的 BST 子树，包含 7 个节点。
