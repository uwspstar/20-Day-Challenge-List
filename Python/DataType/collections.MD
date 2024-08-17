# Python `collections` — Container Datatypes Python `collections` — 容器数据类型

The `collections` module in Python provides a rich set of specialized container datatypes that offer alternatives to the general-purpose built-in containers like `dict`, `list`, `set`, and `tuple`. These container datatypes are designed to handle specific types of data more efficiently or with added functionality. They can help simplify complex data manipulation tasks and improve the performance and readability of your code.  
Python中的`collections`模块提供了一组丰富的专门容器数据类型，作为`dict`、`list`、`set`和`tuple`等通用内置容器的替代品。这些容器数据类型旨在更高效地处理特定类型的数据或提供附加功能。它们可以帮助简化复杂的数据操作任务，并提高代码的性能和可读性。


| Class/Function | Description                                                         | Code Example                                                                                      | Tips                                                                                              |
|----------------|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| `namedtuple()` | Factory function for creating tuple subclasses with named fields    | ```python\nfrom collections import namedtuple\nPoint = namedtuple('Point', 'x y')\np = Point(1, 2)\n``` | Use `namedtuple` to make your code more readable by assigning names to tuple elements.            |
| `deque`        | List-like container with fast appends and pops on either end        | ```python\nfrom collections import deque\ndq = deque([1, 2, 3])\ndq.append(4)\ndq.appendleft(0)\n``` | Ideal for implementing queues and stacks efficiently.                                             |
| `ChainMap`     | Dict-like class for creating a single view of multiple mappings     | ```python\nfrom collections import ChainMap\ndict1 = {'a': 1}\ndict2 = {'b': 2}\ncm = ChainMap(dict1, dict2)\n``` | Use `ChainMap` when you need to combine multiple dictionaries and access them as one.             |
| `Counter`      | Dict subclass for counting hashable objects                         | ```python\nfrom collections import Counter\ncount = Counter('hello world')\n```                    | Great for counting occurrences of elements in an iterable or for frequency analysis.              |
| `OrderedDict`  | Dict subclass that remembers the order entries were added           | ```python\nfrom collections import OrderedDict\nod = OrderedDict()\nod['a'] = 1\nod['b'] = 2\n``` | Use `OrderedDict` when the order of insertion is important and needs to be maintained.            |
| `defaultdict`  | Dict subclass that calls a factory function to supply missing values | ```python\nfrom collections import defaultdict\ndd = defaultdict(int)\ndd['missing'] += 1\n```    | Avoid `KeyError` by providing a default value for missing keys automatically.                     |
| `UserDict`     | Wrapper around dictionary objects for easier dict subclassing       | ```python\nfrom collections import UserDict\nclass MyDict(UserDict):\n    def __missing__(self, key):\n        return 0\n``` | Subclass `UserDict` to customize or extend dictionary behaviors easily.                           |
| `UserList`     | Wrapper around list objects for easier list subclassing             | ```python\nfrom collections import UserList\nclass MyList(UserList):\n    def pop(self):\n        return self.data.pop(0)\n``` | Use `UserList` to create custom list behaviors with a simpler interface than directly subclassing `list`. |
| `UserString`   | Wrapper around string objects for easier string subclassing         | ```python\nfrom collections import UserString\nclass MyString(UserString):\n    def reverse(self):\n        return self.data[::-1]\n``` | `UserString` is useful for creating custom string operations without dealing with the complexities of the `str` class. |


### Key Container Datatypes in `collections` 模块中的关键容器数据类型

