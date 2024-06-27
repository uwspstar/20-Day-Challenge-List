The Python examples you provided demonstrate various useful techniques for working with loops in Python. These techniques can help make your code cleaner, more readable, and efficient. Let's discuss each of these techniques in both English and Chinese.

您提供的 Python 示例演示了如何在 Python 中使用循环的各种有用技巧。这些技巧可以帮助使您的代码更清晰、可读和高效。让我们用英文和中文讨论每一种技巧。

### 1. Looping Over Dictionaries | 遍历字典

#### English
When looping over a dictionary, you can use the `.items()` method to retrieve both the key and its corresponding value at the same time. This method returns pairs of keys and values, making it easy to work with each item directly.

#### 中文
在遍历字典时，可以使用 `.items()` 方法同时提取键及其对应的值。此方法返回键值对，便于直接操作每个项。

**Example | 示例:**
```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print(k, v)
```

### 2. Looping With `enumerate()` | 使用 `enumerate()` 遍历

#### English
When looping over a sequence and you need both the index and the value, `enumerate()` is very useful. It adds a counter to an iterable and returns it in a form of enumerate object.

#### 中文
在遍历序列时，如果需要位置索引和对应的值，`enumerate()` 非常有用。它为可迭代对象添加计数器，并以枚举对象的形式返回。

**Example | 示例:**
```python
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)
```

### 3. Looping Over Multiple Sequences With `zip()` | 使用 `zip()` 遍历多个序列

#### English
`zip()` is used to loop over two or more sequences simultaneously by pairing elements with the same index from each sequence.

#### 中文
`zip()` 用于同时遍历两个或多个序列，通过将每个序列中相同索引的元素配对。

**Example | 示例:**
```python
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
    print('What is your {0}?  It is {1}.'.format(q, a))
```

### 4. Reversed Looping With `reversed()` | 使用 `reversed()` 反向遍历

#### English
`reversed()` allows you to loop over a sequence in reverse order without altering the original sequence.

#### 中文
`reversed()` 允许您反向遍历序列，而无需更改原始序列。

**Example | 示例:**
```python
for i in reversed(range(1, 10, 2)):
    print(i)
```

### 5. Sorting During Looping With `sorted()` | 使用 `sorted()` 在遍历中排序

#### English
`sorted()` sorts any sequence and returns a new sorted list, allowing you to loop over the elements in a sorted order without altering the original sequence.

#### 中文
`sorted()` 对任何序列进行排序，并返回一个新的排序列表，允许您在不更改原始序列的情况下按排序后的顺序遍历元素。

**Example | 示例:**
```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
for i in sorted(basket):
    print(i)
```

### 6. Removing Duplicates and Sorting With `set()` and `sorted()` | 使用 `set()` 和 `sorted()` 去除重复元素并排序

#### English
Combining `set()` and `sorted()` allows you to remove duplicates and loop through the unique elements in a sorted order.

#### 中文
结合使用 `set()` 和 `sorted()` 可以去除重复元素，并按排序后的顺序遍历唯一元素。

**Example | 示例:**
```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
for f in sorted(set(basket)):
    print(f)
```

### 7. Safe List Modification During Looping | 在循环中安全修改列表

#### English
When modifying a list during looping, it's safer and simpler to create a new list to store the modified elements.

#### 中文
在循环中修改列表时，创建一个新列表来存储修改后的元素更安全、更简单。

**Example | 示例:**
```python
import math
raw_data = [56.2, float('NaN

'), 51.7, 55.3, 52.5, float('NaN'), 47.8]
filtered_data = []
for value in raw_data:
    if not math.isnan(value):
        filtered_data.append(value)
print(filtered_data)
```

These looping techniques are foundational in Python programming, enhancing both the effectiveness and efficiency of data manipulation and processing tasks.
