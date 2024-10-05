# 区间 (Interval)

## Definition
区间是一组连续的数值或时间段，通常用于表示范围或界限。区间可以是开区间或闭区间，具体取决于是否包括端点。区间广泛应用于数学、统计学、计算机科学等领域，尤其在处理数据集合、时间安排和优化问题时尤为重要。

## Key Concepts
- **开区间 (Open Interval)**: 不包括端点的区间，表示为 (a, b)，其中 a 和 b 是区间的端点。
- **闭区间 (Closed Interval)**: 包括端点的区间，表示为 [a, b]。
- **半开区间 (Half-Open Interval)**: 仅包括一个端点，表示为 [a, b) 或 (a, b]。
- **区间的合并**: 将多个相交或相邻的区间合并为一个更大的区间，常用于简化问题或数据处理。
- **区间的分割**: 将一个区间分割成多个子区间，以便进行更细致的分析或处理。

## 区间的适用场景
- 处理数值范围，例如计算统计数据中的最小值和最大值。
- 在算法中查找与特定区间相关的元素。
- 优化问题中设定变量的限制条件，例如线性规划。

## Python 区间处理模板
```python
def merge_intervals(intervals):
    if not intervals:  # 检查区间是否为空
        return []
    
    intervals.sort(key=lambda x: x[0])  # 按起始值排序
    merged = [intervals[0]]  # 初始化合并后的区间
    
    for current in intervals[1:]:  # 遍历剩余区间
        last_merged = merged[-1]
        if current[0] <= last_merged[1]:  # 如果有交集
            last_merged[1] = max(last_merged[1], current[1])  # 更新合并后的区间
        else:
            merged.append(current)  # 无交集，直接添加
            
    return merged  # 返回合并后的区间

---
好的，我们继续讲解 LeetCode 区间题目的详细解析和代码注释。以下是前五道区间题目，包括详细分析、逐行中文注释代码及复杂度分析。

---

### 1. LeetCode 56: Merge Intervals（合并区间）

**题目描述**：
给定一个由多个区间组成的列表，将所有重叠的区间合并为一个，并返回合并后的区间列表。每个区间的形式为 `[start, end]`，且 `start` 总是小于或等于 `end`。

**题目分析**：
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

### 2. LeetCode 57: Insert Interval（插入区间）

**题目描述**：
给定一个由多个区间组成的列表和一个新的区间，将新的区间插入到列表中，并保证列表中的区间有序且没有重叠。

**题目分析**：
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

### 3. LeetCode 252: Meeting Rooms（会议室）

**题目描述**：
给定一个由多个会议时间区间组成的列表，判断是否可以将所有会议安排在一个会议室中（即所有会议时间没有重叠）。

**题目分析**：
可以通过对会议时间按照起始时间 `start` 进行排序，然后逐个检查相邻会议的结束时间和起始时间是否有重叠。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否可以安排所有会议的函数
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        # 步骤 1：按照会议的起始时间排序
        intervals.sort(key=lambda x: x[0])

        # 步骤 2：检查相邻会议的结束时间和起始时间是否有重叠
        for i in range(1, len(intervals)):
            if intervals[i][0] < intervals[i - 1][1]:
                return False

        return True

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和判断）。

---

### 4. LeetCode 253: Meeting Rooms II（会议室 II）

**题目描述**：
给定一个由多个会议时间区间组成的列表，计算所需的最少会议室数量，以便安排所有会议。

**题目分析**：
可以将所有会议的开始时间和结束时间分为两个列表，分别排序。然后使用两个指针遍历这两个列表，记录当前正在进行的会议数量，并更新所需会议室的最大值。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算最少会议室数量的函数
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        # 如果区间列表为空，则不需要会议室
        if not intervals:
            return 0

        # 提取所有会议的开始时间和结束时间
        start_times = sorted(intervals[i][0] for i in range(len(intervals)))
        end_times = sorted(intervals[i][1] for i in range(len(intervals)))

        # 初始化指针和正在进行的会议数量
        start_pointer = 0
        end_pointer = 0
        used_rooms = 0

        # 遍历所有开始时间
        while start_pointer < len(intervals):
            # 如果有会议结束，释放会议室
            if start_times[start_pointer] >= end_times[end_pointer]:
                used_rooms -= 1
                end_pointer += 1

            # 安排新的会议
            used_rooms += 1
            start_pointer += 1

        return used_rooms

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(n) - 存储开始时间和结束时间的列表空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(n)，存储所有会议开始时间和结束时间的列表空间。

---

### 5. LeetCode 435: Non-overlapping Intervals（无重叠区间）

**题目描述**：
给定一个由多个区间组成的列表，找到需要移除的最少区间数量，以使剩余区间没有重叠。

**题目分析**：
可以按照区间的结束时间 `end` 进行排序，并记录已选择的区间数量。遍历区间列表时，如果当前区间的起始时间 `start` 小于前一个已选择区间的结束时间 `end`，则该区间需要移除。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义移除最少区间的函数
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        # 如果区间列表为空，直接返回 0
        if not intervals:
            return 0

        # 步骤 1：按照区间的结束时间进行排序
        intervals.sort(key=lambda x: x[1])

        # 步骤 2：初始化变量，记录已选择的区间数量和上一个区间的结束时间
        count = 0
        end = float('-inf')



        # 步骤 3：遍历所有区间
        for interval in intervals:
            # 如果当前区间不与前一个已选择区间重叠，则更新结束时间
            if interval[0] >= end:
                end = interval[1]
            else:
                # 否则，该区间需要移除
                count += 1

        return count

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录已选择的区间数量和判断）。

---

好的，我们继续讲解接下来的五道 LeetCode 区间题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 6. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由多个区间组成的列表 `firstList` 和 `secondList`，找到两个列表中所有的交集区间。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `i` 和 `j` 分别指向两个区间列表的当前区间，判断这两个区间是否有交集，并将交集加入结果列表。然后根据两个区间的结束时间，移动相应的指针。

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

### 7. LeetCode 763: Partition Labels（划分字母区间）

**题目描述**：
给定一个字符串 `S`，将字符串划分为尽可能多的非重叠子串，使得每个字母最多出现在一个子串中。返回每个子串的长度列表。

**题目分析**：
可以使用贪心算法来解决该问题。首先遍历字符串记录每个字母最后出现的位置，然后使用双指针 `start` 和 `end` 来划分区间，当遍历到的字符位置等于当前区间的结束位置时，则完成一个区间的划分。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义划分字母区间的函数
    def partitionLabels(self, S: str) -> List[int]:
        # 记录每个字母最后出现的位置
        last_position = {char: idx for idx, char in enumerate(S)}

        # 初始化结果列表和双指针
        result = []
        start, end = 0, 0

        # 遍历字符串，划分区间
        for i, char in enumerate(S):
            end = max(end, last_position[char])  # 更新当前区间的结束位置
            if i == end:  # 当到达当前区间的结束位置时，划分区间
                result.append(end - start + 1)
                start = i + 1  # 更新起始位置

        return result

# 时间复杂度：O(n) - 遍历字符串的每个字符
# 空间复杂度：O(1) - 只使用了常量级别的额外空间（用于记录最后位置）
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是字符串的长度，需要遍历字符串的每个字符。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录每个字母的最后位置）。

---

### 8. LeetCode 1288: Remove Covered Intervals（删除被覆盖区间）

**题目描述**：
给定一个由多个区间组成的列表，删除所有被覆盖的区间，并返回剩余区间的数量。被覆盖的区间是指某个区间 `[a, b]` 被另一个区间 `[c, d]` 完全覆盖（即 `c <= a` 且 `b <= d`）。

**题目分析**：
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

### 9. LeetCode 986: Find Right Interval（寻找右区间）

**题目描述**：
给定一个由多个区间组成的列表，返回每个区间右侧最近的区间的起始位置。返回的结果列表中，若不存在右侧区间，则返回 -1。

**题目分析**：
可以使用二分查找法来解决该问题。首先将所有区间按照起始位置 `start` 进行排序，然后对于每个区间，使用二分查找法找到右侧最近的区间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义寻找右区间的函数
    def findRightInterval(self, intervals: List[List[int]]) -> List[int]:
        # 如果区间列表为空或只有一个区间，则直接返回
        if not intervals or len(intervals) == 1:
            return [-1] * len(intervals)

        # 步骤 1：记录区间的原始索引，并按照起始位置排序
        indexed_intervals = sorted((interval[0], idx) for idx, interval in enumerate(intervals))

        # 初始化结果列表
        result = []

        # 步骤 2：对于每个区间，使用二分查找找到右侧最近的区间
        for start, end in intervals:
            left, right = 0, len(indexed_intervals)
            while left < right:
                mid = (left + right) // 2
                if indexed_intervals[mid][0] < end:
                    left = mid + 1
                else:
                    right = mid
            # 检查是否存在右侧区间
            result.append(indexed_intervals[left][1] if left < len(indexed_intervals) else -1)

        return result

# 时间复杂度：O(n log n) - 排序和二分查找的时间复杂度
# 空间复杂度：O(n) - 存储结果列表的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序和二分查找的时间复杂度。
- **空间复杂度**：O(n)，用于存储结果列表的空间复杂度。

---

### 10. LeetCode 759: Employee Free Time（员工空闲时间）

**题目描述**：
给定多个员工的工作时间区间，找出所有员工的空闲时间区间（即所有员工都不在工作的时间）。

**题目分析**：
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
    # 定义查找员工空闲

时间的函数
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

好的，我们继续讲解接下来的五道 LeetCode 区间题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 11. LeetCode 732: My Calendar III（我的日历 III）

**题目描述**：
实现一个 `MyCalendarThree` 类，它记录日程安排，并能返回任何时候 `k` 个日程安排重叠的最大值。

**题目分析**：
可以使用扫描线算法来解决该问题。我们将每个日程安排的起始时间视为 `+1` 的操作，将结束时间视为 `-1` 的操作。然后对所有操作进行排序，并依次计算当前的重叠数量和最大重叠数量。

**代码实现**：
```python
# 定义 MyCalendarThree 类
class MyCalendarThree:

    # 初始化日历记录
    def __init__(self):
        self.timeline = {}

    # 定义添加日程安排的函数
    def book(self, start: int, end: int) -> int:
        # 记录起始时间 +1，结束时间 -1
        self.timeline[start] = self.timeline.get(start, 0) + 1
        self.timeline[end] = self.timeline.get(end, 0) - 1

        # 计算当前最大重叠数量
        max_count, ongoing = 0, 0
        for time in sorted(self.timeline):
            ongoing += self.timeline[time]
            max_count = max(max_count, ongoing)

        return max_count

