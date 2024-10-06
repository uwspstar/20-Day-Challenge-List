# 树 (Tree)

### Definition
树是一种非线性数据结构，由节点组成，节点之间通过边相连。树有一个根节点，其他节点称为子节点，具有层次结构。树广泛应用于计算机科学，如数据存储、组织和检索。

### Key Concepts
- **节点 (Node)**: 树的基本组成部分，可以包含数据和指向子节点的指针。
- **边 (Edge)**: 连接两个节点的线，表示节点之间的关系。
- **根节点 (Root)**: 树的最上层节点，没有父节点。
- **叶子节点 (Leaf)**: 没有子节点的节点。
- **高度 (Height)**: 从根节点到叶子节点的最长路径上的边数。

### 树的类型
- **二叉树 (Binary Tree)**: 每个节点最多有两个子节点，称为左子节点和右子节点。
- **二叉搜索树 (Binary Search Tree)**: 一种特殊的二叉树，左子树的所有节点值小于根节点值，右子树的所有节点值大于根节点值。
- **平衡树 (Balanced Tree)**: 树的高度保持在较低水平，确保操作效率，例如 AVL 树和红黑树。
- **N 叉树 (N-ary Tree)**: 每个节点可以有 N 个子节点的树。

### 树的操作
1. **插入 (Insertion)**: 将新节点添加到树中，保持树的结构特性。
2. **删除 (Deletion)**: 移除指定节点，并调整树以维持结构。
3. **遍历 (Traversal)**: 访问树中的每个节点，常用方法有：
   - 前序遍历 (Pre-order)
   - 中序遍历 (In-order)
   - 后序遍历 (Post-order)
   - 层次遍历 (Level-order)

### 时间复杂度分析
- **插入/删除时间复杂度**: O(h)，其中 h 是树的高度，最坏情况下为 O(n)（链式结构）。
- **遍历时间复杂度**: O(n)，需要访问每个节点一次。

### Python 树的实现示例 (二叉树)
```python
class TreeNode:
    def __init__(self, value):
        self.value = value  # 节点值
        self.left = None    # 左子节点
        self.right = None   # 右子节点

def insert(root, value):
    if root is None:
        return TreeNode(value)
    elif value < root.value:
        root.left = insert(root.left, value)  # 插入左子树
    else:
        root.right = insert(root.right, value)  # 插入右子树
    return root

def inorder_traversal(root):
    if root:
        inorder_traversal(root.left)  # 遍历左子树
        print(root.value)              # 访问节点
        inorder_traversal(root.right)  # 遍历右子树
```

---

## 树的遍历 (Tree Traversal)

### Definition
树的遍历是访问树中每个节点的过程。遍历可以分为深度优先遍历（DFS）和广度优先遍历（BFS），常用的遍历方式包括前序遍历、中序遍历、后序遍历和层次遍历。

### 1. 前序遍历 (Pre-order)
**定义**: 在前序遍历中，首先访问根节点，然后遍历左子树，最后遍历右子树。

**步骤**:
1. 访问根节点。
2. 遍历左子树。
3. 遍历右子树。

**时间复杂度**: O(n)，n 是树中节点的数量。

**Python 实现**:
```python
def pre_order_traversal(root):
    if root:
        print(root.value)              # 访问节点
        pre_order_traversal(root.left)  # 遍历左子树
        pre_order_traversal(root.right) # 遍历右子树
```

### 2. 中序遍历 (In-order)
**定义**: 在中序遍历中，首先遍历左子树，然后访问根节点，最后遍历右子树。

**步骤**:
1. 遍历左子树。
2. 访问根节点。
3. 遍历右子树。

**时间复杂度**: O(n)。

**Python 实现**:
```python
def in_order_traversal(root):
    if root:
        in_order_traversal(root.left)  # 遍历左子树
        print(root.value)               # 访问节点
        in_order_traversal(root.right)  # 遍历右子树
```

### 3. 后序遍历 (Post-order)
**定义**: 在后序遍历中，首先遍历左子树，然后遍历右子树，最后访问根节点。

**步骤**:
1. 遍历左子树。
2. 遍历右子树。
3. 访问根节点。

**时间复杂度**: O(n)。

**Python 实现**:
```python
def post_order_traversal(root):
    if root:
        post_order_traversal(root.left)  # 遍历左子树
        post_order_traversal(root.right) # 遍历右子树
        print(root.value)                # 访问节点
```

### 4. 层次遍历 (Level-order)
**定义**: 层次遍历是一种广度优先遍历方法，按照树的层级从上到下、从左到右访问每个节点。

**步骤**:
1. 使用队列来存储当前层的节点。
2. 访问队列中的每个节点，并将其子节点添加到队列中。

**时间复杂度**: O(n)。

**Python 实现**:
```python
from collections import deque

def level_order_traversal(root):
    if root is None:
        return

    queue = deque([root])  # 初始化队列
    while queue:
        node = queue.popleft()  # 弹出队首节点
        print(node.value)        # 访问节点

        if node.left:            # 如果左子节点存在，加入队列
            queue.append(node.left)
        if node.right:           # 如果右子节点存在，加入队列
            queue.append(node.right)
```

---

#### 1. **题目编号和名称**

**题目描述**：
给出题目描述的中文翻译，概括题目要求和输入输出格式。

