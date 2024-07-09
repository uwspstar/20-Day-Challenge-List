# List []
- https://www.w3schools.com/python/python_lists.asp

The list is changeable, meaning that we can change, add, and remove items in a list after it has been created.

### Python List Methods

| Method      | Description                                                  |
|-------------|--------------------------------------------------------------|
| append()    | Adds an element at the end of the list                       |
| clear()     | Removes all the elements from the list                       |
| copy()      | Returns a copy of the list                                   |
| count()     | Returns the number of elements with the specified value      |
| extend()    | Add the elements of a list (or any iterable) to the end of the current list |
| index()     | Returns the index of the first element with the specified value |
| insert()    | Adds an element at the specified position                    |
| pop()       | Removes the element at the specified position                |
| remove()    | Removes the item with the specified value                    |
| reverse()   | Reverses the order of the list                               |
| sort()      | Sorts the list                                               |


## how Python lists work behind the scenes:

- https://neetcode.io/courses/dsa-for-beginners/3
- A Python list is a dynamic array.
- Python lists are implemented as arrays of pointers to the objects.
- The list object itself contains a pointer to an array of pointers, the current size of the array, and the allocated size.
- When elements are added to the list, if there is enough space in the allocated array, they are added directly.
- If there is not enough space, a larger array is allocated and the elements are copied over.
- This makes appending elements to a list on average O(1) in terms of time complexity.
- Python lists can hold objects of different types because they store pointers to objects.
- Memory allocation for Python lists follows a strategy called overallocation, which reduces the frequency of memory reallocation.

- Python 列表是一个动态数组。
- Python 列表实现为对象指针的数组。
- 列表对象本身包含一个指向指针数组的指针、当前数组的大小和已分配的大小。
- 当元素添加到列表时，如果已分配的数组中有足够的空间，它们会直接添加进去。
- 如果没有足够的空间，会分配一个更大的数组，并将元素复制过去。
- 这使得向列表追加元素的平均时间复杂度为 O(1)。
- Python 列表可以包含不同类型的对象，因为它们存储的是对象的指针。
- Python 列表的内存分配采用一种称为过度分配的策略，这减少了内存重新分配的频率。

In Python, a 动态数组 (dynamic array) refers to the implementation of lists, which can grow and shrink in size as needed. Unlike static arrays in some other languages, where the size is fixed at creation, Python lists are flexible in size. Here’s how dynamic arrays work in Python:

- **Dynamic Resizing:** Python lists can change size automatically. When elements are added and there isn’t enough space in the current array, Python allocates a larger array and copies the existing elements over.
- **Array of Pointers:** Python lists are arrays of pointers to the actual objects. This allows lists to store elements of different types.
- **Over-allocation:** To optimize performance, Python often allocates more space than needed, reducing the number of times the array needs to be resized.
- **Time Complexity:** Appending an element to a list has an average time complexity of O(1) due to the over-allocation strategy.

- **动态调整大小:** Python 列表可以自动改变大小。当添加元素且当前数组空间不足时，Python 会分配一个更大的数组并复制现有元素。
- **指针数组:** Python 列表是指向实际对象的指针数组。这允许列表存储不同类型的元素。
- **过度分配:** 为了优化性能，Python 通常会分配比需要更多的空间，减少数组需要调整大小的次数。
- **时间复杂度:** 由于过度分配策略，向列表追加元素的平均时间复杂度为 O(1)。

This flexibility and efficiency make Python lists a powerful and easy-to-use data structure for a wide range of applications.

### Dynamic Arrays:
- Dynamic arrays are much more common and useful because of their ability to be resized.
- In languages like JavaScript and Python, dynamic arrays are the default — these languages are not strictly typed.
- The difference between static and dynamic arrays is that we don’t have to specify a size upon initialization.
- In different languages, dynamic arrays may be assigned a default size. For example, in Java, the default size is 10, and in C#, it is 4.
- Regardless of the initial size, these arrays are automatically resized at runtime when needed.

