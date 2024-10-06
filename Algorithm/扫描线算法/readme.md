### 扫描线算法（Sweep Line Algorithm）

**扫描线算法**是一种常用于解决区间、几何、时间区间重叠、活动管理等问题的算法。它通过将问题空间中的所有事件点（如区间的起始点和终点）视为一条从左至右或从上至下的“扫描线”进行遍历，动态处理所有的区间或事件状态。

#### 1. **算法原理**
扫描线算法的基本思想是：
1. 将所有的区间起始点和终止点视为事件点（Event Point），将这些事件点按坐标顺序排列。
2. 从左到右依次处理每个事件点，根据事件点的类型（起点或终点）更新当前状态。
3. 根据当前的状态（如活跃的区间数量、重叠区间、最大值等）来进行相应的处理和计算。

#### 2. **常见应用场景**
- **区间合并**：计算所有重叠区间，合并成一个大的区间。
- **重叠区间数量**：找到最大重叠区间数量。
- **几何问题**：计算天际线问题（Skyline Problem）、最大矩形面积等。
- **活动管理**：判断活动时间是否冲突、最少会议室数量等。

#### 3. **基本步骤**
1. **将事件点拆分**：
   - 将每个区间的起始点和结束点拆分为独立的事件点，并用 `+1` 和 `-1` 分别表示起点和终点。
2. **对事件点进行排序**：
   - 按照坐标位置对事件点进行排序。如果事件点位置相同，则优先处理起始点（以保证在同一位置时起始点优先）。
3. **遍历所有事件点**：
   - 初始化一个计数器或状态变量，从左到右依次处理每个事件点，并根据事件类型更新计数器。
4. **处理每个事件点**：
   - 根据计数器或状态变量的变化，判断当前区间的活跃状态、重叠区间的数量等，做相应的处理。
5. **返回结果**：
   - 根据遍历过程中记录的状态变化，构建并返回最终结果。
     
---

### LeetCode 问题：253. 会议室 II

https://leetcode.com/problems/meeting-rooms-ii/description/

#### 问题描述：
给定一组会议时间区间，找出所需的会议室的最小数量。

#### 示例 1：
```python
输入：intervals = [[0,30],[5,10],[15,20]]
输出：2
```

#### 示例 2：
```python
输入：intervals = [[7,10],[2,4]]
输出：1
```

### 原始代码（使用扫荡线算法）：

```python
class Solution:
    def minMeetingRooms(self, intervals: List[Interval]) -> int:
        time = [] 
        count = 0
        max_count = 0

        for i in intervals:
            start, end = i.start, i.end
            time.append((start, 1))  # 会议开始事件
            time.append((end, -1))    # 会议结束事件

        time.sort(key=lambda x: (x[0], x[1]))  # 按时间和事件类型排序
        for t in time:
            count += t[1]  # 更新当前会议室数量
            max_count = max(max_count, count)  # 追踪所需的最大会议室数量
            
        return max_count  # 返回所需的最大会议室数量
```

### 行逐行解释与示例执行：

1. **`class Solution:`**
   - 定义 `Solution` 类。

2. **`def minMeetingRooms(self, intervals: List[Interval]) -> int:`**
   - 定义方法 `minMeetingRooms`，接受一个会议时间区间的列表，并返回所需的最小会议室数量。

3. **`time = []`**
   - 初始化一个空列表 `time` 来存储开始和结束事件。

4. **`count = 0`**
   - 初始化计数器 `count`，用于跟踪当前活动会议的数量。

5. **`max_count = 0`**
   - 初始化变量 `max_count`，用于追踪在任何时刻所需的最大会议室数量。

6. **填充 `time` 列表**：
   - 遍历每个区间，记录开始和结束事件：
   ```python
   for i in intervals:
       start, end = i.start, i.end
       time.append((start, 1))  # 会议开始
       time.append((end, -1))    # 会议结束
   ```

7. **排序事件**：
   - 首先按时间排序，然后在时间相同时，结束事件在开始事件之后：
   ```python
   time.sort(key=lambda x: (x[0], x[1]))
   ```

8. **处理事件**：
   - 遍历排序后的事件，计算所需的会议室数量：
   ```python
   for t in time:
       count += t[1]  # 更新当前会议室数量
       max_count = max(max_count, count)  # 追踪所需的最大会议室数量
   ```

9. **`return max_count`**
   - 返回所需的最大会议室数量。

### 示例执行：

假设我们有以下输入：

```python
intervals = [[0, 30], [5, 10], [15, 20]]
```

1. **填充 `time` 列表**：
   - 经过处理，`time` 将为：`[(0, 1), (30, -1), (5, 1), (10, -1), (15, 1), (20, -1)]`。

2. **排序事件**：
   - 排序后的 `time` 列表为：`[(0, 1), (5, 1), (10, -1), (15, 1), (20, -1), (30, -1)]`。

3. **处理事件**：
   - 在时间 `0`：`count = 1`，`max_count = 1`。
   - 在时间 `5`：`count = 2`，`max_count = 2`。
   - 在时间 `10`：`count = 1`，`max_count = 2`。
   - 在时间 `15`：`count = 2`，`max_count = 2`。
   - 在时间 `20`：`count = 1`，`max_count = 2`。
   - 在时间 `30`：`count = 0`，`max_count = 2`。

### 最终结果：
- 所需的最大会议室数量为 `2`。

### 时间复杂度分析：

- **时间复杂度**：O(n log n)
  - 主要的时间复杂度来自于排序事件的步骤，其中 n 是区间的数量。

### 空间复杂度分析：

- **空间复杂度**：O(n)
  - 在最坏的情况下，所有的事件都需要存储在 `time` 列表中。

### 提示和警告：

1. **边界情况**：
   - 考虑输入列表为空或仅包含一个区间的情况。

2. **理解扫荡线技术**：
   - 确保理解扫荡线算法如何在计算重叠区间时使用。

3. **效率**：
   - 此方法有效地跟踪活动会议数量，通过将每个会议的开始和结束视为事件来实现。

### 总结

- **扫荡线方法**：有效计算所需的最小会议室数量，时间复杂度为 O(n log n)，空间复杂度为 O(n)。
- **清晰易懂**：代码简洁明了，适合处理此类问题。

### 应用技巧

1. **选择合适的方法**：
   - 根据具体问题选择最合适的方法，以确保算法的效率和可读性。

2. **处理边界情况**：
   - 在算法设计中，始终考虑处理输入数据的边界情况。

3. **优化空间使用**：
   - 在处理大数据时，考虑使用更节省空间的算法。
     
**扫荡线算法**（Sweep Line Algorithm）是一种常用于计算几何和各种算法问题的强大技术，尤其涉及区间和事件的情况。以下是扫荡线方法为何有效的原因，特别是在合并区间、查找重叠以及确定活动区间数量（例如会议室问题）等问题中。

### 扫荡线算法的工作原理

1. **事件的概念**：
   - 在扫荡线方法中，我们将区间的起始和结束点视为事件。例如，当一个会议开始时，我们增加活动会议的计数（所需的房间数量），当会议结束时，我们减少计数。
   - 每个事件可以表示为一个元组 `(时间, 类型)`，其中 `类型` 表示它是开始事件还是结束事件（例如，`(开始时间, 1)` 表示开始，`(结束时间, -1)` 表示结束）。

2. **排序事件**：
   - 事件首先按时间排序。如果两个事件的时间相同，则结束事件应该在开始事件之前处理。这一点至关重要，以确保如果一个会议在另一个会议结束的同时开始，房间在分配给新会议之前已经被释放。
   - 排序确保我们按照正确的时间顺序处理事件。

