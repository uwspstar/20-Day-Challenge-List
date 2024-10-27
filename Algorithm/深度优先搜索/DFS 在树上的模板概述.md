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

---
### 深度优先搜索（DFS）在二叉树中的应用：从节点的角度思考

#### 介绍
深度优先搜索 (DFS) 是一种常用的数据结构遍历算法。它在树或图的结构中发挥着重要作用。在这篇技术博客中，我们将深入探讨如何在二叉树中使用 DFS，并着重介绍如何**从节点的角度思考 DFS**，而不是将整个树作为一个整体去理解。这种方法符合递归的思想，也更容易理解和实现。

### 什么是 DFS？
DFS 是一种遍历或搜索数据结构（如树或图）的算法。它通过沿着每条路径深入到底部，然后回溯来遍历整个结构。DFS 有两种实现方式：递归和迭代。在树中，我们通常使用递归来实现 DFS。

#### 为什么在树中使用 DFS？
- **逐层深入：** DFS 允许我们从根节点开始，逐层深入到树的最底部，适合解决树中的深度相关问题，如计算树的最大深度、查找最大值、统计节点数量等。
- **符合递归思想：** 树的结构非常适合递归算法，每个节点都可以视为一个子树，这使得 DFS 非常适合树的遍历和操作。

### 从节点的角度思考 DFS
使用 DFS 解决树的问题的关键在于**从节点的角度进行思考**，而不是将整个树视为一个整体。这种思维方式与递归相符，也更易于编写和理解。

#### 为什么从节点的角度思考 DFS？
1. **节点是递归的基本单元：** 在 DFS 中，每次递归调用时实际上是在处理一个节点。我们只需要关注当前节点的状态和如何递归调用其子节点，而不必关心全局树的结构。
2. **简化逻辑：** 从节点的角度出发，每个节点负责自己的一部分工作，然后将结果返回给父节点。这种方式可以逐步解决问题，而不是一次性考虑整个树的结构。
3. **逐层深入：** 在 DFS 中，递归函数会自然地逐层深入到最底部的节点，然后逐步回溯并处理每个节点的结果。

### DFS 基础模板
在树中使用 DFS 时，我们需要定义一个递归函数，它会处理当前节点的逻辑并递归调用子节点。DFS 的基础模板如下：

```python
def dfs(node, state):
    # 1. 处理空节点的情况
    if node is None:
        return

    # 2. 递归处理左右子节点
    left_result = dfs(node.left, state)
    right_result = dfs(node.right, state)

    # 3. 合并结果并返回
    ...
    return ...
```

### 示例分析：从节点的角度理解 DFS
#### 示例 1：计算二叉树的最大深度
##### 问题描述：
给定一棵二叉树，计算其最大深度。

##### 代码实现：
```python
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def max_depth(node):
    # 当前节点为空时，深度为 0
    if not node:
        return 0

    # 递归计算左右子树的最大深度
    left_depth = max_depth(node.left)
    right_depth = max_depth(node.right)

    # 返回左右子树深度的最大值加 1
    return max(left_depth, right_depth) + 1

# 测试示例
root = Node(1, Node(2, Node(4), Node(5)), Node(3))
print(max_depth(root))  # 输出 3
```

##### 运行步骤：
1. **处理当前节点：** 从根节点（1）开始，递归计算左右子树的深度。
2. **对子节点递归：** 递归调用左子节点（2）的 `max_depth()`，并继续递归到叶节点（4 和 5）。
3. **合并结果：** 返回左右子树的最大深度，并加 1，最终输出树的最大深度为 3。

#### 示例 2：查找二叉树中的最大值
##### 问题描述：
给定一棵二叉树，找到其中的最大值。

##### 代码实现：
```python
from math import inf

def find_max(node):
    # 空节点返回负无穷
    if node is None:
        return -inf

    # 递归查找左右子树的最大值
    left_max = find_max(node.left)
    right_max = find_max(node.right)

    # 返回当前节点值、左子树最大值和右子树最大值的最大值
    return max(node.val, left_max, right_max)

# 测试示例
root = Node(5, Node(11, Node(4)), Node(3, Node(8), Node(2)))
print(find_max(root))  # 输出 11
```

##### 运行步骤：
1. **处理当前节点：** 从根节点（5）开始递归。
2. **对子节点递归：** 递归遍历左子节点，找到最大值 11；递归遍历右子节点，找到最大值 8。
3. **合并结果：** 返回整个树的最大值为 11。

#### 示例 3：统计二叉树中的节点数
##### 问题描述：
给定一棵二叉树，统计其节点的总数。

##### 代码实现：
```python
def count_nodes(node):
    # 空节点的数量为 0
    if node is None:
        return 0

    # 递归统计左右子树的节点数
    left_count = count_nodes(node.left)
    right_count = count_nodes(node.right)

    # 总节点数为左右子树节点数之和加 1
    return left_count + right_count + 1

# 测试示例
root = Node(1, Node(2, Node(4), Node(5)), Node(3))
print(count_nodes(root))  # 输出 5
```

##### 运行步骤：
1. **处理当前节点：** 从根节点（1）开始，递归统计左右子树的节点数。
2. **对子节点递归：** 递归遍历左子树，统计节点数为 3；递归遍历右子树，统计节点数为 1。
3. **合并结果：** 返回整个树的节点总数为 5。

