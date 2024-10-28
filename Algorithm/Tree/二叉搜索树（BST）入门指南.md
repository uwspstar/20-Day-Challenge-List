### 二叉搜索树（BST）入门指南

#### 介绍
二叉搜索树（Binary Search Tree，简称 BST）是一种高效的数据结构，广泛应用于各种算法和系统中。本文将深入探讨 BST 的定义、基本操作（搜索、插入、删除）、Python 实现以及其在实际应用中的优势。通过详细的代码示例和逐步解析，帮助初学者轻松掌握二叉搜索树的概念和实现方法。

---

#### 什么是二叉搜索树？

**定义：**
二叉搜索树是一种有根的二叉树，其中每个内部节点的值都大于其左子树中所有节点的值，并且小于其右子树中所有节点的值。空树也被认为是一棵二叉搜索树，因为它自然满足上述定义。

**性质：**
1. **有序性**：对于任意节点，其左子树所有节点的值均小于该节点的值，右子树所有节点的值均大于该节点的值。
2. **无重复节点**：通常情况下，BST 不允许有重复的节点值（具体取决于实现需求）。
3. **动态性**：BST 支持高效的插入和删除操作，适合动态数据集。

---

#### 为什么使用二叉搜索树？

BST 的主要优势在于其高效的搜索、插入和删除操作，时间复杂度平均为 O(log n)，其中 n 是树中的节点数。这使得 BST 在需要频繁查找和更新数据的场景中非常有用。

**应用场景：**
1. **高效查找**：如实现字典、数据库索引等。
2. **有序数据存储**：如实现有序集合、优先队列等。
3. **动态数据集**：如实时系统中的数据更新和查询。

---

### 二叉搜索树的基本操作

##### 1. 搜索（Search）

**目的：** 在 BST 中查找一个特定的值，判断其是否存在。

**实现思路：**
- 从根节点开始。
- 比较目标值与当前节点的值。
  - 若相等，返回 `True`。
  - 若目标值小于当前节点的值，递归搜索左子树。
  - 若目标值大于当前节点的值，递归搜索右子树。
- 若遍历到空节点，返回 `False`。

**代码示例：**

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def find(tree, val):
    if tree is None:
        return False
    if tree.val == val:
        return True
    elif tree.val < val:
        return find(tree.right, val)
    else:
        return find(tree.left, val)

# 测试示例
root = Node(10)
root.left = Node(5)
root.right = Node(15)
root.left.left = Node(3)
root.left.right = Node(7)
root.right.left = Node(12)
root.right.right = Node(18)

print(find(root, 7))  # 输出: True
print(find(root, 20)) # 输出: False
```

**运行步骤：**
1. 从根节点（10）开始，比较目标值（7）与当前节点值（10）。
2. 因为 7 < 10，递归搜索左子树。
3. 在节点（5）处，比较 7 与 5。
4. 因为 7 > 5，递归搜索右子树。
5. 在节点（7）处，找到目标值，返回 `True`。

##### 2. 插入（Insert）

**目的：** 向 BST 中插入一个新的值，保持 BST 的有序性。

**实现思路：**
- 从根节点开始。
- 比较新值与当前节点的值。
  - 若新值小于当前节点，递归插入左子树。
  - 若新值大于当前节点，递归插入右子树。
  - 若相等，根据具体需求决定是否插入（通常不插入重复值）。
- 若遍历到空节点，插入新节点。

**代码示例：**

```python
def insert(tree, val):
    if tree is None:
        return Node(val)
    if val < tree.val:
        tree.left = insert(tree.left, val)
    elif val > tree.val:
        tree.right = insert(tree.right, val)
    return tree

# 测试示例
root = Node(10)
insert(root, 5)
insert(root, 15)
insert(root, 3)
insert(root, 7)
insert(root, 12)
insert(root, 18)

# 中序遍历打印树
def inorder_traversal(node):
    if node:
        inorder_traversal(node.left)
        print(node.val, end=' ')
        inorder_traversal(node.right)