# 时间复杂度：O(n log n) - 排序的时间复杂度（n 为时间点数量）
# 空间复杂度：O(n) - 存储时间点的哈希表空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 为时间点的数量。需要对时间点进行排序。
- **空间复杂度**：O(n)，用于存储时间点及其变化值的哈希表。

---

### 12. LeetCode 495: Teemo Attacking（提莫攻击）

**题目描述**：
给定提莫攻击的时间序列 `timeSeries` 和提莫的毒药持续时间 `duration`，计算提莫总的中毒时间。

**题目分析**：
可以遍历 `timeSeries` 列表，并依次计算每次攻击与上次攻击的时间差。如果时间差小于 `duration`，则说明中毒时间被延长；否则，中毒时间等于 `duration`。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义计算总中毒时间的函数
    def findPoisonedDuration(self, timeSeries: List[int], duration: int) -> int:
        # 如果时间序列为空，则中毒时间为 0
        if not timeSeries:
            return 0

        # 初始化总中毒时间
        total_time = 0

        # 遍历所有攻击时间
        for i in range(len(timeSeries) - 1):
            # 计算当前攻击与下次攻击的时间差
            total_time += min(timeSeries[i + 1] - timeSeries[i], duration)

        # 加上最后一次攻击的中毒时间
        total_time += duration

        return total_time

