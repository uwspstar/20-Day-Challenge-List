### 最长公共前缀问题

#### 问题描述
给定一个字符串数组 `strs`，找出其中最长的公共前缀。如果没有公共前缀，返回空字符串 `""`。

---

### 示例

#### 示例 1：
```text
输入: strs = ["flower","flow","flight"]
输出: "fl"
```

#### 示例 2：
```text
输入: strs = ["dog","racecar","car"]
输出: ""
解释: 没有公共前缀。
```

---

### 约束条件
- \(1 \leq \text{strs.length} \leq 200\)
- \(0 \leq \text{strs[i].length} \leq 200\)
- `strs[i]` 仅由小写英文字母组成。

---

### 解决方案：水平扫描法

#### 思路
- 将第一个字符串视为初始公共前缀。
- 遍历数组中的其他字符串，不断缩短公共前缀，直到找到最长公共前缀或前缀为空。

---

### 实现代码
```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    
    # 初始公共前缀为第一个字符串
    prefix = strs[0]
    
    for string in strs[1:]:
        # 不断缩短 prefix，直到它是 string 的前缀
        while string[:len(prefix)] != prefix and prefix:
            prefix = prefix[:-1]
        # 如果前缀为空，直接返回
        if not prefix:
            return ""
    
    return prefix

# 测试用例
print(longest_common_prefix(["flower","flow","flight"]))  # 输出: "fl"
print(longest_common_prefix(["dog","racecar","car"]))    # 输出: ""
```

---

### 代码解析

1. **初始公共前缀**：
   - 将数组的第一个字符串设为初始公共前缀 `prefix`。
   
2. **逐个比较**：
   - 遍历剩余的字符串数组。
   - 使用 `string[:len(prefix)] != prefix` 检查当前字符串是否以 `prefix` 开头。
   - 如果不是，缩短 `prefix`（移除最后一个字符）并继续检查。

3. **终止条件**：
   - 如果在某次比较中，`prefix` 被缩短为空，则直接返回 `""`。

4. **返回结果**：
   - 遍历完成后，返回最终的 `prefix`。

---

### 示例运行

#### 输入 1：
```python
strs = ["flower", "flow", "flight"]
```

**运行过程**：
- 初始 `prefix = "flower"`
- 比较 `"flow"`：
  - `"flow"[:6] != "flower"`，缩短为 `"flowe"`
  - `"flow"[:5] != "flowe"`，缩短为 `"flow"`
  - `"flow"[:4] == "flow"`，继续。
- 比较 `"flight"`：
  - `"flight"[:4] != "flow"`，缩短为 `"flo"`
  - `"flight"[:3] != "flo"`，缩短为 `"fl"`
  - `"flight"[:2] == "fl"`，继续。
- 最终结果：`"fl"`

#### 输入 2：
```python
strs = ["dog", "racecar", "car"]
```

**运行过程**：
- 初始 `prefix = "dog"`
- 比较 `"racecar"`：
  - `"racecar"[:3] != "dog"`，缩短为 `"do"`
  - `"racecar"[:2] != "do"`，缩短为 `"d"`
  - `"racecar"[:1] != "d"`，缩短为 `""`
- 返回结果：`""`

---

### 时间复杂度

- **最坏情况**：所有字符串相同，最长公共前缀接近字符串长度。
  - 比较每个字符串的每个字符：\(O(S)\)，其中 \(S = \text{所有字符串的总字符数}\)。
- **平均复杂度**：\(O(S)\)。

---

### 空间复杂度
- 使用常量级别的额外空间：\(O(1)\)。

---

### 总结
这种水平扫描法通过不断缩短前缀来找到最长公共前缀，算法简单高效，适用于较小规模的字符串数组。
