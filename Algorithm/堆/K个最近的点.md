### K个最近的点

给定一个二维平面上的点列表。找到距离原点 (0, 0) 最近的K个点。

#### 输入
示例：`[(1, 1), (2, 2), (3, 3)], 1`

#### 输出
示例：`[(1, 1)]`

### 思路解释

#### 直觉
首先，回顾一下基本的几何知识。如果我们不记得的话，两个点 (x1, y1) 和 (x2, y2) 之间的距离公式为 $\sqrt{(x1 - x2)^2 + (y1 - y2)^2}$。对于到原点的距离，即 (x2, y2) 为 (0, 0)，则距离变为 $\sqrt{x1^2 + y1^2}$。

利用堆的特点，“找最近的K个”这个需求自然让我们想到用堆。节点的比较键为其到原点的距离。接着从堆中弹出距离最小的K个点即可。这样就非常简单。

#### 时间复杂度
- **时间复杂度**：$O(n \log n)$

因为我们要将所有元素插入堆中，堆的插入操作是 $O(\log n)$，总共插入 n 次。

#### 空间复杂度
- **空间复杂度**：$O(n)$

### 实现代码

#### Python代码
```python
from heapq import heappop, heappush
from typing import List, Tuple

def k_closest_points(points: List[List[int]], k: int) -> List[List[int]]:
    heap: List[Tuple[int, List[int]]] = []

    # 计算每个点到原点的距离，并将距离和点坐标存入堆中
    for pt in points:
        heappush(heap, (pt[0] ** 2 + pt[1] ** 2, pt))

    res = []
    # 从堆中弹出k个距离最小的点
    for _ in range(k):
        _, pt = heappop(heap)
        res.append(pt)

    return res

if __name__ == "__main__":
    # 输入点的数量和点坐标
    points = [[int(x) for x in input().split()] for _ in range(int(input()))]
    k = int(input())
    res = k_closest_points(points, k)
    for row in res:
        print(" ".join(map(str, row)))
```

**注意**：我们在堆中存储的距离不是欧氏距离，而是平方和，因为这样存储时数据是整数，更精确。

### 使用最大堆的替代解法
尽管问题要求最近的距离，使用最大堆也可以解决。思路如下：

假设已经有了K个最近的点，现在来判断新点是否应该属于这K个点集合。判断的标准是新点是否比当前集合中最远的点更近。如果更近，就将当前集合中的最远点踢出，并加入新点。

我们可以利用最大堆实现这一逻辑。最大堆的堆顶就是距离最远的点。如果新点距离较小，则将最大堆的堆顶弹出，并加入新点。

#### Python代码
```python
from heapq import heappop, heappush
from typing import List, Tuple

def k_closest_points(points: List[List[int]], k: int) -> List[List[int]]:
    def dist(point: List[int]) -> int:
        return -(point[0] ** 2 + point[1] ** 2)  # 取负号以实现最大堆

    max_heap: List[Tuple[int, List[int]]] = []
    
    # 初始化最大堆，包含前k个点
    for i in range(k):
        pt = points[i]
        heappush(max_heap, (dist(pt), pt))

    # 遍历剩余的点，如果某点距离更小，则替换堆顶
    for i in range(k, len(points)):
        pt = points[i]
        if dist(pt) > max_heap[0][0]:
            heappop(max_heap)
            heappush(max_heap, (dist(pt), pt))

    # 从最大堆中弹出所有元素，并反转顺序
    res = []
    while max_heap:
        _, pt = heappop(max_heap)
        res.append(pt)
    res.reverse()
    
    return res

if __name__ == "__main__":
    # 输入点的数量和点坐标
    points = [[int(x) for x in input().split()] for _ in range(int(input()))]
    k = int(input())
    res = k_closest_points(points, k)
    for row in res:
        print(" ".join(map(str, row)))
```
### 解释：`heap: List[Tuple[int, List[int]]] = []`

这行代码的作用是定义并初始化一个名为 `heap` 的空列表。它的类型注释是 `List[Tuple[int, List[int]]]`，表示这是一个列表，列表中的每个元素都是一个包含两个元素的元组 `(int, List[int])`。具体来说：

1. **`List[Tuple[int, List[int]]]`**：
   - `List` 表示这是一个列表类型。
   - `Tuple[int, List[int]]` 表示列表中的元素类型是一个包含两个元素的元组。
     - 第一个元素是一个整数 `int`，表示某个点到原点的距离的平方和。
     - 第二个元素是一个列表 `List[int]`，表示二维平面中的一个点的坐标（例如 `[x, y]`）。

2. **空列表 `[]`**：
   - `[]` 表示初始化时，`heap` 是一个空列表。

3. **用途**：
   - 该 `heap` 列表用于实现一个最小堆（或者最大堆，根据具体需求），来保存点到原点的距离和对应的坐标。
   - 每次插入元素时，我们会将点的距离和点坐标组成一个元组 `(距离平方和, [x, y])`，并将该元组放入 `heap` 中。
   
#### 示例代码片段
在将点添加到堆时，使用如下方式：

```python
for pt in points:
    heappush(heap, (pt[0] ** 2 + pt[1] ** 2, pt))
```

在这个循环中，我们计算了每个点到原点的距离平方和，并将其与点坐标 `pt` 一起作为元组插入到 `heap` 中。

### 总结
- 使用堆（最小堆或最大堆）可以高效地找到K个距离最近的点。
- 通过平方和的方式替代欧氏距离，避免浮点运算误差
