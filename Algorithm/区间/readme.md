
# 区间 (Interval)
 
区间是一组连续的数值或时间段，通常用于表示范围或界限。区间可以是开区间或闭区间，具体取决于是否包括端点。区间广泛应用于数学、统计学、计算机科学等领域，尤其在处理数据集合、时间安排和优化问题时尤为重要。

Key Concepts
开区间 (Open Interval): 不包括端点的区间，表示为 (a, b)，其中 a 和 b 是区间的端点。
闭区间 (Closed Interval): 包括端点的区间，表示为 [a, b]。
半开区间 (Half-Open Interval): 仅包括一个端点，表示为 [a, b) 或 (a, b]。
区间的合并: 将多个相交或相邻的区间合并为一个更大的区间，常用于简化问题或数据处理。
区间的分割: 将一个区间分割成多个子区间，以便进行更细致的分析或处理。

区间的适用场景
处理数值范围，例如计算统计数据中的最小值和最大值。
在算法中查找与特定区间相关的元素。
优化问题中设定变量的限制条件，例如线性规划。

Python 区间处理模板
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
```
