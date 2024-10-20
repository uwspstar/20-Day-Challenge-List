### LeetCode 98: Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

---

### 题目描述：

给定一个二叉树的根节点 `root`，判断该树是否是一个有效的二叉搜索树（BST）。

一个二叉搜索树（BST）定义如下：
- 节点的左子树只包含小于当前节点值的节点。
- 节点的右子树只包含大于当前节点值的节点。
- 左子树和右子树都必须也是二叉搜索树。

#### 示例：

```python
输入: root = [2,1,3]
输出: True
```

```python
输入: root = [5,1,4,null,null,3,6]
输出: False
解释: 节点值 4 的右子节点是 3，不满足 BST 条件。
```

---

### 解题思路：

可以通过**递归**的方法验证每个节点的值是否在合法范围内。对于一个有效的 BST，在遍历树的过程中，需要确保：
1. **左子树**中的所有节点值小于当前节点的值。
2. **右子树**中的所有节点值大于当前节点的值。

#### 具体步骤：

1. 从根节点开始，初始化一个范围 `[low, high]`，表示当前节点的合法取值范围。
2. 如果当前节点为空，则返回 `True`，表示这是一个空树，满足 BST 条件。
3. 如果当前节点的值不在 `[low, high]` 范围内，则返回 `False`，表示不满足 BST 条件。
4. 递归检查左子树和右子树：
   - 左子树的范围更新为 `[low, root.val]`，即左子树所有节点值必须小于当前节点的值。
   - 右子树的范围更新为 `[root.val, high]`，即右子树所有节点值必须大于当前节点的值。
5. 如果左右子树都满足条件，则返回 `True`。

---

### 代码实现（附详细注释）：

```python
from typing import Optional

# 定义树节点
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        # 辅助函数：递归检查当前节点是否在合法范围内
        def valid(root, low=float("-inf"), high=float("inf")):
            # 如果当前节点为空，返回 True
            if not root:
                return True
            
            # 如果当前节点的值不在合法范围内，返回 False
            if not (low < root.val < high):
                return False

            # 递归检查左子树和右子树
            # 左子树：合法范围是 [low, root.val]
            # 右子树：合法范围是 [root.val, high]
            return valid(root.left, low, root.val) and valid(root.right, root.val, high)
        
        # 调用辅助函数检查根节点
        return valid(root)
```

---

### 代码解释：

1. **初始化辅助函数 `valid`**：
   - 这个函数接受三个参数：当前节点 `root`，当前节点值的下界 `low` 和上界 `high`。
   - 初始情况下，`low` 为负无穷大，`high` 为正无穷大。

2. **检查空节点**：
   - 如果当前节点为空，则直接返回 `True`，表示空树是有效的 BST。

3. **检查节点值的合法性**：
   - 如果当前节点的值不在范围 `[low, high]` 内，则返回 `False`，因为不满足 BST 条件。

4. **递归检查左右子树**：
   - 对于左子树，更新上界为当前节点的值 `root.val`，表示左子树所有节点的值必须小于当前节点的值。
   - 对于右子树，更新下界为当前节点的值 `root.val`，表示右子树所有节点的值必须大于当前节点的值。

5. **返回结果**：
   - 如果左右子树都满足条件，则返回 `True`，否则返回 `False`。

---

### 复杂度分析：

- **时间复杂度**：O(n)，其中 `n` 是树中节点的数量。每个节点最多访问一次。
- **空间复杂度**：O(n)，最坏情况下递归栈的深度是树的高度。

---

### 示例分析：

#### 示例 1：

```python
输入: root = [2, 1, 3]
```

- 节点 2 的左子树节点 1 小于 2，右子树节点 3 大于 2。
- 满足 BST 条件，返回 `True`。

#### 示例 2：

```python
输入: root = [5, 1, 4, null, null, 3, 6]
```

- 节点 4 的右子节点是 3，不满足 BST 条件（3 应该在 5 的左侧）。
- 返回 `False`。

---

### 总结：

通过递归遍历树并维护合法的取值范围，可以有效地判断二叉树是否是一个有效的二叉搜索树。这种方法利用了 BST 的定义，保证了每个节点及其子树都满足 BST 条件。