# 时间复杂度：O(n) - 遍历时间序列的每个元素
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是时间序列的长度，需要遍历所有攻击时间。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录总中毒时间和指针）。

---

### 13. LeetCode 1272: Remove Interval（删除区间）

**题目描述**：
给定一个由多个区间组成的列表和一个删除区间 `toBeRemoved`，返回删除该区间后的所有区间列表。

**题目分析**：
可以遍历所有区间，并根据 `toBeRemoved` 区间的起始位置和结束位置，将当前区间进行拆分或保留部分不被覆盖的区间。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义删除区间的函数
    def removeInterval(self, intervals: List[List[int]], toBeRemoved: List[int]) -> List[List[int]]:
        # 初始化结果列表
        result = []
        start, end = toBeRemoved

        # 遍历所有区间
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

### 14. LeetCode 252: Meeting Rooms（会议室）

**题目描述**：
给定一个由多个会议时间区间组成的列表，判断是否可以将所有会议安排在一个会议室中（即所有会议时间没有重叠）。

**题目分析**：
可以通过对会议时间按照起始时间 `start` 进行排序，然后逐个检查相邻会议的结束时间和起始时间是否有重叠。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义判断是否可以安排所有会议的函数
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        # 步骤 1：按照会议的起始时间排序
        intervals.sort(key=lambda x: x[0])

        # 步骤 2：检查相邻会议的结束时间和起始时间是否有重叠
        for i in range(1, len(intervals)):
            if intervals[i][0] < intervals[i - 1][1]:
                return False

        return True

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于指针的移动和判断）。