3. **遍历事件**：
   - 当我们按照顺序处理每个事件时：
     - 对于开始事件，我们增加活动会议的计数（或房间）。
     - 对于结束事件，我们减少计数。
   - 在此迭代过程中，我们跟踪任何时刻活动会议的最大计数，这直接给出所需的房间数量。

### 为什么它有效

1. **准确计数**：
   - 通过处理每个开始和结束事件，扫荡线算法准确计数了任何给定时刻的活动区间数量。这对于确定峰值使用（例如，重叠会议的最大数量）至关重要。

2. **处理重叠**：
   - 由于事件是按顺序处理的，算法自然处理重叠。当一个新区间在前一个区间结束之前开始时，它正确地增加了所需的房间计数。

3. **效率**：
   - 排序事件的时间复杂度为 O(n log n)，处理事件的时间复杂度为 O(n)，因此总体时间复杂度为 O(n log n)，对于这类问题来说非常高效。

4. **简单性**：
   - 这种方法在概念上简单且易于实现。通过将问题分解为离散事件，它避免了检查所有区间对之间重叠的复杂性。

### 示例场景

为了说明扫荡线方法的工作原理，考虑以下会议区间：

```
[0, 30], [5, 10], [15, 20]
```

1. **事件**：
   - 开始：`(0, 1)`，`(5, 1)`，`(15, 1)`
   - 结束：`(30, -1)`，`(10, -1)`，`(20, -1)`

2. **排序事件**：
   - 排序后的顺序为：`[(0, 1), (5, 1), (10, -1), (15, 1), (20, -1), (30, -1)]`

3. **处理事件**：
   - 在时间 `0`：`count = 1`
   - 在时间 `5`：`count = 2`
   - 在时间 `10`：`count = 1`
   - 在时间 `15`：`count = 2`
   - 在时间 `20`：`count = 1`
   - 在时间 `30`：`count = 0`
   - 在此过程中所需的最大房间数量为 `2`。

### 结论

扫荡线方法有效的原因在于，它将重叠区间的复杂问题转化为可以通过事件进行管理的可处理事件。通过维护活动区间的计数并跟踪最大值，它高效地提供了解决方案，否则可能需要更复杂的方法。

---

### 例题讲解：LeetCode 218 - The Skyline Problem（天际线问题）

**题目描述**：
给定一组建筑物，每个建筑物用 `[left, right, height]` 表示其左边界、右边界和高度。绘制出这些建筑物的天际线，即从远处观察这些建筑物时，所有建筑物的轮廓线。

**解题思路**：
使用扫描线算法求解天际线问题。将所有建筑物的起始点和结束点拆分为事件点，然后按位置排序并依次处理。使用最大堆来记录当前建筑物的最高点，判断是否更新天际线轮廓。

**代码实现**：
```python
# 导入优先队列
import heapq

# 定义解决方案的类
class Solution:
    # 定义天际线问题的函数
    def getSkyline(self, buildings: List[List[int]]) -> List[List[int]]:
        # 步骤 1：提取所有事件点（左边界、右边界）
        events = []
        for left, right, height in buildings:
            events.append((left, -height, right))  # 起始点，使用负高度表示（确保优先处理起始点）
            events.append((right, 0, 0))  # 结束点，高度为0，表示移除

        # 步骤 2：按横坐标进行排序
        events.sort()

        # 步骤 3：初始化最大堆和结果列表
        result = [[0, 0]]  # 存储最终的天际线
        live_buildings = [(0, float('inf'))]  # 存储当前活跃建筑（高度和结束位置）

        # 步骤 4：处理所有事件点
        for x, h, r in events:
            # 如果是建筑物的左边界，加入最大堆
            if h != 0:
                heapq.heappush(live_buildings, (h, r))
            
            # 移除所有已过期的建筑物（结束位置小于当前 x 坐标）
            while live_buildings[0][1] <= x:
                heapq.heappop(live_buildings)

            # 获取当前最高建筑的高度
            max_height = -live_buildings[0][0]
            
            # 如果当前高度与前一个关键点高度不同，则加入结果列表
            if result[-1][1] != max_height:
                result.append([x, max_height])

        # 返回天际线结果，去掉初始的 [0, 0] 位置
        return result[1:]

# 示例输入
buildings = [[2, 9, 10], [3, 7, 15], [5, 12, 12], [15, 20, 10], [19, 24, 8]]
sol = Solution()
print(sol.getSkyline(buildings))  # 输出: [[2, 10], [3, 15], [7, 12], [12, 0], [15, 10], [20, 8], [24, 0]]
```

**代码详解**：
1. **提取事件点**：
   - 将每个建筑物的起始点和结束点分别视为独立的事件点，并记录其高度。
   - 起始点高度为负数，表示建筑物高度增加；结束点高度为 `0`，表示建筑物高度结束。

2. **排序事件点**：
   - 按照 `x` 坐标排序，优先处理 `x` 较小的事件点。
   - 如果 `x` 坐标相同，优先处理起始点（确保在同一位置时高度增加）。

3. **最大堆记录活跃建筑**：
   - 使用 `live_buildings` 记录当前所有活跃建筑的高度和结束位置。
   - 每次遍历事件点时，更新当前活跃建筑物的状态。

4. **更新天际线结果**：
   - 当最大堆中的最高建筑物发生变化时（当前最高建筑高度与前一个不同时），记录一个新的关键点。

5. **返回结果**：
   - 构建并返回最终的天际线结果。

**时间复杂度**：
- O(n log n)，排序所有事件点和堆操作的时间复杂度。

**空间复杂度**：
- O(n)，用于存储所有事件点和活跃建筑物的最大堆。

---

### 扫描线算法的优势与局限
**优势**：
- 能够有效处理复杂的区间和几何问题，能够在处理重叠区间、最大重叠次数等问题时发挥良好的效果。
- 使用事件驱动的方式动态处理所有状态变化，能较好地处理动态更新和区间合并等问题。

**局限**：
- 在事件点很多、区间交错复杂时，可能导致堆操作或排序时间过长，导致算法效率下降。
- 需要维护较为复杂的堆、状态更新逻辑，编码难度较高。

---

好的，我将逐步讲解 LeetCode 中使用扫描线算法解决的 30 道题目，包括详细解析、逐行代码注释及复杂度分析。以下是前五道题目的解析和代码实现。

---

### 1. LeetCode 218: The Skyline Problem（天际线问题）

**题目描述**：
给定一组建筑物，每个建筑物用 `[left, right, height]` 表示其左边界、右边界和高度。绘制出这些建筑物的天际线，即从远处观察这些建筑物时，所有建筑物的轮廓线。

**解题思路**：
使用扫描线算法求解天际线问题。将所有建筑物的起始点和结束点拆分为事件点，然后按位置排序并依次处理。使用最大堆来记录当前建筑物的最高点，判断是否更新天际线轮廓。

