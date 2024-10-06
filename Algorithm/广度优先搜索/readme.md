# 广度优先搜索 (Breadth-First Search)

### Definition
广度优先搜索是一种用于图形和树结构的遍历算法。它通过从起始节点开始，逐层访问所有相邻节点，直到找到目标节点或遍历完所有节点。该算法通常使用队列来维护待访问的节点，确保按照层级顺序进行访问。

### Key Concepts
- **图 (Graph)**: 广度优先搜索可以应用于有向图和无向图，表示为邻接列表或邻接矩阵。
- **队列 (Queue)**: 使用队列来跟踪待访问的节点，确保按照先入先出 (FIFO) 的顺序访问节点。
- **访问标记 (Visited Marker)**: 通过标记已访问的节点来避免重复访问，防止死循环。

### 广度优先搜索的步骤
1. **初始化队列**: 将起始节点加入队列，并标记为已访问。
2. **循环访问节点**: 当队列不为空时，执行以下操作：
   - 从队列中取出一个节点并处理。
   - 遍历该节点的所有邻接节点，如果未被访问，则加入队列并标记为已访问。
3. **结束条件**: 当找到目标节点时，停止搜索；或者当队列为空时，表示所有可达节点均已访问。

### 广度优先搜索的适用场景
- 查找最短路径问题
- 网络广播
- 邻接节点遍历
- 连通分量的识别

### Python 广度优先搜索模板
```python
from collections import deque

def bfs(graph, start):
    visited = set()  # 用于记录已访问的节点
    queue = deque([start])  # 初始化队列
    visited.add(start)  # 标记起始节点为已访问

    while queue:  # 当队列不为空时继续
        node = queue.popleft()  # 从队列中取出一个节点
        process(node)  # 处理该节点
        
        for neighbor in graph[node]:  # 遍历邻接节点
            if neighbor not in visited:  # 如果邻接节点未被访问
                visited.add(neighbor)  # 标记为已访问
                queue.append(neighbor)  # 加入队列

def process(node):
    # 处理节点的具体逻辑
    print(node)  # 这里简单输出节点
```

---

Feel free to ask if you need further modifications or additional topics!
