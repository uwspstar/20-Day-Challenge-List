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

Here's an answer using your provided template for **0/1背包问题 (0/1 Knapsack Problem)**:

---

## 0/1背包问题 (0/1 Knapsack Problem)

### Definition
0/1背包问题是一种经典的组合优化问题。给定一组物品，每个物品都有特定的重量和价值，目标是在不超过给定背包容量的情况下，选择物品使得它们的总价值最大。每个物品只能选择一次（即“0/1”），因此称为0/1背包问题。

### Key Concepts
- **物品 (Items)**: 每个物品都有一个特定的重量和价值。
- **背包容量 (Capacity)**: 背包能够承载的最大重量。
- **动态规划 (Dynamic Programming)**: 通过构建一个动态规划数组来记录在每个可能的重量下的最大价值。

### 0/1背包问题的步骤
1. **定义状态**: 使用动态规划数组 `dp[i][j]`，表示前 `i` 个物品在不超过重量 `j` 的情况下能够获得的最大价值。
2. **状态转移**:
   - 如果不选择第 `i` 个物品，`dp[i][j] = dp[i-1][j]`。
   - 如果选择第 `i` 个物品，`dp[i][j] = dp[i-1][j - weights[i-1]] + values[i-1]`（前提是 `weights[i-1] <= j`）。
3. **结果计算**: 最终的结果为 `dp[n][capacity]`，其中 `n` 是物品数量。

### 适用场景
- 资源分配问题
- 货物装载问题
- 投资组合优化

### 时间复杂度分析
- **时间复杂度**: O(n * W)，其中 n 是物品数量，W 是背包的最大容量。每个物品都要遍历一次背包容量。
- **空间复杂度**: O(n * W)，用于存储动态规划数组。

### Python 0/1背包问题模板
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    # 创建动态规划数组
    dp = [[0 for _ in range(capacity + 1)] for _ in range(n + 1)]

    # 填充动态规划数组
    for i in range(1, n + 1):
        for w in range(1, capacity + 1):
            if weights[i - 1] <= w:  # 如果当前物品可以放入背包
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])  # 选择或不选择物品
            else:
                dp[i][w] = dp[i - 1][w]  # 不能放入背包

    return dp[n][capacity]  # 返回最大价值
```

---

Here's an answer using your provided template for **完全背包问题 (Complete Knapsack Problem)**:

---

## 完全背包问题 (Complete Knapsack Problem)

### Definition
完全背包问题是一种组合优化问题。在此问题中，每个物品可以被选择多次，目标是在不超过给定背包容量的情况下，选择物品使得它们的总价值最大。与0/1背包问题不同，完全背包允许无限次选择同一种物品。

### Key Concepts
- **物品 (Items)**: 每个物品都有一个特定的重量和价值。
- **背包容量 (Capacity)**: 背包能够承载的最大重量。
- **动态规划 (Dynamic Programming)**: 通过构建一个动态规划数组来记录在每个可能的重量下的最大价值。

### 完全背包问题的步骤
1. **定义状态**: 使用动态规划数组 `dp[j]`，表示在不超过重量 `j` 的情况下，能够获得的最大价值。
2. **状态转移**:
   - 对于每个物品，遍历所有可能的重量，从物品的重量到背包容量，更新 `dp[j]`：
     - `dp[j] = max(dp[j], dp[j - weights[i]] + values[i])`，其中 `weights[i]` 是当前物品的重量，`values[i]` 是当前物品的价值。
3. **结果计算**: 最终的结果为 `dp[capacity]`，其中 `capacity` 是背包的最大容量。

### 适用场景
- 资源分配问题
- 货物装载问题
- 投资组合优化

### 时间复杂度分析
- **时间复杂度**: O(n * W)，其中 n 是物品数量，W 是背包的最大容量。每个物品都要遍历一次背包容量。
- **空间复杂度**: O(W)，用于存储动态规划数组。

### Python 完全背包问题模板
```python
def complete_knapsack(weights, values, capacity):
    n = len(weights)
    # 创建动态规划数组
    dp = [0] * (capacity + 1)

    # 填充动态规划数组
    for i in range(n):
        for j in range(weights[i], capacity + 1):
            dp[j] = max(dp[j], dp[j - weights[i]] + values[i])  # 更新最大价值

    return dp[capacity]  # 返回最大价值
```

---
