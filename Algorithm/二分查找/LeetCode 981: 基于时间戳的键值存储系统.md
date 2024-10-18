### LeetCode 981: [Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)

---

### 题目描述：

设计一个基于时间戳的键值存储系统，该系统可以存储多个同一键的值，并能根据给定的时间戳 `timestamp` 返回键对应的值。

具体要求如下：
1. 存储的每个键可以有多个值，并且每个值都有一个时间戳。
2. `set(key, value, timestamp)`：存储键 `key` 对应的值 `value`，并且记录该值的时间戳 `timestamp`。
3. `get(key, timestamp)`：返回存储在 `key` 中、且最接近于 `timestamp` 的值。如果没有，则返回空字符串 `""`。

#### 示例：

```python
输入:
["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]

输出:
[null, null, "bar", "bar", null, "bar2", "bar2"]
```

解释：
```
TimeMap kv;
kv.set("foo", "bar", 1); // 存储 foo = bar 并且时间戳 timestamp = 1  
kv.get("foo", 1);        // 返回 "bar"  
kv.get("foo", 3);        // 返回 "bar" 因为最近的时间戳是 1，"bar" 是存储在 timestamp = 1 的值
kv.set("foo", "bar2", 4); // 存储 foo = bar2 并且时间戳 timestamp = 4  
kv.get("foo", 4);        // 返回 "bar2"  
kv.get("foo", 5);        // 返回 "bar2" 因为最近的时间戳是 4
```

---

### 解题思路：

这个问题要求我们实现一个基于时间的键值存储，并且在查询时，能够根据时间戳返回**最接近且小于等于该时间戳**的值。显然，对于每个 `key` 的多个时间戳对应的值，我们需要能够**快速**找到最接近的时间戳。

因此，主要思路是：

1. **存储结构**：
   - 使用一个字典 `time_map` 来存储键值对。每个键 `key` 对应一个列表，列表中的每个元素为 `(timestamp, value)`。
   
2. **二分查找**：
   - 在获取 `get(key, timestamp)` 时，由于 `timestamp` 是递增的，所以对于每个键的时间戳，我们可以对其进行**二分查找**，以快速找到最接近且小于等于该时间戳的值。

---

### 代码实现：

```python
from collections import defaultdict
import bisect

class TimeMap:

    def __init__(self):
        # 使用 defaultdict 来存储每个 key 对应的 (timestamp, value) 列表
        self.time_map = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        # 将 (timestamp, value) 添加到 key 对应的列表中
        self.time_map[key].append((timestamp, value))

    def get(self, key: str, timestamp: int) -> str:
        # 如果 key 不存在，直接返回空字符串
        if key not in self.time_map:
            return ""
        
        # 获取 key 对应的所有 (timestamp, value) 对，进行二分查找
        values = self.time_map[key]
        i = bisect.bisect_right(values, (timestamp, chr(127)))
        
        # 如果二分查找找到的索引为 0，表示没有合适的时间戳，返回空字符串
        if i == 0:
            return ""
        else:
            # 返回最接近的时间戳的值
            return values[i-1][1]
```

---

### 代码解释：

1. **初始化 `__init__`**：
   - 使用 `defaultdict(list)` 存储每个 `key` 对应的 `(timestamp, value)` 列表。
   - 这样可以避免在初始化时手动检查是否存在键值对。

2. **`set(key, value, timestamp)`**：
   - 直接将 `(timestamp, value)` 添加到字典 `time_map` 中对应的 `key` 列表中。
   - 由于输入是按递增时间戳提供的，因此我们不需要对时间戳进行排序。

3. **`get(key, timestamp)`**：
   - 首先检查 `key` 是否存在，如果不存在，直接返回空字符串。
   - 对于存在的键，使用 `bisect_right` 进行二分查找，找到最接近 `timestamp` 且不大于它的时间戳。
   - 如果找不到合适的时间戳，返回空字符串；否则，返回最近的时间戳对应的值。

---

### 复杂度分析：

- **时间复杂度**：
  - `set` 操作：O(1)，因为只是将元素添加到列表末尾。
  - `get` 操作：O(log n)，其中 `n` 是 `key` 对应的时间戳数量，使用了二分查找。
  
- **空间复杂度**：O(n)，其中 `n` 是所有 `(timestamp, value)` 的数量，因为我们需要存储所有的键值对。

---

### 示例讲解：

假设我们进行以下操作：
```python
kv = TimeMap()
kv.set("foo", "bar", 1)   # 存储 "foo" 在时间戳 1 时的值 "bar"
kv.set("foo", "bar2", 4)  # 存储 "foo" 在时间戳 4 时的值 "bar2"
print(kv.get("foo", 1))   # 输出 "bar" （直接找到时间戳 1）
print(kv.get("foo", 3))   # 输出 "bar" （最近的时间戳是 1）
print(kv.get("foo", 4))   # 输出 "bar2" （直接找到时间戳 4）
print(kv.get("foo", 5))   # 输出 "bar2" （最近的时间戳是 4）
```

