### LeetCode 338: 比特位计数 (Counting Bits)

**题目描述**：  
给定一个非负整数 `n`，计算从 `0` 到 `n` 的每个数字的二进制表示中 `1` 的个数，并以数组形式返回。

[LeetCode 338: Counting Bits](https://leetcode.com/problems/counting-bits/)

---

### 解题思路

1. **动态规划思路**：
   - 对于一个数字 `i`，如果我们已知 `i // 2`（也即 `i` 右移一位）的 `1` 的个数，可以快速计算出 `i` 的 `1` 的个数。
   - 具体来说：`res[i] = res[i >> 1] + (i & 1)`。
     - `i >> 1` 表示 `i` 右移一位，等价于 `i // 2`。
     - `(i & 1)` 用来判断 `i` 是否为奇数，若为奇数则最低位是 `1`，为偶数则最低位是 `0`。

2. **公式解释**：
   - `res[i]` 表示 `i` 的二进制中 `1` 的个数。
   - `res[i >> 1]` 表示 `i // 2` 的 `1` 的个数。
   - 通过右移一位，可以复用之前的计算结果。
   - 如果 `i` 是奇数，`(i & 1)` 为 `1`；如果 `i` 是偶数，`(i & 1)` 为 `0`。

---

### 代码实现

```python
from typing import List

class Solution:
    def countBits(self, n: int) -> List[int]:
        # 初始化一个大小为 n+1 的数组，全部填充为 0
        # res[i] 用于存储数字 i 的二进制中 1 的个数
        res = [0] * (n + 1)
        
        # 遍历从 1 到 n 的所有数字，逐个计算每个数字的 1 的个数
        for i in range(1, n + 1):
            # 使用右移操作获得 i // 2 的 1 的个数，加上当前位的 1（如果 i 是奇数）
            res[i] = res[i >> 1] + (i & 1)
        
        # 返回包含从 0 到 n 的每个数字的 1 的个数的数组
        return res
```

---

### 示例讲解

假设输入 `n = 5`，代码的执行过程如下：

1. **初始化**：`res = [0, 0, 0, 0, 0, 0]`

2. **遍历计算每个数字的 `1` 的个数**：
   - `i = 1`：  
     - `res[1] = res[1 >> 1] + (1 & 1) = res[0] + 1 = 0 + 1 = 1`
     - `res = [0, 1, 0, 0, 0, 0]`
   
   - `i = 2`：  
     - `res[2] = res[2 >> 1] + (2 & 1) = res[1] + 0 = 1 + 0 = 1`
     - `res = [0, 1, 1, 0, 0, 0]`
   
   - `i = 3`：  
     - `res[3] = res[3 >> 1] + (3 & 1) = res[1] + 1 = 1 + 1 = 2`
     - `res = [0, 1, 1, 2, 0, 0]`
   
   - `i = 4`：  
     - `res[4] = res[4 >> 1] + (4 & 1) = res[2] + 0 = 1 + 0 = 1`
     - `res = [0, 1, 1, 2, 1, 0]`
   
   - `i = 5`：  
     - `res[5] = res[5 >> 1] + (5 & 1) = res[2] + 1 = 1 + 1 = 2`
     - `res = [0, 1, 1, 2, 1, 2]`

3. **返回结果**：`res = [0, 1, 1, 2, 1, 2]`

---

### 复杂度分析

- **时间复杂度**：O(n)。我们需要遍历从 `1` 到 `n` 的每个数字，对于每个数字计算其二进制中的 `1` 的个数。
- **空间复杂度**：O(n)。数组 `res` 用于存储 `0` 到 `n` 的每个数字的 `1` 的个数。

---

### 总结

- **动态规划优化**：通过右移一位，可以有效复用之前的计算结果，避免重复计算。
- **简单高效**：仅需一次遍历，且用常数时间计算每个数字的 `1` 的个数，是一种空间和时间效率都很高的解法。

该方法是一种高效的动态规划解决方案，适合大范围内快速计算各个数字的二进制 `1` 的个数。

---

在这段代码中，`res[i] = res[i >> 1] + (i & 1)` 是一个动态规划公式，用于计算整数 `i` 的二进制中 `1` 的个数。它的设计思想是利用前面已经计算过的结果，减少重复计算。以下是对公式 `res[i] = res[i >> 1] + (i & 1)` 的详细解释：

### 分解公式的含义

1. **右移操作 `i >> 1`**：
   - `i >> 1` 等价于 `i // 2`，表示将 `i` 右移一位。
   - 右移一位相当于去掉 `i` 的最低位，结果是将 `i` 的二进制数整体向右平移一位。例如，`6` (二进制 `110`) 右移一位得到 `3` (二进制 `11`)。
   - 因为 `i >> 1` 去掉了 `i` 的最低位，所以 `res[i >> 1]` 已经包含了 `i` 除去最低位后其二进制中 `1` 的个数。

2. **按位与操作 `(i & 1)`**：
   - `(i & 1)` 用于检查 `i` 的最低位是 `0` 还是 `1`。
   - 当 `i` 是奇数时，`i & 1` 的结果为 `1`，表示最低位为 `1`；当 `i` 是偶数时，`i & 1` 的结果为 `0`，表示最低位为 `0`。
   - 通过 `(i & 1)` 可以判断 `i` 的最低位是否为 `1`，如果为 `1` 则将 `res[i >> 1]` 的值加 `1`。

3. **公式整体**：
   - `res[i] = res[i >> 1] + (i & 1)` 利用 `i` 的最低位信息来计算 `i` 的二进制 `1` 的个数。
   - `res[i >> 1]` 是 `i` 去掉最低位后的 `1` 的个数，而 `(i & 1)` 决定是否需要加上 `1`（仅当最低位是 `1` 时）。
   - 这样通过已计算的结果 `res[i >> 1]`，只需再加上 `i` 的最低位信息，即可得到 `i` 的二进制 `1` 的总个数。

### 示例解析

假设 `n = 5`，代码会按以下步骤填充 `res` 数组：

- `i = 1`：  
  - `res[1] = res[1 >> 1] + (1 & 1) = res[0] + 1 = 0 + 1 = 1`
  - `res = [0, 1, 0, 0, 0, 0]`

- `i = 2`：  
  - `res[2] = res[2 >> 1] + (2 & 1) = res[1] + 0 = 1 + 0 = 1`
  - `res = [0, 1, 1, 0, 0, 0]`

- `i = 3`：  
  - `res[3] = res[3 >> 1] + (3 & 1) = res[1] + 1 = 1 + 1 = 2`
  - `res = [0, 1, 1, 2, 0, 0]`

- `i = 4`：  
  - `res[4] = res[4 >> 1] + (4 & 1) = res[2] + 0 = 1 + 0 = 1`
  - `res = [0, 1, 1, 2, 1, 0]`

- `i = 5`：  
  - `res[5] = res[5 >> 1] + (5 & 1) = res[2] + 1 = 1 + 1 = 2`
  - `res = [0, 1, 1, 2, 1, 2]`

### 总结

- **`i >> 1`**：复用 `i` 去掉最低位后 `1` 的个数的结果。
- **`(i & 1)`**：判断 `i` 的最低位是否为 `1`，决定是否加 `1`。
- 这种方法利用了动态规划思想，避免了重复计算，提升了效率。
