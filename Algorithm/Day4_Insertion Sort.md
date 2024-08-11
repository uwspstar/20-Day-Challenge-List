# Insertion Sort 插入排序

- [Insertion Sort](https://codebitwave.com/algorithms-101-insertion-sort/)

Insertion Sort is a simple and intuitive comparison-based sorting algorithm. It works by building a sorted portion of the list one element at a time, by repeatedly taking the next element from the unsorted portion and inserting it into its correct position in the sorted portion.  
插入排序是一种简单直观的基于比较的排序算法。它通过逐个构建列表的已排序部分来工作，不断地从未排序部分取出下一个元素，并将其插入到已排序部分的正确位置中。

### How Insertion Sort Works 插入排序如何工作

1. Start with the second element in the list, as a single-element list is already sorted.  
   从列表中的第二个元素开始，因为单元素列表已经排序。

2. Compare this element with the elements in the sorted portion of the list (initially just the first element).  
   将此元素与列表已排序部分中的元素进行比较（最初只有第一个元素）。

3. Shift the elements in the sorted portion to the right until you find the correct position for the current element.  
   将已排序部分中的元素向右移动，直到找到当前元素的正确位置。

4. Insert the current element into its correct position.  
   将当前元素插入到其正确位置。

5. Repeat the process for each subsequent element in the list until the entire list is sorted.  
   对列表中的每个后续元素重复此过程，直到整个列表排序完成。

### Example of Insertion Sort 插入排序的示例

Let's consider a list `[12, 11, 13, 5, 6]` and sort it using Insertion Sort.  
让我们考虑一个列表 `[12, 11, 13, 5, 6]` 并使用插入排序对其进行排序。

#### Step-by-Step Process 分步过程

1. **Initial List**: `[12, 11, 13, 5, 6]`  
   **初始列表**：`[12, 11, 13, 5, 6]`

   - The first element `12` is considered sorted.  
     第一个元素 `12` 被视为已排序。
   - The second element `11` is compared with `12` and placed before it.  
     第二个元素 `11` 与 `12` 进行比较，并放在它之前。

   **List after Step 1**: `[11, 12, 13, 5, 6]`  
   **第1步后的列表**：`[11, 12, 13, 5, 6]`

2. **Second Iteration**:  
   **第二次迭代**：

   - The third element `13` is compared with `12` and `11`, and it remains in its position because it is larger.  
     第三个元素 `13` 与 `12` 和 `11` 进行比较，由于它更大，因此保持在原位。

   **List after Step 2**: `[11, 12, 13, 5, 6]`  
   **第2步后的列表**：`[11, 12, 13, 5, 6]`

3. **Third Iteration**:  
   **第三次迭代**：

   - The fourth element `5` is compared with `13`, `12`, and `11`, and it is placed at the beginning of the list.  
     第四个元素 `5` 与 `13`、`12` 和 `11` 进行比较，并将其放在列表的开头。

   **List after Step 3**: `[5, 11, 12, 13, 6]`  
   **第3步后的列表**：`[5, 11, 12, 13, 6]`

4. **Fourth Iteration**:  
   **第四次迭代**：

   - The fifth element `6` is compared with `13`, `12`, and `11`, and it is placed between `5` and `11`.  
     第五个元素 `6` 与 `13`、`12` 和 `11` 进行比较，并将其放在 `5` 和 `11` 之间。

   **List after Step 4**: `[5, 6, 11, 12, 13]`  
   **第4步后的列表**：`[5, 6, 11, 12, 13]`

5. The list is now fully sorted.  
   现在，列表已经完全排序。

### Python Implementation of Insertion Sort 插入排序的Python实现

Here is the Python code to implement Insertion Sort:  
以下是实现插入排序的Python代码：

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

arr = [12, 11, 13, 5, 6]
insertion_sort(arr)
print("Sorted array:", arr)
```

This code will output:  
这段代码的输出将是：

```
Sorted array: [5, 6, 11, 12, 13]
```

### Analysis of Insertion Sort 插入排序的分析

- **Time Complexity**: O(n²) in the worst case because of the nested loops. However, it performs well on nearly sorted data with a time complexity of O(n).  
  **时间复杂度**：最坏情况下为 O(n²)，因为存在嵌套循环。然而，在接近排序的数据上表现良好，时间复杂度为 O(n)。

- **Space Complexity**: O(1) because it is an in-place sorting algorithm.  
  **空间复杂度**：O(1)，因为这是一个原地排序算法。

- **Stability**: Insertion Sort is stable; the relative order of equal elements is preserved.  
  **稳定性**：插入排序是稳定的；相等元素的相对顺序得以保持。

### Example with Mutable List 示例：使用可变列表

If you apply Insertion Sort to a list, it directly modifies the list in place, reflecting changes as the sort progresses.  
如果您对列表应用插入排序，它会直接在原地修改列表，随着排序的进行反映变化。

```python
arr = [12, 11, 13, 5, 6]
insertion_sort(arr)
print("Sorted array:", arr)  # Output: [5, 6, 11, 12, 13]
```

In this example:  
在这个例子中：

- The original list `arr` is modified in place during sorting.  
  原始列表 `arr` 在排序过程中就地修改。

- After sorting, `arr` contains the sorted elements.  
  排序后，`arr` 包含排序后的元素。

### Conclusion 结论

Insertion Sort is a simple and efficient algorithm for small datasets or nearly sorted lists. It has a time complexity of O(n²) in the worst case but performs better on data that is already partially sorted. It is an in-place, stable sorting algorithm that is easy to understand and implement.  
插入排序是一种适用于小数据集或接近排序列表的简单而高效的算法。它在最坏情况下的时间复杂度为 O(n²)，但在已经部分排序的数据上表现更好。它是一个原地、稳定的排序算法，易于理解和实现。

This algorithm is particularly useful when you have a small number of elements or when the list is already partially sorted.  
当您有少量元素或列表已部分排序时，此算法特别有用。
