# Python Sort: Stable vs. Unstable Sorting Algorithms

- [Stable vs Unstable Sorting in Python](https://codebitwave.com/algorithms-101-stable-vs-unstable-sorting-in-python/)


When working with sorting algorithms, understanding the difference between stable and unstable sorts is crucial. Stability in sorting refers to the preservation of the relative order of equal elements in the sorted output. In this blog post, we'll explore what stable and unstable sorting algorithms are, how they work, and why stability matters in certain scenarios, particularly with Python's built-in sorting functions.

在使用排序算法时，了解稳定排序和不稳定排序之间的区别至关重要。排序中的稳定性是指在排序输出中保持相等元素的相对顺序。在这篇博客文章中，我们将探讨什么是稳定排序和不稳定排序算法，它们是如何工作的，以及为什么在某些情况下（尤其是Python内置排序函数中）稳定性很重要。

## What is a Stable Sort?

### Concept
A sorting algorithm is said to be stable if it preserves the relative order of records with equal keys (i.e., values). In other words, if two items are equal in the unsorted list, they will appear in the same order in the sorted list.

如果一个排序算法在排序后保持具有相等键（即值）的记录的相对顺序，则称其为稳定的排序算法。换句话说，如果两个项目在未排序的列表中是相等的，那么它们在排序后的列表中将以相同的顺序出现。

### Example
Consider the following list of tuples, where the first element of each tuple is the key:

考虑下面的元组列表，其中每个元组的第一个元素是键：

```python
data = [('apple', 2), ('banana', 1), ('orange', 2), ('grape', 1)]
```

Sorting this list by the second element (the key) using a stable sort will maintain the relative order of elements with the same key:

使用稳定排序按第二个元素（键）对该列表进行排序，将保持具有相同键的元素的相对顺序：

```python
sorted_data = sorted(data, key=lambda x: x[1])
# Output: [('banana', 1), ('grape', 1), ('apple', 2), ('orange', 2)]
```

In the sorted list, `'banana'` and `'grape'` maintain their order relative to each other, as do `'apple'` and `'orange'`.

在排序后的列表中，'banana' 和 'grape' 相对于彼此保持顺序，'apple' 和 'orange' 也是如此。

## What is an Unstable Sort?

### Concept
An unstable sort, on the other hand, may not preserve the relative order of records with equal keys. This means that the order of equal elements might change after sorting.

另一方面，不稳定排序可能不会保持具有相等键的记录的相对顺序。这意味着在排序之后，相等元素的顺序可能会发生变化。

### Example
Using an unstable sort algorithm on the same list could result in the following:

在相同的列表上使用不稳定排序算法可能会产生以下结果：

```python
unstable_sorted_data = [('grape', 1), ('banana', 1), ('orange', 2), ('apple', 2)]
```

In this case, `'grape'` appears before `'banana'`, and `'orange'` appears before `'apple'`, even though they were originally in the opposite order.

在这种情况下，'grape' 出现在 'banana' 之前，'orange' 出现在 'apple' 之前，尽管它们最初的顺序是相反的。

## Why Stability Matters

### Practical Applications
Stability is important in situations where the order of equal elements carries significance. For example, if you're sorting records of employees first by department and then by seniority, a stable sort will ensure that employees with the same seniority retain their original relative order within each department.

稳定性在相等元素的顺序具有重要意义的情况下很重要。例如，如果你首先按部门排序员工记录，然后按资历排序，稳定排序将确保具有相同资历的员工在每个部门内保留其原始相对顺序。

### Python's Built-in Sorting Functions

In Python, the built-in `sorted()` function and the `sort()` method of lists are stable. This means that if you sort a list of tuples or objects by one field and then by another, the second sort will not disturb the order of elements that are equal according to the first sort.

在Python中，内置的 `sorted()` 函数和列表的 `sort()` 方法是稳定的。这意味着如果你按一个字段对元组或对象列表进行排序，然后按另一个字段进行排序，第二次排序不会打乱根据第一次排序相等的元素的顺序。

```python
data = [('apple', 2), ('banana', 1), ('orange', 2), ('grape', 1)]
sorted_data = sorted(data, key=lambda x: x[1])
```

Even after sorting by the second element, the order of items with the same second element is preserved.

即使在按第二个元素排序之后，具有相同第二个元素的项目顺序仍然保留。

## Comparison of Stable and Unstable Sorting Algorithms

### Stable Sorting Algorithms
- **Merge Sort (归并排序):** A stable, divide-and-conquer algorithm with a time complexity of O(n log n). It is often preferred when stability is required.
- **Timsort (Tim排序):** A hybrid stable sorting algorithm derived from Merge Sort and Insertion Sort, used by Python's `sorted()` and `sort()` methods.

- **归并排序（Merge Sort）:** 一种稳定的分治算法，时间复杂度为 O(n log n)。当需要稳定性时，它通常是首选。
- **Tim排序（Timsort）:** 一种从归并排序和插入排序派生的混合稳定排序算法，Python 的 `sorted()` 和 `sort()` 方法使用这种算法。

### Unstable Sorting Algorithms
- **Quick Sort (快速排序):** An efficient, in-place, and commonly used sorting algorithm with an average-case time complexity of O(n log n). However, it is typically unstable.
- **Heap Sort (堆排序):** An efficient, in-place sorting algorithm with a time complexity of O(n log n), but it is unstable because it does not preserve the relative order of equal elements.

- **快速排序（Quick Sort）:** 一种高效的、原地的、常用的排序算法，平均时间复杂度为 O(n log n)。然而，它通常是不稳定的。
- **堆排序（Heap Sort）:** 一种高效的、原地的排序算法，时间复杂度为 O(n log n)，但它是不稳定的，因为它不保留相等元素的相对顺序。

### Comparison Table

| Algorithm       | Stability | Time Complexity  | Space Complexity | Usage Scenario                           |
|-----------------|-----------|------------------|------------------|------------------------------------------|
| **Merge Sort**  | Stable    | O(n log n)       | O(n)             | Large datasets, requires stability       |
| **Timsort**     | Stable    | O(n log n)       | O(n)             | Python's default sorting method          |
| **Quick Sort**  | Unstable  | O(n log n)       | O(log n)         | General-purpose sorting                  |
| **Heap Sort**   | Unstable  | O(n log n)       | O(1)             | Memory-efficient sorting, no stability needed |

| **算法**         | **稳定性** | **时间复杂度**    | **空间复杂度**    | **使用场景**                                  |
|-----------------|-----------|------------------|------------------|----------------------------------------------|
| **归并排序**     | 稳定       | O(n log n)       | O(n)             | 大型数据集，需要稳定性                        |
| **Tim排序**      | 稳定       | O(n log n)       | O(n)             | Python 的默认排序方法                          |
| **快速排序**     | 不稳定     | O(n log n)       | O(log n)         | 通用排序                                     |
| **堆排序**       | 不稳定     | O(n log n)       | O(1)             | 内存高效排序，不需要稳定性                      |

## Conclusion

Understanding the distinction between stable and unstable sorting algorithms is essential, especially when working with complex data structures where the order of equal elements matters. Python's built-in sorting functions, being stable, are well-suited for many scenarios where stability is required.

理解稳定排序和不稳定排序算法之间的区别是至关重要的，特别是在处理相等元素顺序很重要的复杂数据结构时。Python 的内置排序函数是稳定的，适用于许多需要稳定性的场景。

When deciding which sorting algorithm to use, consider the nature of the data and whether the order of equal elements is important. In cases where stability is crucial, Merge Sort or Timsort should be your go-to algorithms. However, if performance and space efficiency are more critical, and stability is not a concern, Quick Sort or Heap Sort might be more appropriate.

在决定使用哪种排序算法时，考虑数据的性质以及相等元素的顺序是否重要。在稳定性至关重要的情况下，归并排序或 Tim 排序应该是首选算法。然而，如果性能和空间效率更为重要，且稳定性不是问题，那么快速排序或堆排序可能更合适。