1. **`namedtuple`**: A factory function that returns a tuple subclass with named fields. This allows you to create simple classes that store data in a tuple-like structure, with fields that can be accessed by name rather than by index.  
   **`namedtuple`**：一个工厂函数，返回具有命名字段的元组子类。这允许你创建简单的类，将数据存储在类似元组的结构中，可以通过名称而不是索引来访问字段。

   ```python
   from collections import namedtuple

   # Define a namedtuple type
   Point = namedtuple('Point', ['x', 'y'])
   p = Point(11, 22)

   print(p.x)  # Output: 11
   print(p.y)  # Output: 22
   ```

   **Explanation**:  
   **解释**：
   - `namedtuple` allows you to define a simple class `Point` with fields `x` and `y` that can be accessed like attributes.  
     `namedtuple`允许你定义一个简单的类`Point`，其字段`x`和`y`可以像属性一样访问。

2. **`deque`**: A double-ended queue that supports adding and removing elements from either end with O(1) time complexity. Deques are optimized for quickly appending and popping items, making them ideal for implementing queues and stacks.  
   **`deque`**：双端队列，支持以O(1)的时间复杂度从两端添加和删除元素。Deque针对快速追加和弹出项目进行了优化，非常适合实现队列和栈。

   ```python
   from collections import deque

   # Create a deque and perform operations
   d = deque(['a', 'b', 'c'])
   d.append('d')
   d.appendleft('z')
   print(d)  # Output: deque(['z', 'a', 'b', 'c', 'd'])

   d.pop()      # Removes 'd'
   d.popleft()  # Removes 'z'
   print(d)  # Output: deque(['a', 'b', 'c'])
   ```

   **Explanation**:  
   **解释**：
   - `deque` is useful when you need a queue or stack that allows fast appends and pops from both ends.  
     当你需要一个允许从两端快速追加和弹出的队列或栈时，`deque`非常有用。

3. **`Counter`**: A dictionary subclass for counting hashable objects. It is useful for tallying frequencies of elements in a collection.  
   **`Counter`**：用于计数可散列对象的字典子类。它对于统计集合中元素的频率非常有用。

   ```python
   from collections import Counter

   # Count elements in a list
   words = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
   word_counts = Counter(words)

   print(word_counts)  # Output: Counter({'apple': 3, 'banana': 2, 'orange': 1})
   print(word_counts['apple'])  # Output: 3
   ```

   **Explanation**:  
   **解释**：
   - `Counter` is handy for counting occurrences of items in a collection, like counting the frequency of words in a list.  
     `Counter`对于计算集合中项目的出现次数非常方便，例如计算列表中单词的频率。

4. **`OrderedDict`**: A dictionary subclass that remembers the order in which items were inserted. This is useful when the order of elements is important, such as when creating a sequence of operations.  
   **`OrderedDict`**：记住项目插入顺序的字典子类。当元素的顺序很重要时，这很有用，例如在创建操作序列时。

   ```python
   from collections import OrderedDict

   # Create an OrderedDict and add items
   od = OrderedDict()
   od['apple'] = 1
   od['banana'] = 2
   od['orange'] = 3

   print(od)  # Output: OrderedDict([('apple', 1), ('banana', 2), ('orange', 3)])
   ```

   **Explanation**:  
   **解释**：
   - `OrderedDict` is useful when you need to maintain the order of elements, such as in a sequence of configurations or settings.  
     当你需要保持元素的顺序时，`OrderedDict`非常有用，例如在配置或设置的序列中。

5. **`defaultdict`**: A dictionary subclass that calls a factory function to supply missing values. This is useful when you need to ensure that missing keys return a default value without raising a `KeyError`.  
   **`defaultdict`**：一个调用工厂函数来提供缺失值的字典子类。当你需要确保缺失键返回默认值而不会引发`KeyError`时，这非常有用。

   ```python
   from collections import defaultdict

   # Create a defaultdict with a default value of 0
   dd = defaultdict(int)
   dd['apple'] += 1
   dd['banana'] += 1

   print(dd)  # Output: defaultdict(<class 'int'>, {'apple': 1, 'banana': 1})
   print(dd['orange'])  # Output: 0 (default value)
   ```

   **Explanation**:  
   **解释**：
   - `defaultdict` ensures that if you access a missing key, it automatically creates an entry with the default value specified by the factory function (e.g., `int` returns `0`).  
     `defaultdict`确保如果你访问一个缺失的键，它会自动创建一个带有工厂函数（如`int`返回`0`）指定的默认值的条目。

