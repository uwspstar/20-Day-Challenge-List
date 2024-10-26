### DFS 在树上的模板概述

在树上的深度优先搜索（DFS）是一种常用的遍历技术，用于探索树的所有节点。下面的模板代表了 DFS 的标准结构，可以针对各种树问题进行适应性修改。

### 1. 模板解释

这是标准的 DFS 模板，并附有详细解释：

```python
def dfs(node, state):
    # 基本情况：如果节点为空，处理空情况并返回
    if node is None:
        # 处理空情况（例如返回基值，如 0、None 等）
        return

    # 对左子节点和右子节点进行递归调用
    left = dfs(node.left, state)   # 遍历左子树
    right = dfs(node.right, state)  # 遍历右子树

    # 后序处理：组合或使用左子树和右子树的结果
    # 这里执行主要逻辑，例如寻找最大值、累加值等
    # 示例：如果计算树的深度，返回 max(left, right) + 1

    return ...
```

### 2. 模板各部分解释

- **基本情况**：
  - 基本情况用于检查当前节点是否为 `None`。
  - 这一步是用来处理空情况（例如返回一个基值，如 `0` 用于计数，或空列表用于收集结果）。
  - 它是防止没有更多节点可以访问时继续递归调用的关键。

- **递归调用**：
  - **左子树**：`left = dfs(node.left, state)` – 递归调用遍历当前节点的左子树。
  - **右子树**：`right = dfs(node.right, state)` – 递归调用遍历当前节点的右子树。

- **后序处理**：
  - 在探索完左右子树之后，处理来自左、右子树的结果。
  - 这个步骤取决于具体问题。例如：
    - **寻找最大深度**：结合左右结果，`max(left, right) + 1`。
    - **计算总和**：使用 `left + right + node.val`。

### 3. DFS 变体

#### 前序 DFS（根，左，右）

在**前序 DFS**中，在遍历子节点之前处理当前节点。

```python
def dfs(node, state):
    if node is None:
        return

    # 前序处理
    state.append(node.val)  # 示例：收集节点值

    dfs(node.left, state)
    dfs(node.right, state)
```

#### 中序 DFS（左，根，右）

在**中序 DFS**中，在处理当前节点之前遍历左子树，在遍历右子树之前处理当前节点。

```python
def dfs(node, state):
    if node is None:
        return

    dfs(node.left, state)
    
    # 中序处理
    state.append(node.val)  # 示例：收集节点值

    dfs(node.right, state)
```

#### 后序 DFS（左，右，根）

在**后序 DFS**中，在遍历完子节点后处理当前节点。这种遍历通常用于计算节点总和、寻找直径等问题。

```python
def dfs(node, state):
    if node is None:
        return

    left = dfs(node.left, state)
    right = dfs(node.right, state)

    # 后序处理
    return ...  # 示例：返回 max(left, right) + 1
```

### 4. 示例：计算二叉树的最大深度

以下是使用 DFS 模板计算二叉树最大深度的示例。

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def maxDepth(root: TreeNode) -> int:
    # DFS 函数计算最大深度
    def dfs(node):
        if node is None:
            return 0
        
        left_depth = dfs(node.left)
        right_depth = dfs(node.right)

        # 返回左、右子树最大深度 + 1
        return max(left_depth, right_depth) + 1

    return dfs(root)

# 示例用法：
# 构建二叉树：[3, 9, 20, None, None, 15, 7]
root = TreeNode(3)
root.left = TreeNode(9)
root.right = TreeNode(20, TreeNode(15), TreeNode(7))
print(maxDepth(root))  # 输出: 3
```

### 5. 示例：计算二叉树节点的总和

使用相同的 DFS 模板，以下是计算二叉树所有节点总和的示例。

```python
def sumOfNodes(root: TreeNode) -> int:
    def dfs(node):
        if node is None:
            return 0

        left_sum = dfs(node.left)
        right_sum = dfs(node.right)

        # 返回左子树、右子树和当前节点值的和
        return left_sum + right_sum + node.val

    return dfs(root)

# 示例用法：
# 构建二叉树：[1, 2, 3, 4, 5]
root = TreeNode(1)
root.left = TreeNode(2, TreeNode(4), TreeNode(5))
root.right = TreeNode(3)
print(sumOfNodes(root))  # 输出: 15
```

### 6. 总结

- **DFS 模板**是解决多种树问题的通用工具，可以根据不同需求进行适应性修改。
- 关键在于**正确处理基本情况、递归调用和后序处理**。
- 根据问题需求，DFS 模板可以定制为**前序**、**中序**或**后序**遍历。