在这个过程中，`set` 操作将键值对存储起来，而 `get` 操作使用二分查找找到最接近的时间戳，确保我们可以在较短时间内获取到最准确的结果。

---

### 总结：

这个问题的核心在于如何通过高效的数据结构存储多个时间戳对应的值，并且在查询时能够快速查找到最接近的时间戳。通过使用字典加上二分查找，我们可以在 `O(log n)` 时间内快速地处理查询操作，解决这个问题。

---

如果不能使用 `bisect.bisect_right(values, (timestamp, chr(127)))`，我们可以手动实现二分查找来替代它。下面是使用**手动实现的二分查找**的解决方案。

### 手动实现二分查找代码

```python
from collections import defaultdict

class TimeMap:

    def __init__(self):
        # 使用 defaultdict 来存储每个 key 对应的 (timestamp, value) 列表
        self.time_map = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        # 将 (timestamp, value) 添加到 key 对应的列表中
        self.time_map[key].append((timestamp, value))

    def get(self, key: str, timestamp: int) -> str:
        # 如果 key 不存在，直接返回空字符串
        if key not in self.time_map:
            return ""
        
        # 获取 key 对应的所有 (timestamp, value) 对
        values = self.time_map[key]
        
        # 手动实现二分查找，找到最后一个 timestamp 小于等于查询 timestamp 的位置
        return self.binary_search(values, timestamp)

    def binary_search(self, values: list, timestamp: int) -> str:
        left, right = 0, len(values) - 1
        idx = -1  # 初始化 idx，表示找到的最近时间戳的索引位置
        
        while left <= right:
            mid = (left + right) // 2
            
            # 如果当前时间戳小于等于给定的 timestamp，则可能是我们需要的解
            if values[mid][0] <= timestamp:
                idx = mid  # 记录当前的索引
                left = mid + 1  # 移动左边界，继续向右找更大的时间戳
            else:
                right = mid - 1  # 当前时间戳太大，向左搜索
        
        # 如果找到合适的时间戳，返回对应的值；如果没有找到，返回空字符串
        if idx == -1:
            return ""
        else:
            return values[idx][1]
```

### 代码解释

1. **`set` 操作**：
   - 这部分与之前相同，将 `(timestamp, value)` 存储在 `time_map` 字典中，字典的键是 `key`，值是一个包含时间戳和对应值的列表。

2. **`get` 操作**：
   - 如果 `key` 不存在，直接返回 `""`。
   - 使用手动实现的二分查找方法 `binary_search()` 来查找最接近且小于等于 `timestamp` 的时间戳对应的值。

3. **`binary_search` 函数**：
   - 二分查找的目标是找到最后一个**小于等于 `timestamp`** 的 `values[mid][0]`。我们通过调整左右边界 `left` 和 `right` 来缩小搜索范围。
   - 如果当前时间戳 `values[mid][0] <= timestamp`，那么有可能是答案，记录 `mid` 并继续向右查找（`left = mid + 1`）是否有更接近的时间戳。
   - 如果当前时间戳 `values[mid][0] > timestamp`，则需要向左搜索（`right = mid - 1`）。
   - 最后返回最近的时间戳对应的值，如果没有合适的时间戳，则返回 `""`。

---

### 复杂度分析

- **时间复杂度**：
  - `set` 操作是 O(1)，因为我们只是将值添加到列表末尾。
  - `get` 操作的时间复杂度是 O(log n)，其中 `n` 是 `key` 对应的时间戳数量，二分查找的复杂度为 O(log n)。
  
- **空间复杂度**：O(n)，需要存储所有 `(timestamp, value)` 的键值对。

---

### 示例

```python
kv = TimeMap()
kv.set("foo", "bar", 1)   # 存储 "foo" 在时间戳 1 时的值 "bar"
kv.set("foo", "bar2", 4)  # 存储 "foo" 在时间戳 4 时的值 "bar2"
print(kv.get("foo", 1))   # 输出 "bar" （直接找到时间戳 1）
print(kv.get("foo", 3))   # 输出 "bar" （最近的时间戳是 1）
print(kv.get("foo", 4))   # 输出 "bar2" （直接找到时间戳 4）
print(kv.get("foo", 5))   # 输出 "bar2" （最近的时间戳是 4）
```

输出：
```
bar
bar
bar2
bar2
```

---

### 总结

我们使用了手动实现的二分查找来代替 `bisect.bisect_right`，确保能够高效地找到最后一个小于等于 `timestamp` 的时间戳。这个解决方案在处理带有时间戳的键值对存储和查询时非常有效，特别是当我们需要在大量数据中进行快速查询时。