---

### 15. LeetCode 1288: Remove Covered Intervals（删除被覆盖区间）

**题目描述**：
给定一个由多个区间组成的列表，删除所有被覆盖的区间，并返回剩余区间的数量。被覆盖的区间是指某个区间 `[a, b]` 被另一个区间 `[c, d]` 完全覆盖（即 `c <= a` 且 `b <= d`）。

**题目分析**：
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

好的，我们继续讲解接下来的五道 LeetCode 区间题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 16. LeetCode 218: The Skyline Problem（天际线问题）

**题目描述**：
给定一组建筑物，每个建筑物用 `[left, right, height]` 表示其左边界、右边界和高度。绘制出这些建筑物的天际线，即从远处观察这些建筑物时，所有建筑物的轮廓线。

**题目分析**：
可以使用扫描线算法和优先队列（最大堆）来解决该问题。将每个建筑物的起始点和结束点作为事件点进行处理。对事件点进行排序，然后依次处理每个事件点，更新当前最高建筑的高度，并将关键点加入结果列表。

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
            events.append((left, -height, right))  # 起始点，使用负高度表示
            events.append((right, 0, 0))  # 结束点，高度为0

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

        # 返回天际线结果
        return result[1:]

# 时间复杂度：O(n log n) - 排序和最大堆操作的时间复杂度
# 空间复杂度：O(n) - 存储事件点和堆空间的复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 是所有建筑物的数量。排序事件点和最大堆操作的时间复杂度。
- **空间复杂度**：O(n)，用于存储事件点和堆的空间复杂度。

---

### 17. LeetCode 1229: Meeting Scheduler（会议安排）

**题目描述**：
给定两个由多个时间区间组成的列表 `slots1` 和 `slots2`，以及一个整数 `duration`，找出两个列表中重叠的时间区间，并返回满足 `duration` 时间的最早时间区间。如果没有这样的时间区间，则返回空列表。

**题目分析**：
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

### 18. LeetCode 56: Merge Intervals（合并区间）

**题目描述**：
给定一个由多个区间组成的列表，将所有重叠的区间合并为一个，并返回合并后的区间列表。每个区间的形式为 `[start, end]`，且 `start` 总是小于或等于 `end`。

**题目分析**：
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

### 19. LeetCode 57: Insert Interval（插入区间）

**题目描述**：
给定一个由多个区间组成的列表和一个新的区间，将新的区间插入到列表中，并保证列表中的区间有序且没有重叠。

**题目分析**：
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
        while i < len(intervals) and intervals[i][0] <= newInterval[1

]:
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

### 20. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由多个区间组成的列表 `firstList` 和 `secondList`，找到两个列表中所有的交集区间。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `i` 和 `j` 分别指向两个区间列表的当前区间，判断这两个区间是否有交集，并将交集加入结果列表。然后根据两个区间的结束时间，移动相应的指针。

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

好的，我们继续讲解接下来的五道 LeetCode 区间题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 21. LeetCode 715: Range Module（区间模块）

**题目描述**：
实现一个 `RangeModule` 类，支持以下三种操作：
1. `addRange(left, right)`：增加一个区间 `[left, right)` 到当前模块中。
2. `removeRange(left, right)`：从当前模块中移除区间 `[left, right)`。
3. `queryRange(left, right)`：查询区间 `[left, right)` 是否完全包含在当前模块中。

