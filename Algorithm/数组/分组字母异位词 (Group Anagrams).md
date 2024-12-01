### 题目：分组字母异位词 (Group Anagrams)

**题目描述**：
给定一个字符串数组 `strs`，将其中的字母异位词组合在一起。字母异位词是指字母相同但排列不同的字符串。

---

### 代码实现：
```python
from typing import List
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)  # 创建一个默认字典，键为元组，值为列表
        
        for s in strs:
            count = [0] * 26  # 初始化一个长度为26的列表，用于记录每个字母的出现次数
            for c in s:
                count[ord(c) - ord('a')] += 1  # 根据字母的ASCII值计算索引并增加计数
            res[tuple(count)].append(s)  # 将字母频率表转换为元组作为键
        return list(res.values())  # 将字典的值转换为列表并返回
```

---

### 时间和空间复杂度分析：

#### **时间复杂度**：
- 外层循环：遍历每个字符串，共 `O(N)`，其中 `N` 是 `strs` 中字符串的数量。
- 内层循环：对每个字符串 `s` 统计字母频率，时间复杂度为 `O(K)`，其中 `K` 是字符串的平均长度。
- 因此，总时间复杂度为 **O(N * K)**。

#### **空间复杂度**：
- 需要存储 `count` 数组，占用 `O(26)` 的空间，简化为常量 `O(1)`。
- 使用字典存储所有异位词分组，最坏情况下需要 **O(N * K)** 空间。
- 总空间复杂度为 **O(N * K)**。

---

### 示例运行步骤：

#### 输入：
```python
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
```

#### **步骤 1**：初始化
- 创建一个空的 `defaultdict`，用于存储字母频率作为键，字母异位词作为值：
  ```python
  res = defaultdict(list)
  ```

#### **步骤 2**：处理第一个字符串 `"eat"`
- 初始化 `count` 数组：
  ```python
  count = [0, 0, 0, ..., 0]  # 长度为26
  ```
- 遍历字符串 `"eat"`：
  - 字母 `'e'`：`count[ord('e') - ord('a')] += 1` → `count[4] = 1`
  - 字母 `'a'`：`count[ord('a') - ord('a')] += 1` → `count[0] = 1`
  - 字母 `'t'`：`count[ord('t') - ord('a')] += 1` → `count[19] = 1`
- `count` 转换为元组 `(1, 0, 0, ..., 1, ..., 1)`，作为字典键：
  ```python
  res[(1, 0, ..., 1)] = ["eat"]
  ```

#### **步骤 3**：处理字符串 `"tea"`
- 计算 `count` 数组，结果同上 `(1, 0, ..., 1)`：
  ```python
  res[(1, 0, ..., 1)].append("tea") → res = {(1, 0, ..., 1): ["eat", "tea"]}
  ```

#### **步骤 4**：处理其他字符串
- `"tan"` 和 `"nat"` 的 `count` 都为 `(1, 0, 1, ..., 1)`，分组到一起：
  ```python
  res[(1, 0, 1, ..., 1)] = ["tan", "nat"]
  ```
- `"bat"` 的 `count` 为 `(1, 1, 0, ..., 0)`，单独分组：
  ```python
  res[(1, 1, 0, ..., 0)] = ["bat"]
  ```

#### **步骤 5**：返回结果
最终将 `res.values()` 转换为列表：
```python
result = [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
```

---

### 总结：
- **关键点**：
  - 使用字母频率数组来唯一表示每个字母异位词分组。
  - 使用 `defaultdict` 将同一组字母异位词存储在一起。
- **优点**：
  - 利用字母频率表避免对字符串排序，提高效率。

---

### 示例输出：
```python
输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出: [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
```
