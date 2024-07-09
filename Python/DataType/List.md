# List
- https://www.w3schools.com/python/python_lists.asp

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



