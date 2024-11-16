### LeetCode 199: 二叉树的右视图 (Binary Tree Right Side View)  
https://leetcode.com/problems/binary-tree-right-side-view/

#### **题目描述**：
给定一棵二叉树，返回从右侧观察到的节点值。每一层中，最右侧的节点会被记录下来。

---

#### 示例输入输出：

**输入**：
```plaintext
        1
       / \
      2   3
       \    \
        5    4
```

**输出**：
```plaintext
[1, 3, 4]
```

---

### **Python 实现代码**：

```python
from typing import List, Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        # 存储结果的列表
        res = []

        # 深度优先搜索 (DFS) 辅助函数
        def dfs(node, depth):
            if not node:  # 如果节点为空，直接返回
                return None
            
            # 如果当前深度的结果尚未记录，添加该节点的值
            if depth == len(res):
                res.append(node.val)

            # 优先遍历右子树
            dfs(node.right, depth + 1)
            # 然后遍历左子树
            dfs(node.left, depth + 1)

        # 从根节点开始深度优先搜索
        dfs(root, 0)

        return res

# 示例调用
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.right = TreeNode(5)
root.right.right = TreeNode(4)

solution = Solution()
print(solution.rightSideView(root))  # 输出: [1, 3, 4]
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
   - `val` 是节点的值，`left` 和 `right` 是左子树和右子树的引用。

2. **初始化结果列表**：
   ```python
   res = []
   ```
   - 用于存储每一层右视图的节点值。

3. **定义 DFS 辅助函数**：
   ```python
   def dfs(node, depth):
       if not node:
           return None
   ```
   - 如果节点为空，直接返回。

4. **记录每层右侧节点值**：
   ```python
   if depth == len(res):
       res.append(node.val)
   ```
   - 每层的第一个访问到的节点值会被记录到结果中（即右视图）。

5. **优先遍历右子树**：
   ```python
   dfs(node.right, depth + 1)
   dfs(node.left, depth + 1)
   ```
   - 先遍历右子树，确保右侧的节点优先记录。
   - 再遍历左子树，以覆盖剩余层次。

6. **从根节点启动 DFS**：
   ```python
   dfs(root, 0)
   ```
   - 从根节点开始，以深度 `0` 开始递归。

7. **返回结果**：
   ```python
   return res
   ```
   - 返回记录的右视图节点值。

---

### **时间复杂度分析 (Big O)**：

- **时间复杂度**：  
  O(N)，其中 `N` 是树中节点的数量。每个节点被访问一次。

- **空间复杂度**：  
  O(H)，其中 `H` 是树的高度，用于递归调用栈。

---

### **示例运行讲解**：

**输入**：
```plaintext
        1
       / \
      2   3
       \    \
        5    4
```

#### 运行过程：
1. 从根节点 `1` 开始，深度为 `0`：
   - 当前深度等于结果列表长度，记录值 `1`。

2. 遍历右子树节点 `3`，深度为 `1`：
   - 当前深度等于结果列表长度，记录值 `3`。

3. 遍历右子树节点 `4`，深度为 `2`：
   - 当前深度等于结果列表长度，记录值 `4`。

4. 回溯并遍历左子树，节点 `2` 和 `5`：
   - 因为深度已经被记录，跳过值。

**最终结果**：
```plaintext
[1, 3, 4]
```

---

### **总结**：

1. 通过深度优先搜索 (DFS)，优先遍历右子树，确保右视图的节点值被优先记录。
2. 每层深度只记录一个节点，避免重复值。
3. 此解法高效，适用于大多数二叉树的右视图问题。

最终结果：
```plaintext
[1, 3, 4]
```

---

### 广度优先搜索的方法？

除了深度优先搜索 (DFS) 的方法外，还可以使用**广度优先搜索 (BFS)** 方法来解决二叉树的右视图问题。这种方法利用队列按层遍历树，在每一层中记录最后一个节点值，从而构造右视图。

以下是使用 BFS 的实现：

#### **Python 实现代码**：

```python
from typing import List, Optional
from collections import deque

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        # 如果根节点为空，直接返回空列表
        if not root:
            return []
        
        # 定义结果列表和队列
        res = []
        queue = deque([root])
        
        # 开始按层遍历
        while queue:
            level_size = len(queue)
            for i in range(level_size):
                node = queue.popleft()
                
                # 如果是该层的最后一个节点，加入结果
                if i == level_size - 1:
                    res.append(node.val)
                
                # 将左右子节点加入队列
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return res

# 示例调用
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.right = TreeNode(5)
root.right.right = TreeNode(4)

solution = Solution()
print(solution.rightSideView(root))  # 输出: [1, 3, 4]
```

---

### **代码逐行解析**：

1. **初始化队列**：
   ```python
   queue = deque([root])
   ```
   - 使用双端队列 `deque` 存储每一层的节点，从而实现按层遍历。

2. **按层遍历树**：
   ```python
   level_size = len(queue)
   ```
   - `level_size` 表示当前层的节点数量。

3. **记录每层最后一个节点值**：
   ```python
   if i == level_size - 1:
       res.append(node.val)
   ```
   - 在每一层的最后一个节点时，将其值加入结果列表。

4. **加入子节点**：
   ```python
   if node.left:
       queue.append(node.left)
   if node.right:
       queue.append(node.right)
   ```
   - 将当前节点的左右子节点加入队列，继续遍历下一层。

5. **返回结果**：
   ```python
   return res
   ```

---

### **时间复杂度分析 (Big O)**：

- **时间复杂度**：  
  O(N)，其中 `N` 是二叉树的节点数量。每个节点被访问一次。

- **空间复杂度**：  
  O(W)，其中 `W` 是二叉树的最大宽度。在最坏情况下，队列中会同时存储一层的所有节点。

---

### **与 DFS 方法的比较**：

| 方法         | 时间复杂度 | 空间复杂度 | 特点                  |
| ------------ | ---------- | ---------- | --------------------- |
| 深度优先搜索 (DFS) | O(N)       | O(H)       | 递归实现，空间消耗取决于树的高度 |
| 广度优先搜索 (BFS) | O(N)       | O(W)       | 使用队列，按层遍历，逻辑更直观   |

- **DFS 的优点**：
  - 更适合需要按特定深度递归操作的场景。
  - 实现简洁，递归思想自然。
  
- **BFS 的优点**：
  - 按层遍历，逻辑直观，每层的右视图节点更容易提取。
  - 不依赖递归栈，更适合树的高度较大的情况，避免栈溢出。

---

### **改进后的示例运行讲解**：

**输入**：
```plaintext
        1
       / \
      2   3
       \    \
        5    4
```

#### BFS 运行过程：
1. 初始化队列：`queue = [1]`，结果列表 `res = []`。
   
2. 第一层：
   - 遍历节点 `1`，记录右视图值：`res = [1]`。
   - 将左右子节点 `2, 3` 加入队列：`queue = [2, 3]`。

3. 第二层：
   - 遍历节点 `2` 和 `3`，记录右视图值：`res = [1, 3]`。
   - 将节点 `5` 和 `4` 加入队列：`queue = [5, 4]`。

4. 第三层：
   - 遍历节点 `5` 和 `4`，记录右视图值：`res = [1, 3, 4]`。

---

### **总结**：

1. BFS 方法更适合右视图问题，因为按层遍历可以自然地记录每一层的最后一个节点值。
2. 如果树较高或递归深度较深，BFS 比 DFS 更稳定。
3. 在实际使用中，可以根据问题需求选择 BFS 或 DFS。  

最终结果：  
```plaintext
[1, 3, 4]
```