**题目分析**：
可以使用有序字典或平衡树来存储所有已被添加的区间。每次操作时，利用区间的起始和结束位置，判断或更新区间的状态。

**代码实现**：
```python
# 引入有序字典
from sortedcontainers import SortedDict

# 定义区间模块的类
class RangeModule:

    # 初始化区间模块
    def __init__(self):
        self.intervals = SortedDict()

    # 定义添加区间的函数
    def addRange(self, left: int, right: int) -> None:
        # 找到小于或等于 left 的区间起始点
        it = self.intervals.bisect_right(left)
        if it != 0 and self.intervals.items()[it - 1][1] >= left:
            it -= 1
        # 合并所有与 [left, right) 相交的区间
        while it < len(self.intervals) and self.intervals.items()[it][0] <= right:
            left = min(left, self.intervals.items()[it][0])
            right = max(right, self.intervals.items()[it][1])
            self.intervals.popitem(it)
        self.intervals[left] = right

    # 定义移除区间的函数
    def removeRange(self, left: int, right: int) -> None:
        # 找到小于或等于 left 的区间起始点
        it = self.intervals.bisect_right(left)
        if it != 0 and self.intervals.items()[it - 1][1] > left:
            it -= 1
        # 处理所有与 [left, right) 相交的区间
        to_add = []
        while it < len(self.intervals) and self.intervals.items()[it][0] < right:
            l, r = self.intervals.popitem(it)
            if l < left:
                to_add.append((l, left))
            if r > right:
                to_add.append((right, r))
        for l, r in to_add:
            self.intervals[l] = r

    # 定义查询区间的函数
    def queryRange(self, left: int, right: int) -> bool:
        # 找到小于或等于 left 的区间起始点
        it = self.intervals.bisect_right(left)
        if it == 0:
            return False
        return self.intervals.items()[it - 1][1] >= right

# 时间复杂度：O(n log n) - 查询、添加和移除操作的时间复杂度
# 空间复杂度：O(n) - 存储所有区间的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 为区间数量。查询、添加和移除操作都需要进行 `log n` 次比较。
- **空间复杂度**：O(n)，用于存储所有区间的有序字典或平衡树。

---

### 22. LeetCode 452: Minimum Number of Arrows to Burst Balloons（用最少数量的箭引爆气球）

**题目描述**：
给定多个气球的坐标区间 `[x_start, x_end]`，最少需要多少支箭才能将所有气球引爆。

**题目分析**：
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

### 23. LeetCode 352: Data Stream as Disjoint Intervals（将数据流变为不相交的区间）

**题目描述**：
实现一个 `SummaryRanges` 类，它支持以下两种操作：
1. `addNum(val)`：将值 `val` 插入到数据流中。
2. `getIntervals()`：返回数据流中不相交的区间列表。

**题目分析**：
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

### 24. LeetCode 986: Interval List Intersections（区间列表的交集）

**题目描述**：
给定两个由多个区间组成的列表 `firstList` 和 `secondList`，找到两个列表中所有的交集区间。

**题目分析**：
可以使用双指针法来解决该问题。定义两个指针 `i` 和 `j` 分别指向两个区间列表的当前区间，判断这两个区间是否有交集，并将交集加入结果列表。然后根据两个区间的结束

时间，移动相应的指针。

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

### 25. LeetCode 435: Non-overlapping Intervals（无重叠区间）

**题目描述**：
给定一个由多个区间组成的列表，找到需要移除的最少区间数量，以使剩余区间没有重叠。

**题目分析**：
可以按照区间的结束时间 `end` 进行排序，并记录已选择的区间数量。遍历区间列表时，如果当前区间的起始时间 `start` 小于前一个已选择区间的结束时间 `end`，则该区间需要移除。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义移除最少区间的函数
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        # 如果区间列表为空，直接返回 0
        if not intervals:
            return 0

        # 步骤 1：按照区间的结束时间进行排序
        intervals.sort(key=lambda x: x[1])

        # 步骤 2：初始化变量，记录已选择的区间数量和上一个区间的结束时间
        count = 0
        end = float('-inf')

        # 步骤 3：遍历所有区间
        for interval in intervals:
            # 如果当前区间不与前一个已选择区间重叠，则更新结束时间
            if interval[0] >= end:
                end = interval[1]
            else:
                # 否则，该区间需要移除
                count += 1

        return count

# 时间复杂度：O(n log n) - 排序的时间复杂度
# 空间复杂度：O(1) - 只使用了常量级别的额外空间
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，排序的时间复杂度。
- **空间复杂度**：O(1)，只使用了常量级别的额外空间（用于记录已选择的区间数量和判断）。

---

好的，我们继续讲解接下来的五道 LeetCode 区间题目，包括详细解析、逐行中文注释代码及复杂度分析。

---

### 26. LeetCode 128: Longest Consecutive Sequence（最长连续序列）

**题目描述**：
给定一个未排序的整数数组 `nums`，找出数字的最长连续序列（元素相邻且不重复），并返回其长度。

**题目分析**：
可以使用哈希表（集合）来存储所有的数字，然后遍历集合中的每个数字 `num`。对于每个 `num`，如果它是序列的起始数字（即 `num - 1` 不存在），则继续向后查找 `num + 1`、`num + 2` 等，直到找不到为止，从而得到最长连续序列的长度。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义查找最长连续序列的函数
    def longestConsecutive(self, nums: List[int]) -> int:
        # 使用集合去重，并便于 O(1) 时间复杂度查找
        num_set = set(nums)
        longest_streak = 0

        # 遍历集合中的每个数字
        for num in num_set:
            # 仅当当前数字是序列的起始数字时，开始查找连续序列
            if num - 1 not in num_set:
                current_num = num
                current_streak = 1

                # 查找当前数字的后续数字
                while current_num + 1 in num_set:
                    current_num += 1
                    current_streak += 1

                # 更新最长连续序列的长度
                longest_streak = max(longest_streak, current_streak)

        return longest_streak

# 时间复杂度：O(n) - 遍历所有数字和集合操作的时间复杂度
# 空间复杂度：O(n) - 使用集合存储所有数字的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n)，其中 n 是数组的长度。每个数字仅遍历一次，集合的查找操作为 O(1)。
- **空间复杂度**：O(n)，使用集合存储所有数字的空间复杂度。

---

### 27. LeetCode 731: My Calendar II（我的日历 II）

**题目描述**：
实现一个 `MyCalendarTwo` 类，它记录日程安排，并能检测是否有三重预定（即有三个重叠的区间）。

**题目分析**：
可以使用扫描线算法和两个列表来记录区间的变化。每次添加区间时，先判断该区间是否会导致三重预定，如果不会，则添加该区间，否则不添加。

**代码实现**：
```python
# 定义 MyCalendarTwo 类
class MyCalendarTwo:

    # 初始化日历记录
    def __init__(self):
        self.bookings = []  # 记录所有已预订的区间
        self.overlaps = []  # 记录所有双重预订的区间

    # 定义添加日程安排的函数
    def book(self, start: int, end: int) -> bool:
        # 检查是否会导致三重预订
        for s, e in self.overlaps:
            if start < e and end > s:  # 当前区间与已有双重预订区间重叠
                return False

        # 更新双重预订的区间
        for s, e in self.bookings:
            if start < e and end > s:  # 当前区间与已有预订区间重叠
                self.overlaps.append((max(start, s), min(end, e)))

        # 添加当前区间到预订列表
        self.bookings.append((start, end))
        return True