6. **`ChainMap`**: A class for managing multiple dictionaries as a single unit. This is useful when you want to search through multiple dictionaries for a key, checking each one in the order they were provided.  
   **`ChainMap`**：用于将多个字典作为单一单位管理的类。当你想要在多个字典中搜索一个键，按照它们提供的顺序检查每一个字典时，这非常有用。

   ```python
   from collections import ChainMap

   dict1 = {'a': 1, 'b': 2}
   dict2 = {'b': 3, 'c': 4}
   combined = ChainMap(dict1, dict2)

   print(combined['b'])  # Output: 2 (found in dict1)
   print(combined['c'])  # Output: 4 (found in dict2)
   ```

   **Explanation**:  
   **解释**：
   - `ChainMap` allows you to combine multiple dictionaries and search through them as if they were a single dictionary, respecting the order in which the dictionaries were combined.  
     `ChainMap`允许你组合多个字典，并像它们是单个字典一样搜索它们，遵循字典组合的顺序。

### Practical Uses of Container Datatypes in `collections` 模块中容器数据类型的实际应用

1. **Data Organization**: The `collections` module's container datatypes are particularly useful for organizing and managing complex data structures. For instance, `defaultdict` can be used to group items, `Counter` for tallying frequencies, and `OrderedDict` for maintaining ordered configurations.  
   **数据组织**：`collections`模块的容器数据类型特别适用于组织和管理复杂的数据结构。例如，`defaultdict`可以用于分组项目，`Counter`用于统计频率，`OrderedDict`用于维护有序的配置。

   ```python
   # Grouping items by their first letter using defaultdict
   from collections import defaultdict

   grouped = defaultdict(list)
   words = ['apple', 'banana', 'cherry', 'apricot', 'blueberry']
   for word in words:
       grouped[word[0]].append(word)

   print(grouped)  # Output: defaultdict(<class 'list'>, {'a': ['apple', 'apricot'], 'b': ['banana', 'blueberry'], 'c': ['cherry']})
   ```

2. **Simplifying Code**: Container datatypes in `collections` can help simplify your code by reducing the need for boilerplate code. For example, using `named

tuple` to replace simple classes reduces the amount of code needed to define data containers.  
   **简化代码**：`collections`中的容器数据类型可以帮助简化代码，减少模板代码的需求。例如，使用`namedtuple`来替换简单的类，减少了定义数据容器所需的代码量。

   ```python
   # Without namedtuple
   class Point:
       def __init__(self, x, y):
           self.x = x
           self.y = y

   # With namedtuple
   from collections import namedtuple
   Point = namedtuple('Point', ['x', 'y'])

   p1 = Point(10, 20)
   print(p1.x, p1.y)  # Output: 10 20
   ```

3. **Performance Optimization**: Some container datatypes, like `deque` and `Counter`, are optimized for specific tasks. For example, `deque` provides O(1) time complexity for appends and pops, making it more efficient than lists for queue and stack operations.  
   **性能优化**：某些容器数据类型，如`deque`和`Counter`，针对特定任务进行了优化。例如，`deque`提供了O(1)时间复杂度的追加和弹出操作，使其在队列和栈操作中比列表更高效。

   ```python
   from collections import deque

   d = deque()
   d.append(1)
   d.appendleft(0)
   print(d)  # Output: deque([0, 1])
   ```

### Conclusion 结论

