# Bubble Sort 冒泡排序

- [Bubble Sort](https://codebitwave.com/algorithms-101-bubble-sort/)
- 
Bubble Sort is a simple comparison-based sorting algorithm. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted. The algorithm gets its name because larger elements "bubble" to the top of the list as the sort progresses.  
冒泡排序是一种简单的基于比较的排序算法。它通过反复遍历列表，比较相邻元素，如果顺序错误则交换它们。这一过程反复进行，直到列表排序完成。该算法之所以得名，是因为在排序过程中较大的元素会“冒泡”到列表的顶部。

### How Bubble Sort Works 冒泡排序如何工作

1. Start at the beginning of the list.  
   从列表的开头开始。

2. Compare the first two elements. If the first is greater than the second, swap them.  
   比较前两个元素。如果第一个大于第二个，则交换它们。

3. Move to the next pair of elements, compare them, and swap if necessary.  
   移动到下一个元素对，进行比较，并在必要时交换。

4. Continue this process until the end of the list. The largest element will "bubble" to the end of the list after each pass.  
   继续此过程直到列表末尾。最大的元素将在每次遍历后“冒泡”到列表的末尾。

5. Repeat the entire process for the remaining elements, excluding the last sorted elements, until the whole list is sorted.  
   对剩余元素重复整个过程，排除最后已排序的元素，直到整个列表排序完成。

### Example of Bubble Sort 冒泡排序的示例

Let's consider a list `[64, 34, 25, 12, 22, 11, 90]` and sort it using Bubble Sort.  
让我们考虑一个列表 `[64, 34, 25, 12, 22, 11, 90]` 并使用冒泡排序对其进行排序。

#### Step-by-Step Process 分步过程

1. **Initial List**: `[64, 34, 25, 12, 22, 11, 90]`  
   **初始列表**：`[64, 34, 25, 12, 22, 11, 90]`

   - Compare `64` and `34`, swap them.  
     比较 `64` 和 `34`，交换它们。
   - Compare `64` and `25`, swap them.  
     比较 `64` 和 `25`，交换它们。
   - Continue this process until the last pair `11` and `90`. Since `90` is already the largest, it remains in place.  
     继续这个过程直到最后一对 `11` 和 `90`。由于 `90` 已经是最大的，因此保持在原位。

   **List after Step 1**: `[34, 25, 12, 22, 11, 64, 90]`  
   **第1步后的列表**：`[34, 25, 12, 22, 11, 64, 90]`

2. **Second Iteration**:  
   **第二次迭代**：

   - The last element `90` is now sorted, so we ignore it and start again from the beginning.  
     最后一个元素 `90` 已经排序，因此我们忽略它并从头开始。
   - Compare `34` and `25`, swap them.  
     比较 `34` 和 `25`，交换它们。
   - Continue the process until `64` and `11`, swap them.  
     继续这个过程直到 `64` 和 `11`，交换它们。

   **List after Step 2**: `[25, 12, 22, 11, 34, 64, 90]`  
   **第2步后的列表**：`[25, 12, 22, 11, 34, 64, 90]`

3. **Third Iteration**:  
   **第三次迭代**：

   - Now `64` and `90` are sorted, so we ignore them and start again.  
     现在 `64` 和 `90` 已经排序，因此我们忽略它们并重新开始。
   - Compare `25` and `12`, swap them.  
     比较 `25` 和 `12`，交换它们。
   - Continue the process until `34` and `11`, swap them.  
     继续这个过程直到 `34` 和 `11`，交换它们。

   **List after Step 3**: `[12, 22, 11, 25, 34, 64, 90]`  
   **第3步后的列表**：`[12, 22, 11, 25, 34, 64, 90]`

4. **Fourth Iteration**:  
   **第四次迭代**：

   - Continue the process.  
     继续这个过程。
   - Swap where necessary.  
     在必要时交换。

   **List after Step 4**: `[12, 11, 22, 25, 34, 64, 90]`  
   **第4步后的列表**：`[12, 11, 22, 25, 34, 64, 90]`

5. **Fifth Iteration**:  
   **第五次迭代**：

   - The list is nearly sorted, only a final pass is needed.  
     列表几乎已经排序，只需最后一次遍历。
   - Swap `12` and `11`.  
     交换 `12` 和 `11`。

   **List after Step 5**: `[11, 12, 22, 25, 34, 64, 90]`  
   **第5步后的列表**：`[11, 12, 22, 25, 34, 64, 90]`

6. The list is now fully sorted.  
   现在，列表已经完全排序。

### Python Implementation of Bubble Sort 冒泡排序的Python实现

Here is the Python code to implement Bubble Sort:  
以下是实现冒泡排序的Python代码：

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped:
            break

arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(arr)
print("Sorted array:", arr)
```

This code will output:  
这段代码的输出将是：

```
Sorted array: [11, 12, 22, 25, 34, 64, 90]
```

### Analysis of Bubble Sort 冒泡排序的分析

- **Time Complexity**: O(n²) because of the two nested loops. The best case (when the list is already sorted) is O(n).  
  **时间复杂度**：O(n²)，因为有两个嵌套循环。最佳情况（列表已经排序）为 O(n)。

- **Space Complexity**: O(1) because it is an in-place sorting algorithm.  
  **空间复杂度**：O(1)，因为这是一个原地排序算法。

- **Stability**: Bubble Sort is stable; the relative order of equal elements is preserved.  
  **稳定性**：冒泡排序是稳定的；相等元素的相对顺序得以保持。

### Example with Mutable List 示例：使用可变列表

If you apply Bubble Sort to a list, it directly modifies the list in place, reflecting changes as the sort progresses.  
如果您对列表应用冒泡排序，它会直接在原地修改列表，随着排序的进行反映变化。

```python
arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(arr)
print("Sorted array:", arr)  # Output: [11, 12, 22, 25, 34, 64, 90]
```

In this example:  
在这个例子中：

- The original list `arr` is modified in place during sorting.  
  原始列表 `arr` 在排序过程中就地修改。

- After sorting, `arr` contains the sorted elements.  
  排序后，`arr` 包含排序后的元素。

### Conclusion 结论

Bubble Sort is one of the simplest sorting algorithms to understand and implement, making it a good educational tool. However, it is not efficient for large datasets due to its O(n²) time complexity. It is a stable, in-place sorting algorithm, but its performance can be significantly improved with optimizations like early termination when no swaps are needed during a pass.  
冒泡排序是最简单易懂和实现的排序算法之一，是一种很好的教育工具。然而，由于其O(n²)的时间复杂度，它对于大数据集来说效率不高。它是一种稳定的原地排序算法，但通过优化，例如在遍历期间

不需要交换时提前终止，可以显著提高其性能。

Bubble Sort is best suited for small datasets or for educational purposes to demonstrate how sorting algorithms work.  
冒泡排序最适合小数据集或用于教育目的，展示排序算法如何工作。
