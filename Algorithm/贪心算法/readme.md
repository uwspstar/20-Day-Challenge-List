# 贪心算法
### 贪心算法 (Greedy Algorithm)

#### Definition  
贪心算法是一种构造最优解的方法，它遵循 "在每一步选择中都采取在当前状态下最好或最优的选择" 原则。贪心算法并不保证每次选择都是全局最优解，而是基于局部最优解的假设来逐步构建全局解。在某些问题中，贪心策略能够获得全局最优解。

#### Key Concepts  
1. **局部最优 (Local Optimality)**: 在每一步选择中，只考虑当前能够获得的最佳解，而不考虑未来可能的后果。
2. **全局最优 (Global Optimality)**: 贪心算法的目标是通过一系列局部最优解，尽可能接近全局最优解。
3. **可行性 (Feasibility)**: 每次贪心选择必须是合法的，满足问题的约束条件。
4. **问题的贪心性质**: 某些问题可以通过贪心算法来解决，这类问题通常需要满足贪心选择的性质和最优子结构。

#### 贪心算法的步骤  
1. **初始化**：初始化一个解集合，通常是空的。
2. **做出贪心选择**：在每一步都做出当前最优的选择。
3. **更新问题状态**：更新剩余问题的状态，继续做出新的贪心选择，直到解决问题。
4. **输出结果**：最终获得的解集合就是贪心算法的结果。

#### 贪心算法的适用场景  
- 活动选择问题
- 最小生成树
- 最短路径问题
- 背包问题

#### Python 贪心算法模板

```python
def greedy_algorithm(data):
    # 初始化解集
    result = []
    # 遍历数据进行贪心选择
    for item in data:
        if 满足条件:
            result.append(item)
    return result
```

### 10 道 LeetCode 贪心算法题目及详细解释

---

#### 1. LeetCode 55: 跳跃游戏 (Jump Game)

##### Problem Description  
给定一个非负整数数组，你最初位于数组的第一个位置。数组中的每个元素代表你在该位置可以跳跃的最大长度。判断你是否能够到达最后一个位置。

##### 解法：贪心法  
从左到右遍历数组，维护当前可以跳到的最远距离。如果最远距离能覆盖最后一个位置，则返回 `True`。

##### Python 代码：

```python
def canJump(nums):
    max_reach = 0  # 初始化当前能跳到的最远距离
    for i, jump in enumerate(nums):  # 遍历数组
        if i > max_reach:  # 如果当前索引超过了最远距离，返回 False
            return False
        max_reach = max(max_reach, i + jump)  # 更新最远可达距离
    return True  # 如果遍历完成，说明可以到达最后一个位置
```

##### 解释：
- 初始化 `max_reach` 记录可以跳到的最远距离。
- 在遍历数组时，如果当前位置超过了最远可达距离，则说明无法到达。
- 每次更新 `max_reach`，计算当前位置加上可跳跃的步数。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 2. LeetCode 45: 跳跃游戏 II (Jump Game II)

##### Problem Description  
给定一个非负整数数组，你最初位于数组的第一个位置。数组中的每个元素代表你在该位置可以跳跃的最大长度。你的目标是使用最少的跳跃次数到达最后一个位置。

##### 解法：贪心法  
通过贪心选择，在每次跳跃时选择能够跳到的最远位置。

##### Python 代码：

```python
def jump(nums):
    jumps = 0  # 记录跳跃次数
    current_end = 0  # 当前跳跃的边界
    farthest = 0  # 记录最远可达的位置
    for i in range(len(nums) - 1):  # 遍历数组
        farthest = max(farthest, i + nums[i])  # 更新最远可达距离
        if i == current_end:  # 到达当前跳跃的边界
            jumps += 1  # 进行跳跃
            current_end = farthest  # 更新边界
    return jumps
```

##### 解释：
- `farthest` 记录从当前可以跳到的最远位置。
- 每次当遍历到当前跳跃的边界时，更新跳跃次数，并设置新的跳跃边界。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 3. LeetCode 435: 无重叠区间 (Non-overlapping Intervals)

##### Problem Description  
给定一组区间，找到需要移除区间的最小数量，使剩余区间互不重叠。

##### 解法：贪心法  
将区间按结束时间排序，每次选择结束时间最早且与前一个区间不重叠的区间。

##### Python 代码：

```python
def eraseOverlapIntervals(intervals):
    if not intervals:
        return 0
    intervals.sort(key=lambda x: x[1])  # 按结束时间排序
    end = intervals[0][1]  # 初始化第一个区间的结束时间
    count = 0  # 记录需要移除的区间数量
    for i in range(1, len(intervals)):  # 遍历剩余区间
        if intervals[i][0] < end:  # 如果当前区间与前一个区间重叠
            count += 1  # 需要移除当前区间
        else:
            end = intervals[i][1]  # 更新不重叠的区间结束时间
    return count
```

