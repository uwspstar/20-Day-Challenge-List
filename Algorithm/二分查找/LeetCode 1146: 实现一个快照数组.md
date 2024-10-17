### LeetCode 1146: [Snapshot Array](https://leetcode.com/problems/snapshot-array/)

---

### 题目描述：

实现一个快照数组 `SnapshotArray`，支持以下操作：

1. **`SnapshotArray(int length)`**：初始化一个长度为 `length` 的数组，所有的值初始化为 `0`。
2. **`void set(int index, int val)`**：将数组指定索引位置 `index` 的值设置为 `val`。
3. **`int snap()`**：拍一个快照，并返回快照的 ID（即快照次数从 `0` 开始递增）。
4. **`int get(int index, int snap_id)`**：根据指定的快照 `snap_id`，获取当时数组在索引 `index` 处的值。

---

### 示例：

#### 示例 1:
```
输入：
["SnapshotArray","set","snap","set","get"]
[[3],[0,5],[],[0,6],[0,0]]

输出：
[null,null,0,null,5]
```

解释：
1. SnapshotArray(3) 初始化一个长度为 3 的数组，初始值为 [0, 0, 0]。
2. set(0, 5) 将索引 `0` 处的值设置为 `5`，数组变为 [5, 0, 0]。
3. snap() 拍摄快照，返回快照 ID 为 0。
4. set(0, 6) 将索引 `0` 处的值设置为 `6`，数组变为 [6, 0, 0]。
5. get(0, 0) 获取快照 `0` 时，索引 `0` 的值，为 `5`。

---

### 解题思路：

这道题目要求实现一个可以支持**快照**功能的数组。为了实现高效的快照操作，可以利用**哈希表 + 二分查找**的思路。

#### 关键思路：
1. **存储值的变化**：并不是每次都保存整个数组的快照，而是仅在某个索引位置的值变化时，保存该索引值的变化及其对应的快照 ID。
2. **每个索引使用哈希表**：对每个索引维护一个哈希表，哈希表的键为快照 ID，值为该快照下该索引的值。
3. **二分查找**：当需要获取某个快照时，可以通过二分查找快速查找快照 ID 对应的值。

---

### 代码实现：

```python
class SnapshotArray:

    def __init__(self, length: int):
        # 使用字典存储每个索引位置的历史值变化，键是索引，值是一个字典（snap_id: value）
        self.arr = [{} for _ in range(length)]
        # 初始化快照 id
        self.snap_id = 0

    def set(self, index: int, val: int) -> None:
        # 将当前 snap_id 和值 val 存储在对应的索引的字典中
        self.arr[index][self.snap_id] = val

    def snap(self) -> int:
        # 返回当前快照的 id，然后 snap_id 自增
        self.snap_id += 1
        return self.snap_id - 1

    def get(self, index: int, snap_id: int) -> int:
        # 获取在指定 snap_id 时的值，如果没有，则返回之前的最近值
        if snap_id in self.arr[index]:
            return self.arr[index][snap_id]
        # 如果 snap_id 处没有值，向前找到最近的快照值
        for i in range(snap_id, -1, -1):
            if i in self.arr[index]:
                return self.arr[index][i]
        return 0
```

---

### 代码解释：

1. **初始化**：
   - `arr` 是一个包含字典的数组，每个字典保存某个索引位置在不同快照下的值变化。
   - `snap_id` 是一个自增的变量，表示当前快照的 ID。

2. **`set` 函数**：
   - 在调用 `set` 函数时，我们将当前的快照 ID 和对应的值保存到该索引的字典中。

3. **`snap` 函数**：
   - 调用 `snap` 函数时，返回当前的快照 ID，并将 `snap_id` 自增。

4. **`get` 函数**：
   - `get` 函数尝试获取指定 `snap_id` 下的值，如果该 `snap_id` 下没有值，向前查找最近一次的快照值。若没有历史值，则返回 0（即初始状态）。

---

### 优化版本：使用有序列表进行二分查找

在之前的实现中，每次 `get` 操作需要线性扫描找到快照 ID 对应的值，这可能会导致时间复杂度较高。我们可以通过为每个索引位置保存**快照 ID 及其对应的值**，并使用**二分查找**来优化查找操作。

### 代码实现：

```python
import collections
import bisect

class SnapshotArray:
    def __init__(self, length: int):
        # 对每个索引位置使用字典存储 snap_id 和相应的值
        self.arr = [collections.defaultdict(list) for _ in range(length)]
        self.snap_id = 0  # 初始化快照 ID

    def set(self, index: int, val: int) -> None:
        # 在当前的 snap_id 下，设置该索引的值
        if len(self.arr[index][self.snap_id]) == 0 or self.arr[index][self.snap_id][-1] != val:
            self.arr[index][self.snap_id].append(val)

    def snap(self) -> int:
        # 返回当前的快照 ID，并将快照 ID 自增
        self.snap_id += 1   
        return self.snap_id - 1

    def get(self, index: int, snap_id: int) -> int:
        # 尝试查找该索引位置对应的 snap_id，如果不存在则返回最接近的 snap_id 对应的值
        idx = bisect.bisect_right(list(self.arr[index].keys()), snap_id)
        if idx == 0:
            return 0
        return self.arr[index][list(self.arr[index].keys())[idx-1]][-1]
```

---

### 优化说明：

1. **二分查找**：
   - 使用 `bisect_right` 函数可以快速找到 `snap_id` 对应的位置，从而获取该位置的值，时间复杂度为 `O(log n)`。

2. **时间复杂度优化**：
   - `set` 操作的时间复杂度为 `O(1)`，因为我们只需插入新值。
   - `get` 操作的时间复杂度为 `O(log s)`，其中 `s` 是存储的快照数。相比之前的线性查找，二分查找可以显著提高查找效率。

---

### 示例讲解：

假设我们有如下输入：
```
SnapshotArray(3) -> 初始化一个长度为 3 的数组
set(0, 5) -> 在索引 0 处设置值 5，数组变为 [5, 0, 0]
snap() -> 拍一个快照，返回快照 ID 为 0
set(0, 6) -> 在索引 0 处设置值 6，数组变为 [6, 0, 0]
get(0, 0) -> 获取快照 0 时索引 0 的值，结果为 5
```

通过使用二分查找，我们可以高效地找到指定快照下的值，而不必遍历所有快照记录。

---

### 总结：

- 通过对快照数组进行二分查找优化，`get` 操作可以更加高效，特别是在快照记录较多的情况下。
- 使用 `collections.defaultdict` 和 `bisect` 模块，我们可以轻松维护快照 ID 和值的对应关系并进行快速查找。

这样优化后，我们能以更高效的方式解决快照数组的问题，并减少复杂度。