The `collections` module in Python provides a versatile set of container datatypes that extend the capabilities of the built-in data structures. By using these specialized containers—such as `namedtuple`, `deque`, `Counter`, `OrderedDict`, `defaultdict`, and `ChainMap`—you can handle complex data manipulation tasks more efficiently and with greater clarity. These tools are especially useful for organizing data, simplifying code, and optimizing performance in your Python programs. Understanding how to leverage these container datatypes can greatly enhance your coding productivity and the performance of your applications.  
Python中的`collections`模块提供了一组多功能的容器数据类型，扩展了内置数据结构的功能。通过使用这些专门的容器——如`namedtuple`、`deque`、`Counter`、`OrderedDict`、`defaultdict`和`ChainMap`——你可以更高效地处理复杂的数据操作任务，并提高代码的清晰度。这些工具在数据组织、代码简化和性能优化方面尤其有用。了解如何利用这些容器数据类型可以大大提高你的编码效率和应用程序的性能。

------

## The `collections` Module in Python

The `collections` module in Python provides a rich set of specialized container datatypes that offer alternatives to the general-purpose built-in containers like `dict`, `list`, `set`, and `tuple`. These container datatypes are designed to handle specific types of data more efficiently or with added functionality. They can help simplify complex data manipulation tasks and improve the performance and readability of your code.

**Python 中的 `collections` 模块提供了一组丰富的专门容器数据类型，作为 `dict`、`list`、`set` 和 `tuple` 等通用内置容器的替代品。这些容器数据类型旨在更高效地处理特定类型的数据或提供附加功能。它们可以帮助简化复杂的数据操作任务，并提高代码的性能和可读性。**

### 1. **NamedTuple**

[English] A `namedtuple` is a factory function for creating tuple subclasses with named fields. This allows you to access elements by name instead of position, making your code more readable and self-documenting.

**Syntax:**
```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'gender'])
```

**Example:**
```python
Person = namedtuple('Person', ['name', 'age', 'gender'])
john = Person(name='John Doe', age=30, gender='Male')

print(john.name)  # Output: John Doe
print(john.age)   # Output: 30
```

**What Happens:** `namedtuple` creates a new data type `Person` with fields `name`, `age`, and `gender`. You can now create instances of `Person` and access fields by name.

**Behind the Scenes:** `namedtuple` enhances readability and reduces the chance of errors that can occur when accessing tuple elements by position, as the names clarify the purpose of each element.

**Chinese** `namedtuple` 是一个用于创建带有命名字段的元组子类的工厂函数。这使你可以通过名称而不是位置访问元素，从而使代码更具可读性和自文档化。

**语法:**
```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'gender'])
```

**示例:**
```python
Person = namedtuple('Person', ['name', 'age', 'gender'])
john = Person(name='John Doe', age=30, gender='Male')

print(john.name)  # 输出: John Doe
print(john.age)   # 输出: 30
```

**What Happens:** `namedtuple` 创建了一个新的数据类型 `Person`，具有 `name`、`age` 和 `gender` 字段。现在，你可以创建 `Person` 的实例并通过名称访问字段。

**Behind the Scenes:** `namedtuple` 提高了可读性，并减少了通过位置访问元组元素时可能发生的错误，因为名称明确了每个元素的用途。

### 2. **Deque**

[English] A `deque` (double-ended queue) is a list-like container with fast appends and pops on either end. It is ideal for implementing queues and stacks, and it provides a more efficient alternative to lists when you need to add or remove elements from both ends frequently.

**Syntax:**
```python
from collections import deque

d = deque([1, 2, 3])
```

**Example:**
```python
d = deque([1, 2, 3])
d.append(4)
d.appendleft(0)
print(d)  # Output: deque([0, 1, 2, 3, 4])

d.pop()
d.popleft()
print(d)  # Output: deque([1, 2, 3])
```

**What Happens:** The `deque` allows appending elements to both ends and removing elements from both ends efficiently.

**Behind the Scenes:** `deque` is implemented as a doubly linked list, which provides O(1) time complexity for append and pop operations at both ends, making it more suitable than a list for these tasks.

