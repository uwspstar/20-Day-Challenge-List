# 深度优先搜索 (Depth-First Search)

### Definition
深度优先搜索是一种用于图形和树结构的遍历算法。它通过从起始节点开始，沿着一条路径尽可能深地探索，直到达到终点或没有更多可探索的节点，然后回溯到上一个节点，继续探索其他路径。

### Key Concepts
- **图 (Graph)**: 深度优先搜索可以应用于有向图和无向图，表示为邻接列表或邻接矩阵。
- **栈 (Stack)**: 使用栈来跟踪待访问的节点，确保后进先出 (LIFO) 的顺序访问节点。
- **访问标记 (Visited Marker)**: 通过标记已访问的节点来避免重复访问，防止死循环。

### 深度优先搜索的步骤
1. **初始化栈**: 将起始节点加入栈，并标记为已访问。
2. **循环访问节点**: 当栈不为空时，执行以下操作：
   - 从栈中弹出一个节点并处理。
   - 遍历该节点的所有邻接节点，如果未被访问，则加入栈并标记为已访问。
3. **结束条件**: 当找到目标节点时，停止搜索；或者当栈为空时，表示所有可达节点均已访问。

### 深度优先搜索的适用场景
- 查找路径问题
- 图的连通分量
- 拓扑排序
- 决策树的遍历

### 时间复杂度分析
- **时间复杂度**: O(V + E)，其中 V 是图中的顶点数量，E 是边的数量。每个顶点和每条边都被访问一次。
- **空间复杂度**: O(V)，用于存储访问标记和栈的空间。

### Python 深度优先搜索模板
```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()  # 初始化访问标记

    visited.add(start)  # 标记当前节点为已访问
    process(start)  # 处理当前节点

    for neighbor in graph[start]:  # 遍历邻接节点
        if neighbor not in visited:  # 如果邻接节点未被访问
            dfs(graph, neighbor, visited)  # 递归访问邻接节点

def process(node):
    # 处理节点的具体逻辑
    print(node)  # 这里简单输出节点
```

---

Feel free to ask if you need further modifications or additional topics!
