# 背包问题 (Knapsack Problem)

### Definition
背包问题是一种经典的优化问题，目标是从一组物品中选择一部分物品，使得它们的总重量不超过给定的限制，同时总价值最大。背包问题有多种变种，最常见的是0/1背包问题和完全背包问题。

### Key Concepts
- **物品 (Items)**: 每个物品都有一个特定的重量和价值。
- **背包容量 (Capacity)**: 背包能够承载的最大重量。
- **选择策略 (Selection Strategy)**: 选择物品时可以是包括或不包括某个物品（0/1背包），或者可以多次选择某个物品（完全背包）。

### 背包问题的步骤
1. **定义状态**: 使用动态规划数组 `dp`，其中 `dp[i]` 表示在不超过重量 `i` 的情况下，能够获得的最大价值。
2. **状态转移**: 遍历所有物品，对于每个物品，根据其重量和价值更新 `dp` 数组。
3. **结果计算**: 最终的结果为 `dp[capacity]`，即在给定容量下的最大价值。

### 背包问题的适用场景
- 资源分配问题
- 货物装载问题
- 投资组合优化

### 时间复杂度分析
- **时间复杂度**: O(n * W)，其中 n 是物品数量，W 是背包的最大容量。每个物品都要遍历一次背包容量。
- **空间复杂度**: O(W)，用于存储动态规划数组。

### Python 背包问题模板 (0/1 背包问题)
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [0] * (capacity + 1)  # 初始化动态规划数组

    # 遍历所有物品
    for i in range(n):
        for w in range(capacity, weights[i] - 1, -1):  # 从后向前遍历
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])  # 状态转移

    return dp[capacity]  # 返回最大价值
```

---

Feel free to ask if you need further modifications or additional topics!