**题目分析**：
分析题目中涉及到的树结构特点，比如二叉树、二叉搜索树、完全二叉树、平衡二叉树等。分析题目要求，可以结合树的遍历方式（如前序、中序、后序遍历）来分析解法。

**代码实现**：
逐行解释代码中的每一行逻辑及设计思想，并用中文注释代码。

**时间和空间复杂度分析**：
- 时间复杂度：分析算法的时间复杂度，比如 O(n)、O(log n) 等，说明为什么是这个复杂度。
- 空间复杂度：分析算法的空间复杂度，包括递归调用栈的开销、辅助数据结构的存储等。

---

#### 示例（以下是模板的示例题目）：

### LeetCode 104: Maximum Depth of Binary Tree（最大二叉树深度）

**题目描述**：
给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。说明：叶子节点是指没有子节点的节点。

**题目分析**：
该题属于树的深度优先搜索（DFS）问题。最大深度可以通过递归来计算，即从根节点开始，分别计算左子树和右子树的最大深度，然后取左右子树深度的最大值加 1 作为当前节点的深度。该解法也可以使用广度优先搜索（BFS）来实现，但时间和空间复杂度相同。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义最大深度计算函数
    def maxDepth(self, root: TreeNode) -> int:
        # 如果当前节点为空，返回深度 0
        if not root:
            return 0
        # 递归计算左子树和右子树的最大深度
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        # 返回当前节点的最大深度（左子树和右子树的最大深度 + 1）
        return max(left_depth, right_depth) + 1

# 时间复杂度：O(n) - 每个节点遍历一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- 时间复杂度：O(n)，其中 n 是树的节点数量，因为每个节点只会被遍历一次。
- 空间复杂度：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

30道LeetCode树相关的题目，每次展示5道，内容包括逐行中文注释代码及复杂度分析。我们先从最常见的树题目开始。

---

### [1. LeetCode 104: Maximum Depth of Binary Tree（最大二叉树深度）](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Algorithm/Tree/LeetCode%20104%3A%20Maximum%20Depth%20of%20Binary%20Tree.md)

**题目描述**：
给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。说明：叶子节点是指没有子节点的节点。

**题目分析**：
该题可以使用深度优先搜索（DFS）或者广度优先搜索（BFS）来解。最常见的方式是递归（DFS），从根节点开始遍历到叶子节点，计算左右子树的最大深度，最终取左右子树的最大深度加 1 作为当前节点的深度。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义计算二叉树最大深度的函数
    def maxDepth(self, root: TreeNode) -> int:
        # 如果当前节点为空，返回深度 0
        if not root:
            return 0
        # 递归计算左子树和右子树的最大深度
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        # 返回当前节点的最大深度（左子树和右子树的最大深度 + 1）
        return max(left_depth, right_depth) + 1

# 时间复杂度：O(n) - 每个节点遍历一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- 时间复杂度：O(n)，其中 n 是树的节点数量，因为每个节点只会被遍历一次。
- 空间复杂度：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 2. LeetCode 101: Symmetric Tree（对称二叉树）

**题目描述**：
给定一个二叉树，检查它是否是镜像对称的。

**题目分析**：
要判断一个二叉树是否是镜像对称的，可以使用递归（DFS）或者迭代（BFS）来解题。对于递归解法，判断左子树和右子树是否是对称的，具体来说，左子树的左节点是否等于右子树的右节点，左子树的右节点是否等于右子树的左节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义检查二叉树是否对称的函数
    def isSymmetric(self, root: TreeNode) -> bool:
        # 如果根节点为空，直接返回 True
        if not root:
            return True
        
        # 定义递归函数判断左右子树是否镜像对称
        def isMirror(left, right):
            # 如果左右子树都为空，则对称
            if not left and not right:
                return True
            # 如果左右子树其中一个为空，另一个不为空，则不对称
            if not left or not right:
                return False
            # 如果左右子树的值不同，则不对称
            if left.val != right.val:
                return False
            # 递归判断左子树的左节点和右子树的右节点，左子树的右节点和右子树的左节点是否对称
            return isMirror(left.left, right.right) and isMirror(left.right, right.left)

        # 调用递归函数判断左右子树是否对称
        return isMirror(root.left, root.right)

# 时间复杂度：O(n) - 每个节点遍历一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- 时间复杂度：O(n)，每个节点访问一次。
- 空间复杂度：O(h)，递归调用栈的开销。

---

好的，我们继续讲解接下来的五道 LeetCode 树相关题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 8. LeetCode 199: Binary Tree Right Side View（二叉树的右视图）

**题目描述**：
给定一个二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

**题目分析**：
该题可以通过层次遍历（BFS）或者递归（DFS）来解。利用 BFS 逐层遍历二叉树，记录每层的最后一个节点值，即为右视图。DFS 则按照 “根-右-左” 的顺序遍历，每一层第一个被访问到的节点就是右视图的节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义右视图计算函数
    def rightSideView(self, root: TreeNode) -> List[int]:
        # 如果根节点为空，返回空列表
        if not root:
            return []

        # 使用 BFS 进行层次遍历
        queue = deque([root])
        right_view = []

        while queue:
            level_size = len(queue)  # 当前层的节点数
            for i in range(level_size):
                node = queue.popleft()  # 弹出队首节点
                # 如果是当前层的最后一个节点，加入右视图列表
                if i == level_size - 1:
                    right_view.append(node.val)
                # 将左子节点加入队列
                if node.left:
                    queue.append(node.left)
                # 将右子节点加入队列
                if node.right:
                    queue.append(node.right)

        return right_view

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最多队列中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，队列中可能包含树中所有节点。

