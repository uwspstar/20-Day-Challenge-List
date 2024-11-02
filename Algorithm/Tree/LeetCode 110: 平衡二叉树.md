### LeetCode 110: 平衡二叉树
[LeetCode 110: Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

**题目描述**：  
给定一个二叉树，判断它是否是高度平衡的二叉树。在这里，高度平衡二叉树的定义是：每个节点的左右两个子树的高度差的绝对值不超过 1。

---

### 代码说明

在这个代码中，`isBalanced` 函数用于判断一个二叉树是否平衡，而 `height` 函数计算树中每个节点的高度。下面我们来逐步分析代码的工作原理、运行过程、以及该解法的时间复杂度。


```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True  # 空树是平衡的

        # 计算左右子树的高度
        l_h = self.height(root.left)
        r_h = self.height(root.right)

        # 如果左右子树高度差超过 1，则返回 False
        if abs(l_h - r_h) > 1:
            return False
        
        # 递归判断左右子树是否平衡
        return self.isBalanced(root.left) and self.isBalanced(root.right)
    
    def height(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0  # 空节点的高度为 0
        
        # 计算左右子树的最大高度并加上当前节点
        return 1 + max(self.height(root.left), self.height(root.right))
```

---

### 代码运行过程和解释

1. **`isBalanced`函数的逻辑**：
   - 首先检查当前树的根节点是否为空，如果为空，则返回 `True`，因为空树是平衡的。
   - 然后，使用 `height` 函数计算根节点左、右子树的高度。
   - 如果左右子树高度差大于 `1`，则说明树不平衡，直接返回 `False`。
   - 否则，递归调用 `isBalanced` 函数检查左右子树是否平衡。
   
2. **`height`函数的逻辑**：
   - `height` 函数用于计算节点的高度。如果节点为空，返回高度 `0`。
   - 如果节点不为空，则递归计算左右子树的高度，并返回 `1 + max(左子树高度, 右子树高度)`。

---

### 示例讲解

假设输入的二叉树如下：

```
      1
     / \
    2   2
   /
  3
 /
4
```

**运行过程**：

1. 从根节点 `1` 开始调用 `isBalanced`。
   - 计算左子树高度 `l_h = height(2)`。
   - 递归进入 `height(2)`，再调用 `height(3)`，最后到达 `height(4)`。
   - 节点 `4` 高度为 `1`，节点 `3` 高度为 `2`，节点 `2` 高度为 `3`。
   - 左子树高度 `l_h = 3`。

2. 回到根节点 `1`，计算右子树高度 `r_h = height(2)`。
   - 节点 `2` 高度为 `1`。
   - 右子树高度 `r_h = 1`。

3. 检查左右子树的高度差 `abs(l_h - r_h) = abs(3 - 1) = 2`，大于 `1`，因此返回 `False`，表示树不平衡。

---

### 时间复杂度分析

- **时间复杂度**：O(n^2)。
   - 每次调用 `isBalanced` 时，都需要计算左右子树的高度，而 `height` 函数本身是一个 O(n) 操作，因为它需要访问每个节点。因此，这种做法在最坏情况下会导致 O(n^2) 的复杂度。
   - 可以优化为 O(n) 的复杂度，使用自底向上的递归方式，在一次递归中同时检查平衡性并计算高度。

- **空间复杂度**：O(h)，其中 h 是树的高度。
   - 在递归调用中，空间复杂度主要受递归栈的限制。在最坏情况下，树为线性结构时，空间复杂度会达到 O(n)。

---

**代码实现**：
```python
# 定义树节点的类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义判断平衡的函数
    def isBalanced(self, root: TreeNode) -> bool:
        # 定义一个内部函数来计算节点的高度
        def height(node):
            # 如果节点为空，则高度为 0
            if not node:
                return 0
            # 递归计算左右子树的高度
            left_height = height(node.left)
            right_height = height(node.right)
            
            # 如果左右子树不平衡，则直接返回 -1 表示不平衡
            if left_height == -1 or right_height == -1 or abs(left_height - right_height) > 1:
                return -1
            # 否则返回当前节点的高度
            return max(left_height, right_height) + 1

        # 树的根节点调用 height 函数
        return height(root) != -1
```

```pyrhon
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True  # 空树是平衡的

        # 计算左右子树的高度
        l_h = self.height(root.left)
        r_h = self.height(root.right)

        # 如果左右子树高度差超过 1，则返回 False
        if abs(l_h - r_h) > 1:
            return False
        
        # 递归判断左右子树是否平衡
        return self.isBalanced(root.left) and self.isBalanced(root.right)
    
    def height(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0  # 空节点的高度为 0
        
        # 计算左右子树的最大高度并加上当前节点
        return 1 + max(self.height(root.left), self.height(root.right))

```


---

### 代码说明：

1. **递归计算高度**：
   - 使用一个内部函数 `height(node)` 来递归地计算树中每个节点的高度。
   - 如果 `node` 为 `None`（即叶节点的子节点），返回高度 `0`。
   
2. **平衡判断**：
   - 对于每个节点，先计算其左右子树的高度，即 `left_height` 和 `right_height`。
   - 检查左右子树的平衡情况：
     - 如果任意一边高度返回 `-1`（表示不平衡），或 `abs(left_height - right_height) > 1`（左右子树高度差大于 1），则返回 `-1` 表示该节点不平衡。
   - 否则，返回当前节点的高度 `max(left_height, right_height) + 1`。

3. **提前退出的优化**：
   - `if left_height == -1 or right_height == -1` 表示左右子树中已有不平衡情况，无需继续递归。
   - 这样可以减少计算，提高算法效率。

4. **结果判断**：
   - 调用 `height(root) != -1`，只要根节点返回的高度不为 `-1`，则表示整棵树平衡。

---

### 示例讲解：

假设输入的二叉树为：
```
      1
     / \
    2   2
   / \
  3   3
 / \
4   4
```

**运行过程**：

1. 从根节点 `1` 开始，调用 `height` 函数。
2. 递归计算节点 `1` 的左子树高度，进入 `height(2)`。
3. 递归计算节点 `2` 的左子树高度，进入 `height(3)`。
4. 递归计算节点 `3` 的左子树高度，进入 `height(4)`。
   - 节点 `4` 没有子树，高度返回 `1`。
5. 回到节点 `3`，计算右子树高度，右子树为空，返回高度 `1`。
   - 节点 `3` 的左右子树高度差为 `0`，返回 `2`。
6. 回到节点 `2`，计算右子树高度，右子树高度为 `1`。
   - 节点 `2` 的左右子树高度差为 `1`，返回 `3`。
7. 回到根节点 `1`，计算右子树高度，高度为 `1`。
   - 根节点 `1` 的左右子树高度差为 `2`，返回 `-1` 表示树不平衡。

最终返回 `False`，表示该树不平衡。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 n 是树的节点数。我们需要访问每个节点一次以计算高度。
- **空间复杂度**：O(h)，其中 h 是树的高度。递归调用的栈深度为树的高度，最坏情况下（例如链式结构），空间复杂度达到 O(n)。