# 时间复杂度：O(n^2) - 遍历所有已预订区间和双重预订区间
# 空间复杂度：O(n) - 存储所有区间的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，其中 n 是预订的数量。每次添加区间时，都需要与所有已有区间和双重预订区间进行比较。
- **空间复杂度**：O(n)，存储所有已预订区间和双重预订区间的空间复杂度。

---

### 28. LeetCode 1244: Design A Leaderboard（设计排行榜）

**题目描述**：
设计一个排行榜类 `Leaderboard`，支持以下操作：
1. `addScore(playerId, score)`：为指定的玩家增加得分。
2. `top(K)`：返回前 `K` 名玩家的总得分。
3. `reset(playerId)`：将指定玩家的得分重置为 0。

**题目分析**：
可以使用哈希表存储每个玩家的得分，并在 `top(K)` 操作时，将得分按从大到小排序，并返回前 `K` 个得分的总和。

**代码实现**：
```python
# 定义 Leaderboard 类
class Leaderboard:

    # 初始化排行榜
    def __init__(self):
        self.scores = {}

    # 定义增加得分的函数
    def addScore(self, playerId: int, score: int) -> None:
        # 更新玩家的得分
        if playerId in self.scores:
            self.scores[playerId] += score
        else:
            self.scores[playerId] = score

    # 定义返回前 K 名玩家总得分的函数
    def top(self, K: int) -> int:
        # 获取所有玩家的得分列表，并排序
        top_scores = sorted(self.scores.values(), reverse=True)
        return sum(top_scores[:K])

    # 定义重置玩家得分的函数
    def reset(self, playerId: int) -> None:
        # 将玩家得分重置为 0
        if playerId in self.scores:
            self.scores[playerId] = 0

# 时间复杂度：O(n log n) - 排序玩家得分列表的时间复杂度
# 空间复杂度：O(n) - 存储所有玩家得分的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n log n)，其中 n 是玩家数量。排序玩家得分列表的时间复杂度。
- **空间复杂度**：O(n)，存储所有玩家得分的空间复杂度。

---

### 29. LeetCode 406: Queue Reconstruction by Height（根据身高重建队列）

**题目描述**：
给定一组人物，每个人由 `(h, k)` 表示，其中 `h` 是身高，`k` 是排在其前面的身高不低于 `h` 的人数。重建这个队列，并返回结果。

**题目分析**：
可以按照身高从高到低、`k` 值从小到大进行排序，然后依次将每个人插入到结果队列中 `k` 指定的位置。

**代码实现**：
```python
# 定义解决方案的类
class Solution:
    # 定义根据身高重建队列的函数
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        # 步骤 1：按照身高从高到低、k 值从小到大排序
        people.sort(key=lambda x: (-x[0], x[1]))

        # 步骤 2：按照 k 值将每个人插入到结果队列中
        result = []
        for person in people:
            result.insert(person[1], person)

        return result

