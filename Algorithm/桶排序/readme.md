# 桶排序 (Bucket Sort)

### Definition
桶排序是一种分布式排序算法，它将输入数据分到有限数量的桶中。每个桶单独进行排序（通常使用其他排序算法），然后将所有桶中的元素合并到一起。桶排序特别适用于均匀分布的数据。

### Key Concepts
- **桶 (Bucket)**: 将数据分成多个桶，每个桶用于存放特定范围内的元素。
- **排序 (Sorting)**: 对每个桶中的元素进行排序，通常采用插入排序、快速排序或其他排序算法。
- **合并 (Merging)**: 将所有桶中的元素合并成一个有序数组。

### 桶排序的步骤
1. **创建桶**: 根据数据的范围和数量创建多个桶。
2. **分配元素**: 将输入数组中的元素分配到相应的桶中。
3. **排序桶内元素**: 对每个桶内的元素进行排序。
4. **合并桶**: 将所有桶内的元素按顺序合并成一个有序数组。

### 桶排序的适用场景
- 数据均匀分布时效果良好
- 需要在特定范围内排序的数据
- 适用于浮点数等连续值的排序

### 时间复杂度分析
- **最佳情况**: O(n + k)，当数据均匀分布且桶数足够多时，排序过程非常高效。
- **平均情况**: O(n + k)，同样依赖于均匀分布。
- **最坏情况**: O(n^2)，如果所有数据都落入一个桶中，且使用的排序算法为O(n^2)的情况（如插入排序）。
  
其中，n 是待排序的元素数量，k 是桶的数量。

### Python 桶排序模板
```python
def bucket_sort(arr, bucket_size=5):
    if len(arr) == 0:
        return arr

    # 确定桶的最小值和最大值
    min_value = min(arr)
    max_value = max(arr)

    # 计算桶的数量
    bucket_count = (max_value - min_value) // bucket_size + 1
    buckets = [[] for _ in range(bucket_count)]  # 创建桶

    # 将元素分配到桶中
    for num in arr:
        index = (num - min_value) // bucket_size
        buckets[index].append(num)

    # 对每个桶进行排序并合并结果
    sorted_array = []
    for bucket in buckets:
        sorted_array.extend(sorted(bucket))  # 使用内置的排序函数对每个桶排序

    return sorted_array
```

---

Feel free to ask if you need further modifications or additional topics!