##### 解释：
- 首先将所有区间按结束时间进行排序，这样能尽量保留更多的区间。
- 每次选择结束时间最早且与前一个区间不重叠的区间。
- 如果发现区间重叠，计数需要移除的区间。

##### 时间复杂度：O(n log n)  
##### 空间复杂度：O(1)

---

#### 4. LeetCode 452: 用最少数量的箭引爆气球 (Minimum Number of Arrows to Burst Balloons)

##### Problem Description  
在二维平面上有一些气球，气球用水平线段表示。你需要至少几支箭才能引爆所有气球。

##### 解法：贪心法  
将气球按右边界排序，尽量用一支箭爆炸更多的气球。

##### Python 代码：

```python
def findMinArrowShots(points):
    if not points:
        return 0
    points.sort(key=lambda x: x[1])  # 按右边界排序
    arrows = 1  # 至少需要一支箭
    end = points[0][1]  # 初始化第一个气球的右边界
    for i in range(1, len(points)):  # 遍历剩余气球
        if points[i][0] > end:  # 如果当前气球的左边界大于上一个气球的右边界
            arrows += 1  # 需要一支新箭
            end = points[i][1]  # 更新右边界
    return arrows
```

##### 解释：
- 将所有气球按右边界排序。
- 使用贪心法，尽量用一支箭射中更多的气球，只有当气球的左边界超出当前右边界时才需要增加箭。

##### 时间复杂度：O(n log n)  
##### 空间复杂度：O(1)

---

#### 5. LeetCode 406: 根据身高重建队列 (Queue Reconstruction by Height)

##### Problem Description  
假设有一群人站成一列，每个人用一个整数对 `(h, k)` 来表示，其中 `h` 是这个人的身高，`k` 是排在这个人前面且身高大于或等于 `h` 的人数。请你重新构造这个队列。

##### 解法：贪心法  
首先按身高降序，`k` 值升序排序，然后依次插入队列中。

##### Python 代码：

```python
def reconstructQueue(people):
    # 按身高降序排序，如果身高相同，按 k 升序排序
    people.sort(key=lambda x: (-x[0], x[1]))
    result = []
    # 依次将每个人插入到队列的指定位置
    for person in people:
        result.insert(person[1], person)
    return result
```

##### 解释：
- 首先将所有人按身高降序排列，身高相同时按 `k` 值升序排列。
- 依次将每个人按照 `

k` 值插入到队列的正确位置。

##### 时间复杂度：O(n^2)  
##### 空间复杂度：O(n)

---

#### 6. LeetCode 121: 买卖股票的最佳时机 (Best Time to Buy and Sell Stock)

##### Problem Description  
给定一个数组，它的第 `i` 个元素是一支给定股票第 `i` 天的价格。你只能选择某一天买入这只股票，并选择在未来某一天卖出该股票，设计一个算法来计算你所能获取的最大利润。

##### 解法：贪心法  
每次只要遇到比之前更低的价格，就更新买入的时间点，然后计算当前最大利润。

##### Python 代码：

```python
def maxProfit(prices):
    min_price = float('inf')  # 初始化最低价格
    max_profit = 0  # 初始化最大利润
    for price in prices:  # 遍历价格数组
        min_price = min(min_price, price)  # 更新最低价格
        max_profit = max(max_profit, price - min_price)  # 更新最大利润
    return max_profit
```

##### 解释：
- 记录最低价格 `min_price`，然后计算每次可能的最大利润。
- 如果价格低于 `min_price`，更新最低买入点；否则，计算利润并更新最大利润。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 7. LeetCode 605: 种花问题 (Can Place Flowers)

##### Problem Description  
假设你有一个很长的花坛，其中一部分地块种植了花，另一部分却没有。花坛中的花不能相邻种植。给定一个整数数组 `flowerbed` 表示花坛，判断是否可以在不打破规则的情况下种下 `n` 朵花。

##### 解法：贪心法  
逐个遍历花坛，找到可以种花的位置，种下 `n` 朵花时返回 `True`。

##### Python 代码：

```python
def canPlaceFlowers(flowerbed, n):
    count = 0  # 记录已经种的花的数量
    for i in range(len(flowerbed)):  # 遍历花坛
        if flowerbed[i] == 0 and (i == 0 or flowerbed[i - 1] == 0) and (i == len(flowerbed) - 1 or flowerbed[i + 1] == 0):  
            flowerbed[i] = 1  # 在可以种花的位置种一朵花
            count += 1  # 更新已种花的数量
        if count >= n:  # 如果已种花数达到 n
            return True
    return False  # 如果遍历结束仍未种满，返回 False
```