### 动态数组:
- 动态数组更常见且更有用，因为它们可以调整大小。
- 在 JavaScript 和 Python 这样的语言中，动态数组是默认的 — 这些语言不是严格类型的。
- 静态数组和动态数组的区别在于，我们在初始化时不必指定大小。
- 在不同的语言中，动态数组可能会被分配一个默认大小。例如，在 Java 中，默认大小是 10，在 C# 中是 4。
- 无论初始大小是多少，这些数组在需要时会在运行时自动调整大小。

Let’s delve deeper into how dynamic arrays automatically resize at runtime with the 5Ws (Who, What, When, Where, Why, and How) and include examples:

**Who:**
- The process of resizing a dynamic array is handled by the programming language’s runtime environment.

**What:**
- Dynamic arrays automatically adjust their size to accommodate new elements when they exceed their current capacity.

**When:**
- This resizing occurs during runtime, specifically when an operation (like adding a new element) causes the array to exceed its current capacity.

**Where:**
- This process happens internally within the dynamic array implementation in the programming language.

**Why:**
- The resizing ensures that the dynamic array can continue to hold additional elements without running out of space, providing flexibility to the programmer.

**How:**
- When the dynamic array reaches its capacity, a larger array is allocated.
- The elements from the original array are copied to the new array.
- The original array is then replaced with the new array, often with a size that is a multiple of the original to reduce the frequency of resizing operations.

### Examples:

**Python Example:**

```python
# Creating a dynamic array (list) in Python
dynamic_array = []

# Adding elements to the dynamic array
for i in range(15):  # Exceeding initial capacity (e.g., hypothetical initial capacity is 10)
    dynamic_array.append(i)
    print(dynamic_array)
```

**Explanation:**
- Initially, the list is empty. When elements are appended, if the list's current capacity is exceeded, Python allocates a new larger list, copies existing elements, and then continues adding the new element.

**JavaScript Example:**

```javascript
// Creating a dynamic array in JavaScript
let dynamicArray = [];

// Adding elements to the dynamic array
for (let i = 0; i < 15; i++) {  // Exceeding initial capacity
    dynamicArray.push(i);
    console.log(dynamicArray);
}
```
- Similarly, in JavaScript, the array starts with a default size. When the capacity is exceeded during the push operation, the engine reallocates a larger array and moves the elements to this new array.

### Internal Mechanism:

1. **Initial State:**
   - The dynamic array starts with an initial capacity.
   
2. **Adding Elements:**
   - As elements are added, the array keeps track of its capacity.
   
3. **Exceeding Capacity:**
   - When the capacity is exceeded, a new array (usually double the size of the old one) is allocated.
   
4. **Copying Elements:**
   - Existing elements are copied from the old array to the new one.
   
5. **Continuing Operations:**
   - The operation (e.g., append or push) that triggered the resizing completes with the new array.

This process ensures that dynamic arrays can grow as needed, providing a seamless experience for developers without worrying about manual memory management.

**谁:**
- 动态数组的调整大小过程由编程语言的运行时环境处理。

**什么:**
- 当动态数组超过当前容量时，自动调整其大小以容纳新元素。

**什么时候:**
- 这种调整发生在运行时，具体来说是在添加新元素使数组超过其当前容量时。

**哪里:**
- 这个过程发生在编程语言的动态数组实现内部。

**为什么:**
- 调整大小确保动态数组可以继续容纳额外的元素，而不会耗尽空间，为程序员提供灵活性。

**如何:**
- 当动态数组达到其容量时，会分配一个更大的数组。
- 将原数组中的元素复制到新数组中。
- 然后用新数组替换原数组，通常新数组的大小是原数组的倍数，以减少调整大小的频率。

### 示例:

**Python 示例:**

```python
# 在 Python 中创建一个动态数组（列表）
dynamic_array = []

# 向动态数组添加元素
for i in range(15):  # 超过初始容量（例如，假设初始容量为 10）
    dynamic_array.append(i)
    print(dynamic_array)
```

**解释:**
- 最初，列表是空的。当添加元素时，如果列表的当前容量不足，Python 会分配一个更大的列表，复制现有元素，然后继续添加新元素。

**JavaScript 示例:**

```javascript
// 在 JavaScript 中创建一个动态数组
let dynamicArray = [];

// 向动态数组添加元素
for (let i = 0; i < 15; i++) {  // 超过初始容量
    dynamicArray.push(i);
    console.log(dynamicArray);
}
```