### 使用返回值 vs. 全局变量
#### 1. **使用返回值（分治法）**
在返回值传递信息的情况下，我们将信息从子节点传递到父节点。这种方式符合分治法的思想。

##### 示例：查找最大值
```python
def dfs(node):
    if node is None:
        return float('-inf')

    left_max = dfs(node.left)
    right_max = dfs(node.right)
    return max(node.val, left_max, right_max)
```

#### 2. **使用全局变量**
全局变量用于记录遍历过程中出现的最大值。

##### 示例：查找最大值
```python
max_val = float('-inf')

def dfs(node):
    global max_val
    if node is None:
        return

    max_val = max(max_val, node.val)
    dfs(node.left)
    dfs(node.right)

def get_max_val(root):
    dfs(root)
    return max_val
```

### 如何选择使用返回值或全局变量？
- **返回值：** 更适合分治问题，因为返回值可以将信息从子节点传递到父节点。
- **全局变量：** 有时会更简单，特别是在合并步骤复杂时，可以减少代码复杂性。

### 总结
1. **从节点的角度思考 DFS**：在处理每个节点时，只需关注当前节点的状态，并递归处理子节点。这样可以简化逻辑，逐层解决问题。
2. **返回值 vs. 全局变量**：根据具体问题的需要选择适合的方式来传递信息。
3. **DFS 模板：** 掌握基础 DFS 模板，可以解决各种树相关的问题。

从节点的角度理解 DFS，可以让你在解决树的问题时更加高效和清晰。希望这篇博客对初学者在学习和应用 DFS 时有所帮助！

---

### 从节点的角度思考 DFS

在树中使用深度优先搜索 (DFS) 时，关键是**从节点的角度进行思考**，而不是将整棵树作为一个整体去看。这种思维方式与递归非常契合，因为递归是逐步深入、逐层处理的问题。

#### 为什么从节点的角度思考？
1. **节点是递归的基本单元：**
   在递归中，每次调用递归函数时，实际上是在处理一个节点。你只需要专注于当前节点应该做什么，而不是去思考整个树结构。
   
2. **逐步解决问题：**
   在 DFS 中，每个节点负责自己的一部分工作（如计算子树的最大值、统计节点数等），然后将结果传递给上一级节点。这样，问题逐层解决，而不是一次性处理整个树。

3. **简化逻辑：**
   从节点的角度出发，你只需要关心当前节点的状态以及如何递归调用子节点，而不必同时考虑整个树的所有细节。

#### 从节点角度的 DFS 步骤
在具体实现 DFS 时，可以将树中的每个节点视为独立的处理单元。以下是如何从节点角度思考的详细步骤：

1. **当前节点的状态：**
   每个节点只需要知道自己当前的值、左子节点和右子节点。这样，你可以直接在当前节点做决策，而不需要考虑全局树的结构。
   
   **例如：** 在求树的最大深度问题中，当前节点的状态就是计算它的左右子树的深度，然后取其最大值加 1。

2. **对子节点的递归：**
   当前节点需要对左子节点和右子节点递归调用相同的 DFS 函数。每个子节点会递归处理自己，并将结果返回给当前节点。这样，递归自然会处理剩下的部分。

3. **合并结果：**
   每个节点会在得到左右子节点的结果后，结合自己的状态，合并这些结果并返回给父节点。

#### 代码示例：从节点的角度思考 DFS
以求二叉树的最大深度为例，代码实现如下：

```python
class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def max_depth(node):
    # 当前节点为空时，深度为 0
    if not node:
        return 0

    # 递归处理左右子节点
    left_depth = max_depth(node.left)
    right_depth = max_depth(node.right)

    # 返回左右子树深度的最大值加 1
    return max(left_depth, right_depth) + 1

# 测试示例
root = Node(1, Node(2, Node(4), Node(5)), Node(3))
print(max_depth(root))  # 输出 3
```

#### 运行步骤（逐步分析从节点的角度）
1. **处理当前节点：**
   - 当递归调用时，我们将根节点（值为 1）视为当前节点。
   - 当前节点会递归处理它的左右子树。

2. **对子节点递归：**
   - 当前节点递归调用 `max_depth()`，并传入其左子节点（值为 2）。
   - 递归继续下去，直至到达叶节点（值为 4 和 5）。

3. **合并结果：**
   - 叶节点返回 0（因为它们没有子节点）。
   - 当前节点（值为 2）将左子节点和右子节点的深度进行比较，取其最大值并加 1，返回给父节点。

#### 总结：为什么这种方式有效？
1. **简化递归逻辑：**
   从节点的角度思考 DFS，可以让递归逻辑更加简洁和清晰，因为每个节点只需要处理自己和子节点。

2. **分治思想的体现：**
   每个节点解决自己的问题，然后递归地处理其子节点，相当于将问题分解成多个小问题，这也是分治思想的体现。

3. **递归的自然特性：**
   递归本身就是逐层深入、逐步回溯的过程。DFS 的节点思维方式自然符合递归的特性，因为我们是一步步深入到最底层的节点，然后逐步向上回溯，处理每个节点的结果。

从节点的角度思考 DFS，不仅是为了理解树的遍历过程，更是为了让你能够轻松地分解复杂问题，并逐步解决每个节点的具体任务。