# 时间复杂度：O(n^2) - 插入操作的时间复杂度
# 空间复杂度：O(n) - 存储结果队列的空间复杂度
```

**时间和空间复杂度分析**：
- **时间复杂度**：O(n^2)，其中 n 是人数。每次插入操作的时间复杂度为 O(n)。
- **空间复杂度**：O(n)，存储结果队列的空间复杂度。

---

### 30. LeetCode 57: Insert Interval（插入区间）

**题目描述**：
给定一个由多个区间组成的列表和一个新的区间，将新的区间插入到列表中，并保证列表中的区间有序且没有重叠。

**题目分析**：
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
        while i < len(intervals) and intervals[i][1

] < newInterval[0]:
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

解决 LeetCode 区间问题通常需要遵循一些通用的步骤和策略。以下是一个通用的解决区间问题的步骤框架，可以适用于大多数 LeetCode 区间题目。对于每个步骤，我将分别给出具体操作和需要注意的事项。

---

### 通用解决步骤（Generic Steps）

1. **理解题目描述（Understanding the Problem）**
   - **确定输入和输出**：
     - 明确输入是什么样的区间列表或数据（例如：列表、二维数组、数值等）。
     - 明确输出要求，例如：合并、删除、查找重叠区间、查找不相交区间等。
   - **分析区间关系**：
     - 识别区间之间的关系，包括是否有重叠、包含关系等。
   - **确定题目中的限制条件**：
     - 确认是否有时间复杂度、空间复杂度的限制，以及边界条件（空列表、单个元素等）。

2. **预处理（Preprocessing）**
   - **排序区间**（常见于需要处理相邻或重叠区间的题目）：
     - 按照区间的起始位置 `start` 进行排序，或者按结束位置 `end` 排序。
     - 排序后，区间之间的关系更容易进行比较，例如判断是否重叠、合并等。
   - **去重**（如果题目要求或数据中可能有重复区间）：
     - 使用集合或排序 + 去重的方式，去掉冗余区间，简化问题处理。

3. **遍历区间列表（Iterate Through the Intervals）**
   - **单遍历法**：
     - 适用于处理每个区间独立的题目，例如查找、合并、插入等。
     - 使用一个或多个指针（双指针法）遍历区间列表，根据当前区间的起始位置和结束位置，执行相应的操作。
   - **双指针法**：
     - 适用于比较两个区间列表的题目，例如：区间交集、区间合并等。
     - 定义两个指针 `i` 和 `j` 分别指向两个区间列表，根据当前区间的起始和结束位置，移动指针并计算区间关系。
   - **扫描线法（扫描线算法）**：
     - 适用于复杂区间操作，例如：统计重叠区间、找到最大重叠次数等。
     - 将区间的起始点和结束点作为事件点，每个事件点记录一个 `+1` 或 `-1` 的操作。对所有事件点排序，然后逐个处理，维护一个动态的计数器。

4. **合并或分割区间（Merge or Split Intervals）**
   - **合并区间**：
     - 当区间 `A` 和 `B` 有重叠时（即 `A.end >= B.start`），将其合并为一个新的区间 `[A.start, max(A.end, B.end)]`。
   - **分割区间**：
     - 当需要删除一个区间 `[left, right)` 时，可以将受影响的区间分割成不被覆盖的部分，并保留这些部分。

5. **特殊情况处理（Edge Cases Handling）**
   - **处理空输入**：
     - 确认输入列表是否为空，如果为空，直接返回预设的结果。
   - **单一元素或单个区间**：
     - 针对只有一个元素或单个区间的情况，单独处理或直接返回原输入。
   - **没有重叠的区间**：
     - 确认输入是否已经按顺序排列，并没有重叠区间，直接返回。

6. **结果构建与返回（Result Construction and Return）**
   - 将处理后的区间列表或结果数据构建成所需的格式，并返回。
   - 例如，返回的区间需要按照某种顺序排列、需要转换成其他形式的输出。

---

### 示例通用模板（Generic Template）

以下是基于上述通用步骤的代码模板，适用于大多数 LeetCode 区间问题。

```python
def solve_intervals_problem(intervals: List[List[int]]) -> List[List[int]]:
    # 1. 确认输入是否为空
    if not intervals:
        return []

    # 2. 排序区间（根据题目需求选择按起始位置或结束位置排序）
    intervals.sort(key=lambda x: x[0])  # 按起始位置排序

    # 3. 初始化结果列表
    result = []
    # 定义当前合并区间
    current_interval = intervals[0]

    # 4. 遍历所有区间，进行合并或分割操作
    for interval in intervals[1:]:
        # 检查是否有重叠，如果有重叠则合并
        if interval[0] <= current_interval[1]:
            # 更新当前合并区间的结束位置
            current_interval[1] = max(current_interval[1], interval[1])
        else:
            # 否则，将当前区间加入结果列表，并更新当前合并区间
            result.append(current_interval)
            current_interval = interval

    # 将最后一个合并区间加入结果列表
    result.append(current_interval)

    # 5. 返回处理后的结果
    return result