**解释:**
- 类似地，在 JavaScript 中，数组从默认大小开始。当在推送操作期间超过容量时，引擎重新分配一个更大的数组，并将元素移动到这个新数组中。

### 内部机制:

1. **初始状态:**
   - 动态数组从初始容量开始。
   
2. **添加元素:**
   - 随着元素的添加，数组跟踪其容量。
   
3. **超过容量:**
   - 当超过容量时，会分配一个新数组（通常是旧数组大小的两倍）。
   
4. **复制元素:**
   - 将现有元素从旧数组复制到新数组中。
   
5. **继续操作:**
   - 触发调整大小的操作（例如，append 或 push）使用新数组完成。

这个过程确保动态数组可以根据需要增长，为开发人员提供无缝体验，而无需担心手动内存管理。

### Amortized time complexity
Let’s break down the process of resizing dynamic arrays and the concept of `amortized time complexity` in more detail:

### Explanation:

**When all elements from the first array have been copied over, it does not make sense to keep it in memory - this space will be deallocated.**
- Once the elements are copied from the original array to the new, larger array, the original array is no longer needed.
- The memory occupied by the original array is released back to the system.

### Amortized Time Complexity:

**This operation will run in amortized O(1).**
- Although resizing the array and copying elements take O(n) time, it does not happen every time an element is added.
- Instead, resizing happens infrequently enough that the average time per element added is constant.

**Amortized time complexity is the average time taken per operation, that once it happens, it won’t happen again for so long that the cost becomes “amortized”.**
- Amortized time complexity provides a more accurate measure of performance for operations that have occasional expensive steps (like resizing) but are generally fast.
- The expensive steps (resizing) are spread out over many inexpensive steps (adding elements), resulting in a low average cost per operation.

**This makes sense because it is not always that the array needs to be resized, in which case we would perform O(n) operations.**
- Most of the time, adding an element to a dynamic array takes O(1) time.
- Only when the array runs out of space does it need to be resized, which is an O(n) operation.
- Since resizing is infrequent, the overall time complexity for adding elements remains O(1) on average.

### Example in Python:

```python
# Creating a dynamic array (list) in Python
dynamic_array = []

# Adding elements to the dynamic array
for i in range(15):  # Exceeding initial capacity (hypothetical initial capacity is 10)
    dynamic_array.append(i)
    print(dynamic_array)
```

### Chinese Explanation:

**当第一个数组中的所有元素都被复制过来后，保留它在内存中没有意义 - 这个空间将被释放。**
- 一旦元素从原数组复制到新的更大数组中，原数组就不再需要了。
- 原数组占用的内存将被释放回系统。

### 均摊时间复杂度:

**这个操作的均摊时间复杂度是 O(1)。**
- 虽然调整数组大小和复制元素需要 O(n) 时间，但这并不是每次添加元素时都会发生。
- 相反，调整大小的频率足够低，使得每次添加元素的平均时间是恒定的。

**均摊时间复杂度是每次操作的平均时间，一旦它发生，就不会在短时间内再次发生，成本变得“均摊”。**
- 均摊时间复杂度提供了操作性能的更准确衡量，这些操作偶尔有昂贵的步骤（如调整大小），但通常是快速的。
- 昂贵的步骤（调整大小）分布在许多廉价的步骤（添加元素）中，导致每次操作的平均成本较低。

**这很有道理，因为并不是每次数组都需要调整大小，在这种情况下我们将执行 O(n) 操作。**
- 大多数时候，向动态数组添加元素的时间是 O(1)。
- 只有在数组空间不足时才需要调整大小，这是一个 O(n) 操作。
- 由于调整大小不频繁，添加元素的总体时间复杂度在平均情况下仍然是 O(1)。

### Python 示例:

```python
# 在 Python 中创建一个动态数组（列表）
dynamic_array = []

# 向动态数组添加元素
for i in range(15):  # 超过初始容量（假设初始容量为 10）
    dynamic_array.append(i)
    print(dynamic_array)
```

By understanding amortized time complexity, we see why dynamic arrays are efficient for typical use cases despite the occasional expensive resizing operation.