---

### 9. LeetCode 110: Balanced Binary Tree（平衡二叉树）

**题目描述**：
给定一个二叉树，判断它是否是高度平衡的二叉树。一棵高度平衡二叉树定义为：每个节点的左右两个子树的高度差的绝对值不超过 1。

**题目分析**：
可以使用递归（DFS）来解决该问题。每次递归时计算左右子树的高度，如果某个节点的左右子树高度差超过 1，则返回 `False`。在计算高度的过程中，可以同时判断是否平衡，从而避免重复计算高度。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义判断是否为平衡二叉树的函数
    def isBalanced(self, root: TreeNode) -> bool:
        # 定义一个辅助函数，返回树的高度，如果不平衡则返回 -1
        def height(node):
            # 如果当前节点为空，高度为 0
            if not node:
                return 0
            # 递归计算左子树的高度
            left_height = height(node.left)
            # 如果左子树不平衡，直接返回 -1
            if left_height == -1:
                return -1
            # 递归计算右子树的高度
            right_height = height(node.right)
            # 如果右子树不平衡，直接返回 -1
            if right_height == -1:
                return -1
            # 如果当前节点的左右子树高度差大于 1，则不平衡
            if abs(left_height - right_height) > 1:
                return -1
            # 返回当前节点的高度
            return max(left_height, right_height) + 1

        # 如果高度为 -1，则不平衡，否则平衡
        return height(root) != -1

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 10. LeetCode 236: Lowest Common Ancestor of a Binary Tree（二叉树的最近公共祖先）

**题目描述**：
给定一个二叉树，找到该树中两个指定节点的最近公共祖先（LCA）。最近公共祖先的定义为：在树中，节点 p 和 q 的最近公共祖先是满足 `p` 和 `q` 都在它的子树中（含自身）的最低节点。

**题目分析**：
可以使用递归来查找最近公共祖先。在遍历的过程中，如果当前节点是 `p` 或 `q`，则返回该节点。如果左子树和右子树都包含 `p` 或 `q`，则当前节点为最近公共祖先。否则返回非空的子树。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找最近公共祖先的函数
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        # 如果当前节点为空，或当前节点为 p 或 q，返回当前节点
        if not root or root == p or root == q:
            return root
        # 在左子树中查找 p 和 q
        left = self.lowestCommonAncestor(root.left, p, q)
        # 在右子树中查找 p 和 q
        right = self.lowestCommonAncestor(root.right, p, q)
        # 如果 p 和 q 分别位于当前节点的左右子树，则当前节点为最近公共祖先
        if left and right:
            return root
        # 否则，返回非空子树
        return left if left else right

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 11. LeetCode 124: Binary Tree Maximum Path Sum（二叉树中的最大路径和）

**题目描述**：
给定一个非空二叉树，返回其最大路径和。路径被定义为从树中任意节点出发，沿父节点-子节点连接，达到任意节点的路径，路径至多包含一个拐点（即不能回头）。

**题目分析**：
该题可以通过递归（DFS）来解决。在递归过程中，计算每个节点的最大路径和，包括当前节点的最大单边贡献值（最大左子树路径或最大右子树路径）。更新全局最大路径和，并返回该节点的最大贡献值。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义计算最大路径和的函数
    def maxPathSum(self, root: TreeNode) -> int:
        # 初始化全局最大路径和
        self.max_sum = float('-inf')

        # 定义一个辅助函数，返回某个节点的最大路径和
        def get_max_gain(node):
            if not node:
                return 0
            # 递归计算左右子树的最大贡献值（若为负则舍弃）
            left_gain = max(get_max_gain(node.left), 0)
            right_gain = max(get_max_gain(node.right), 0)
            # 更新当前节点的最大路径和
            current_max_path = node.val + left_gain + right_gain
            # 更新全局最大路径和
            self.max_sum = max(self.max_sum, current_max_path)
            # 返回该节点的最大贡献值

（单边）
            return node.val + max(left_gain, right_gain)

        # 调用辅助函数计算最大路径和
        get_max_gain(root)
        return self.max_sum

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 12. LeetCode 450: Delete Node in a BST（二叉搜索树中的删除节点）

**题目描述**：
给定一个二叉搜索树（BST）的根节点 `root` 和一个值 `key`，删除 BST 中值为 `key` 的节点，并确保删除后的 BST 仍然是有效的。

**题目分析**：
删除节点有三种情况：
1. 节点是叶子节点，直接删除。
2. 节点只有一个子节点，删除该节点并用其子节点替代。
3. 节点有两个子节点，用其右子树中的最小节点或左子树中的最大节点替代该节点，并递归删除替代节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义删除节点的函数
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
        # 如果根节点为空，返回 None
        if not root:
            return None
        # 查找目标节点
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            # 情况 1：目标节点是叶子节点或只有一个子节点
            if not root.left:
                return root.right
            if not root.right:
                return root.left
            # 情况 2：目标节点有两个子节点
            # 查找右子树的最小节点替代当前节点
            min_node = self.getMin(root.right)
            root.val = min_node.val
            # 递归删除右子树中的最小节点
            root.right = self.deleteNode(root.right, min_node.val)
        return root

    # 查找最小节点的辅助函数
    def getMin(self, node: TreeNode) -> TreeNode:
        while node.left:
            node = node.left
        return node

