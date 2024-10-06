# 归并排序 (Merge Sort)

### Definition
归并排序是一种基于分治法的排序算法。它将一个数组分成两个子数组，分别对这两个子数组进行排序，然后将排序好的子数组合并成一个有序数组。归并排序具有良好的时间复杂度和稳定性，适用于大规模数据排序。

### Key Concepts
- **分治法 (Divide and Conquer)**: 将问题分解为更小的子问题，分别解决后合并结果。
- **合并 (Merge)**: 将两个已排序的子数组合并成一个有序数组。
- **递归 (Recursion)**: 归并排序通常通过递归方式实现，直到数组的长度为1为止。

### 归并排序的步骤
1. **分割**: 将数组从中间分成两个子数组。
2. **递归排序**: 对每个子数组进行递归调用归并排序，直到子数组的长度为1。
3. **合并**: 将两个已排序的子数组合并成一个新的有序数组。

### 归并排序的适用场景
- 大规模数据排序
- 需要稳定排序的场景
- 外部排序（处理无法全部加载到内存的数据）

### Python 归并排序模板
```python
def merge_sort(arr):
    if len(arr) <= 1:  # 基础情况：数组长度为1或更小
        return arr

    mid = len(arr) // 2  # 计算中点
    left_half = merge_sort(arr[:mid])  # 递归排序左半部分
    right_half = merge_sort(arr[mid:])  # 递归排序右半部分

    return merge(left_half, right_half)  # 合并已排序的子数组

def merge(left, right):
    sorted_array = []
    i = j = 0

    # 合并两个已排序的数组
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            sorted_array.append(left[i])
            i += 1
        else:
            sorted_array.append(right[j])
            j += 1

    # 处理剩余元素
    sorted_array.extend(left[i:])
    sorted_array.extend(right[j:])
    
    return sorted_array
```

---

Feel free to ask if you need further modifications or additional topics!