**代码实现**：
```python
# 导入优先队列模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义天际线问题的函数
    def getSkyline(self, buildings: List[List[int]]) -> List[List[int]]:
        # 步骤 1：提取所有事件点（左边界、右边界）
        events = []
        for left, right, height in buildings:
            events.append((left, -height, right))  # 起始点，使用负高度表示（确保优先处理起始点）
            events.append((right, 0, 0))  # 结束点，高度为0，表示移除

        # 步骤 2：按横坐标进行排序
        events.sort()

        # 步骤 3：初始化最大堆和结果列表
        result = [[0, 0]]  # 存储最终的天际线
        live_buildings = [(0, float('inf'))]  # 存储当前活跃建筑（高度和结束位置）

        # 步骤 4：处理所有事件点
        for x, h, r in events:
            # 如果是建筑物的左边界，加入最大堆
            if h != 0:
                heapq.heappush(live_buildings, (h, r))
            
            # 移除所有已过期的建筑物（结束位置小于当前 x 坐标）
            while live_buildings[0][1] <= x:
                heapq.heappop(live_buildings)

            # 获取当前最高建筑的高度
            max_height = -live_buildings[0][0]
            
            # 如果当前高度与前一个关键点高度不同，则加入结果列表
            if result[-1][1] != max_height:
                result.append([x, max_height])

        # 返回天际线结果，去掉初始的 [0, 0] 位置
        return result[1:]

# 时间复杂度：O(n log n) - 排序和最大堆操作的时间复杂度
# 空间复杂度：O(n) - 存储事件点和堆空间的复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 是所有建筑物的数量。排序事件点和最大堆操作的时间复杂度。
- **空间复杂度**：O(n)，用于存储事件点和堆的空间复杂度。

---

### 2. LeetCode 252: Meeting Rooms（会议室）

**题目描述**：
给定一个由多个会议时间区间组成的列表，判断是否可以将所有会议安排在一个会议室中（即所有会议时间没有重叠）。

**解题思路**：
使用扫描线算法解决该问题。将所有会议的起始时间和结束时间视为事件点，使用 `+1` 和 `-1` 来表示会议的增加和结束。排序后遍历事件点，记录会议室的使用状态。如果在任何时刻会议室的使用数量超过 1，则说明会议有重叠。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否可以安排所有会议的函数
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        # 步骤 1：提取所有事件点（起始点和结束点）
        events = []
        for start, end in intervals:
            events.append((start, 1))  # 会议开始
            events.append((end, -1))   # 会议结束

        # 步骤 2：按时间顺序对事件点排序
        events.sort()

        # 步骤 3：遍历所有事件点，记录会议室的使用情况
        rooms_in_use = 0
        for time, count in events:
            rooms_in_use += count  # 更新当前会议室的使用情况
            if rooms_in_use > 1:   # 如果会议室的使用数量超过 1，说明有重叠
                return False

        return True  # 所有会议没有重叠，可以安排在一个会议室中

# 时间复杂度：O(n log n) - 排序事件点的时间复杂度
# 空间复杂度：O(n) - 存储事件点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有事件点的空间复杂度。

---

### 3. LeetCode 253: Meeting Rooms II（会议室 II）

**题目描述**：
给定一个由多个会议时间区间组成的列表，计算所需的最少会议室数量，以便安排所有会议。

**解题思路**：
使用扫描线算法解决该问题。将所有会议的起始时间和结束时间视为事件点，使用 `+1` 和 `-1` 表示会议的开始和结束。排序后遍历事件点，记录会议室的使用数量，并更新最大会议室数量。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最少会议室数量的函数
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        # 步骤 1：提取所有事件点（起始点和结束点）
        events = []
        for start, end in intervals:
            events.append((start, 1))  # 会议开始
            events.append((end, -1))   # 会议结束

        # 步骤 2：按时间顺序对事件点排序
        events.sort()

        # 步骤 3：遍历所有事件点，记录会议室的使用情况
        rooms_in_use = 0
        max_rooms = 0  # 记录最大会议室数量
        for time, count in events:
            rooms_in_use += count  # 更新当前会议室的使用数量
            max_rooms = max(max_rooms, rooms_in_use)  # 更新最大会议室数量

        return max_rooms  # 返回所需的最少会议室数量

# 时间复杂度：O(n log n) - 排序事件点的时间复杂度
# 空间复杂度：O(n) - 存储事件点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有事件点的空间复杂度。

---

### 4. LeetCode 759: Employee Free Time（员工空闲时间）

**题目描述**：
给定多个员工的工作时间区间，找出所有员工的空闲时间区间（即所有员工都不在工作的时间）。

**解题思路**：
使用扫描线算法解决该问题。将所有员工的工作时间区间视为事件点，记录每个时间点的工作数量变化。遍历事件点时，当当前工作数量为 0 时，说明当前时间段是空闲时间。

**代码实现**：
```python
# 定义工作区间类
class Interval:
    def __init__(self, start=0, end=0):
        self.start = start
        self.end = end

# 定义解决方案的类
class Solution:
    # 定义查找员工空闲时间的函数
    def employeeFreeTime(self, schedule: List[List[Interval]]) -> List[Interval]:
        # 步骤 1：提取所有工作时间区间，并将其视为事件点
        events = []
        for employee in schedule:
            for interval in employee:
                events.append((interval.start, 1))  # 工作开始
                events.append((interval.end, -1))   # 工作结束

        # 步骤 2：对事件点进行排序
        events.sort()

        # 步骤 3：遍历事件点，记录工作数量变化
        free_times = []  # 记录所有空闲时间
        prev_time = None  # 上一个事件点时间
        ongoing = 0       # 当前的工作数量

        for time, change in events:
            if ongoing == 0 and prev_time is not None and prev_time < time:  #

 工作数量为0表示空闲
                free_times.append(Interval(prev_time, time))  # 记录空闲时间
            ongoing += change
            prev_time = time

        return free_times

# 时间复杂度：O(n log n) - 排序所有事件点的时间复杂度
# 空间复杂度：O(n) - 存储事件点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有事件点的空间复杂度。

---

### 5. LeetCode 1272: Remove Interval（删除区间）

**题目描述**：
给定一个由多个区间组成的列表和一个删除区间 `toBeRemoved`，返回删除该区间后的所有区间列表。