# 时间复杂度：O(h) - h 为树的高度
# 空间复杂度：O(h) - 递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(h)，其中 h 是树的高度，查找和删除节点的时间均为 O(h)。
- **空间复杂度**：O(h)，递归调用栈的最大深度。

---

好的，我们继续讲解接下来的五道 LeetCode 树相关题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 13. LeetCode 222: Count Complete Tree Nodes（完全二叉树的节点个数）

**题目描述**：
给定一棵完全二叉树，返回其节点的个数。完全二叉树定义为：每一层都是满的，只有最后一层的节点可能不满，并且所有节点都尽量向左排列。

**题目分析**：
对于一般的二叉树，可以使用深度优先搜索（DFS）或者广度优先搜索（BFS）来遍历每个节点计数，时间复杂度为 O(n)。但是对于完全二叉树，可以利用完全二叉树的性质，通过判断左右子树高度，快速计算节点个数，从而将时间复杂度降为 O(log^2 n)。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义计算完全二叉树节点个数的函数
    def countNodes(self, root: TreeNode) -> int:
        # 定义辅助函数计算树的高度
        def get_height(node):
            height = 0
            while node:
                node = node.left
                height += 1
            return height

        # 如果根节点为空，返回 0
        if not root:
            return 0

        # 计算左子树和右子树的高度
        left_height = get_height(root.left)
        right_height = get_height(root.right)

        # 如果左子树和右子树高度相同，说明左子树是满二叉树
        if left_height == right_height:
            # 左子树节点个数为 2^left_height，递归计算右子树的节点个数
            return (1 << left_height) + self.countNodes(root.right)
        else:
            # 如果高度不同，说明右子树是满二叉树，左子树还需继续递归
            return (1 << right_height) + self.countNodes(root.left)

# 时间复杂度：O(log^2 n) - 计算每个节点的高度需要 O(log n)，共需 O(log n) 次递归
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log^2 n)，因为每次递归都要计算高度，时间复杂度为 O(log n)，并且需要递归 log n 次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 14. LeetCode 116: Populating Next Right Pointers in Each Node（填充每个节点的下一个右侧节点指针）

**题目描述**：
给定一个完美二叉树（所有叶子节点都在同一层，每个父节点都有两个子节点），填充它的每个节点的 `next` 指针，使得该指针指向其右侧的下一个节点。如果没有右侧节点，则将 `next` 指针设为 `None`。

**题目分析**：
可以使用层次遍历（BFS）或者递归（DFS）来解决该问题。对于每一层，从左到右依次连接每个节点的 `next` 指针。DFS 递归时，可以在递归函数中将左子节点的 `next` 指向右子节点，并将右子节点的 `next` 指向相邻节点的左子节点。

**代码实现**：
```python
# 定义树的节点类（带有 next 指针）
class Node:
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义填充下一个右侧节点指针的函数
    def connect(self, root: 'Node') -> 'Node':
        # 如果根节点为空，返回 None
        if not root:
            return None

        # 使用递归来连接节点
        def connect_two_nodes(node1, node2):
            if not node1 or not node2:
                return
            # 将第一个节点的 next 指向第二个节点
            node1.next = node2
            # 连接同一个父节点的两个子节点
            connect_two_nodes(node1.left, node1.right)
            # 连接跨父节点的两个子节点
            connect_two_nodes(node1.right, node2.left)

        # 连接根节点的左右子节点
        connect_two_nodes(root.left, root.right)
        return root

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 15. LeetCode 117: Populating Next Right Pointers in Each Node II（填充每个节点的下一个右侧节点指针 II）

**题目描述**：
与 LeetCode 116 类似，但该题是普通二叉树（不是完美二叉树）。填充它的每个节点的 `next` 指针，使得该指针指向其右侧的下一个节点。如果没有右侧节点，则将 `next` 指针设为 `None`。

**题目分析**：
该题不能直接使用递归来解决，需要使用层次遍历（BFS）。可以利用一个指针 `next_level_start` 来记录下一层的开始节点，通过遍历当前层来连接下一层的 `next` 指针。

**代码实现**：
```python
# 定义树的节点类（带有 next 指针）
class Node:
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next

# 定义解决方案的类
class Solution:
    # 定义填充下一个右侧节点指针的函数
    def connect(self, root: 'Node') -> 'Node':
        # 如果根节点为空，返回 None
        if not root:
            return None

        # 初始化当前节点和下一层起始节点
        current = root
        next_level_start = Node(0)  # 虚拟节点，指向下一层的起始节点

        while current:
            # 使用一个指针遍历下一层节点
            tail = next_level_start
            # 遍历当前层的所有节点
            while current:
                # 连接左子节点
                if current.left:
                    tail.next = current.left
                    tail = tail.next
                # 连接右子节点
                if current.right:
                    tail.next = current.right
                    tail = tail.next
                # 移动到当前层的下一个节点
                current = current.next
            # 移动到下一层的起始节点
            current = next_level_start.next
            next_level_start.next = None  # 重置虚拟节点

        return root

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(1)，除了节点指针外，未使用额外的存储空间。

---

### 16. LeetCode 144: Binary Tree Preorder Traversal（二叉树的前序遍历）

