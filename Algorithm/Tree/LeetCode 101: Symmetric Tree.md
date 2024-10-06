以下是 LeetCode 问题 **"对称二叉树" (问题 101)** 的完整解决方案，包括详细的代码解释、示例执行和复杂度分析。

### LeetCode 问题：101. 对称二叉树

https://leetcode.com/problems/symmetric-tree/description/

#### 问题描述：
给定一个二叉树，检查它是否是镜像对称的。

#### 示例 1：
```python
输入：
    1
   / \
  2   2
 / \ / \
3  4 4  3
输出：true
```

#### 示例 2：
```python
输入：
    1
   / \
  2   2
   \   \
   3    3
输出：false
```

### 原始代码（递归方法）：

```python
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
```

### 行逐行解释与示例执行：

1. **`class Solution:`**
   - 定义 `Solution` 类。

2. **`def isSymmetric(self, root: TreeNode) -> bool:`**
   - 定义方法 `isSymmetric`，接受一个二叉树的根节点，并返回该树是否对称的布尔值。

3. **`if not root:`**
   - 检查根节点是否为空。如果为空，则树是对称的，返回 `True`。

4. **定义递归函数**：
   - **`def isMirror(left, right):`**
     - 定义内部递归函数 `isMirror`，用于检查两个子树是否镜像对称。

5. **检查子树为空的情况**：
   - **`if not left and not right:`**
     - 如果左右子树都为空，则它们是对称的，返回 `True`。

6. **检查子树不对称的情况**：
   - **`if not left or not right:`**
     - 如果其中一个子树为空而另一个不为空，则它们不对称，返回 `False`。

7. **检查节点值是否相同**：
   - **`if left.val != right.val:`**
     - 如果左右子树的值不同，则它们不对称，返回 `False`。

8. **递归检查子树**：
   - **`return isMirror(left.left, right.right) and isMirror(left.right, right.left)`**
     - 递归检查左子树的左节点和右子树的右节点，以及左子树的右节点和右子树的左节点是否对称。

9. **调用递归函数**：
   - **`return isMirror(root.left, root.right)`**
     - 调用 `isMirror` 函数来判断根节点的左子树和右子树是否对称。

### 示例执行：

假设我们有以下输入：

```python
输入：
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

1. **初始调用**：
   - 调用 `isSymmetric`，根节点为 `1`。
   - 检查左子树 `2` 和右子树 `2` 是否对称。

2. **第一层递归**：
   - 对于左子树 `2` 和右子树 `2`：
     - 两者值相同，继续递归检查：
       - 左子树的左节点 `3` 和右子树的右节点 `3`。
       - 左子树的右节点 `4` 和右子树的左节点 `4`。

3. **第二层递归**：
   - 对于 `3` 和 `3`：
     - 两者值相同，继续递归检查：
       - 左右子树均为空，返回 `True`。
   - 对于 `4` 和 `4`：
     - 两者值相同，继续递归检查：
       - 左右子树均为空，返回 `True`。

4. **最终结果**：
   - 由于所有检查均返回 `True`，因此树是对称的，最终返回 `True`。

### 时间复杂度分析：

- **时间复杂度**：O(n)
  - 每个节点仅被访问一次，因此时间复杂度为 O(n)，其中 n 是树中的节点数量。

### 空间复杂度分析：

- **空间复杂度**：O(h)
  - 其中 h 是树的高度。递归调用栈的深度为 h。

### 提示和警告：

1. **边界情况**：
   - 考虑根节点为空或只有一个节点的情况。

2. **理解递归**：
   - 确保理解如何根据左右子树检查对称的逻辑。

3. **效率**：
   - 此方法有效地检查二叉树的对称性，利用递归结构使得实现简单明了。

### 总结

- **递归方法**：有效地检查二叉树的对称性，时间复杂度为 O(n)，空间复杂度为 O(h)。
- **清晰易懂**：代码简洁明了，适合处理此类问题。

### 应用技巧

1. **选择合适的方法**：
   - 根据具体问题选择最合适的方法，以确保算法的效率和可读性。

2. **处理边界情况**：
   - 在算法设计中，始终考虑处理输入数据的边界情况。

3. **优化空间使用**：
   - 在处理大数据时，考虑使用更节省空间的算法。