**解题思路**：
可以将所有区间的起始点和结束点拆分为事件点，并根据 `toBeRemoved` 区间的起始位置和结束位置，进行分割或保留部分不被覆盖的区间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除区间的函数
    def removeInterval(self, intervals: List[List[int]], toBeRemoved: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []
        start, end = toBeRemoved

        # 步骤 1：遍历所有区间
        for interval in intervals:
            # 如果当前区间在要删除区间的左侧或右侧，则不受影响，直接加入结果列表
            if interval[1] <= start or interval[0] >= end:
                result.append(interval)
            else:
                # 否则，将未被覆盖的部分加入结果列表
                if interval[0] < start:
                    result.append([interval[0], start])
                if interval[1] > end:
                    result.append([end, interval[1]])

        return result

# 时间复杂度：O(n) - 遍历区间列表的每个元素
# 空间复杂度：O(n) - 存储结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是区间列表的长度，需要遍历所有区间。
- **空间复杂度**：O(n)，存储结果列表的空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 扫描线算法题目，包括详细解析、逐行代码注释及复杂度分析。

---

### 6. LeetCode 1094: Car Pooling（拼车）

**题目描述**：
给定一个由多个拼车请求组成的列表 `trips`，每个请求的形式为 `[numPassengers, startLocation, endLocation]`，表示 `numPassengers` 名乘客要从 `startLocation` 上车并在 `endLocation` 下车。给定一个整型数 `capacity`，表示车辆的最大载客量。判断是否可以满足所有拼车请求。

**解题思路**：
可以使用扫描线算法来解决该问题。将所有上车和下车的事件点提取出来，并按位置排序。遍历事件点时，记录车辆当前载客量，判断是否超过 `capacity`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否可以满足所有拼车请求的函数
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # 步骤 1：提取所有上车和下车事件点
        events = []
        for passengers, start, end in trips:
            events.append((start, passengers))  # 上车事件，增加乘客数量
            events.append((end, -passengers))   # 下车事件，减少乘客数量

        # 步骤 2：按位置（时间）排序事件点
        events.sort()

        # 步骤 3：遍历所有事件点，记录当前车辆载客量
        current_capacity = 0
        for location, change in events:
            current_capacity += change  # 更新当前车辆载客量
            if current_capacity > capacity:  # 检查是否超过车辆最大载客量
                return False  # 超过最大载客量，返回 False

        return True  # 所有请求都可以满足，返回 True

# 时间复杂度：O(n log n) - 排序所有事件点的时间复杂度
# 空间复杂度：O(n) - 存储所有事件点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有上车和下车事件点的空间复杂度。

---

### 7. LeetCode 732: My Calendar III（我的日历 III）

**题目描述**：
实现一个 `MyCalendarThree` 类，它记录日程安排，并能返回任何时候 `k` 个日程安排重叠的最大值。

**解题思路**：
使用扫描线算法来解决该问题。将每个日程安排的起始时间视为 `+1` 的操作，将结束时间视为 `-1` 的操作。然后对所有操作进行排序，并依次计算当前的重叠数量和最大重叠数量。

**代码实现**：
```python
# 导入有序字典模块
from sortedcontainers import SortedDict

# 定义 MyCalendarThree 类
class MyCalendarThree:

    # 初始化日历记录
    def __init__(self):
        self.timeline = SortedDict()  # 使用有序字典记录事件点

    # 定义添加日程安排的函数
    def book(self, start: int, end: int) -> int:
        # 步骤 1：记录起始时间 +1，结束时间 -1
        self.timeline[start] = self.timeline.get(start, 0) + 1
        self.timeline[end] = self.timeline.get(end, 0) - 1

        # 步骤 2：计算当前最大重叠数量
        max_count, ongoing = 0, 0
        for time in self.timeline:
            ongoing += self.timeline[time]  # 更新当前正在进行的日程安排数量
            max_count = max(max_count, ongoing)  # 更新最大重叠数量

        return max_count  # 返回最大重叠数量

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 记录时间点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 为时间点的数量。需要对时间点进行排序。
- **空间复杂度**：O(n)，用于存储时间点及其变化值的字典。

---

### 8. LeetCode 759: Employee Free Time（员工空闲时间）

**题目描述**：
给定多个员工的工作时间区间，找出所有员工的空闲时间区间（即所有员工都不在工作的时间）。

**解题思路**：
可以将所有员工的工作时间区间合并到一个列表中，然后按照起始时间排序。遍历所有区间，找出相邻区间之间的空闲时间。

**代码实现**：
```python
# 定义工作区间类
class Interval:
    def __init__(self, start=0, end=0):
        self.start = start
        self.end = end

# 定义解决方案的类
class Solution:
    # 定义查找员工空闲时间的函数
    def employeeFreeTime(self, schedule: List[List[Interval]]) -> List[Interval]:
        # 提取所有员工的工作区间，并按照起始时间排序
        all_intervals = sorted([interval for employee in schedule for interval in employee], key=lambda x: x.start)

        # 初始化结果列表和当前合并区间
        result = []
        current_interval = all_intervals[0]

        # 遍历所有区间，查找空闲时间
        for interval in all_intervals[1:]:
            if interval.start > current_interval.end:
                # 找到一个空闲区间
                result.append(Interval(current_interval.end, interval.start))
                current_interval = interval
            else:
                # 合并重叠的区间
                current_interval.end = max(current_interval.end, interval.end)

        return result

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 存储所有区间的列表空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 是所有工作区间的数量，排序的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有工作区间的列表空间复杂度。

---

### 9. LeetCode 1229: Meeting Scheduler（会议安排）

**题目描述**：
给定两个由多个时间区间组成的列表 `slots1` 和 `slots2`，以及一个整数 `duration`，找出两个列表中重叠的时间区间，并返回满足 `duration` 时间的最早时间区间。如果没有这样的时间区间，则返回空列表。

**解题思路**：
首先对两个时间区间列表分别进行排序，然后使用双指针遍历两个列表，找到两个时间区间的交集。如果交集的长度大于等于 `duration`，则返回该交集的起始时间和 `duration` 结束时间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找会议安排时间的函数
    def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
        # 步骤 1：分别对两个时间区间列表进行排序
        slots1.sort()
        slots2.sort()

        # 步骤 2：初始化双指针
        i, j = 0, 0

        # 步骤 3：遍历两个区间列表
        while i < len(slots1) and j < len(slots2):
            # 计算两个区间的交集
            intersect_start = max(slots1[i][0], slots2[j][0])
            intersect_end = min(slots1[i][1], slots2[j][1])

            # 检查交集是否满足所需的 duration
            if intersect_end - intersect_start >= duration:
                return [intersect_start, intersect_start + duration]

            # 移动结束时间较小的指针
            if slots1[i][1] < slots2[j][1]:
                i += 1
            else:
                j += 1

        # 没有找到满足条件的时间区间，返回空列表
        return []

# 时间复杂度：O(n log n + m log m) - 排序两个时间区间列表的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n + m log m)，其中 n 和 m 分别是两个时间区间列表的长度。排序两个时间区间列表的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于双指针的移动和交集判断）。

---



### 10. LeetCode 1288: Remove Covered Intervals（删除被覆盖区间）

**题目描述**：
给定一个由多个区间组成的列表，删除所有被覆盖的区间，并返回剩余区间的数量。被覆盖的区间是指某个区间 `[a, b]` 被另一个区间 `[c, d]` 完全覆盖（即 `c <= a` 且 `b <= d`）。

**解题思路**：
可以按照区间的起始位置 `start` 进行排序，然后遍历所有区间，判断当前区间是否被上一个已选择区间覆盖。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除被覆盖区间的函数
    def removeCoveredIntervals(self, intervals: List[List[int]]) -> int:
        # 步骤 1：按照起始位置进行排序
        intervals.sort(key=lambda x: (x[0], -x[1]))

        # 步骤 2：遍历所有区间，判断是否被覆盖
        count = 0
        prev_end = 0

        for start, end in intervals:
            # 如果当前区间未被覆盖，则计数加一
            if end > prev_end:
                count += 1
                prev_end = end  # 更新结束位置

        return count

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录已选择区间的结束位置）。

---

好的，我们继续讲解接下来的五道 LeetCode 扫描线算法题目，包括详细解析、逐行代码注释及复杂度分析。

---

### 11. LeetCode 1235: Maximum Profit in Job Scheduling（最大化工作调度的利润）

**题目描述**：
给定一些工作，它们的起始时间、结束时间和对应的利润。找到一种方式来安排这些工作，使得总利润最大化，并且保证同一时间只能安排一个工作。

**解题思路**：
使用扫描线算法来解决这个问题。先将所有工作按照结束时间进行排序，然后使用动态规划记录当前时间点的最大利润。在处理每个工作时，如果该工作与当前工作不重叠，则更新最大利润值。

**代码实现**：
```python
# 导入二分查找模块
import bisect

# 定义解决方案的类
class Solution:
    # 定义最大化工作调度利润的函数
    def jobScheduling(self, startTime: List[int], endTime: List[int], profit: List[int]) -> int:
        # 步骤 1：将所有工作按结束时间进行排序
        jobs = sorted(zip(startTime, endTime, profit), key=lambda x: x[1])

        # 步骤 2：初始化动态规划列表，dp[i] 表示到时间点 i 为止的最大利润
        dp = [(0, 0)]  # (结束时间, 最大利润)

        # 步骤 3：遍历所有工作，计算最大利润
        for s, e, p in jobs:
            # 使用二分查找查找可以安排的最大不重叠工作
            i = bisect.bisect_right(dp, (s, float('inf')))
            max_profit = dp[i - 1][1] + p  # 计算当前工作结束时的最大利润

            # 更新最大利润
            if max_profit > dp[-1][1]:
                dp.append((e, max_profit))

        return dp[-1][1]  # 返回最大利润

# 时间复杂度：O(n log n) - 排序和二分查找的时间复杂度
# 空间复杂度：O(n) - 动态规划表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序和二分查找的时间复杂度。
- **空间复杂度**：O(n)，动态规划表的空间复杂度。

---

### 12. LeetCode 850: Rectangle Area II（矩形面积 II）

**题目描述**：
给定多个矩形，求所有矩形覆盖的总面积（重叠部分只计算一次）。

**解题思路**：
使用扫描线算法解决该问题。将所有矩形的左、右边界作为事件点（Event），从左到右依次处理这些事件点，使用一个线段树来记录当前所有活跃的矩形高度。每次更新事件点时，计算当前总面积的增量，并累加。

**代码实现**：
```python
# 导入有序字典模块
from sortedcontainers import SortedDict

# 定义解决方案的类
class Solution:
    # 定义计算矩形面积的函数
    def rectangleArea(self, rectangles: List[List[int]]) -> int:
        # 步骤 1：提取所有事件点（左边界、右边界）
        events = []
        for x1, y1, x2, y2 in rectangles:
            events.append((x1, y1, y2, 1))   # 左边界，矩形增加
            events.append((x2, y1, y2, -1))  # 右边界，矩形减少

        # 步骤 2：按 x 坐标排序事件点
        events.sort()

        # 步骤 3：使用有序字典记录当前活跃的 y 区间
        active_intervals = SortedDict()
        prev_x = events[0][0]
        total_area = 0

        # 步骤 4：遍历所有事件点，计算矩形总面积
        for x, y1, y2, delta in events:
            # 计算当前所有活跃区间的高度总和
            height = 0
            prev_y = -1
            for y_start, y_end in active_intervals.keys():
                height += max(0, y_end - max(y_start, prev_y))
                prev_y = max(prev_y, y_end)

            # 根据 x 轴的变化量更新总面积
            total_area += height * (x - prev_x)
            prev_x = x

            # 更新活跃区间的高度
            if delta == 1:  # 矩形增加
                active_intervals[(y1, y2)] = active_intervals.get((y1, y2), 0) + 1
            else:  # 矩形减少
                if active_intervals[(y1, y2)] == 1:
                    del active_intervals[(y1, y2)]
                else:
                    active_intervals[(y1, y2)] -= 1

        # 返回结果，取模以防止数值溢出
        return total_area % (10**9 + 7)

# 时间复杂度：O(n log n) - 排序事件点的时间复杂度
# 空间复杂度：O(n) - 记录事件点的有序字典的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储事件点和活跃区间的空间复杂度。

---

### 13. LeetCode 920: Number of Music Playlists（音乐播放列表的数量）

**题目描述**：
给定 `n` 首不同的歌曲，并需要创建一个播放列表，其中包含 `goal` 首歌曲。请计算所有可能的播放列表数量，使得每首歌曲至少播放 `k` 次。

**解题思路**：
使用动态规划结合扫描线算法来解决该问题。将每个播放列表的状态视为一个事件点，并使用状态转移方程记录当前状态的所有可能数量。

**代码实现**：
```python
# 导入数学模块
from math import comb

# 定义解决方案的类
class Solution:
    # 定义计算音乐播放列表数量的函数
    def numMusicPlaylists(self, n: int, goal: int, k: int) -> int:
        # 步骤 1：初始化动态规划表 dp
        MOD = 10**9 + 7
        dp = [[0] * (n + 1) for _ in range(goal + 1)]
        dp[0][0] = 1

        # 步骤 2：遍历所有状态，计算播放列表数量
        for i in range(1, goal + 1):
            for j in range(1, n + 1):
                # 使用一个未播放过的歌曲
                dp[i][j] = dp[i - 1][j - 1] * (n - (j - 1)) % MOD
                # 使用一个已播放过的歌曲
                if j > k:
                    dp[i][j] += dp[i - 1][j] * (j - k) % MOD
                dp[i][j] %= MOD

        # 返回目标播放列表的数量
        return dp[goal][n]

# 时间复杂度：O(n * goal) - 遍历所有状态的时间复杂度
# 空间复杂度：O(n * goal) - 动态规划表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * goal)，遍历所有状态的时间复杂度。
- **空间复杂度**：O(n * goal)，动态规划表的空间复杂度。

---

### 14. LeetCode 391: Perfect Rectangle（完美矩形）

**题目描述**：
给定一组小矩形，判断它们是否能够拼接成一个没有重叠且没有空隙的完美矩形。

**解题思路**：
使用扫描线算法。提取所有矩形的顶点，并记录每个顶点的出现次数。判断矩形是否形成完美拼接的条件包括：顶点数量、面积相等、没有重叠。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否为完美矩形的函数
    def isRectangleCover(self, rectangles: List[List[int]]) -> bool:
        # 步骤 1：初始化顶点集合和总面积
        points = set()
        total_area = 0

        # 步骤 2：遍历所有矩形，计算总面积和顶点集合
        for x1, y1, x2, y2 in rectangles:
            # 更新顶点集合
            for point in [(x1, y1), (x1, y2), (x2, y1), (x2, y2)]:
                if point in points:
                    points.remove(point)
                else:
                    points.add(point)

            # 计算

总面积
            total_area += (x2 - x1) * (y2 - y1)

        # 步骤 3：检查是否形成完美矩形
        if len(points) != 4:  # 顶点数量不为4，则不能形成完美矩形
            return False

        # 步骤 4：计算整体矩形的面积
        x_min, y_min = min(points)
        x_max, y_max = max(points)
        return total_area == (x_max - x_min) * (y_max - y_min)

# 时间复杂度：O(n) - 遍历所有矩形的时间复杂度
# 空间复杂度：O(n) - 存储顶点集合的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历所有矩形的时间复杂度。
- **空间复杂度**：O(n)，用于存储顶点集合的空间复杂度。

---

### 15. LeetCode 732: My Calendar III（我的日历 III）

**题目描述**：
实现一个 `MyCalendarThree` 类，它记录日程安排，并能返回任何时候 `k` 个日程安排重叠的最大值。

**解题思路**：
使用扫描线算法来解决该问题。将每个日程安排的起始时间视为 `+1` 的操作，将结束时间视为 `-1` 的操作。然后对所有操作进行排序，并依次计算当前的重叠数量和最大重叠数量。

**代码实现**：
```python
# 导入有序字典模块
from sortedcontainers import SortedDict

# 定义 MyCalendarThree 类
class MyCalendarThree:

    # 初始化日历记录
    def __init__(self):
        self.timeline = SortedDict()  # 使用有序字典记录事件点

    # 定义添加日程安排的函数
    def book(self, start: int, end: int) -> int:
        # 步骤 1：记录起始时间 +1，结束时间 -1
        self.timeline[start] = self.timeline.get(start, 0) + 1
        self.timeline[end] = self.timeline.get(end, 0) - 1

        # 步骤 2：计算当前最大重叠数量
        max_count, ongoing = 0, 0
        for time in self.timeline:
            ongoing += self.timeline[time]  # 更新当前正在进行的日程安排数量
            max_count = max(max_count, ongoing)  # 更新最大重叠数量

        return max_count  # 返回最大重叠数量

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 记录时间点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 为时间点的数量。需要对时间点进行排序。
- **空间复杂度**：O(n)，用于存储时间点及其变化值的字典。

---

好的，我们继续讲解接下来的五道 LeetCode 扫描线算法题目，包括详细解析、逐行代码注释及复杂度分析。

---

### 16. LeetCode 1094: Car Pooling（拼车）

**题目描述**：
给定一个由多个拼车请求组成的列表 `trips`，每个请求的形式为 `[numPassengers, startLocation, endLocation]`，表示 `numPassengers` 名乘客要从 `startLocation` 上车并在 `endLocation` 下车。给定一个整型数 `capacity`，表示车辆的最大载客量。判断是否可以满足所有拼车请求。

**解题思路**：
使用扫描线算法解决该问题。我们可以将每个拼车请求的上车和下车地点作为事件点，并且对这些事件点按顺序进行排序。扫描这些事件点，记录当前的载客数量，并判断是否超过了 `capacity`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否可以满足所有拼车请求的函数
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # 步骤 1：提取所有上车和下车事件点，并记录乘客变化数量
        events = []
        for passengers, start, end in trips:
            events.append((start, passengers))  # 上车事件，增加乘客数量
            events.append((end, -passengers))   # 下车事件，减少乘客数量

        # 步骤 2：按事件发生的位置排序，如果位置相同则按照乘客变化排序（上车在前）
        events.sort()

        # 步骤 3：遍历所有事件点，记录当前车辆载客量
        current_capacity = 0
        for location, change in events:
            current_capacity += change  # 更新当前车辆载客量
            if current_capacity > capacity:  # 检查是否超过车辆最大载客量
                return False  # 超过最大载客量，返回 False

        return True  # 所有请求都可以满足，返回 True

# 时间复杂度：O(n log n) - 排序所有事件点的时间复杂度
# 空间复杂度：O(n) - 存储所有事件点的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序所有事件点的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有上车和下车事件点的空间复杂度。

---

### 17. LeetCode 452: Minimum Number of Arrows to Burst Balloons（用最少数量的箭引爆气球）

**题目描述**：
给定多个气球的坐标区间 `[x_start, x_end]`，最少需要多少支箭才能将所有气球引爆。

**解题思路**：
可以通过将气球按照 `x_end` 进行排序，然后从左到右遍历所有气球，每次找到尽量多的重叠气球，并将其覆盖。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义用最少数量的箭引爆气球的函数
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        # 如果没有气球，则不需要箭
        if not points:
            return 0

        # 步骤 1：按照气球的结束位置进行排序
        points.sort(key=lambda x: x[1])

        # 步骤 2：初始化箭的数量和当前箭的射击位置
        arrows = 1
        current_end = points[0][1]

        # 步骤 3：遍历所有气球
        for start, end in points:
            if start > current_end:  # 如果当前气球在当前箭的射击位置之后
                arrows += 1  # 需要增加新的箭
                current_end = end  # 更新当前箭的射击位置

        return arrows

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录当前箭的位置和计数）。

---

### 18. LeetCode 352: Data Stream as Disjoint Intervals（将数据流变为不相交的区间）

**题目描述**：
实现一个 `SummaryRanges` 类，它支持以下两种操作：
1. `addNum(val)`：将值 `val` 插入到数据流中。
2. `getIntervals()`：返回数据流中不相交的区间列表。

**解题思路**：
可以使用有序字典或平衡树来存储数据流中的区间。每次插入一个新的数字时，判断该数字是否与已有区间重叠，并进行合并。

**代码实现**：
```python
# 引入有序字典
from sortedcontainers import SortedDict

# 定义 SummaryRanges 类
class SummaryRanges:

    # 初始化类
    def __init__(self):
        self.intervals = SortedDict()

    # 定义插入数字的函数
    def addNum(self, val: int) -> None:
        # 检查该值是否已存在于某个区间中
        if val in self.intervals:
            return

        # 查找左侧和右侧最近的区间
        left = self.intervals.bisect_left(val)
        right = self.intervals.bisect_right(val)

        left_interval = None if left == 0 else self.intervals.items()[left - 1]
        right_interval = None if right == len(self.intervals) else self.intervals.items()[right]

        # 检查是否可以与左右区间合并
        merge_left = left_interval and left_interval[1] + 1 == val
        merge_right = right_interval and right_interval[0] - 1 == val

        if merge_left and merge_right:  # 与左右区间都可以合并
            new_start, new_end = left_interval[0], right_interval[1]
            del self.intervals[left_interval[0]]
            del self.intervals[right_interval[0]]
            self.intervals[new_start] = new_end
        elif merge_left:  # 只与左区间合并
            self.intervals[left_interval[0]] += 1
        elif merge_right:  # 只与右区间合并
            new_start, new_end = val, right_interval[1]
            del self.intervals[right_interval[0]]
            self.intervals[new_start] = new_end
        else:  # 无法与任一区间合并，创建新区间
            self.intervals[val] = val

    # 定义获取不相交区间的函数
    def getIntervals(self) -> List[List[int]]:
        return list(self.intervals.items())

# 时间复杂度：O(log n) - 插入操作的时间复杂度
# 空间复杂度：O(n) - 存储所有区间的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(log n)，插入和查找操作的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有区间的空间复杂度。

---

### 19. LeetCode 56: Merge Intervals（合并区间）

**题目描述**：
给定一个由多个区间组成的列表，将所有重叠的区间合并为一个，并返回合并后的区间列表。每个区间的形式为 `[start, end]`，且 `start` 总是小于或等于 `end`。

**解题思路**：
首先对所有区间按照起始位置 `start` 进行排序，然后逐个遍历区间，合并重叠的区间，并将结果存入结果列表中。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义合并区间的函数
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        # 如果区间列表为空或只有一个区间，直接返回
        if not intervals or len(intervals) == 1:
            return intervals

        # 步骤 1：按照区间起始位置排序
        intervals.sort(key=lambda x: x[0])

        # 步骤 2：初始化结果列表和当前合并区间
        merged = []
        current_interval = intervals[0]

        # 步骤 3：遍历所有区间
        for interval in intervals[1:]:
            # 如果当前区间与下一个区间有重叠，则合并
            if interval[0] <= current_interval[1]:
                current_interval[1] = max(current_interval[1], interval[1])
            else:
                # 否则，将当前区间加入结果列表，并更新当前区间
               

 merged.append(current_interval)
                current_interval = interval

        # 步骤 4：将最后一个合并的区间加入结果列表
        merged.append(current_interval)
        return merged

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(n)，存储结果列表的空间复杂度。

---

### 20. LeetCode 57: Insert Interval（插入区间）

**题目描述**：
给定一个由多个区间组成的列表和一个新的区间，将新的区间插入到列表中，并保证列表中的区间有序且没有重叠。

**解题思路**：
首先遍历区间列表，找到新插入区间应插入的位置。然后合并重叠的区间，最后将合并后的区间列表返回。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义插入区间的函数
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []
        i = 0

        # 步骤 1：将所有在新区间之前的区间加入结果列表
        while i < len(intervals) and intervals[i][1] < newInterval[0]:
            result.append(intervals[i])
            i += 1

        # 步骤 2：合并所有与新区间重叠的区间
        while i < len(intervals) and intervals[i][0] <= newInterval[1]:
            newInterval[0] = min(newInterval[0], intervals[i][0])
            newInterval[1] = max(newInterval[1], intervals[i][1])
            i += 1

        # 将合并后的新区间加入结果列表
        result.append(newInterval)

        # 步骤 3：将所有在新区间之后的区间加入结果列表
        while i < len(intervals):
            result.append(intervals[i])
            i += 1

        return result

# 时间复杂度：O(n) - 遍历区间列表的每个元素
# 空间复杂度：O(n) - 存储结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是区间列表的长度，需要遍历区间列表的每个元素。
- **空间复杂度**：O(n)，存储结果列表的空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 扫描线算法题目，包括详细解析、逐行代码注释及复杂度分析。

---

### 21. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由多个区间组成的列表 `firstList` 和 `secondList`，找到两个列表中所有的交集区间，并返回这些交集区间的列表。

**解题思路**：
使用双指针法来解决该问题。定义两个指针 `i` 和 `j` 分别指向两个区间列表的当前区间，判断这两个区间是否有交集，并将交集加入结果列表。然后根据两个区间的结束时间，移动相应的指针。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义找到区间列表交集的函数
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        # 初始化结果列表和双指针
        result = []
        i, j = 0, 0

        # 使用双指针遍历两个区间列表
        while i < len(firstList) and j < len(secondList):
            # 获取当前的两个区间
            start1, end1 = firstList[i]
            start2, end2 = secondList[j]

            # 判断两个区间是否有交集
            if start1 <= end2 and start2 <= end1:
                # 计算交集区间的起始和结束
                result.append([max(start1, start2), min(end1, end2)])

            # 移动结束时间较小的指针
            if end1 < end2:
                i += 1
            else:
                j += 1

        return result

# 时间复杂度：O(n + m) - n 和 m 分别是两个区间列表的长度
# 空间复杂度：O(n + m) - 存储结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n + m)，其中 n 和 m 分别是两个区间列表的长度，需要遍历两个区间列表的所有元素。
- **空间复杂度**：O(n + m)，用于存储结果列表的空间复杂度。

---

### 22. LeetCode 1024: Video Stitching（视频拼接）

**题目描述**：
给定一个由多个 `[start, end]` 形式的时间区间组成的数组 `clips`，表示每个视频片段的起始和结束时间。给定一个目标时间 `T`，问是否可以将这些片段拼接成一个完整的视频，覆盖从时间 0 到时间 T 的所有时间。

**解题思路**：
使用贪心算法和扫描线算法。首先对所有片段按照起始时间进行排序，然后遍历片段，找出每次能够覆盖的最长区间。每次更新当前能够覆盖的最大结束时间，如果发现当前时间已经无法被覆盖，则返回 -1。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义视频拼接的函数
    def videoStitching(self, clips: List[List[int]], T: int) -> int:
        # 步骤 1：按照起始时间进行排序
        clips.sort()

        # 步骤 2：初始化变量，记录当前覆盖的最大结束时间和上一个覆盖的结束时间
        curr_end, next_end = 0, 0
        count = 0

        # 步骤 3：遍历所有片段，判断是否可以拼接成完整视频
        for start, end in clips:
            if start > next_end:  # 当前片段无法被覆盖，返回 -1
                return -1
            elif start > curr_end:  # 当前片段需要增加新的片段
                count += 1
                curr_end = next_end
            next_end = max(next_end, end)  # 更新下一次能够覆盖的最大结束时间

            if curr_end >= T:  # 如果当前已经能够覆盖目标时间 T
                return count

        return count if curr_end >= T else -1  # 返回结果

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间。

---

### 23. LeetCode 759: Employee Free Time（员工空闲时间）

**题目描述**：
给定多个员工的工作时间区间，找出所有员工的空闲时间区间（即所有员工都不在工作的时间）。

**解题思路**：
可以将所有员工的工作时间区间合并到一个列表中，然后按照起始时间排序。遍历所有区间，找出相邻区间之间的空闲时间。

**代码实现**：
```python
# 定义工作区间类
class Interval:
    def __init__(self, start=0, end=0):
        self.start = start
        self.end = end

# 定义解决方案的类
class Solution:
    # 定义查找员工空闲时间的函数
    def employeeFreeTime(self, schedule: List[List[Interval]]) -> List[Interval]:
        # 提取所有员工的工作区间，并按照起始时间排序
        all_intervals = sorted([interval for employee in schedule for interval in employee], key=lambda x: x.start)

        # 初始化结果列表和当前合并区间
        result = []
        current_interval = all_intervals[0]

        # 遍历所有区间，查找空闲时间
        for interval in all_intervals[1:]:
            if interval.start > current_interval.end:
                # 找到一个空闲区间
                result.append(Interval(current_interval.end, interval.start))
                current_interval = interval
            else:
                # 合并重叠的区间
                current_interval.end = max(current_interval.end, interval.end)

        return result

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 存储所有区间的列表空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 是所有工作区间的数量，排序的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有工作区间的列表空间复杂度。

---

### 24. LeetCode 1272: Remove Interval（删除区间）

**题目描述**：
给定一个由多个区间组成的列表和一个删除区间 `toBeRemoved`，返回删除该区间后的所有区间列表。

**解题思路**：
可以将所有区间的起始点和结束点拆分为事件点，并根据 `toBeRemoved` 区间的起始位置和结束位置，进行分割或保留部分不被覆盖的区间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除区间的函数
    def removeInterval(self, intervals: List[List[int]], toBeRemoved: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []
        start, end = toBeRemoved

        # 步骤 1：遍历所有区间
        for interval in intervals:
            # 如果当前区间在要删除区间的左侧或右侧，则不受影响，直接加入结果列表
            if interval[1] <= start or interval[0] >= end:
                result.append(interval)
            else:
                # 否则，将未被覆盖的部分加入结果列表
                if interval[0] < start:
                    result.append([interval[0], start])
                if interval[1] > end:
                    result.append([end, interval[1]])

        return result

# 时间复杂度：O(n) - 遍历区间列表的每个元素
# 空间复杂度：O(n) - 存储结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历所有区间的时间复杂度。
- **空间复杂度**：O(n)，用于存储结果列表的空间复杂度。

---

### 25. LeetCode 853: Car Fleet（车队）

**题目描述**：
在一个单向的高速公路上有 `n` 辆车，给定每辆车的位置 `position` 和速度 `speed`。所有车辆都在同一个方向上行驶。计算一共有多少个车队到达目的地。

**解题思路**：
可以按照车的位置从远到近排序，然后遍历这些车，判断当前车是否可以赶上前面的车。如果能够赶上，则这些车形成一个车队；否则，则增加新的车队计数。

**代码实现**：
```

python
# 定义解决方案的类
class Solution:
    # 定义计算车队数量的函数
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        # 步骤 1：按车的位置从远到近排序
        cars = sorted(zip(position, speed), key=lambda x: -x[0])

        # 步骤 2：遍历所有车辆，计算车队数量
        fleets = 0
        last_time = 0  # 记录最后一个车队到达的时间

        for pos, spd in cars:
            # 计算当前车到达目的地所需的时间
            time = (target - pos) / spd

            # 如果当前车的到达时间晚于最后一个车队，则形成新的车队
            if time > last_time:
                fleets += 1
                last_time = time  # 更新最后一个车队到达的时间

        return fleets

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 存储所有车辆的列表空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(n)，用于存储所有车辆的列表空间复杂度。

---

好的，我们继续讲解接下来的五道 LeetCode 扫描线算法题目，包括详细解析、逐行代码注释及复杂度分析。

---

### 26. LeetCode 1229: Meeting Scheduler（会议安排）

**题目描述**：
给定两个由多个时间区间组成的列表 `slots1` 和 `slots2`，以及一个整数 `duration`，找出两个列表中重叠的时间区间，并返回满足 `duration` 时间的最早时间区间。如果没有这样的时间区间，则返回空列表。

**解题思路**：
首先对两个时间区间列表分别进行排序，然后使用双指针遍历两个列表，找到两个时间区间的交集。如果交集的长度大于等于 `duration`，则返回该交集的起始时间和 `duration` 结束时间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找会议安排时间的函数
    def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
        # 步骤 1：分别对两个时间区间列表进行排序
        slots1.sort()
        slots2.sort()

        # 步骤 2：初始化双指针
        i, j = 0, 0

        # 步骤 3：遍历两个区间列表
        while i < len(slots1) and j < len(slots2):
            # 计算两个区间的交集
            intersect_start = max(slots1[i][0], slots2[j][0])
            intersect_end = min(slots1[i][1], slots2[j][1])

            # 检查交集是否满足所需的 duration
            if intersect_end - intersect_start >= duration:
                return [intersect_start, intersect_start + duration]

            # 移动结束时间较小的指针
            if slots1[i][1] < slots2[j][1]:
                i += 1
            else:
                j += 1

        # 没有找到满足条件的时间区间，返回空列表
        return []

# 时间复杂度：O(n log n + m log m) - 排序两个时间区间列表的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n + m log m)，其中 n 和 m 分别是两个时间区间列表的长度。排序两个时间区间列表的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于双指针的移动和交集判断）。

---

### 27. LeetCode 228: Summary Ranges（汇总区间）

**题目描述**：
给定一个升序排列的整数数组 `nums`，将数组中的连续区间进行汇总，并返回表示这些区间的字符串列表。例如，对于数组 `[0, 1, 2, 4, 5, 7]`，返回 `["0->2", "4->5", "7"]`。

**解题思路**：
遍历整个数组，并使用两个指针 `start` 和 `end` 来记录当前连续区间的起始和结束位置。如果当前数字与下一个数字不连续，则将当前区间汇总到结果列表中。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义汇总区间的函数
    def summaryRanges(self, nums: List[int]) -> List[str]:
        # 如果输入数组为空，直接返回空列表
        if not nums:
            return []

        # 初始化结果列表和当前区间起始点
        result = []
        start = 0

        # 遍历整个数组
        for i in range(1, len(nums) + 1):
            # 如果当前数字与前一个数字不连续，或已到达数组末尾
            if i == len(nums) or nums[i] != nums[i - 1] + 1:
                # 如果当前区间起始点等于终止点，说明只有一个数字
                if start == i - 1:
                    result.append(str(nums[start]))
                else:
                    result.append(f"{nums[start]}->{nums[i - 1]}")
                # 更新区间起始点
                start = i

        return result

# 时间复杂度：O(n) - 遍历数组的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度，需要遍历数组中的每个元素。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录区间起始位置和结果字符串）。

---

### 28. LeetCode 1353: Maximum Number of Events That Can Be Attended（可以参加的最多会议数量）

**题目描述**：
给定一组会议时间区间 `[startDay, endDay]`，求最多可以参加的会议数量。每个会议在 `startDay` 开始，并在 `endDay` 结束。参加会议的规则是：每次只能参加一个会议，并且参会时间不能重叠。

**解题思路**：
将会议按照结束时间进行排序，然后使用贪心算法。遍历所有会议，并尽量选择在当前最早可以参加的会议时间点参会。使用一个集合来记录已经参加过的会议日期。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义可以参加的最多会议数量的函数
    def maxEvents(self, events: List[List[int]]) -> int:
        # 步骤 1：按照会议的结束时间进行排序
        events.sort(key=lambda x: (x[1], x[0]))

        # 步骤 2：使用一个集合记录已经参加过的会议日期
        attended_days = set()

        # 步骤 3：遍历所有会议，选择可以参加的会议
        for start, end in events:
            # 从会议的起始日到结束日，选择第一个未被参加的日期
            for day in range(start, end + 1):
                if day not in attended_days:
                    attended_days.add(day)
                    break

        return len(attended_days)  # 返回参加的会议数量

# 时间复杂度：O(n log n) - 排序所有会议的时间复杂度
# 空间复杂度：O(n) - 存储参加会议日期的集合空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序所有会议的时间复杂度。
- **空间复杂度**：O(n)，用于存储参加会议日期的集合空间复杂度。

---

### 29. LeetCode 616: Add Bold Tag in String（在字符串中添加粗体标签）

**题目描述**：
给定一个字符串 `s` 和一个单词列表 `dict`，在 `s` 中的所有单词 `dict` 出现的位置加上 `<b>` 和 `</b>` 标签，并返回新的字符串。

**解题思路**：
可以使用扫描线算法。首先找到所有单词在字符串中的出现位置，并使用扫描线记录每个位置的粗体状态，然后合并重叠的粗体标签，生成最终的字符串。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义添加粗体标签的函数
    def addBoldTag(self, s: str, dict: List[str]) -> str:
        # 步骤 1：创建一个布尔数组，记录每个字符是否需要加粗
        bold = [False] * len(s)

        # 步骤 2：遍历单词列表，标记所有需要加粗的字符位置
        for word in dict:
            start = s.find(word)
            while start != -1:
                for i in range(start, start + len(word)):
                    bold[i] = True
                start = s.find(word, start + 1)

        # 步骤 3：根据布尔数组，生成带有粗体标签的字符串
        result = []
        i = 0
        while i < len(s):
            if bold[i]:
                result.append("<b>")
                while i < len(s) and bold[i]:
                    result.append(s[i])
                    i += 1
                result.append("</b>")
            else:
                result.append(s[i])
                i += 1

        return "".join(result)

# 时间复杂度：O(n * m) - 遍历所有单词和字符串的时间复杂度
# 空间复杂度：O(n) - 存储布尔数组的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n * m)，其中 n 是字符串 `s` 的长度，m 是单词列表的长度。需要遍历所有单词和字符串。
- **空间复杂度**：O(n)，用于存储布

尔数组 `bold` 的空间复杂度。

---

### 30. LeetCode 163: Missing Ranges（缺失的区间）

**题目描述**：
给定一个排序的整数数组 `nums` 和一个区间 `[lower, upper]`，返回缺失的数字区间。例如，`nums = [0, 1, 3, 50, 75]`，`lower = 0`，`upper = 99`，返回 `["2", "4->49", "51->74", "76->99"]`。

**解题思路**：
使用扫描线算法，遍历数组中的每个数字，并将当前数字与前一个数字的差值用来判断是否存在缺失的区间。最后，将 `upper` 和数组末尾的差值也加入结果中。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找缺失区间的函数
    def findMissingRanges(self, nums: List[int], lower: int, upper: int) -> List[str]:
        # 初始化结果列表和当前指针
        result = []
        prev = lower - 1  # 用于记录前一个数字

        # 遍历数组中的所有数字
        for num in nums + [upper + 1]:
            if num == prev + 2:  # 恰好缺失一个数字
                result.append(str(prev + 1))
            elif num > prev + 2:  # 缺失多个数字
                result.append(f"{prev + 1}->{num - 1}")
            prev = num  # 更新前一个数字

        return result

# 时间复杂度：O(n) - 遍历所有数组元素的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，遍历所有数组元素的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录前一个数字 `prev`）。