**Chinese** `deque`（双端队列）是一种类似列表的容器，具有在两端快速追加和弹出元素的功能。它非常适合实现队列和栈，并且当你需要频繁地从两端添加或删除元素时，它提供了比列表更高效的替代方案。

**语法:**
```python
from collections import deque

d = deque([1, 2, 3])
```

**示例:**
```python
d = deque([1, 2, 3])
d.append(4)
d.appendleft(0)
print(d)  # 输出: deque([0, 1, 2, 3, 4])

d.pop()
d.popleft()
print(d)  # 输出: deque([1, 2, 3])
```

**What Happens:** `deque` 允许高效地在两端追加元素和移除元素。

**Behind the Scenes:** `deque` 实现为双向链表，这为两端的 append 和 pop 操作提供了 O(1) 时间复杂度，使其比列表更适合这些任务。

### 3. **Counter**

[English] A `Counter` is a dictionary subclass designed for counting hashable objects. It is particularly useful for tallying elements in an iterable, counting frequencies in data, and more.

**Syntax:**
```python
from collections import Counter

counter = Counter(iterable)
```

**Example:**
```python
words = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
word_count = Counter(words)
print(word_count)  # Output: Counter({'apple': 3, 'banana': 2, 'orange': 1})
```

**What Happens:** The `Counter` counts the occurrences of each element in the list `words` and returns a dictionary-like object with the counts.

**Behind the Scenes:** `Counter` uses a dictionary to store the elements as keys and their counts as values, providing a simple and efficient way to perform frequency analysis.

**Chinese** `Counter` 是一个字典子类，用于对可哈希对象进行计数。它在对可迭代对象的元素进行统计、计算数据中的频率等方面特别有用。

**语法:**
```python
from collections import Counter

counter = Counter(iterable)
```

**示例:**
```python
words = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']
word_count = Counter(words)
print(word_count)  # 输出: Counter({'apple': 3, 'banana': 2, 'orange': 1})
```

**What Happens:** `Counter` 计算列表 `words` 中每个元素的出现次数，并返回一个类似字典的对象，其中包含计数。

**Behind the Scenes:** `Counter` 使用字典将元素存储为键，并将其计数存储为值，提供了一种简单有效的方式进行频率分析。

### 4. **OrderedDict**

[English] An `OrderedDict` is a dictionary subclass that remembers the order in which keys were inserted. This is particularly useful when the order of elements is important, such as when generating consistent outputs or when the order of items matters.

**Syntax:**
```python
from collections import OrderedDict

ordered_dict = OrderedDict()
```

**Example:**
```python
ordered_dict = OrderedDict()
ordered_dict['a'] = 1
ordered_dict['b'] = 2
ordered_dict['c'] = 3
print(ordered_dict)  # Output: OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```

**What Happens:** The `OrderedDict` keeps track of the order in which items are added and maintains this order when iterating over the dictionary.

**Behind the Scenes:** In Python 3.7 and later, the built-in `dict` maintains insertion order by default, but `OrderedDict` can still be useful in earlier versions or for explicitly stating that order is significant.

**Chinese** `OrderedDict` 是一个字典子类，它记住键插入的顺序。当元素的顺序很重要时，例如在生成一致的输出或当项目顺序重要时，它特别有用。

**语法:**
```python
from collections import OrderedDict

ordered_dict = OrderedDict()
```

**示例:**
```python
ordered_dict = OrderedDict()
ordered_dict['a'] = 1
ordered_dict['b'] = 2
ordered_dict['c'] = 3
print(ordered_dict)  # 输出: OrderedDict([('a', 1), ('b', 2), ('c', 3)])
```

**What Happens:** `OrderedDict` 记录项目添加的顺序，并在迭代字典时保持该顺序。

**Behind the Scenes:** 在 Python 3.7 及更高版本中，内置的 `dict` 默认保持插入顺序，但在早期版本中或当你明确表示顺序很重要时，`OrderedDict` 仍然有用。

