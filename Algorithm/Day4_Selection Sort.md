# Selection Sort 选择排序

- [Selection Sort](https://codebitwave.com/algorithms-101-selection-sort/)
- [Is Selection Sort Stable](https://codebitwave.com/algorithms-101-is-selection-sort-stable/)


Selection Sort is a simple comparison-based sorting algorithm. It works by repeatedly finding the minimum element (considering ascending order) from the unsorted part of the list and putting it at the beginning.  
选择排序是一种基于比较的简单排序算法。它通过反复从未排序部分中找到最小元素（考虑升序）并将其放在开头来工作。

### How Selection Sort Works 选择排序如何工作

1. Start with the first element in the list, assume it is the minimum.  
   从列表中的第一个元素开始，假设它是最小的。

2. Compare this element with the next element in the list. If the next element is smaller, update the minimum.  
   将此元素与列表中的下一个元素进行比较。如果下一个元素较小，则更新最小值。

3. Continue this process until the end of the list. Swap the found minimum element with the first element.  
   继续这个过程直到列表的末尾。将找到的最小元素与第一个元素交换。

4. Move the boundary of the sorted and unsorted part of the list by one element to the right, and repeat the process.  
   将排序部分和未排序部分的边界向右移动一个元素，并重复该过程。

5. Continue until the list is fully sorted.  
   继续进行，直到列表完全排序。

### Example of Selection Sort 选择排序的示例

Let's consider a list `[64, 25, 12, 22, 11]` and sort it using Selection Sort.  
让我们考虑一个列表 `[64, 25, 12, 22, 11]` 并使用选择排序对其进行排序。

#### Step-by-Step Process 分步过程

1. **Initial List**: `[64, 25, 12, 22, 11]`  
   **初始列表**：`[64, 25, 12, 22, 11]`

   - The first element `64` is assumed to be the minimum.  
     第一个元素 `64` 被假设为最小值。
   - Find the minimum value in the list, which is `11`, and swap it with `64`.  
     在列表中找到最小值，即 `11`，并将其与 `64` 交换。

   **List after Step 1**: `[11, 25, 12, 22, 64]`  
   **第1步后的列表**：`[11, 25, 12, 22, 64]`

2. **Second Iteration**:  
   **第二次迭代**：

   - Now, start from the second element `25`.  
     现在，从第二个元素 `25` 开始。
   - Find the minimum in the remaining list `[25, 12, 22, 64]`, which is `12`, and swap it with `25`.  
     在剩余的列表 `[25, 12, 22, 64]` 中找到最小值，即 `12`，并将其与 `25` 交换。

   **List after Step 2**: `[11, 12, 25, 22, 64]`  
   **第2步后的列表**：`[11, 12, 25, 22, 64]`

3. **Third Iteration**:  
   **第三次迭代**：

   - Now, start from the third element `25`.  
     现在，从第三个元素 `25` 开始。
   - Find the minimum in the remaining list `[25, 22, 64]`, which is `22`, and swap it with `25`.  
     在剩余的列表 `[25, 22, 64]` 中找到最小值，即 `22`，并将其与 `25` 交换。

   **List after Step 3**: `[11, 12, 22, 25, 64]`  
   **第3步后的列表**：`[11, 12, 22, 25, 64]`

4. **Fourth Iteration**:  
   **第四次迭代**：

   - Now, start from the fourth element `25`.  
     现在，从第四个元素 `25` 开始。
   - The remaining list is `[25, 64]`, which is already in order, so no swap is needed.  
     剩余的列表是 `[25, 64]`，它已经有序，因此不需要交换。

   **List after Step 4**: `[11, 12, 22, 25, 64]`  
   **第4步后的列表**：`[11, 12, 22, 25, 64]`

5. The list is now fully sorted.  
   现在，列表已经完全排序。

### Python Implementation of Selection Sort 选择排序的Python实现

Here is the Python code to implement Selection Sort:  
以下是实现选择排序的Python代码：

```python
def selection_sort(arr):
    for i in range(len(arr)):
        min_idx = i
        for j in range(i+1, len(arr)):
            if arr[min_idx] > arr[j]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

arr = [64, 25, 12, 22, 11]
selection_sort(arr)
print("Sorted array:", arr)
```

This code will output:  
这段代码的输出将是：

```
Sorted array: [11, 12, 22, 25, 64]
```

### Analysis of Selection Sort 选择排序的分析

- **Time Complexity**: O(n²) because there are two nested loops.  
  **时间复杂度**：O(n²)，因为有两个嵌套循环。

- **Space Complexity**: O(1) because it is an in-place sorting algorithm.  
  **空间复杂度**：O(1)，因为这是一个原地排序算法。

- **Stability**: Selection Sort is not stable; the relative order of equal elements might not be preserved.  
  **稳定性**：选择排序是不稳定的；相等元素的相对顺序可能不会保持。

### Example with Mutable List 示例：使用可变列表

If you apply Selection Sort to a list, it directly modifies the list in place, reflecting changes as the sort progresses.  
如果您对列表应用选择排序，它会直接在原地修改列表，随着排序的进行反映变化。

```python
arr = [64, 25, 12, 22, 11]
selection_sort(arr)
print("Sorted array:", arr)  # Output: [11, 12, 22, 25, 64]
```

In this example:  
在这个例子中：

- The original list `arr` is modified in place during sorting.  
  原始列表 `arr` 在排序过程中就地修改。

- After sorting, `arr` contains the sorted elements.  
  排序后，`arr` 包含排序后的元素。

### Conclusion 结论

Selection Sort is a straightforward sorting algorithm that is easy to implement but not efficient for large datasets due to its O(n²) time complexity. It is an in-place sorting algorithm, making it space-efficient but not stable.  
选择排序是一种简单的排序算法，易于实现，但由于其O(n²)的时间复杂度，对大数据集来说效率不高。它是一种原地排序算法，使其空间效率高，但不稳定。

This algorithm is best suited for small datasets or educational purposes where simplicity and ease of understanding are more important than performance.  
该算法最适合小数据集或教育用途，在这种情况下，简单性和易理解性比性能更重要。
