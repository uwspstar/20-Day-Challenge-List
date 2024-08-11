# Modified Binary Search 修改版二分搜索

Modified Binary Search adjusts the classic binary search algorithm to cater to specific conditions, such as searching in a rotated sorted array. This pattern involves applying the core principles of binary search while incorporating modifications to handle unique cases. Understanding the foundational binary search algorithm is essential for effectively implementing the Modified Binary Search pattern.  
修改版二分搜索调整了经典的二分搜索算法，以适应特定条件，例如在旋转排序数组中搜索。此模式涉及应用二分搜索的核心原理，同时进行修改以处理特殊情况。理解基础的二分搜索算法对于有效实现修改版二分搜索模式至关重要。

### How Modified Binary Search Works 修改版二分搜索如何工作

1. **Understand the Problem Context**: Identify the specific conditions that necessitate modifications to the classic binary search. For example, searching in a rotated sorted array where the array has been pivoted around an unknown point.  
   **理解问题背景**：确定需要对经典二分搜索进行修改的特定条件。例如，在旋转排序数组中搜索，其中数组已围绕未知点旋转。

2. **Divide the Array**: Use the binary search method to divide the array into two halves. Determine which half of the array is properly sorted.  
   **划分数组**：使用二分搜索方法将数组分为两半。确定哪一半数组是正确排序的。

3. **Focus on the Relevant Half**: Depending on the target value and the sorted half, decide whether to continue searching in the left or right half of the array.  
   **专注于相关的一半**：根据目标值和已排序的那一半，决定是继续在数组的左半部分还是右半部分搜索。

4. **Adjust the Search Range**: Modify the search range based on the target’s relationship with the middle element and the identified sorted half.  
   **调整搜索范围**：根据目标值与中间元素的关系以及已识别的排序部分来调整搜索范围。

5. **Repeat Until Found**: Continue dividing and narrowing the search range until the target element is found or the range is exhausted.  
   **重复直到找到目标**：继续划分并缩小搜索范围，直到找到目标元素或范围耗尽。

### Example of Modified Binary Search 修改版二分搜索的示例

Consider the following rotated sorted array:  
考虑以下旋转排序数组：

```
Array: [6, 7, 1, 2, 3, 4, 5]
```

We want to find the target value `3`.  
我们想找到目标值 `3`。

#### Step-by-Step Process of Modified Binary Search 修改版二分搜索的分步过程

1. **Initial Array**:  
   **初始数组**：

   - Array: `[6, 7, 1, 2, 3, 4, 5]`  
     数组：`[6, 7, 1, 2, 3, 4, 5]`
   - Target: `3`  
     目标值：`3`

2. **Divide the Array**:  
   **划分数组**：

   - Middle element is `2` (index 3).  
     中间元素是 `2`（索引 3）。
   - Left half: `[6, 7, 1]`  
     左半部分：`[6, 7, 1]`
   - Right half: `[2, 3, 4, 5]`  
     右半部分：`[2, 3, 4, 5]`

3. **Determine the Sorted Half**:  
   **确定排序的一半**：

   - Right half `[2, 3, 4, 5]` is sorted.  
     右半部分 `[2, 3, 4, 5]` 是排序的。
   - Since `3` falls within this range, focus on the right half.  
     由于 `3` 落在这个范围内，专注于右半部分。

4. **Adjust the Search Range**:  
   **调整搜索范围**：

   - New search range: `[2, 3, 4, 5]`  
     新的搜索范围：`[2, 3, 4, 5]`
   - Middle element is `3` (index 4).  
     中间元素是 `3`（索引 4）。

5. **Target Found**:  
   **找到目标**：

   - The target `3` is found at index `4`.  
     目标 `3` 在索引 `4` 处找到。

### Python Implementation of Modified Binary Search 修改版二分搜索的Python实现

Here is the Python code to implement Modified Binary Search for finding a target in a rotated sorted array:  
以下是实现修改版二分搜索以在旋转排序数组中查找目标的Python代码：

```python
def modified_binary_search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if nums[mid] == target:
            return mid
        
        # Determine which side is properly sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
                
    return -1

# Example array and target
nums = [6, 7, 1, 2, 3, 4, 5]
target = 3
result = modified_binary_search(nums, target)
print("Target found at index:", result)
```

This code will output the index of the target value `3` in the array:  
这段代码将输出数组中目标值 `3` 的索引：

```
Target found at index: 4
```

### Analysis of Modified Binary Search 修改版二分搜索的分析

- **Time Complexity**: O(log n), where `n` is the number of elements in the array. The algorithm maintains the logarithmic time complexity of classic binary search by dividing the array in half at each step.  
  **时间复杂度**：O(log n)，其中 `n` 是数组中的元素数量。该算法通过在每一步将数组分成两半，保持了经典二分搜索的对数时间复杂度。

- **Space Complexity**: O(1), as the algorithm uses a constant amount of additional space.  
  **空间复杂度**：O(1)，因为算法使用的额外空间是常量。

- **Use Cases**: The Modified Binary Search is particularly useful in problems such as searching in rotated sorted arrays, finding the minimum in a rotated array, or solving variations of binary search that involve additional conditions or constraints.  
  **使用案例**：修改版二分搜索在以下问题中特别有用：在旋转排序数组中搜索、在旋转数组中找到最小值，或解决涉及额外条件或约束的二分搜索变体。

### Example with a Different Array 示例：使用不同的数组

Consider the following rotated sorted array:  
考虑以下旋转排序数组：

```
Array: [8, 9, 10, 2, 3, 4, 5, 6, 7]
```

Target: `5`  
目标值：`5`

Using Modified Binary Search, the target `5` can be found at index `6`.  
使用修改版二分搜索，目标 `5` 可以在索引 `6` 处找到。

### Conclusion 结论

The Modified Binary Search is a powerful extension of the classic binary search algorithm, tailored to handle specific conditions such as searching in rotated sorted arrays. By adapting the search strategy to focus on the relevant portion of the array, this pattern retains the efficiency of binary search while addressing more complex problems.  
修改版二分搜索是经典二分搜索算法的强大扩展，专为处理特定条件（如在旋转排序数组中搜索）而设计。通过调整搜索策略以专注于数组的相关部分，该模式在解决更复杂问题时保留了二分搜索的效率。

This method is essential for solving problems that involve variations of binary search, making it a versatile tool in algorithm design and problem-solving.  
这种方法对于解决涉及二分搜索变体的问题至关重要，使其成为算法设计和问题解决中的一种多功能工具。