inorder_traversal(root)  # 输出: 3 5 7 10 12 15 18
```

**运行步骤：**
1. 从根节点（10）开始，比较新值（7）与当前节点值（10）。
2. 因为 7 < 10，递归插入左子树。
3. 在节点（5）处，比较 7 与 5。
4. 因为 7 > 5，递归插入右子树。
5. 在节点（7）处，找到空位置，插入新节点（7）。

##### 3. 删除（Delete）（可选）

**目的：** 从 BST 中删除一个特定的值，保持 BST 的有序性。

**实现思路：**
- 首先找到要删除的节点。
- 根据节点的子节点情况进行删除：
  - **无子节点**：直接删除节点。
  - **只有一个子节点**：用子节点替换当前节点。
  - **有两个子节点**：找到右子树中最小的节点（后继节点），用其值替换当前节点，然后删除后继节点。

**代码示例：**

```python
def find_min(node):
    while node.left:
        node = node.left
    return node

def delete_node(tree, val):
    if tree is None:
        return tree
    if val < tree.val:
        tree.left = delete_node(tree.left, val)
    elif val > tree.val:
        tree.right = delete_node(tree.right, val)
    else:
        # 节点有一个或无子节点
        if tree.left is None:
            return tree.right
        elif tree.right is None:
            return tree.left
        # 节点有两个子节点
        temp = find_min(tree.right)
        tree.val = temp.val
        tree.right = delete_node(tree.right, temp.val)
    return tree

# 测试示例
root = Node(10)
insert(root, 5)
insert(root, 15)
insert(root, 3)
insert(root, 7)
insert(root, 12)
insert(root, 18)

print("\n删除 5 后的中序遍历:")
root = delete_node(root, 5)
inorder_traversal(root)  # 输出: 3 7 10 12 15 18
```

**运行步骤：**
1. 从根节点（10）开始，寻找要删除的值（5）。
2. 比较 5 与 10，递归搜索左子树。
3. 在节点（5）处，找到目标值。
4. 节点（5）有两个子节点，找到右子树中的最小值（7）。
5. 用 7 替换节点（5）的值，删除节点（7）。
6. 最终中序遍历输出：3 7 10 12 15 18。

---

### 改进：自平衡二叉搜索树

**问题：**
在最坏情况下（如插入一个已排序的序列），BST 会退化成一个链表，导致搜索、插入和删除操作的时间复杂度退化为 O(n)。

**解决方案：**
引入自平衡机制，确保树的高度始终保持在 O(log n) 的水平。常见的自平衡二叉搜索树包括 AVL 树和红黑树。

**AVL 树简介：**
AVL 树是一种自平衡的二叉搜索树，任何节点的左右子树高度差不超过 1。通过旋转操作（左旋、右旋）来维护平衡。

**注意：**
虽然自平衡树在理论上保证了高效的操作时间复杂度，但其实现较为复杂，通常在面试中不需要深入实现。了解其基本概念和优势即可。

---

### BST 与其他数据结构的比较

| 数据结构    | 搜索时间复杂度 | 插入时间复杂度 | 删除时间复杂度 | 是否有序 | 空间复杂度 | 备注                                       |
|-------------|----------------|----------------|----------------|----------|------------|--------------------------------------------|
| **BST**     | O(h)           | O(h)           | O(h)           | 是       | O(n)       | 需保持平衡以保证 O(log n) 时间               |
| **哈希表**  | O(1) 平均      | O(1) 平均      | O(1) 平均      | 否       | O(n)       | 不支持有序操作和范围查询                     |
| **排序数组**| O(log n) 二分查找 | O(n)            | O(n)            | 是       | O(n)       | 插入和删除操作效率低                         |
| **堆**      | O(n)           | O(log n)        | O(log n)        | 否       | O(n)       | 适用于优先队列等应用                         |

**总结：**
- **BST** 适合需要有序数据和高效动态更新的场景。
- **哈希表** 适合需要快速查找但不需要有序的数据。
- **排序数组** 适合静态数据集，查找效率高但更新效率低。
- **堆** 适合需要频繁获取最值的场景，如优先队列。

---

### 应用场景及代码示例

#### 1. 高效查找：实现字典

BST 可以用来实现字典（映射）数据结构，通过键值对的方式存储和查找数据。

**代码示例：**

```python
class BSTDictionary:
    def __init__(self):
        self.root = None

    def insert(self, key, value):
        if self.root is None:
            self.root = Node(key, value)
        else:
            self._insert(self.root, key, value)

    def _insert(self, node, key, value):
        if key < node.val:
            if node.left is None:
                node.left = Node(key, value)
            else:
                self._insert(node.left, key, value)
        elif key > node.val:
            if node.right is None:
                node.right = Node(key, value)
            else:
                self._insert(node.right, key, value)
        else:
            # 如果键已存在，更新值
            node.value = value

    def find(self, key):
        return self._find(self.root, key)

    def _find(self, node, key):
        if node is None:
            return None
        if key == node.val:
            return node.value
        elif key < node.val:
            return self._find(node.left, key)
        else:
            return self._find(node.right, key)

