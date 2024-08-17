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