### 5. **DefaultDict**

[English] A `defaultdict` is a dictionary subclass that automatically provides a default value for a nonexistent key. This eliminates the need to check whether a key exists before adding a value, simplifying your code.

**Syntax:**
```python
from collections import defaultdict

default_dict = defaultdict(default_factory)
```

**Example:**
```

python
default_dict = defaultdict(int)
default_dict['a'] += 1
default_dict['b'] += 2
print(default_dict)  # Output: defaultdict(<class 'int'>, {'a': 1, 'b': 2})
```

**What Happens:** The `defaultdict` automatically initializes missing keys with a default value (in this case, `int`, which defaults to 0).

**Behind the Scenes:** `defaultdict` provides a convenient way to handle dictionaries that require default values, reducing the need for conditional checks and simplifying your code logic.

**Chinese** `defaultdict` 是一个字典子类，它为不存在的键自动提供默认值。这消除了在添加值之前检查键是否存在的需要，简化了代码。

**语法:**
```python
from collections import defaultdict

default_dict = defaultdict(default_factory)
```

**示例:**
```python
default_dict = defaultdict(int)
default_dict['a'] += 1
default_dict['b'] += 2
print(default_dict)  # 输出: defaultdict(<class 'int'>, {'a': 1, 'b': 2})
```

**What Happens:** `defaultdict` 自动为缺失的键初始化一个默认值（在本例中为 `int`，默认值为 0）。

**Behind the Scenes:** `defaultdict` 提供了一种方便的方式来处理需要默认值的字典，减少了条件检查的需要，简化了代码逻辑。

### **When to Use `collections` Module Datatypes (何时使用 `collections` 模块的数据类型)**

[English] The specialized container datatypes in the `collections` module are particularly useful when you need more functionality or efficiency than the built-in containers can provide. They are ideal for scenarios where you need to:

- **Count elements efficiently** (use `Counter`).
- **Maintain element order** (use `OrderedDict`).
- **Manage queues and stacks** (use `deque`).
- **Provide default values for missing keys** (use `defaultdict`).
- **Improve readability and maintainability with named fields** (use `namedtuple`).

**Example:**
Using `Counter` to tally word frequencies in a text:

```python
from collections import Counter

text = "apple banana apple cherry cherry apple"
word_counts = Counter(text.split())
print(word_counts)  # Output: Counter({'apple': 3, 'cherry': 2, 'banana': 1})
```

**What Happens:** `Counter` tallies the occurrences of each word in the text, simplifying the task of frequency analysis.

**Behind the Scenes:** The `collections` module provides a suite of tools that extend the capabilities of standard containers, allowing you to write more efficient and expressive code.

**Chinese** 当你需要比内置容器提供更多功能或效率时，`collections` 模块中的专门容器数据类型特别有用。它们特别适合以下场景：

- **高效计数元素**（使用 `Counter`）。
- **维护元素顺序**（使用 `OrderedDict`）。
- **管理队列和栈**（使用 `deque`）。
- **为缺失的键提供默认值**（使用 `defaultdict`）。
- **通过命名字段提高可读性和可维护性**（使用 `namedtuple`）。

**示例:**
使用 `Counter` 统计文本中的单词频率:

```python
from collections import Counter

text = "apple banana apple cherry cherry apple"
word_counts = Counter(text.split())
print(word_counts)  # 输出: Counter({'apple': 3, 'cherry': 2, 'banana': 1})
```

**What Happens:** `Counter` 统计文本中每个单词的出现次数，简化了频率分析的任务。

**Behind the Scenes:** `collections` 模块提供了一套扩展标准容器功能的工具，使你能够编写更高效和更具表达性的代码。

In summary, the `collections` module offers powerful tools for data handling that go beyond the basic containers in Python. By leveraging these specialized datatypes, you can improve the efficiency, readability, and maintainability of your code in various scenarios.