class Node:
    def __init__(self, key, value):
        self.val = key
        self.value = value
        self.left = None
        self.right = None

# 测试示例
bst_dict = BSTDictionary()
bst_dict.insert('apple', 3)
bst_dict.insert('banana', 5)
bst_dict.insert('cherry', 2)

print(bst_dict.find('banana'))  # 输出: 5
print(bst_dict.find('grape'))   # 输出: None
```

**说明：**
- **插入操作**：通过键值对插入数据，保持 BST 的有序性。
- **查找操作**：通过键快速查找对应的值。

**提示与注意：**
- **键的唯一性**：确保字典中的键是唯一的，避免重复插入引起混乱。
- **平衡性**：为了保持高效的查找，建议使用自平衡 BST 实现字典。

#### 2. 有序数据存储：实现有序集合

有序集合需要保持元素的有序性，并支持高效的插入和查找操作。BST 是实现有序集合的理想选择。

**代码示例：**

```python
class OrderedSet:
    def __init__(self):
        self.root = None

    def insert(self, val):
        if self.root is None:
            self.root = Node(val)
        else:
            self._insert(self.root, val)

    def _insert(self, node, val):
        if val < node.val:
            if node.left is None:
                node.left = Node(val)
            else:
                self._insert(node.left, val)
        elif val > node.val:
            if node.right is None:
                node.right = Node(val)
            else:
                self._insert(node.right, val)
        # 如果值已存在，不插入

    def inorder(self):
        return self._inorder(self.root)

    def _inorder(self, node):
        if node:
            yield from self._inorder(node.left)
            yield node.val
            yield from self._inorder(node.right)

# 测试示例
ordered_set = OrderedSet()
ordered_set.insert(10)
ordered_set.insert(5)
ordered_set.insert(15)
ordered_set.insert(3)
ordered_set.insert(7)
ordered_set.insert(12)
ordered_set.insert(18)

print("有序集合中的元素:")
print(list(ordered_set.inorder()))  # 输出: [3, 5, 7, 10, 12, 15, 18]
```

**说明：**
- **插入操作**：插入元素时保持 BST 的有序性，不允许重复元素。
- **中序遍历**：返回有序集合中的元素。

**提示与注意：**
- **元素唯一性**：确保集合中的元素是唯一的。
- **平衡性**：为了保持高效的操作，建议使用自平衡 BST 实现有序集合。

#### 3. 动态数据集：实时系统中的数据更新和查询

在实时系统中，数据经常需要被动态更新和查询。BST 可以高效地支持这些操作，适用于需要频繁插入、删除和查找的数据集。

**代码示例：**

```python
class RealTimeData:
    def __init__(self):
        self.root = None

    def insert(self, timestamp, data):
        if self.root is None:
            self.root = Node(timestamp, data)
        else:
            self._insert(self.root, timestamp, data)

    def _insert(self, node, timestamp, data):
        if timestamp < node.val:
            if node.left is None:
                node.left = Node(timestamp, data)
            else:
                self._insert(node.left, timestamp, data)
        elif timestamp > node.val:
            if node.right is None:
                node.right = Node(timestamp, data)
            else:
                self._insert(node.right, timestamp, data)
        else:
            # 如果时间戳已存在，更新数据
            node.data = data

    def query(self, start, end):
        result = []
        self._query(self.root, start, end, result)
        return result

    def _query(self, node, start, end, result):
        if node is None:
            return
        if start < node.val:
            self._query(node.left, start, end, result)
        if start <= node.val <= end:
            result.append((node.val, node.data))
        if node.val < end:
            self._query(node.right, start, end, result)

