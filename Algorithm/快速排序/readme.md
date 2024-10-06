# 快速排序 (Quick Sort)

### Definition
快速排序是一种高效的排序算法，采用分治法的策略。通过选择一个基准元素，将待排序的数组分成两个部分：左侧为小于基准的元素，右侧为大于基准的元素。然后递归地对这两部分进行排序，最终形成一个有序的数组。快速排序在平均情况下具有较好的时间复杂度，且常用于大规模数据的排序。

### Key Concepts
- **基准元素 (Pivot)**: 选择一个元素作为基准，用于将数组分成两部分。
- **分区 (Partitioning)**: 根据基准元素将数组划分成左右两部分，左侧的元素均小于基准，右侧的元素均大于基准。
- **递归 (Recursion)**: 对分区后的两个子数组进行递归排序。

### 快速排序的步骤
1. **选择基准元素**: 通常选择数组的第一个元素、最后一个元素或中间元素作为基准。
2. **分区**: 遍历数组，将小于基准的元素放在左侧，大于基准的元素放在右侧。
3. **递归排序**: 对基准元素左右的子数组进行递归调用快速排序。

### 快速排序的适用场景
- 大规模数据排序
- 对于平均时间复杂度要求较高的应用
- 在内存限制较小的环境下进行排序

### Python 快速排序模板
```python
def quick_sort(arr):
    if len(arr) <= 1:  # 基础情况：数组长度为1或更小
        return arr

    pivot = arr[len(arr) // 2]  # 选择基准元素
    left = [x for x in arr if x < pivot]  # 小于基准的元素
    middle = [x for x in arr if x == pivot]  # 等于基准的元素
    right = [x for x in arr if x > pivot]  # 大于基准的元素

    return quick_sort(left) + middle + quick_sort(right)  # 递归排序并合并结果
```

---

Feel free to ask if you need further modifications or additional topics!
