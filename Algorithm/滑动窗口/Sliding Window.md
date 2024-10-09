# 灵活滑动窗口 (Flexible Sliding Window)

## Definition
灵活滑动窗口是一种处理动态变化的窗口大小的技术，通过在数组或序列中维护一个有效的窗口，以实现特定条件的搜索或计算。该技术能够处理最长或最短子数组等问题，通常用于字符串、数组等数据结构。

## Key Concepts
- **动态窗口 (Dynamic Window)**: 窗口的大小和位置会根据条件的变化而变化。
- **条件验证 (Condition Validation)**: 通过检查当前窗口的有效性，决定是否需要移动窗口的边界。

## 灵活滑动窗口的步骤
1. 初始化窗口和结果变量。
2. 通过扩展右边界，逐步将新元素加入窗口。
3. 根据条件的有效性，动态调整左边界，确保窗口有效。
4. 更新结果变量，记录当前窗口满足条件时的最长或最短长度。

## 适用场景
- 查找满足特定条件的最长或最短子数组。
- 处理不固定大小的滑动窗口问题，如查找子字符串、子数组等。

## Python 灵活滑动窗口模板 - 最长子数组
```python
def sliding_window_flexible_longest(input):
    window = []  # 初始化窗口
    ans = 0
    left = 0
    
    for right in range(len(input)):
        window.append(input[right])  # 扩展右边界
        while invalid(window):  # 确保窗口有效
            window.remove(input[left])  # 移除左侧元素
            left += 1
        ans = max(ans, len(window))  # 更新最长子数组长度
    
    return ans  # 返回满足条件的最长子数组长度
```

## Python 灵活滑动窗口模板 - 最短子数组
```python
def sliding_window_flexible_shortest(input):
    window = []  # 初始化窗口
    ans = float("inf")  # 初始化为正无穷
    left = 0
    
    for right in range(len(input)):
        window.append(input[right])  # 扩展右边界
        while valid(window):  # 确保窗口有效
            ans = min(ans, len(window))  # 更新最短子数组长度
            window.remove(input[left])  # 移除左侧元素
            left += 1
    
    return ans if ans != float("inf") else 0  # 返回满足条件的最短子数组长度
```

## Python 固定大小滑动窗口模板
```python
def sliding_window_fixed(input, window_size):
    ans = input[0:window_size]  # 初始化窗口
    for right in range(window_size, len(input)):
        left = right - window_size  # 计算左边界
        window = input[left:right + 1]  # 更新窗口
        ans = optimal(ans, window)  # 更新最优解
    return ans  # 返回最优解
```

## Tips
- 确保在每次窗口更新时，及时检查窗口的有效性。
- 根据具体问题定义 `valid` 和 `invalid` 函数，以确保窗口符合条件。

## Warning
- 当处理大型数据时，使用 `list.remove()` 可能会导致性能问题，考虑使用 `collections.deque` 进行优化。

## Complexity Analysis
- **时间复杂度**: O(n)，每个元素最多被处理两次。
- **空间复杂度**: O(n)，存储窗口内容所需的空间。

---

This format provides a comprehensive understanding of both the flexible longest and shortest sliding window techniques. If you have any specific modifications or additional questions, feel free to ask!