**题目描述**：
给定一个二叉树，返回它的 **前序遍历** 的结果。前序遍历的顺序是：根节点 -> 左子树 -> 右子树。

**题目分析**：
可以使用递归（DFS）或者迭代（使用栈）来实现前序遍历。递归法直接调用左右子树，而迭代法通过栈来模拟递归过程。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义前序遍历的函数（迭代法）
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        # 如果根节点为空，返回空列表
        if not root:
            return []


        
        # 使用栈来进行迭代前序遍历
        stack, result = [root], []
        
        while stack:
            # 弹出栈顶节点并访问
            node = stack.pop()
            result.append(node.val)
            # 先压入右子节点，再压入左子节点（因为栈是后进先出，左子节点先访问）
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        
        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最坏情况下栈中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，栈中可能包含所有节点。

---

### 17. LeetCode 94: Binary Tree Inorder Traversal（二叉树的中序遍历）

**题目描述**：
给定一个二叉树，返回它的 **中序遍历** 的结果。中序遍历的顺序是：左子树 -> 根节点 -> 右子树。

**题目分析**：
可以使用递归（DFS）或者迭代（使用栈）来实现中序遍历。递归法直接调用左右子树，而迭代法通过栈来模拟递归过程，并通过指针来追踪当前节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义中序遍历的函数（迭代法）
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        # 初始化栈和结果列表
        stack, result = [], []
        current = root
        
        # 使用指针遍历所有节点
        while stack or current:
            # 不断将左子节点压入栈中
            while current:
                stack.append(current)
                current = current.left
            # 弹出栈顶节点并访问
            current = stack.pop()
            result.append(current.val)
            # 移动到右子节点
            current = current.right
        
        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最坏情况下栈中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，栈中可能包含所有节点。

---

好的，我们继续讲解接下来的五道 LeetCode 树相关题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 18. LeetCode 145: Binary Tree Postorder Traversal（二叉树的后序遍历）

**题目描述**：
给定一个二叉树，返回它的 **后序遍历** 的结果。后序遍历的顺序是：左子树 -> 右子树 -> 根节点。

**题目分析**：
可以使用递归（DFS）或者迭代（使用栈）来实现后序遍历。递归法直接调用左右子树，迭代法通过栈来模拟递归过程，并使用一个指针 `prev` 来标记前一个访问的节点，帮助确定当前节点是否可以出栈访问。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义后序遍历的函数（迭代法）
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        # 初始化栈和结果列表
        stack, result = [], []
        current = root
        prev = None  # 记录上一个访问的节点

        while stack or current:
            # 不断将左子节点压入栈中
            while current:
                stack.append(current)
                current = current.left
            # 获取栈顶节点但不出栈
            current = stack[-1]
            # 如果当前节点没有右子节点或右子节点已经被访问过，则可以访问当前节点
            if not current.right or current.right == prev:
                result.append(current.val)
                stack.pop()  # 弹出栈顶节点
                prev = current  # 更新上一个访问的节点
                current = None  # 重置当前节点
            else:
                # 如果当前节点有右子节点且未被访问，则访问右子节点
                current = current.right

        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最坏情况下栈中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，栈中可能包含所有节点。

---

### 19. LeetCode 297: Serialize and Deserialize Binary Tree（二叉树的序列化与反序列化）

**题目描述**：
设计一个算法，将二叉树序列化和反序列化。序列化是将树转换为字符串，反序列化是将字符串重构为二叉树。实现以下两个函数：
- `serialize(root)`：将树转换为字符串。
- `deserialize(data)`：将字符串重构为树。

**题目分析**：
可以使用前序遍历来进行序列化和反序列化。序列化时将 `None` 节点表示为一个特殊字符，如 `#`。反序列化时，根据字符串的顺序逐个重建节点，并递归重建左右子树。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Codec:
    # 序列化函数：将二叉树转换为字符串
    def serialize(self, root: TreeNode) -> str:
        def dfs(node):
            # 如果节点为空，返回 #
            if not node:
                return "#"
            # 返回当前节点的值，并递归处理左右子树
            return str(node.val) + "," + dfs(node.left) + "," + dfs(node.right)
        
        return dfs(root)

    # 反序列化函数：将字符串重构为二叉树
    def deserialize(self, data: str) -> TreeNode:
        # 将字符串分割为列表
        data_list = data.split(",")

        def dfs():
            # 获取当前值
            val = data_list.pop(0)
            # 如果值为 #，返回 None
            if val == "#":
                return None
            # 构建当前节点，并递归构建左右子树
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node

        return dfs()

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 存储序列化结果及递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，用于存储序列化结果的字符串及递归调用栈的开销。

---

### 20. LeetCode 102: Binary Tree Level Order Traversal（二叉树的层序遍历）

**题目描述**：
给定一个二叉树，返回其节点值的层序遍历结果（即逐层从左到右的遍历结果）。

**题目分析**：
可以使用广度优先搜索（BFS）来实现层序遍历。通过队列来逐层遍历每个节点，并将节点值按层级加入结果列表中。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义层序遍历的函数
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        # 如果根节点为空，返回空列表
        if not root:
            return []
        
        # 使用队列进行层次遍历
        queue = deque([root])
        result = []

        while queue:
            level = []
            level_size = len(queue)  # 当前层的节点数
            for _ in range(level_size):
                node = queue.popleft()  # 弹出队首节点
                level.append(node.val)  # 加入当前层的结果列表
                # 将左子节点加入队列
                if node.left:
                    queue.append(node.left)
                # 将右子节点加入队列
                if node.right:
                    queue.append(node.right)
            # 将当前层的结果加入总结果列表
            result.append(level)

        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最多队列中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，队列中可能包含所有节点。

