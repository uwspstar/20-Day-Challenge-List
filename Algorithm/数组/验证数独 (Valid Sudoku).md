### **题目**：验证数独 (Valid Sudoku)

验证一个 9x9 的数独是否有效。规则如下：
1. 每一行的数字必须唯一（1-9）。
2. 每一列的数字必须唯一（1-9）。
3. 每个 3x3 小方格的数字必须唯一（1-9）。

---

### **代码实现**
```python
from collections import defaultdict
from typing import List

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        # 定义行、列和 3x3 子方格的哈希集合
        set_row = defaultdict(set)
        set_col = defaultdict(set)
        set_sqr = defaultdict(set)

        for row in range(9):
            for col in range(9):
                if board[row][col] == ".":  # 跳过空格
                    continue

                # 检查当前数字是否已经出现在当前行、列或子方格中
                if (board[row][col] in set_row[row]
                    or board[row][col] in set_col[col]
                    or board[row][col] in set_sqr[(row // 3, col // 3)]):
                    return False
                
                # 将数字添加到对应的集合中
                set_row[row].add(board[row][col])
                set_col[col].add(board[row][col])
                set_sqr[(row // 3, col // 3)].add(board[row][col])

        return True
```

---

### **时间和空间复杂度分析**

#### **时间复杂度**：
- 遍历整个数独的每个单元格，共 \( 9 \times 9 = 81 \) 次。
- 每次检查和添加到集合操作的时间复杂度为 \( O(1) \)。
- **总时间复杂度：\( O(81) = O(1) \)**（常量时间复杂度，因为数独大小固定）。

#### **空间复杂度**：
- 使用了三个哈希集合分别存储行、列和子方格的数字，每个集合最多存储 9 个数字。
- **总空间复杂度：\( O(9 + 9 + 9) = O(1) \)**。

---

### **示例运行步骤**

#### **输入**：
```python
board = [
    ["5", "3", ".", ".", "7", ".", ".", ".", "."],
    ["6", ".", ".", "1", "9", "5", ".", ".", "."],
    [".", "9", "8", ".", ".", ".", ".", "6", "."],
    ["8", ".", ".", ".", "6", ".", ".", ".", "3"],
    ["4", ".", ".", "8", ".", "3", ".", ".", "1"],
    ["7", ".", ".", ".", "2", ".", ".", ".", "6"],
    [".", "6", ".", ".", ".", ".", "2", "8", "."],
    [".", ".", ".", "4", "1", "9", ".", ".", "5"],
    [".", ".", ".", ".", "8", ".", ".", "7", "9"]
]
```

---

#### **运行过程**：

1. **初始化集合**：
   ```python
   set_row = defaultdict(set)
   set_col = defaultdict(set)
   set_sqr = defaultdict(set)
   ```

2. **遍历每个单元格**：
   - 第一个非空单元格：`board[0][0] = "5"`。
     - 行 `0`、列 `0` 和子方格 `(0, 0)` 中都没有 `"5"`。
     - 将 `"5"` 添加到集合：
       ```python
       set_row[0] = {"5"}
       set_col[0] = {"5"}
       set_sqr[(0, 0)] = {"5"}
       ```
   - 继续检查其他非空单元格，按相同逻辑更新集合。

3. **冲突检查**：
   - 如果任何数字已经存在于对应的行、列或子方格的集合中，直接返回 `False`。
   - 否则继续遍历所有单元格。

4. **结束时返回**：
   - 如果所有单元格都检查完且没有冲突，返回 `True`。

---

### **示例输出**：
#### 输入：
```python
board = [
    ["5", "3", ".", ".", "7", ".", ".", ".", "."],
    ["6", ".", ".", "1", "9", "5", ".", ".", "."],
    [".", "9", "8", ".", ".", ".", ".", "6", "."],
    ["8", ".", ".", ".", "6", ".", ".", ".", "3"],
    ["4", ".", ".", "8", ".", "3", ".", ".", "1"],
    ["7", ".", ".", ".", "2", ".", ".", ".", "6"],
    [".", "6", ".", ".", ".", ".", "2", "8", "."],
    [".", ".", ".", "4", "1", "9", ".", ".", "5"],
    [".", ".", ".", ".", "8", ".", ".", "7", "9"]
]
```
#### 输出：
```python
True
```

---

### **总结**
- **核心思路**：
  - 利用哈希集合跟踪每一行、列和子方格中的数字。
  - 检查当前单元格的数字是否重复。
- **优点**：
  - 时间复杂度为常量，适合处理固定大小的数独问题。
- **注意点**：
  - 子方格索引的计算公式为 `(row // 3, col // 3)`。

---

### **`set_row = defaultdict(set)` 的含义**

`defaultdict` 是 Python 中 `collections` 模块提供的一个数据结构，是字典 `dict` 的子类。它的特点是，当访问一个不存在的键时，不会抛出 `KeyError`，而是自动创建一个默认值。这里的默认值是 `set`，即一个空集合。

```python
from collections import defaultdict

# 初始化一个默认值为 set 的 defaultdict
set_row = defaultdict(set)
```

---

### **功能说明**

1. **默认值为 `set`**：
   - 每次访问一个不存在的键时，`defaultdict` 会自动调用 `set()` 来创建一个空集合。
   - 这样可以避免手动初始化键值。

2. **用途**：
   - 在处理数独时，用 `set_row[row]` 来存储第 `row` 行中已经出现的数字。
   - 如果访问的 `row` 尚未存储过，`defaultdict` 会自动为这个行号初始化一个空集合。

---

### **代码示例**

#### **普通字典需要手动初始化**：
```python
# 使用普通字典
set_row = {}
row = 0

# 如果尝试访问不存在的键，会抛出 KeyError
# set_row[row].add("5")  # 抛出 KeyError

# 手动初始化
if row not in set_row:
    set_row[row] = set()
set_row[row].add("5")

print(set_row)  # 输出：{0: {"5"}}
```

#### **使用 `defaultdict` 自动初始化**：
```python
from collections import defaultdict

# 使用 defaultdict
set_row = defaultdict(set)
row = 0

# 直接访问不存在的键，会自动初始化为空集合
set_row[row].add("5")

print(set_row)  # 输出：defaultdict(<class 'set'>, {0: {'5'}})
```

---

### **在数独代码中的作用**

#### **初始化**：
```python
set_row = defaultdict(set)  # 存储每一行的数字
```

#### **使用**：
- 如果当前行中已经存在某个数字，说明数独无效。
- 如果当前行中不存在该数字，则将数字添加到集合中。

示例：
```python
set_row[0].add("5")  # 在第 0 行添加数字 "5"
set_row[0].add("3")  # 在第 0 行添加数字 "3"

# 检查是否存在重复
if "5" in set_row[0]:  # 返回 True，表示第 0 行已存在 "5"
    print("重复")
```

---

### **输出示例**

**输入**：
```python
from collections import defaultdict

set_row = defaultdict(set)

# 添加一些数字
set_row[0].add("5")
set_row[1].add("8")
set_row[1].add("3")
```

**输出**：
```python
defaultdict(<class 'set'>, {0: {'5'}, 1: {'8', '3'}})
```

---

### **总结（中文解释）**

- **`defaultdict(set)` 是一个特殊的字典**：
  - 键不存在时，会自动创建一个空集合。
  - 适合用来存储动态增加的元素，比如每行的数独数字。

- **好处**：
  - 避免了手动初始化，代码更加简洁高效。
  - 避免了访问不存在键时的 `KeyError` 异常。

- **在数独中的应用**：
  - 用来跟踪每一行、列或子方格中的数字，确保没有重复项。