```

### 适用场景（Use Cases）

1. **合并区间（Merge Intervals）**
   - 排序后遍历所有区间，合并重叠区间。
2. **查找重叠区间（Find Overlapping Intervals）**
   - 使用双指针法或扫描线法查找区间之间的交集。
3. **删除区间（Remove Intervals）**
   - 先查找需要删除的区间，然后分割或跳过这些区间。
4. **查找最大重叠（Maximum Overlapping）**
   - 使用扫描线算法，记录每个时间点的区间变化，找到最大重叠的时间点。

### 典型例题（Typical Problems）

1. **LeetCode 56: Merge Intervals**
2. **LeetCode 57: Insert Interval**
3. **LeetCode 435: Non-overlapping Intervals**
4. **LeetCode 1288: Remove Covered Intervals**
5. **LeetCode 986: Interval List Intersections**

以上步骤和模板可以作为处理 LeetCode 区间问题的通用框架。对于每个特定题目，可以在此基础上进行相应的修改和优化。希望这些步骤和模板能帮助你更好地理解和解决 LeetCode 区间类题目！如果有具体问题需要进一步讲解，请告诉我！

以上是接下来的五道区间题目的详细解析和代码注释。如果有任何问题，或者需要继续讲解其他题目，请告诉我！我会继续补充详细分析。
