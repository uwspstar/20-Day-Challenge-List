### LeetCode 973: K Closest Points to Origin

https://leetcode.com/problems/k-closest-points-to-origin/

**题目描述**：
给定一个二维平面上的点列表，找到离原点 (0, 0) 最近的 k 个点。

**示例**：

输入：`[(1, 1), (2, 2), (3, 3)]`, `k = 1`  
输出：`[(1, 1)]`

**代码实现**：
```python
# 导入堆模块
import heapq

# 定义解决方案的类
class Solution:
    # 定义查找最近 k 个点的函数
    def kClosest(self, points, k):
        # 创建一个最大堆来存储距离最小的点
        max_heap = []
        
        # 遍历所有的点
        for x, y in points:
            # 计算每个点到原点的欧几里得距离的平方（省略平方根，比较距离平方即可）
            distance = -(x ** 2 + y ** 2)
            # 将点和距离入堆
            heapq.heappush(max_heap, (distance, (x, y)))
            # 如果堆的大小超过 k，则弹出最远的点
            if len(max_heap) > k:
                heapq.heappop(max_heap)
        
        # 从堆中取出最近的 k 个点
        return [point for (_, point) in max_heap]

# 示例调用
points = [(1, 1), (2, 2), (3, 3)]
k = 1
solution = Solution()
print(solution.kClosest(points, k))  # 输出 [(1, 1)]
```

### 代码解析：
1. **导入堆模块**：
   ```python
   import heapq
   ```
   - `heapq` 模块提供了堆的实现，适用于优先队列操作。
   - 在此题中，使用最大堆来存储距离最小的点。

2. **定义类和函数**：
   ```python
   class Solution:
       def kClosest(self, points, k):
   ```
   - `Solution` 是主类。
   - `kClosest` 函数接受一个点列表 `points` 和整数 `k`，返回距离原点最近的 `k` 个点。

3. **初始化最大堆**：
   ```python
   max_heap = []
   ```
   - `max_heap` 是最大堆，用于存储 `k` 个距离最小的点。

4. **遍历每个点**：
   ```python
   for x, y in points:
       distance = -(x ** 2 + y ** 2)
       heapq.heappush(max_heap, (distance, (x, y)))
   ```
   - `x, y` 是每个点的坐标。
   - `distance` 计算每个点到原点的距离的平方。为了方便最大堆比较，取距离的负值，使得更接近的点更优先保留在堆中。
   - `heapq.heappush` 将点及其距离推入堆。

5. **控制堆的大小**：
   ```python
   if len(max_heap) > k:
       heapq.heappop(max_heap)
   ```
   - 如果堆大小超过 `k`，则弹出距离最远的点，确保堆内保留 `k` 个最近的点。

6. **返回结果**：
   ```python
   return [point for (_, point) in max_heap]
   ```
   - 使用列表推导式提取堆中保存的 `k` 个点并返回。

### 时间复杂度分析 (Big O)：
- **时间复杂度**：O(N log K)，其中 `N` 是点的数量，`K` 是所需的最近点数。每次 `heappush` 和 `heappop` 操作需要 O(log K) 时间。
- **空间复杂度**：O(K)，用于存储堆中的最近点。

### 示例讲解：

给定输入 `[(1, 1), (2, 2), (3, 3)]` 和 `k = 1`，我们逐步运行代码：

1. **初始化**：
   - 最大堆 `max_heap = []`

2. **遍历第一个点 `(1, 1)`**：
   - 计算距离平方：`distance = -(1^2 + 1^2) = -2`
   - 将 `(-2, (1, 1))` 插入堆中，`max_heap = [(-2, (1, 1))]`

3. **遍历第二个点 `(2, 2)`**：
   - 计算距离平方：`distance = -(2^2 + 2^2) = -8`
   - 将 `(-8, (2, 2))` 插入堆中，`max_heap = [(-8, (2, 2)), (-2, (1, 1))]`
   - 堆大小超过 `k = 1`，弹出最远的点，弹出 `(-8, (2, 2))`
   - `max_heap = [(-2, (1, 1))]`

4. **遍历第三个点 `(3, 3)`**：
   - 计算距离平方：`distance = -(3^2 + 3^2) = -18`
   - 将 `(-18, (3, 3))` 插入堆中，`max_heap = [(-18, (3, 3)), (-2, (1, 1))]`
   - 堆大小超过 `k = 1`，弹出最远的点，弹出 `(-18, (3, 3))`
   - `max_heap = [(-2, (1, 1))]`

5. **返回结果**：
   - 提取堆中的点，返回 `[(1, 1)]`
