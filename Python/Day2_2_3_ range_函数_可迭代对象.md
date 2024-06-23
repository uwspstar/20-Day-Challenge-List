Indeed, the `range()` function in Python returns a range object, which is an iterable that behaves similarly to lists in many aspects but is not the same. A `range` object does not store all its items at once, which is a key difference from lists. Instead, it calculates the elements on-the-fly as needed, thus saving memory. This characteristic makes it particularly useful when dealing with large ranges of numbers.

确实，Python中的`range()`函数返回一个range对象，这是一个可迭代对象，在许多方面的行为与列表类似，但并不相同。`range`对象不会一次存储所有其项，这是它与列表的一个关键区别。相反，它根据需要即时计算元素，从而节省内存。这种特性使其在处理大范围数字时特别有用。

### Understanding Iterable Objects

An iterable object is an object that implements the `__iter__()` method which returns an iterator, or it can define a `__getitem__()` method that can take sequential indexes starting from zero. You can loop over an iterable, and it will produce items one by one, as the `range` object does.

### 理解可迭代对象

可迭代对象是实现了`__iter__()`方法（该方法返回一个迭代器）或定义了`__getitem__()`方法（该方法可以从零开始接受顺序索引）的对象。您可以遍历一个可迭代对象，它会像`range`对象那样逐一产生项目。

### Usage with `for` and Functions like `sum()`

The `for` loop in Python uses the iterable protocol to iterate over items of any iterable. This includes custom objects that implement iterable methods, as well as built-in data types like lists, tuples, and of course, range objects.

Python中的`for`循环使用可迭代协议遍历任何可迭代对象的项目。这包括实现了可迭代方法的自定义对象，以及列表、元组等内置数据类型，当然还有range对象。

Functions like `sum()` also take advantage of iterable objects by consuming their items one by one:

像`sum()`这样的函数也通过逐一消费其项目来利用可迭代对象：

```python
# Example of using range with sum()
r = range(10)  # This is an iterable of numbers from 0 to 9
total = sum(r)
print(total)  # Outputs: 45, which is the sum of numbers 0 through 9
```

Here, `sum()` function iterates over the range object and calculates the total sum of its elements, all without ever creating a full list in memory.

在这里，`sum()`函数迭代range对象并计算其元素的总和，而无需在内存中创建完整列表。

### Conclusion

Using iterables like `range` objects is efficient, especially in terms of memory usage, because they generate items only as needed. They are a fundamental part of Python, facilitating efficient loops and operations over large datasets without the overhead of storing all elements in memory at once.

### 结论

使用像`range`对象这样的可迭代对象在内存使用方面非常高效，因为它们只在需要时生成项目。它们是Python的基本部分，有助于有效地循环和操作大数据集，而无需一次性将所有元素存储在内存中。