# 测试示例
real_time = RealTimeData()
real_time.insert(10, "Event A")
real_time.insert(5, "Event B")
real_time.insert(15, "Event C")
real_time.insert(3, "Event D")
real_time.insert(7, "Event E")
real_time.insert(12, "Event F")
real_time.insert(18, "Event G")

print("查询时间范围 5 到 15 的事件:")
print(real_time.query(5, 15))  
# 输出: [(5, 'Event B'), (7, 'Event E'), (10, 'Event A'), (12, 'Event F'), (15, 'Event C')]
```

**说明：**
- **插入操作**：根据时间戳插入事件数据，保持 BST 的有序性。
- **查询操作**：在给定的时间范围内查询事件，利用 BST 的有序性高效地进行范围查询。

**提示与注意：**
- **时间戳唯一性**：确保每个事件的时间戳是唯一的，或定义处理重复时间戳的策略。
- **平衡性**：实时系统要求高效的操作，建议使用自平衡 BST 以确保查询和插入的效率。

---

### 总结

1. **从节点的角度思考 DFS**：在处理每个节点时，只需关注当前节点的状态，并递归处理子节点。这样可以简化逻辑，逐层解决问题。
2. **返回值 vs. 全局变量**：根据具体问题的需要选择适合的方式来传递信息。
3. **BST 模板**：掌握基础 BST 操作模板，可以解决各种树相关的问题。

### 提示与注意事项

- **保持平衡**：为了确保 BST 的操作效率，尽量保持树的平衡。可以使用自平衡树（如 AVL 树）或其他平衡策略。
- **处理重复值**：根据需求决定是否允许重复值。如果允许，需定义插入策略（如将重复值插入到右子树）。
- **递归实现**：BST 的许多操作依赖于递归，理解递归的执行流程对于正确实现 BST 非常重要。
- **内存管理**：在删除节点时，注意正确处理子节点，避免内存泄漏或悬挂指针（在使用低级语言时）。

### 最终建议

- **多练习 BST 的实现和操作**，巩固理解。
- **尝试解决不同类型的 BST 问题**，如查找第 k 小元素、验证 BST 的有效性等。
- **学习自平衡树的基本原理**，了解如何维护树的平衡。

通过持续学习和实践，你将能够熟练掌握二叉搜索树，并在实际应用中发挥其优势。

---

### 比较表

| 操作类型 | 搜索时间复杂度 | 插入时间复杂度 | 删除时间复杂度 | 是否有序 | 空间复杂度 | 备注                                       |
|----------|----------------|----------------|----------------|----------|------------|--------------------------------------------|
| **BST**  | O(h)           | O(h)           | O(h)           | 是       | O(n)       | 需保持平衡以保证 O(log n) 时间               |
| **哈希表** | O(1) 平均      | O(1) 平均      | O(1) 平均      | 否       | O(n)       | 不支持有序操作和范围查询                     |
| **排序数组** | O(log n) 二分查找 | O(n)            | O(n)            | 是       | O(n)       | 插入和删除操作效率低                         |
| **堆**     | O(n)           | O(log n)        | O(log n)        | 否       | O(n)       | 适用于优先队列等应用                         |

---

### 提示与建议

- **理解递归**：BST 的许多操作（如查找、插入、删除）都依赖于递归，理解递归的工作原理对掌握 BST 至关重要。
- **保持平衡**：为了确保操作效率，学习和使用自平衡 BST，如 AVL 树，可以显著提升性能。
- **处理边界情况**：在实现 BST 操作时，确保处理好空树和叶子节点的情况，避免潜在的错误。
- **多练习**：通过解决各种 BST 相关的 LeetCode 问题，如查找子树、计算深度、验证 BST 等，来巩固理解和提升技能。

### 结论

二叉搜索树（BST）是一种功能强大且高效的数据结构，适用于需要快速查找、插入和删除操作的各种应用场景。通过深入理解 BST 的定义、基本操作及其应用场景，并通过 Python 实现相关代码，你可以在算法和系统设计中灵活应用 BST，提升问题解决能力。

---

### 相关 LeetCode 题目

#### 前序 DFS 相关题目
1. [144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)
2. [113. 路径总和 II](https://leetcode.cn/problems/path-sum-ii/)
3. [129. 求根节点到叶节点数字之和](https://leetcode.cn/problems/sum-root-to-leaf-numbers/)
4. [100. 相同的树](https://leetcode.cn/problems/same-tree/)
5. [437. 路径总和 III](https://leetcode.cn/problems/path-sum-iii/)

#### 中序 DFS 相关题目
1. [94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
2. [230. 二叉搜索树中第 K 小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/)
3. [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)
4. [501. 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)
5. [783. 二叉搜索树节点最小距离](https://leetcode.cn/problems/minimum-distance-between-bst-nodes/)

#### 后序 DFS 相关题目
1. [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)
2. [110. 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)
3. [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)
4. [1123. 最深叶节点的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-deepest-leaves/)
5. [124. 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/)

---

### 前序 DFS 相关题目

#### 1. LeetCode 144: 二叉树的前序遍历
[LeetCode 144: Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

#### 题目描述
给定一个二叉树的根节点，返回二叉树的前序遍历序列。

- **前序遍历**：根节点 -> 左子树 -> 右子树

#### 代码实现与详细注释
```python
from typing import List, Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []

        # 辅助函数，递归前序遍历
        def dfs(node):
            if not node:
                return
            
            # 访问根节点
            result.append(node.val)
            # 递归访问左子树
            dfs(node.left)
            # 递归访问右子树
            dfs(node.right)

        dfs(root)
        return result
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 2. LeetCode 113: 路径总和 II
[LeetCode 113: Path Sum II](https://leetcode.com/problems/path-sum-ii/)

#### 题目描述
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径上节点值之和等于目标和的路径。

#### 代码实现与详细注释
```python
from typing import List, Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        result = []

        def dfs(node, path, current_sum):
            if not node:
                return
            
            # 添加当前节点值到路径
            path.append(node.val)
            current_sum += node.val

            # 检查是否为叶子节点且路径和等于目标和
            if not node.left and not node.right and current_sum == targetSum:
                result.append(list(path))
            else:
                # 递归访问左子树和右子树
                dfs(node.left, path, current_sum)
                dfs(node.right, path, current_sum)

            # 回溯
            path.pop()

        dfs(root, [], 0)
        return result
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 3. LeetCode 129: 求根节点到叶节点数字之和
[LeetCode 129: Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

#### 题目描述
给定一个二叉树，计算从根节点到叶子节点的所有路径所表示的数字之和。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        def dfs(node, current_sum):
            if not node:
                return 0
            
            # 计算当前路径的数字
            current_sum = current_sum * 10 + node.val
            
            # 如果是叶子节点，返回当前路径的数字
            if not node.left and not node.right:
                return current_sum

            # 递归计算左右子树的数字和
            return dfs(node.left, current_sum) + dfs(node.right, current_sum)

        return dfs(root, 0)
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 4. LeetCode 100: 相同的树
[LeetCode 100: Same Tree](https://leetcode.com/problems/same-tree/)

#### 题目描述
给定两棵二叉树，检查它们是否相同。

- 两棵树相同，当且仅当它们的结构相同，且对应节点值相同。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        # 如果两棵树都为空，则相同
        if not p and not q:
            return True
        
        # 如果只有一棵树为空或节点值不同，则不相同
        if not p or not q or p.val != q.val:
            return False

        # 递归检查左右子树
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 5. LeetCode 437: 路径总和 III
[LeetCode 437: Path Sum III](https://leetcode.com/problems/path-sum-iii/)

#### 题目描述
给定一个二叉树和一个目标和，计算路径总和等于目标和的路径数量。这些路径不需要从根节点开始，也不需要在叶子节点结束。

#### 代码实现与详细注释
```python
from typing import Optional
from collections import defaultdict

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        prefix_sum = defaultdict(int)
        prefix_sum[0] = 1

        def dfs(node, current_sum):
            if not node:
                return 0

            current_sum += node.val
            count = prefix_sum[current_sum - targetSum]
            prefix_sum[current_sum] += 1

            # 递归访问左右子树
            count += dfs(node.left, current_sum)
            count += dfs(node.right, current_sum)

            # 回溯
            prefix_sum[current_sum] -= 1

            return count

        return dfs(root, 0)
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

### 中序 DFS 相关题目

#### 1. LeetCode 94: 二叉树的中序遍历
[LeetCode 94: Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

#### 题目描述
给定一个二叉树的根节点，返回二叉树的中序遍历序列。

- **中序遍历**：左子树 -> 根节点 -> 右子树

#### 代码实现与详细注释
```python
from typing import List, Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []

        # 辅助函数，递归中序遍历
        def dfs(node):
            if not node:
                return
            
            # 递归访问左子树
            dfs(node.left)
            # 访问根节点
            result.append(node.val)
            # 递归访问右子树
            dfs(node.right)

        dfs(root)
        return result
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 2. LeetCode 230: 二叉搜索树中第 K 小的元素
[LeetCode 230: Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

#### 题目描述
给定一个二叉搜索树的根节点和一个整数 `k`，返回树中第 `k` 小的元素。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        self.k = k
        self.result = None

        # 辅助函数，中序遍历
        def inorder(node):
            if not node or self.result is not None:
                return
            
            # 递归访问左子树
            inorder(node.left)

            # 访问当前节点，检查是否是第 k 小元素
            self.k -= 1
            if self.k == 0:
                self.result = node.val
                return
            
            # 递归访问右子树
            inorder(node.right)

        inorder(root)
        return self.result
```

#### 复杂度分析
- **时间复杂度**：O(n)，最坏情况下需要遍历所有节点。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 3. LeetCode 98: 验证二叉搜索树
[LeetCode 98: Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

#### 题目描述
给定一个二叉树，编写一个函数来检查它是否是一个**有效的二叉搜索树**（Binary Search Tree, BST）。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        # 辅助函数，用于递归验证每个节点是否满足二叉搜索树的性质
        def isValid(node, minVal, maxVal):
            # 如果当前节点为空，则满足条件
            if not node:
                return True
            
            # 如果当前节点值不在 minVal 和 maxVal 范围内，则不是二叉搜索树
            if not (minVal < node.val < maxVal):
                return False
            
            # 递归检查左子树和右子树
            # 左子树：所有节点必须小于当前节点值
            # 右子树：所有节点必须大于当前节点值
            return isValid(node.left, minVal, node.val) and isValid(node.right, node.val, maxVal)
        
        # 初始调用，最小值设为负无穷大，最大值设为正无穷大
        return isValid(root, float('-inf'), float('inf'))
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 4. LeetCode 501: 二叉搜索树中的众数
[LeetCode 501: Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

#### 题目描述
给定一个二叉搜索树的根节点，找到出现频率最高的元素。

#### 代码实现与详细注释
```python
from typing import List, Optional
from collections import defaultdict

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        self.count = defaultdict(int)
        self.max_count = 0
        self.result = []

        # 中序遍历二叉搜索树
        def inorder(node):
            if not node:
                return
            
            inorder(node.left)
            
            # 统计节点值的频率
            self.count[node.val] += 1
            if self.count[node.val] > self.max_count:
                self.max_count = self.count[node.val]
                self.result = [node.val]
            elif self.count[node.val] == self.max_count:
                self.result.append(node.val)
            
            inorder(node.right)

        inorder(root)
        return self.result
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(n)，用于存储节点频率。

---

#### 5. LeetCode 783: 二叉搜索树节点最小距离
[LeetCode 783: Minimum Distance Between BST Nodes](https://leetcode.com/problems/minimum-distance-between-bst-nodes/)

#### 题目描述
给定一个二叉搜索树的根节点，返回该树中任意两节点值之间的最小差。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def minDiffInBST(self, root: Optional[TreeNode]) -> int:
        self.prev = -float('inf')
        self.min_diff = float('inf')

        # 中序遍历
        def inorder(node):
            if not node:
                return
            
            inorder(node.left)
            
            # 更新最小差值
            self.min_diff = min(self.min_diff, node.val - self.prev)
            self.prev = node.val
            
            inorder(node.right)

        inorder(root)
        return self.min_diff
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

### 后序 DFS 相关题目

#### 1. LeetCode 104: 二叉树的最大深度
[LeetCode 104: Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

#### 题目描述
给定一个二叉树，找出其最大深度。

- 二叉树的最大深度是从根节点到最远叶子节点的最长路径上的节点数。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        # 如果节点为空，则深度为 0
        if not root:
            return 0

        # 递归计算左子树和右子树的最大深度
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)

        # 当前节点的最大深度为左右子树最大深度加 1
        return 1 + max(left_depth, right_depth)
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 2. LeetCode 110: 平衡二叉树
[LeetCode 110: Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

#### 题目描述
给定一个二叉树，判断它是否是**平衡的二叉树**。

- 一个平衡的二叉树定义为：一个二叉树的每个节点的左右两个子树的高度差的绝对值不超过 1。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(node):
            # 如果当前节点为空，返回平衡状态为 True，高度为 0
            if not node:
                return True, 0

            # 递归计算左右子树的平衡状态和高度
            left_balanced, left_height = dfs(node.left)
            right_balanced, right_height = dfs(node.right)

            # 当前节点的平衡状态：左右子树都平衡且高度差不超过 1
            balanced = left_balanced and right_balanced and abs(left_height - right_height) <= 1
            # 当前节点的高度为左右子树的最大高度加 1
            height = 1 + max(left_height, right_height)

            return balanced, height

        # 返回根节点的平衡状态
        return dfs(root)[0]
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 3. LeetCode 543: 二叉树的直径
[LeetCode 543: Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

#### 题目描述
给定一棵二叉树，找到它的直径。

- 二叉树的直径是任意两个节点路径中边数的最大值。这条路径可能不经过根节点。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.diameter = 0

        def dfs(node):
            if not node:
                return 0

            # 计算左子树和右子树的深度
            left_depth = dfs(node.left)
            right_depth = dfs(node.right)

            # 更新二叉树的直径
            self.diameter = max(self.diameter, left_depth + right_depth)

            # 返回当前节点的深度
            return 1 + max(left_depth, right_depth)

        dfs(root)
        return self.diameter
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 4. LeetCode 1123: 最深叶节点的最近公共祖先
[LeetCode 1123: Lowest Common Ancestor of Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/)

#### 题目描述
给定一棵二叉树，返回树中最深叶节点的最近公共祖先。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def lcaDeepestLeaves(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        def dfs(node):
            if not node:
                return 0, None
            
            # 递归计算左右子树的深度和最近公共祖先
            left_depth, left_lca = dfs(node.left)
            right_depth, right_lca = dfs(node.right)

            # 如果左右子树的深度相同，当前节点就是最近公共祖先
            if left_depth == right_depth:
                return left_depth + 1, node
            # 如果左子树的深度更大，返回左子树的最近公共祖先
            elif left_depth > right_depth:
                return left_depth + 1, left_lca
            # 如果右子树的深度更大，返回右子树的最近公共祖先
            else:
                return right_depth + 1, right_lca

        return dfs(root)[1]
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。

---

#### 5. LeetCode 124: 二叉树中的最大路径和
[LeetCode 124: Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

#### 题目描述
给定一个非空二叉树，返回其最大路径和。

- 路径和定义为任意两个节点之间路径上的节点值之和。路径不必经过根节点。

#### 代码实现与详细注释
```python
from typing import Optional

# 定义二叉树节点类
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.max_sum = float('-inf')

        def dfs(node):
            if not node:
                return 0

            # 递归计算左右子树的最大路径和
            left_gain = max(dfs(node.left), 0)
            right_gain = max(dfs(node.right), 0)

            # 更新全局最大路径和
            self.max_sum = max(self.max_sum, node.val + left_gain + right_gain)

            # 返回当前节点的最大贡献值
            return node.val + max(left_gain, right_gain)

        dfs(root)
        return self.max_sum
```

#### 复杂度分析
- **时间复杂度**：O(n)，其中 n 是二叉树的节点数。
- **空间复杂度**：O(h)，其中 h 是二叉树的高度。