##### 解释：
- 遍历花坛数组，找到满足种花条件的空地。
- 每次种花时，确保两侧都为空，种下 `n` 朵花时返回 `True`。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 8. LeetCode 763: 划分字母区间 (Partition Labels)

##### Problem Description  
给定一个字符串 `S`，将字符串划分为尽可能多的片段，使得每个字母最多只出现在一个片段中。

##### 解法：贪心法  
从左到右扫描字符串，找到每个字符的最远出现位置，并尽量扩展当前片段。

##### Python 代码：

```python
def partitionLabels(S):
    last = {char: i for i, char in enumerate(S)}  # 记录每个字符最后出现的位置
    result = []
    start, end = 0, 0  # 初始化片段的起始和结束位置
    for i, char in enumerate(S):  # 遍历字符串
        end = max(end, last[char])  # 扩展当前片段
        if i == end:  # 如果遍历到当前片段的末尾
            result.append(end - start + 1)  # 记录片段长度
            start = i + 1  # 更新下一个片段的起点
    return result
```

##### 解释：
- 通过遍历字符串，记录每个字符的最后出现位置。
- 每次扫描到当前片段的末尾时，记录该片段的长度。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 9. LeetCode 134: 加油站 (Gas Station)

##### Problem Description  
在一条环路上有 `n` 个加油站，其中第 `i` 个加油站有汽油 `gas[i]` 升。你有一辆油箱容量无限的车，它从第 `i` 个加油站开往第 `i + 1` 个加油站需要汽油 `cost[i]` 升。你从某个加油站出发，且需要跑完一圈，计算是否能完成这个环路。

##### 解法：贪心法  
如果总汽油量大于等于总耗油量，则一定存在起点，遍历每个站点找到合适的起点。

##### Python 代码：

```python
def canCompleteCircuit(gas, cost):
    total_tank, current_tank = 0, 0  # 初始化总油量和当前油量
    start = 0  # 初始化起点
    for i in range(len(gas)):  # 遍历每个加油站
        total_tank += gas[i] - cost[i]  # 更新总油量
        current_tank += gas[i] - cost[i]  # 更新当前油量
        if current_tank < 0:  # 如果当前油量不足
            start = i + 1  # 选择下一个加油站作为起点
            current_tank = 0  # 重置当前油量
    return start if total_tank >= 0 else -1  # 如果总油量足够返回起点，否则返回 -1
```

##### 解释：
- 每次遍历加油站时，计算当前油量是否足够开到下一个站点。
- 如果当前油量不足，更新起点为下一个站点，重置当前油量。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

#### 10. LeetCode 860: 柠檬水找零 (Lemonade Change)

##### Problem Description  
在柠檬水摊位上，每杯柠檬水售价 5 美元。顾客排队购买柠檬水，且他们只会给你 5 美元、10 美元或 20 美元的钞票。你必须给每个顾客正确找零，判断你是否能给所有顾客正确找零。

##### 解法：贪心法  
优先使用大面额找零，以保证后续顾客能获得正确的找零。

##### Python 代码：

```python
def lemonadeChange(bills):
    five, ten = 0, 0  # 记录 5 美元和 10 美元的数量
    for bill in bills:  # 遍历每个顾客的付款
        if bill == 5:  # 如果顾客支付 5 美元
            five += 1  # 收下 5 美元
        elif bill == 10:  # 如果顾客支付 10 美元
            if five == 0:  # 如果没有 5 美元找零
                return False
            five -= 1  # 找零 5 美元
            ten += 1  # 收下 10 美元
        else:  # 如果顾客支付 20 美元
            if ten > 0 and five > 0:  # 优先用 10 美元和 5 美元找零
                ten -= 1
                five -= 1
            elif five >= 3:  # 否则用三个 5 美元找零
                five -= 3
            else:
                return False  # 如果无法找零，返回 False
    return True  # 如果能够给所有顾客找零，返回 True
```

##### 解释：
- 根据贪心策略，优先使用大面额钞票进行找零，以保证后续找零的可行性。
- 如果发现无法给某个顾客找零，立即返回 `False`。

##### 时间复杂度：O(n)  
##### 空间复杂度：O(1)

---

### Conclusion  
贪心算法是一种强大的策略，能够快速解决一类问题，但并不总是适用于所有问题。通过局部最优的选择，贪心算法可以在一些特定的情况下找到全局最优解。