---

### 21. LeetCode 129: Sum Root to Leaf Numbers（求根节点到叶节点数字之和）

**题目描述**：
给定一个二叉树，树中每个节点的值为 0 到 9 之间的数字。每条从根节点到叶节点的路径表示一个数字，将所有路径表示的数字相加，返回总和。

**题目分析**：
可以使用递归（DFS）或迭代来解题。在递归时记录当前节点到根节点的路径值，并在到达叶子节点时将路径值累加到总和中。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义求根节点到叶节点数字之和的函数
    def sumNumbers(self, root: TreeNode) -> int:
        # 定义递归辅助函数
        def dfs(node, current_sum):
            # 如果当前节点为空，返回 0
            if not node:
                return 0
            # 更新当前路径值
            current_sum = current_sum * 10 + node.val
            # 如果当前节点是叶子节点，返回路径值
            if not node.left and not node.right:
                return current_sum
            # 递归累加左右子树的路径值
            return dfs(node.left, current_sum) + dfs(node.right, current_sum)

        # 调用递归函数计算总和
        return dfs(root, 0)

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n

)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 22. LeetCode 1448: Count Good Nodes in Binary Tree（统计二叉树中好节点的数目）

**题目描述**：
给定一棵二叉树，统计其中的“好节点”数目。一个节点被定义为“好节点”当且仅当在从根节点到该节点的路径中，节点值不小于路径中所有节点的值。

**题目分析**：
可以使用递归（DFS）来解决该问题。每次递归时，传递当前路径中的最大值，并在访问每个节点时判断该节点是否大于或等于当前路径中的最大值，从而统计好节点的数目。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义统计好节点数目的函数
    def goodNodes(self, root: TreeNode) -> int:
        # 定义递归辅助函数
        def dfs(node, max_val):
            # 如果当前节点为空，返回 0
            if not node:
                return 0
            # 统计当前节点是否为好节点
            good_node_count = 1 if node.val >= max_val else 0
            # 更新路径中的最大值
            max_val = max(max_val, node.val)
            # 递归统计左右子树中的好节点数目
            good_node_count += dfs(node.left, max_val)
            good_node_count += dfs(node.right, max_val)
            return good_node_count

        # 从根节点开始统计，初始最大值为根节点的值
        return dfs(root, root.val)

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

好的，我们继续讲解接下来的五道 LeetCode 树相关题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 23. LeetCode 513: Find Bottom Left Tree Value（找树左下角的值）

**题目描述**：
给定一个二叉树的根节点 `root`，请找出该二叉树中最底层最左边节点的值。

**题目分析**：
可以使用广度优先搜索（BFS）来逐层遍历树，每次都从左到右遍历每一层的节点，并记录每层第一个节点值。当遍历到最后一层时，第一个节点即为最左边节点的值。递归（DFS）也可以解决该问题，通过维护一个当前最大深度的变量，每次更新更深层次的左侧节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找树左下角节点值的函数
    def findBottomLeftValue(self, root: TreeNode) -> int:
        # 使用广度优先搜索（BFS）来遍历二叉树
        queue = deque([root])
        # 记录最后一层的最左节点值
        bottom_left_value = root.val
        
        while queue:
            # 遍历当前层的所有节点
            for _ in range(len(queue)):
                node = queue.popleft()
                # 更新最左侧节点值为当前节点值
                bottom_left_value = node.val
                # 将左子节点加入队列（先处理左子树）
                if node.left:
                    queue.append(node.left)
                # 将右子节点加入队列
                if node.right:
                    queue.append(node.right)

        # 返回最底层最左边节点的值
        return bottom_left_value

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最多队列中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，队列中可能包含所有节点。

---

### 24. LeetCode 987: Vertical Order Traversal of a Binary Tree（二叉树的垂序遍历）

**题目描述**：
给定一个二叉树的根节点 `root`，按照二叉树节点的垂直顺序遍历结果进行返回。每个节点的位置由它的水平距离和深度来确定。首先按水平距离排序，然后按深度排序，如果位置相同则按节点值排序。

**题目分析**：
可以通过深度优先搜索（DFS）或广度优先搜索（BFS）来遍历树，记录每个节点的水平距离和深度，并用一个字典来存储每个水平距离上的节点列表。最后按照字典键值的顺序来返回垂序遍历结果。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义二叉树的垂序遍历函数
    def verticalTraversal(self, root: TreeNode) -> List[List[int]]:
        # 使用字典记录每个水平距离对应的节点值
        col_table = defaultdict(list)
        # 使用队列进行广度优先遍历，记录节点及其水平距离和深度
        queue = deque([(root, 0, 0)])

        while queue:
            node, row, col = queue.popleft()
            # 将节点值按水平距离和深度存储到字典中
            if node:
                col_table[col].append((row, node.val))
                # 将左子节点加入队列（水平距离 - 1）
                queue.append((node.left, row + 1, col - 1))
                # 将右子节点加入队列（水平距离 + 1）
                queue.append((node.right, row + 1, col + 1))

        # 按水平距离排序并返回结果
        sorted_columns = sorted(col_table.keys())
        result = []
        for col in sorted_columns:
            # 对每个水平距离的节点按深度和值进行排序
            result.append([val for row, val in sorted(col_table[col])])

        return result

