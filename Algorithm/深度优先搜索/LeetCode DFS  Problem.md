| No. | LeetCode Problem | Description |
| --- | ---------------- | ----------- |
| 1   | [LeetCode 94: Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) | 使用 DFS 进行二叉树的中序遍历。 |
| 2   | [LeetCode 98: Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) | 使用 DFS 验证是否为二叉搜索树。 |
| 3   | [LeetCode 100: Same Tree](https://leetcode.com/problems/same-tree/) | 使用 DFS 判断两棵树是否相同。 |
| 4   | [LeetCode 101: Symmetric Tree](https://leetcode.com/problems/symmetric-tree/) | 使用 DFS 判断二叉树是否对称。 |
| 5   | [LeetCode 104: Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | 使用 DFS 计算二叉树的最大深度。 |
| 6   | [LeetCode 110: Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) | 使用 DFS 判断二叉树是否平衡。 |
| 7   | [LeetCode 111: Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) | 使用 DFS 计算二叉树的最小深度。 |
| 8   | [LeetCode 112: Path Sum](https://leetcode.com/problems/path-sum/) | 使用 DFS 检查是否存在从根节点到叶子节点的路径总和为给定值。 |
| 9   | [LeetCode 113: Path Sum II](https://leetcode.com/problems/path-sum-ii/) | 使用 DFS 找到所有路径总和等于给定值的路径。 |
| 10  | [LeetCode 124: Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) | 使用 DFS 找到二叉树的最大路径和。 |
| 11  | [LeetCode 129: Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/) | 使用 DFS 计算从根到叶子节点形成的所有数字之和。 |
| 12  | [LeetCode 144: Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/) | 使用 DFS 进行二叉树的前序遍历。 |
| 13  | [LeetCode 145: Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/) | 使用 DFS 进行二叉树的后序遍历。 |
| 14  | [LeetCode 199: Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) | 使用 DFS 获取二叉树的右视图。 |
| 15  | [LeetCode 222: Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/) | 使用 DFS 计算完全二叉树的节点数。 |
| 16  | [LeetCode 230: Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) | 使用 DFS 在二叉搜索树中找到第 K 小的元素。 |
| 17  | [LeetCode 236: Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) | 使用 DFS 找到二叉树中两个节点的最近公共祖先。 |
| 18  | [LeetCode 257: Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/) | 使用 DFS 找出所有从根到叶子节点的路径。 |
| 19  | [LeetCode 337: House Robber III](https://leetcode.com/problems/house-robber-iii/) | 使用 DFS 解决在树状结构中的打家劫舍问题。 |
| 20  | [LeetCode 404: Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/) | 使用 DFS 计算左叶子节点之和。 |
| 21  | [LeetCode 437: Path Sum III](https://leetcode.com/problems/path-sum-iii/) | 使用 DFS 找出路径总和等于给定值的所有路径。 |
| 22  | [LeetCode 508: Most Frequent Subtree Sum](https://leetcode.com/problems/most-frequent-subtree-sum/) | 使用 DFS 找出子树和出现频率最高的值。 |
| 23  | [LeetCode 513: Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value/) | 使用 DFS 找到二叉树最底层最左边的节点值。 |
| 24  | [LeetCode 543: Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) | 使用 DFS 找出二叉树的直径。 |
| 25  | [LeetCode 572: Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/) | 使用 DFS 判断一棵树是否是另一棵树的子树。 |
| 26  | [LeetCode 617: Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/) | 使用 DFS 合并两棵二叉树。 |
| 27  | [LeetCode 662: Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/) | 使用 DFS 找出二叉树的最大宽度。 |
| 28  | [LeetCode 687: Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/) | 使用 DFS 找出最长同值路径。 |
| 29  | [LeetCode 863: All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) | 使用 DFS 找出二叉树中距离为 K 的所有节点。 |
| 30  | [LeetCode 968: Binary Tree Cameras](https://leetcode.com/problems/binary-tree-cameras/) | 使用 DFS 计算监控所有节点所需的最小摄像头数量。 |

---

### LeetCode 94: Binary Tree Inorder Traversal（中序遍历二叉树）
[LeetCode 94](https://leetcode.com/problems/binary-tree-inorder-traversal/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode]):
            if not node:
                return
            
            # 递归遍历左子树
            dfs(node.left)
            # 处理当前节点
            result.append(node.val)
            # 递归遍历右子树
            dfs(node.right)

        dfs(root)
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 最坏情况下，递归栈的深度为 O(n)（树的高度），存储结果列表的空间也为 O(n)。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited exactly once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - The space required for the recursion stack can be up to O(n) in the worst case, and the result list requires O(n) space to store all node values.

---

### LeetCode 98: Validate Binary Search Tree（验证二叉搜索树）
[LeetCode 98](https://leetcode.com/problems/validate-binary-search-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def dfs(node: Optional[TreeNode], lower=float('-inf'), upper=float('inf')) -> bool:
            if not node:
                return True
            
            val = node.val
            # 检查当前节点值是否在范围内
            if val <= lower or val >= upper:
                return False
            
            # 递归检查右子树
            if not dfs(node.right, val, upper):
                return False
            # 递归检查左子树
            if not dfs(node.left, lower, val):
                return False
            
            return True

        return dfs(root)

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 100: Same Tree（相同的树）
[LeetCode 100](https://leetcode.com/problems/same-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # 如果两棵树都为空，返回 True
        if not p and not q:
            return True
        # 如果只有一棵树为空或值不同，返回 False
        if not p or not q or p.val != q.val:
            return False
        
        # 递归检查左右子树是否相同
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是两棵树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the trees.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 101: Symmetric Tree（对称二叉树）
[LeetCode 101](https://leetcode.com/problems/symmetric-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        # 定义内部函数用于 DFS
        def dfs(left: Optional[TreeNode], right: Optional[TreeNode]) -> bool:
            # 如果左右子树都为空，返回 True
            if not left and not right:
                return True
            # 如果只有一棵子树为空或值不同，返回 False
            if not left or not right or left.val != right.val:
                return False
            
            # 递归检查外侧和内侧子树
            return dfs(left.left, right.right) and dfs(left.right, right.left)

        return dfs(root, root)  # 从根节点开始检查

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 104: Maximum Depth of Binary Tree（二叉树的最大深度）
[LeetCode 104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        # 递归计算左右子树的最大深度
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        
        # 返回左右子树深度的最大值加 1
        return max(left_depth, right_depth) + 1

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 110: Balanced Binary Tree（平衡二叉树）
[LeetCode 110](https://leetcode.com/problems/balanced-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            
            left_depth = dfs(node.left)
            right_depth = dfs(node.right)
            
            # 如果左右子树不平衡或当前子树不平衡，返回 -1
            if left_depth == -1 or right_depth == -1 or abs(left_depth - right_depth) > 1:
                return -1
            
            return max(left_depth, right_depth) + 1

        # 通过 DFS 判断树是否平衡
        return dfs(root) != -1

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 112: Path Sum（路径总和）
[LeetCode 112](https://leetcode.com/problems/path-sum/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False

        # 如果是叶子节点，判断路径总和是否满足目标
        if not root.left and not root.right:
            return targetSum == root.val

        # 递归检查左右子树是否存在满足条件的路径
        return (self.hasPathSum(root.left, targetSum - root.val) or
                self.hasPathSum(root.right, targetSum - root.val))

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 113: Path Sum II（路径总和 II）
[LeetCode 113](https://leetcode.com/problems/path-sum-ii/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode], current_path: List[int], current_sum: int):
            if not node:
                return
            
            # 更新当前路径和
            current_path.append(node.val)
            current_sum += node.val
            
            # 如果是叶子节点且路径总和等于目标值，加入结果
            if not node.left and not node.right and current_sum == targetSum:
                result.append(list(current_path))
            
            # 递归遍历左右子树
            dfs(node.left, current_path, current_sum)
            dfs(node.right, current_path, current_sum)
            
            # 回溯，移除当前节点
            current_path.pop()

        dfs(root, [], 0)
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈和存储路径的列表在最坏情况下可能为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and the path list can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 124: Binary Tree Maximum Path Sum（二叉树中的最大路径和）
[LeetCode 124](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        max_sum = float('-inf')  # 初始化最大路径和

        def dfs(node: Optional[TreeNode]) -> int:
            nonlocal max_sum
            if not node:
                return 0
            
            # 递归计算左右子树的贡献值，若为负则置 0
            left_gain = max(dfs(node.left), 0)
            right_gain = max(dfs(node.right), 0)
            
            # 更新最大路径和
            current_path_sum = node.val + left_gain + right_gain
            max_sum = max(max_sum, current_path_sum)
            
            # 返回当前节点的最大贡献值
            return node.val + max(left_gain, right_gain)

        dfs(root)
        return max_sum

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 129: Sum Root to Leaf Numbers（从根到叶节点数字之和）
[LeetCode 129](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        def dfs(node: Optional[TreeNode], current_sum: int) -> int:
            if not node:
                return 0
            
            # 更新当前路径和
            current_sum = current_sum * 10 + node.val
            
            # 如果是叶子节点，返回当前路径和
            if not node.left and not node.right:
                return current_sum
            
            # 递归计算左右子树的路径和
            return dfs(node.left, current_sum) + dfs(node.right, current_sum)

        return dfs(root, 0)

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 144: Binary Tree Preorder Traversal（前序遍历二叉树）
[LeetCode 144](https://leetcode.com/problems/binary-tree-preorder-traversal/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode]):
            if not node:
                return
            
            # 处理当前节点
            result.append(node.val)
            # 递归遍历左子树
            dfs(node.left)
            # 递归遍历右子树
            dfs(node.right)

        dfs(root)
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

I'll continue providing solutions for the DFS-related tree problems, maintaining the specified template:

### LeetCode 145: Binary Tree Postorder Traversal（后序遍历二叉树）
[LeetCode 145](https://leetcode.com/problems/binary-tree-postorder-traversal/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode]):
            if not node:
                return
            
            # 递归遍历左子树
            dfs(node.left)
            # 递归遍历右子树
            dfs(node.right)
            # 处理当前节点
            result.append(node.val)

        dfs(root)
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 199: Binary Tree Right Side View（二叉树的右视图）
[LeetCode 199](https://leetcode.com/problems/binary-tree-right-side-view/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode], depth: int):
            if not node:
                return
            
            # 如果当前深度等于结果列表长度，说明是该深度的第一个节点
            if depth == len(result):
                result.append(node.val)
            
            # 优先递归遍历右子树
            dfs(node.right, depth + 1)
            # 再递归遍历左子树
            dfs(node.left, depth + 1)

        dfs(root, 0)
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 222: Count Complete Tree Nodes（完全二叉树的节点个数）
[LeetCode 222](https://leetcode.com/problems/count-complete-tree-nodes/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        left_height = self.getHeight(root.left)
        right_height = self.getHeight(root.right)
        
        # 如果左子树和右子树高度相同，则左子树为满二叉树
        if left_height == right_height:
            return (1 << left_height) + self.countNodes(root.right)
        else:
            return (1 << right_height) + self.countNodes(root.left)

    def getHeight(self, node: Optional[TreeNode]) -> int:
        height = 0
        while node:
            height += 1
            node = node.left
        return height

# 时间复杂度：O(log^2 n)
# 1. 每次递归减少一半节点，高度计算为 O(log n)，总时间复杂度为 O(log^2 n)。
# 空间复杂度：O(log n)
# 1. 递归栈深度为 O(log n)，因为在每个递归中处理半棵树。
```

### Complexity Analysis
- **Time Complexity**: O(log² n)
  - Each recursive call processes half of the nodes, and computing the height takes O(log n), leading to O(log² n).
- **Space Complexity**: O(log n)
  - In the worst case, the recursion stack depth reaches O(log n) due to the binary search of the complete tree.

---

### LeetCode 230: Kth Smallest Element in a BST（二叉搜索树中第 K 小的元素）
[LeetCode 230](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        self.count = 0  # 节点计数
        self.result = None  # 结果变量

        def dfs(node: Optional[TreeNode]):
            if not node or self.result is not None:
                return
            
            # 递归遍历左子树
            dfs(node.left)
            # 更新计数并检查是否为第 k 小的元素
            self.count += 1
            if self.count == k:
                self.result = node.val
                return
            # 递归遍历右子树
            dfs(node.right)

        dfs(root)
        return self.result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉搜索树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - In the worst case, all nodes are visited once in the DFS traversal.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack depth reaches O(n), especially if the tree is skewed.

---

### LeetCode 236: Lowest Common Ancestor of a Binary Tree（二叉树的最近公共祖先）
[LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def lowestCommonAncestor(self, root: Optional[TreeNode], p: TreeNode, q: TreeNode) -> Optional[TreeNode]:
        # 如果到达叶节点或找到 p/q，返回当前节点
        if not root or root == p or root == q:
            return root

        # 递归查找左子树和右子树
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        # 如果 p 和 q 分别在左右子树中，当前节点为最近公共祖先
        if left and right:
            return root
        
        # 否则返回不为空的那个子树
        return left if left else right

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 257: Binary Tree Paths（二叉树的所有路径）
[LeetCode 257](https://leetcode.com/problems/binary-tree-paths/)

```python
from typing import List, Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        result = []  # 结果列表

        def dfs(node: Optional[TreeNode], path: str):
            if not node:
                return
            
            # 更新路径字符串
            path += str(node.val)
            
            # 如果是叶子节点，添加路径到结果中
            if not node.left and not node.right:
                result.append(path)
            else:
                # 递归遍历左右子树
                dfs(node.left, path + "->")
                dfs(node.right, path + "->")

        dfs(root, "")
        return result

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈和存储路径的字符串在最坏情况下可能为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and path string can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 337: House Robber III（打家劫舍 III）
[LeetCode 337](https://leetcode.com/problems/house-robber-iii/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rob(self, root: Optional[TreeNode]) -> int:
        def dfs(node: Optional[TreeNode]) -> (int, int):
            if not node:
                return (0, 0)
            
            # 递归计算左右子树的抢劫情况
            left = dfs(node.left)
            right = dfs(node.right)
            
            # 当前节点不抢时的最大值
            not_rob = max(left) + max(right)
            # 当前节点抢时的最大值
            rob = node.val + left[0] + right[0]
            
            return (not_rob, rob)

        return max(dfs(root))

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 404: Sum of Left Leaves（左叶子之和）
[LeetCode 404](https://leetcode.com/problems/sum-of-left-leaves/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        def dfs(node: Optional[TreeNode], is_left: bool) -> int:
            if not node:
                return 0

            # 如果是左叶子节点，返回节点值
            if not node.left and not node.right and is_left:
                return node.val
            
            # 递归计算左子树和右子树的左叶子和
            return dfs(node.left, True) + dfs(node.right, False)

        return dfs(root, False)

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n), especially if the tree is skewed.

---

### LeetCode 437: Path Sum III（路径总和 III）
[LeetCode 437](https://leetcode.com/problems/path-sum-iii/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        self.count = 0  # 路径计数
        prefix_sum = {0: 1}  # 前缀和字典

        def dfs(node: Optional[TreeNode], current_sum: int):
            if not node:
                return

            # 更新当前前缀和
            current_sum += node.val
            # 检查有多少条路径符合条件
            self.count += prefix_sum.get(current_sum - targetSum, 0)
            # 更新前缀和字典
            prefix_sum[current_sum] = prefix_sum.get(current_sum, 0) + 1
            
            # 递归计算左右子树
            dfs(node.left, current_sum)
            dfs(node.right, current_sum)
            
            # 回溯，减少当前节点的前缀和计数
            prefix_sum[current_sum] -= 1

        dfs(root, 0)
        return self.count

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈和前缀和字典在最坏情况下可能为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and prefix sum dictionary can reach a size of O(n).

---

### LeetCode 508: Most Frequent Subtree Sum（最频繁子树和）
[LeetCode 508](https://leetcode.com/problems/most-frequent-subtree-sum/)

```python
from typing import Optional, List
from collections import defaultdict

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def findFrequentTreeSum(self, root: Optional[TreeNode]) -> List[int]:
        sum_count = defaultdict(int)  # 子树和计数字典

        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            
            # 计算当前子树的和
            current_sum = node.val + dfs(node.left) + dfs(node.right)
            sum_count[current_sum] += 1  # 更新子树和计数
            return current_sum

        if not root:
            return []

        dfs(root)
        max_freq = max(sum_count.values())  # 找到最大频率
        return [s for s, count in sum_count.items() if count == max_freq]

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈和子树和计数字典在最坏情况下可能为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and subtree sum dictionary can reach a size of O(n).

---

### LeetCode 513: Find Bottom Left Tree Value（找树左下角的值）
[LeetCode 513](https://leetcode.com/problems/find-bottom-left-tree-value/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        max_depth = -1  # 最大深度
        bottom_left_val = root.val  # 左下角的值

        def dfs(node: Optional[TreeNode], depth: int):
            nonlocal max_depth, bottom_left_val
            if not node:
                return

            # 如果是新的最大深度，更新左下角的值
            if depth > max_depth:
                max_depth = depth
                bottom_left_val = node.val

            # 递归优先遍历左子树，再遍历右子树
            dfs(node.left, depth + 1)
            dfs(node.right, depth + 1)

        dfs(root, 0)
        return bottom_left_val

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 543: Diameter of Binary Tree（二叉树的直径）
[LeetCode 543](https://leetcode.com/problems/diameter-of-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        max_diameter = 0  # 最大直径

        def dfs(node: Optional[TreeNode]) -> int:
            nonlocal max_diameter
            if not node:
                return 0

            # 递归计算左右子树的深度
            left_depth = dfs(node.left)
            right_depth = dfs(node.right)

            # 更新最大直径
            max_diameter = max(max_diameter, left_depth + right_depth)

            # 返回当前节点的最大深度
            return max(left_depth, right_depth) + 1

        dfs(root)
        return max_diameter

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 572: Subtree of Another Tree（另一个树的子树）
[LeetCode 572](https://leetcode.com/problems/subtree-of-another-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False

        # 检查两棵树是否相同
        def is_same(tree1: Optional[TreeNode], tree2: Optional[TreeNode]) -> bool:
            if not tree1 and not tree2:
                return True
            if not tree1 or not tree2 or tree1.val != tree2.val:
                return False
            return is_same(tree1.left, tree2.left) and is_same(tree1.right, tree2.right)

        # 如果当前节点匹配，则返回 True；否则递归检查左右子树
        return is_same(root, subRoot) or self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

# 时间复杂度：O(n * m)
# 1. 对每个节点调用一次 is_same 函数，其中 n 是 root 的节点数，m 是 subRoot 的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n * m)
  - For each node in the main tree, the function checks whether the subtree rooted at that node matches the subRoot tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 617: Merge Two Binary Trees（合并二叉树）
[LeetCode 617](https://leetcode.com/problems/merge-two-binary-trees/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 and not root2:
            return None

        # 计算新节点的值
        new_val = (root1.val if root1 else 0) + (root2.val if root2 else 0)
        new_node = TreeNode(new_val)

        # 递归合并左右子树
        new_node.left = self.mergeTrees(root1.left if root1 else None, root2.left if root2 else None)
        new_node.right = self.mergeTrees(root1.right if root1 else None, root2.right if root2 else None)

        return new_node

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，其中 n 是两棵树节点数之和。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once, where n is the total number of nodes in both trees.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 662: Maximum Width of Binary Tree（二叉树的最大宽度）
[LeetCode 662](https://leetcode.com/problems/maximum-width-of-binary-tree/)

```python
from typing import Optional
from collections import deque

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def widthOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        max_width = 0
        queue = deque([(root, 0)])  # 队列中存储节点和其索引

        while queue:
            level_length = len(queue)
            _, first_index = queue[0]  # 当前层第一个节点的索引

            for _ in range(level_length):
                node, index = queue.popleft()
                # 将左右子节点添加到队列中
                if node.left:
                    queue.append((node.left, 2 * index))
                if node.right:
                    queue.append((node.right, 2 * index + 1))
            
            # 更新最大宽度
            max_width = max(max_width, index - first_index + 1)

        return max_width

# 时间复杂度：O(n)
# 1. 每个节点在 BFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 队列的最大长度可能达到 O(n)。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the BFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - The maximum width of the queue can be O(n) in the worst case.

---

### LeetCode 687: Longest Univalue Path（最长同值路径）
[LeetCode 687](https://leetcode.com/problems/longest-univalue-path/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def longestUnivaluePath(self, root: Optional[TreeNode]) -> int:
        max_length = 0

        def dfs(node: Optional[TreeNode]) -> int:
            nonlocal max_length
            if not node:
                return 0

            # 递归计算左右子树的同值路径长度
            left_length = dfs(node.left)
            right_length = dfs(node.right)

            # 计算当前节点的同值路径长度
            left_univalue = left_length + 1 if node.left and node.left.val == node.val else 0
            right_univalue = right_length + 1 if node.right and node.right.val == node.val else 0

            # 更新最大同值路径长度
            max_length = max(max_length, left_univalue + right_univalue)

            return max(left_univalue, right_univalue)

        dfs(root)
        return max_length

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 863: All Nodes Distance K in Binary Tree（二叉树中距离为 K 的所有节点）
[LeetCode 863](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

```python
from typing import Optional, List
from collections import defaultdict, deque

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def distanceK(self, root: Optional[TreeNode], target: TreeNode, k: int) -> List[int]:
        if not root:
            return []
        
        # 构建无向图
        graph = defaultdict(list)

        def build_graph(node: Optional[TreeNode], parent: Optional[TreeNode]):
            if not node:
                return
            
            if parent:
                graph[node.val].append(parent.val)
                graph[parent.val].append(node.val)
            
            build_graph(node.left, node)
            build_graph(node.right, node)

        build_graph(root, None)

        # BFS 从目标节点开始
        queue = deque([(target.val, 0)])
        visited = {target.val}
        result = []

        while queue:
            node, dist = queue.popleft()
            
            if dist == k:
                result.append(node)
            
            if dist < k:
                for neighbor in graph[node]:
                    if neighbor not in visited:
                        visited.add(neighbor)
                        queue.append((neighbor, dist + 1))

        return result

# 时间复杂度：O(n)
# 1. 构建图和 BFS 遍历的时间复杂度均为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 无向图、队列和递归栈在最坏情况下可能达到 O(n) 的大小。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Constructing the graph and BFS traversal both require O(n), where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the graph, queue, and recursion stack can all take up to O(n) space.

---

### LeetCode 968: Binary Tree Cameras（二叉树摄像头）
[LeetCode 968](https://leetcode.com/problems/binary-tree-cameras/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def minCameraCover(self, root: Optional[TreeNode]) -> int:
        self.cameras = 0

        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 2  # 节点为空，视为已覆盖
            
            left = dfs(node.left)
            right = dfs(node.right)

            # 如果左右子节点有任一未覆盖，当前节点需要安装摄像头
            if left == 0 or right == 0:
                self.cameras += 1
                return 1  # 当前节点安装摄像头
            
            # 如果左右子节点已覆盖，当前节点视为未覆盖
            return 2 if left == 1 or right == 1 else 0

        # 如果根节点未被覆盖，安装摄像头
        if dfs(root) == 0:
            self.cameras += 1

        return self.cameras

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 1048: Longest String Chain（最长字符串链）
[LeetCode 1048](https://leetcode.com/problems/longest-string-chain/)

```python
from typing import List

class Solution:
    def longestStrChain(self, words: List[str]) -> int:
        words.sort(key=len)  # 按字符串长度排序
        dp = {}  # 动态规划字典

        max_length = 1

        for word in words:
            dp[word] = 1

            # 遍历去掉每个字符后的前驱字符串
            for i in range(len(word)):
                predecessor = word[:i] + word[i+1:]
                if predecessor in dp:
                    dp[word] = max(dp[word], dp[predecessor] + 1)

            max_length = max(max_length, dp[word])

        return max_length

# 时间复杂度：O(n * m^2)
# 1. n 是单词数，m 是单词的平均长度；在每个单词上检查 m 个前驱字符串。
# 空间复杂度：O(n * m)
# 1. 动态规划字典和字符串存储需要 O(n * m) 的空间。
```

### Complexity Analysis
- **Time Complexity**: O(n * m²)
  - For each word, checking all its possible predecessors takes O(m²), where n is the number of words and m is the average length of the words.
- **Space Complexity**: O(n * m)
  - The dynamic programming dictionary can store up to O(n * m) strings.

---

### LeetCode 1245: Tree Diameter（树的直径）
[LeetCode 1245](https://leetcode.com/problems/tree-diameter/)

```python
from typing import List
from collections import defaultdict

class Solution:
    def treeDiameter(self, edges: List[List[int]]) -> int:
        graph = defaultdict(list)

        # 构建无向图
        for u, v in edges:
            graph[u].append(v)
            graph[v].append(u)

        def dfs(node: int, parent: int) -> int:
            depths = [0, 0]

            for neighbor in graph[node]:
                if neighbor == parent:
                    continue
                depth = dfs(neighbor, node) + 1
                depths.append(depth)
                depths.sort(reverse=True)
                depths = depths[:2]

            # 更新最大直径
            self.max_diameter = max(self.max_diameter, sum(depths))
            return depths[0]

        self.max_diameter = 0
        dfs(0, -1)
        return self.max_diameter

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，其中 n 是树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈和无向图在最坏情况下可能为 O(n)。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and the graph can take up to O(n) space.

---

### LeetCode 979: Distribute Coins in Binary Tree（二叉树中的硬币分配）
[LeetCode 979](https://leetcode.com/problems/distribute-coins-in-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def distributeCoins(self, root: Optional[TreeNode]) -> int:
        self.moves = 0  # 记录移动次数

        def dfs(node: Optional[TreeNode]) -> int:
            if not node:
                return 0

            # 递归计算左右子树的硬币余额
            left_balance = dfs(node.left)
            right_balance = dfs(node.right)

            # 更新移动次数
            self.moves += abs(left_balance) + abs(right_balance)

            # 返回当前节点的硬币余额
            return node.val + left_balance + right_balance - 1

        dfs(root)
        return self.moves

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 1448: Count Good Nodes in Binary Tree（统计二叉树中好节点的数目）
[LeetCode 1448](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)

```python
from typing import Optional

# 定义二叉树的节点结构
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def goodNodes(self, root: Optional[TreeNode]) -> int:
        def dfs(node: Optional[TreeNode], max_val: int) -> int:
            if not node:
                return 0

            # 判断当前节点是否为好节点
            good = 1 if node.val >= max_val else 0

            # 更新最大值
            max_val = max(max_val, node.val)

            # 递归计算左右子树的好节点数
            good += dfs(node.left, max_val)
            good += dfs(node.right, max_val)

            return good

        return dfs(root, root.val if root else float('-inf'))

# 时间复杂度：O(n)
# 1. 每个节点在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是二叉树的节点数。
# 空间复杂度：O(n)
# 1. 递归栈的深度最坏情况下为 O(n)，特别是在树为链状结构时。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each node is visited once in the DFS traversal, where n is the total number of nodes in the tree.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack can reach a depth of O(n).

---

### LeetCode 1376: Time Needed to Inform All Employees（通知所有员工所需的时间）
[LeetCode 1376](https://leetcode.com/problems/time-needed-to-inform-all-employees/)

```python
from typing import List
from collections import defaultdict

class Solution:
    def numOfMinutes(self, n: int, headID: int, manager: List[int], informTime: List[int]) -> int:
        # 构建下属关系图
        subordinates = defaultdict(list)
        for i, m in enumerate(manager):
            if m != -1:
                subordinates[m].append(i)

        def dfs(employee: int) -> int:
            # 递归计算下属的通知时间
            max_time = 0
            for subordinate in subordinates[employee]:
                max_time = max(max_time, dfs(subordinate))

            # 返回当前员工的总通知时间
            return max_time + informTime[employee]

        return dfs(headID)

# 时间复杂度：O(n)
# 1. 每个员工在 DFS 中被访问一次，因此时间复杂度为 O(n)，其中 n 是员工数。
# 空间复杂度：O(n)
# 1. 递归栈和下属关系图在最坏情况下可能为 O(n)。
```

### Complexity Analysis
- **Time Complexity**: O(n)
  - Each employee is visited once in the DFS traversal, where n is the total number of employees.
- **Space Complexity**: O(n)
  - In the worst case, the recursion stack and the subordinates dictionary can reach a size of O(n).
