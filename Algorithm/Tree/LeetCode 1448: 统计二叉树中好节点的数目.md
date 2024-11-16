### LeetCode 1448: 统计二叉树中好节点的数目 (Count Good Nodes in Binary Tree)  

https://leetcode.com/problems/count-good-nodes-in-binary-tree/

#### **题目描述**：
给定一个二叉树，如果从根节点到某个节点的路径中，该节点的值大于或等于路径上所有节点的值，则称该节点为**好节点**。返回树中好节点的总数。

---

#### 示例输入输出：

**输入**：
```plaintext
        3
       / \
      1   4
     /   / \
    3   1   5
```

**输出**：
```plaintext
4
```

**解释**：
- 好节点包括：根节点 `3`，左子树节点 `3`，右子树节点 `4` 和 `5`。

---

### **Python 实现代码**：

```python
# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        # 定义深度优先搜索 (DFS) 的辅助函数
        def dfs(node, max_val):
            if not node:
                return 0
            
            # 判断当前节点是否是好节点
            good = 1 if node.val >= max_val else 0
            
            # 更新路径上的最大值
            max_val = max(max_val, node.val)
            
            # 递归遍历左子树和右子树，累加好节点数量
            good += dfs(node.left, max_val)
            good += dfs(node.right, max_val)
            
            return good
        
        # 从根节点开始 DFS，初始最大值为根节点值
        return dfs(root, root.val)

# 示例调用
root = TreeNode(3)
root.left = TreeNode(1)
root.right = TreeNode(4)
root.left.left = TreeNode(3)
root.right.left = TreeNode(1)
root.right.right = TreeNode(5)

solution = Solution()
print(solution.goodNodes(root))  # 输出: 4
```

---

### **代码逐行解析**：

1. **定义二叉树节点类**：
   ```python
   class TreeNode:
       def __init__(self, val=0, left=None, right=None):
           self.val = val
           self.left = left
           self.right = right
   ```
   - `TreeNode` 类用于表示二叉树的每个节点。
   - 包含节点值 `val` 和左右子节点 `left` 和 `right`。

2. **定义 DFS 辅助函数**：
   ```python
   def dfs(node, max_val):
       if not node:
           return 0
   ```
   - 如果当前节点为空，直接返回 `0`。
   - `max_val` 记录从根节点到当前节点路径上的最大值。

3. **判断当前节点是否是好节点**：
   ```python
   good = 1 if node.val >= max_val else 0
   ```
   - 如果当前节点值大于或等于路径上的最大值，则是好节点，计数为 `1`。

4. **更新路径最大值**：
   ```python
   max_val = max(max_val, node.val)
   ```

5. **递归遍历左右子树**：
   ```python
   good += dfs(node.left, max_val)
   good += dfs(node.right, max_val)
   ```
   - 累加左子树和右子树中的好节点数量。

6. **从根节点开始 DFS**：
   ```python
   return dfs(root, root.val)
   ```
   - 以根节点值作为初始路径最大值，开始递归。

---

### **时间复杂度分析 (Big O)**：

- **时间复杂度**：  
  O(N)，其中 `N` 是二叉树的节点数量。每个节点被访问一次。

- **空间复杂度**：  
  O(H)，其中 `H` 是树的高度，用于递归调用栈。

---

### **示例运行讲解**：

**输入**：
```plaintext
        3
       / \
      1   4
     /   / \
    3   1   5
```

#### 运行过程：
1. 从根节点 `3` 开始，`max_val = 3`，是好节点，计数为 `1`。
   
2. 遍历左子树：
   - 节点 `1`，`max_val = 3`，不是好节点，计数不变。
   - 节点 `3`，`max_val = 3`，是好节点，计数增加到 `2`。

3. 遍历右子树：
   - 节点 `4`，`max_val = 3`，是好节点，计数增加到 `3`。
   - 节点 `1`，`max_val = 4`，不是好节点，计数不变。
   - 节点 `5`，`max_val = 4`，是好节点，计数增加到 `4`。

#### 最终结果：
```plaintext
4
```

---

### **是否有更好的方法？**

#### 1. **改进方式：使用迭代 DFS**

可以使用栈模拟 DFS，从而避免递归栈溢出的问题：

```python
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        stack = [(root, root.val)]  # 初始化栈，存储节点和路径最大值
        count = 0
        
        while stack:
            node, max_val = stack.pop()
            if node:
                # 判断是否是好节点
                if node.val >= max_val:
                    count += 1
                
                # 更新路径最大值，并将左右子节点加入栈
                max_val = max(max_val, node.val)
                stack.append((node.right, max_val))
                stack.append((node.left, max_val))
        
        return count
```

---

### **DFS 和 迭代 DFS 方法的比较**：

| 方法             | 时间复杂度 | 空间复杂度 | 特点                   |
| ---------------- | ---------- | ---------- | ---------------------- |
| 递归 DFS         | O(N)       | O(H)       | 实现简单，适用于较小树 |
| 迭代 DFS (栈模拟) | O(N)       | O(H)       | 避免递归栈溢出问题     |

---

### **总结**：

1. 递归 DFS 和迭代 DFS 都适用于该问题，选择哪种方法取决于实际需求。
2. 本题重点是沿路径传递最大值，判断当前节点是否是好节点。

最终结果：
```plaintext
4
```