# 时间复杂度：O(n log n) - 排序操作占主要复杂度
# 空间复杂度：O(n) - 存储节点的水平距离和深度信息
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，主要复杂度来源于排序操作。
- **空间复杂度**：O(n)，字典用于存储每个水平距离的节点信息。

---

### 25. LeetCode 863: All Nodes Distance K in Binary Tree（二叉树中所有距离为 K 的节点）

**题目描述**：
给定一个二叉树的根节点 `root`、一个目标节点 `target` 和一个整数 `K`，返回所有与目标节点距离为 K 的节点值。

**题目分析**：
可以通过将二叉树转化为图来解决该问题。首先通过 DFS 记录每个节点的父节点信息，然后使用 BFS 从目标节点开始遍历，找到所有距离为 K 的节点。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找距离为 K 的所有节点的函数
    def distanceK(self, root: TreeNode, target: TreeNode, K: int) -> List[int]:
        # 定义父节点字典
        parent = {}

        # 记录每个节点的父节点
        def dfs(node, par=None):
            if node:
                parent[node] = par
                dfs(node.left, node)
                dfs(node.right, node)

        # 建立父节点关系
        dfs(root)

        # 使用队列进行广度优先搜索（BFS）
        queue = deque([(target, 0)])
        seen = {target}  # 记录已访问的节点
        result = []

        while queue:
            node, dist = queue.popleft()
            # 如果当前节点距离为 K，则加入结果列表
            if dist == K:
                result.append(node.val)
            # 否则继续遍历当前节点的邻居节点（左右子节点及父节点）
            for neighbor in (node.left, node.right, parent[node]):
                if neighbor and neighbor not in seen:
                    seen.add(neighbor)
                    queue.append((neighbor, dist + 1))

        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 存储父节点关系及队列中的节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，用于存储父节点关系及 BFS 队列中的节点。

---

### 26. LeetCode 508: Most Frequent Subtree Sum（出现次数最多的子树元素和）

**题目描述**：
给定一个二叉树的根节点 `root`，返回出现次数最多的子树元素和。子树元素和是指某个节点及其子树中所有节点值的和。

**题目分析**：
使用 DFS 递归遍历每个节点，计算每个节点的子树和，并使用哈希表记录每个子树和出现的次数。最后找出出现次数最多的子树和。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找出现次数最多的子树元素和的函数
    def findFrequentTreeSum(self, root: TreeNode) -> List[int]:
        # 如果根节点为空，返回空列表
        if not root:
            return []

        # 定义哈希表记录子树和的出现次数
        subtree_sum_count = defaultdict(int)
        max_count = 0

        # 定义递归计算子树和的函数
        def dfs(node):
            nonlocal max_count
            if not node:
                return 0
            # 计算当前节点的子树和
            subtree_sum = node.val + dfs(node.left) + dfs(node.right)
            # 更新子树和

出现的次数
            subtree_sum_count[subtree_sum] += 1
            # 更新最大出现次数
            max_count = max(max_count, subtree_sum_count[subtree_sum])
            return subtree_sum

        # 调用递归函数计算所有子树和
        dfs(root)

        # 找出所有出现次数等于最大次数的子树和
        return [s for s, count in subtree_sum_count.items() if count == max_count]

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 存储子树和的哈希表及递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，用于存储子树和的哈希表及递归调用栈的开销。

---

### 27. LeetCode 662: Maximum Width of Binary Tree（二叉树的最大宽度）

**题目描述**：
给定一个二叉树的根节点 `root`，返回该树的最大宽度。最大宽度是所有层中最宽的层的节点数目。

**题目分析**：
可以使用广度优先搜索（BFS）来遍历树，并使用一个队列记录节点的索引位置。每层宽度等于该层最右侧节点的索引减去最左侧节点的索引再加 1。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义计算二叉树最大宽度的函数
    def widthOfBinaryTree(self, root: TreeNode) -> int:
        # 如果根节点为空，返回 0
        if not root:
            return 0

        # 初始化最大宽度和队列，队列中记录节点和索引位置
        max_width = 0
        queue = deque([(root, 0)])

        while queue:
            # 当前层的节点数及第一个节点的索引位置
            level_length = len(queue)
            _, first_index = queue[0]

            # 遍历当前层的所有节点
            for _ in range(level_length):
                node, index = queue.popleft()
                # 计算相对于当前层第一个节点的相对索引位置
                if node.left:
                    queue.append((node.left, 2 * index))
                if node.right:
                    queue.append((node.right, 2 * index + 1))

            # 更新最大宽度（当前层最后一个节点的索引 - 第一个节点的索引 + 1）
            max_width = max(max_width, index - first_index + 1)

        return max_width

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最多队列中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，队列中可能包含所有节点。

---

好的，我们继续讲解接下来的五道 LeetCode 树相关题目，包括题目描述、逐行中文注释代码及复杂度分析。

---

### 28. LeetCode 230: Kth Smallest Element in a BST（二叉搜索树中第K小的元素）

**题目描述**：
给定一个二叉搜索树（BST），找到其中第 `k` 小的元素。

**题目分析**：
二叉搜索树具有左子树节点值小于根节点、右子树节点值大于根节点的特点，因此可以使用中序遍历（Inorder Traversal）来遍历二叉搜索树。中序遍历时的顺序即为节点值从小到大排列的顺序，因此可以在中序遍历时计数，当计数值等于 `k` 时，即找到了第 `k` 小的元素。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找第K小元素的函数
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        # 初始化计数器和结果变量
        self.k = k
        self.result = None

        # 定义中序遍历的递归函数
        def inorder(node):
            if not node or self.result is not None:
                return
            # 递归遍历左子树
            inorder(node.left)
            # 访问当前节点并计数
            self.k -= 1
            if self.k == 0:
                self.result = node.val
                return
            # 递归遍历右子树
            inorder(node.right)

        # 调用中序遍历函数
        inorder(root)
        return self.result

# 时间复杂度：O(n) - 最坏情况下遍历所有节点
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，在最坏情况下（完全不平衡树），可能需要遍历所有节点。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 29. LeetCode 98: Validate Binary Search Tree（验证二叉搜索树）

**题目描述**：
给定一个二叉树，判断其是否是一个有效的二叉搜索树（BST）。有效的 BST 定义如下：
1. 节点的左子树只包含小于当前节点的数。
2. 节点的右子树只包含大于当前节点的数。
3. 所有左子树和右子树自身也必须是二叉搜索树。

**题目分析**：
可以使用递归或中序遍历来验证二叉搜索树。递归方法中，每次递归时传递当前节点值的有效区间（min_val, max_val），并检查左右子树是否符合二叉搜索树的条件。中序遍历则通过遍历所有节点，并比较前一个节点和当前节点的值，判断是否符合递增顺序。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义判断是否为二叉搜索树的函数（递归法）
    def isValidBST(self, root: TreeNode) -> bool:
        # 定义递归函数
        def validate(node, low=-float('inf'), high=float('inf')):
            # 如果当前节点为空，返回 True
            if not node:
                return True
            # 如果当前节点值不在有效范围内，返回 False
            if not (low < node.val < high):
                return False
            # 递归检查左子树和右子树
            return (validate(node.left, low, node.val) and
                    validate(node.right, node.val, high))

        # 调用递归函数验证二叉搜索树
        return validate(root)

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。

---

### 30. LeetCode 103: Binary Tree Zigzag Level Order Traversal（二叉树的锯齿形层序遍历）

**题目描述**：
给定一个二叉树，返回其节点值的锯齿形层序遍历（zigzag level order）。即第一层从左到右，第二层从右到左，第三层再从左到右，依此类推。

**题目分析**：
可以使用广度优先搜索（BFS）来逐层遍历树，并根据当前层数（奇偶性）来决定本层的遍历方向。如果当前层数为奇数，则从右到左插入节点值；如果为偶数，则从左到右插入节点值。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义二叉树锯齿形层序遍历的函数
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        # 如果根节点为空，返回空列表
        if not root:
            return []
        
        # 使用队列进行广度优先遍历
        queue = deque([root])
        result = []
        left_to_right = True  # 标记当前层的遍历方向

        while queue:
            level = deque()  # 当前层的节点值列表
            for _ in range(len(queue)):
                node = queue.popleft()
                # 根据当前层的遍历方向插入节点值
                if left_to_right:
                    level.append(node.val)
                else:
                    level.appendleft(node.val)
                # 将左子节点加入队列
                if node.left:
                    queue.append(node.left)
                # 将右子节点加入队列
                if node.right:
                    queue.append(node.right)
            # 切换遍历方向
            left_to_right = not left_to_right
            # 将当前层的节点值列表加入结果
            result.append(list(level))

        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(n) - 最多队列中存储 n 个节点
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(n)，在最坏情况下，队列中可能包含所有节点。

---

### 31. LeetCode 113: Path Sum II（路径总和 II）

**题目描述**：
给定一个二叉树和一个目标和 `sum`，找到所有从根节点到叶子节点的路径，这些路径上的节点值相加等于目标和 `sum`。

**题目分析**：
可以使用递归（DFS）来解决该问题。每次递归时将当前节点值加入路径列表中，并在叶子节点检查路径值是否等于目标和 `sum`。如果满足条件，则将路径加入结果列表中。遍历结束后，移除当前节点值（回溯）。

**代码实现**：
```python
# 定义树的节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# 定义解决方案的类
class Solution:
    # 定义查找所有满足条件路径的函数
    def pathSum(self, root: TreeNode, target_sum: int) -> List[List[int]]:
        # 定义结果列表和当前路径列表
        result = []
        path = []

        # 定义递归函数
        def dfs(node, remaining_sum):
            if not node:
                return
            # 将当前节点值加入路径
            path.append(node.val)
            # 如果当前节点是叶子节点，且路径和等于目标和，加入结果列表
            if not node.left and not node.right and node.val == remaining_sum:
                result.append(list(path))
            else:
                # 递归遍历左子树和右子树
                dfs(node.left, remaining_sum - node.val)
                dfs(node.right, remaining_sum - node.val)
            # 回

溯：移除当前节点值
            path.pop()

        # 调用递归函数
        dfs(root, target_sum)
        return result

# 时间复杂度：O(n) - 每个节点被访问一次
# 空间复杂度：O(h) - h 为树的高度，递归调用栈的开销
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是树的节点数，每个节点只会被访问一次。
- **空间复杂度**：O(h)，其中 h 是树的高度，递归调用栈的最大深度。
