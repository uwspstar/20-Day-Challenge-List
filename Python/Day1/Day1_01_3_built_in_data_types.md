# Built-in Data Types
In Python, there are several built-in data types that you'll frequently encounter. These data types are fundamental to handling various kinds of data in Python programs. Here's an overview in both English and Chinese, along with a comparison table:

### In summary, there are 15 built-in data types in Python:

1. int
2. float
3. complex
4. str
5. list
6. tuple
7. range
8. dict
9. set
10. frozenset
11. bool
12. bytes
13. bytearray
14. memoryview
15. NoneType


Python has several built-in data types that are used to handle various kinds of data. These data types can be broadly categorized as follows:

### Numeric Types
1. **int**: Integer type, represents whole numbers.
2. **float**: Floating-point type, represents real numbers with a decimal point.
3. **complex**: Complex number type, represents numbers with a real and imaginary part.

### Sequence Types
4. **str**: String type, represents text.
5. **list**: List type, a mutable sequence of items.
6. **tuple**: Tuple type, an immutable sequence of items.
7. **range**: Range type, represents a sequence of numbers.

### Mapping Type
8. **dict**: Dictionary type, represents a collection of key-value pairs.

### Set Types
9. **set**: Set type, an unordered collection of unique items.
10. **frozenset**: Frozenset type, an immutable version of a set.

### Boolean Type
11. **bool**: Boolean type, represents True or False values.

### Binary Types
12. **bytes**: Bytes type, represents binary data.
13. **bytearray**: Bytearray type, a mutable sequence of bytes.
14. **memoryview**: Memoryview type, provides a view of the memory of another binary object.

### None Type
15. **NoneType**: Represents the absence of a value or a null value. The sole instance of this type is `None`.



------

1. **Integers (`int`)** - Used for representing whole numbers without a fractional component.
   **整数（`int`）** - 用于表示没有小数部分的整数。
<details>
<summary>Integers vs (`int`)</summary>

In Python, there is no functional difference between using "Integers" and "int" because "int" is the actual data type used to represent integers in Python. The term "Integers" is more of a conceptual or descriptive term, whereas "int" is the actual type name used in Python code.

Here are a few points to clarify:

1. **Conceptual Term vs. Type Name**:
    - **Integers**: This term generally refers to the set of whole numbers, including positive, negative numbers, and zero. It is used to describe the concept of these numbers.
    - **int**: This is the actual built-in type in Python used to represent integer values.

2. **Usage in Python Code**:
    - You use `int` to create integer objects and to check for integer types.
    ```python
    a = 5  # a is an integer
    print(type(a))  # Output: <class 'int'>

    # Checking if a variable is an integer
    print(isinstance(a, int))  # Output: True
    ```

3. **Type Annotation**:
    - When you annotate types in Python (e.g., for function parameters and return values), you use `int`.
    ```python
    def add(x: int, y: int) -> int:
        return x + y
    ```

4. **Documentation and Descriptions**:
    - In documentation or explanations, you might see the term "integer" used to describe values of type `int`.

In summary, "Integers" is a conceptual term, while `int` is the actual type you use in Python code to work with integer values.

</details>


3. **Floating-point numbers (`float`)** - Used for representing real numbers, typically those with a fractional component.
   **浮点数（`float`）** - 用于表示实数，通常是带有小数部分的数。

4. **Strings (`str`)** - Used for representing sequences of characters, text data.
   **字符串（`str`）** - 用于表示字符序列，文本数据。

5. **Booleans (`bool`)** - Used to represent two values: True and False.
   **布尔值（`bool`）** - 用来表示两个值：True 和 False。

6. **Lists (`list`)** - Used to store collections of items (elements can be of different data types).
   **列表（`list`）** - 用来存储项目的集合（元素可以是不同的数据类型）。

7. **Tuples (`tuple`)** - Similar to lists but immutable (cannot be changed after creation).
   **元组（`tuple`）** - 类似于列表，但是不可变（创建后不能更改）。

8. **Dictionaries (`dict`)** - Used to store key-value pairs.
   **字典（`dict`）** - 用于存储键值对。

9. **Sets (`set`)** - Used to store unique items; they automatically remove duplicates.
   **集合（`set`）** - 用来存储唯一的项目；它们自动删除重复项。

### Comparison Table

| Data Type   | Description in English                                  | Description in Chinese                               |
|-------------|---------------------------------------------------------|-----------------------------------------------------|
| `int`       | Whole numbers without fractional parts.                 | 没有小数部分的整数。                                  |
| `float`     | Numbers with fractional parts.                          | 带有小数部分的数。                                   |
| `str`       | Sequence of characters, used for text.                  | 字符序列，用于文本。                                 |
| `bool`      | True or False values.                                   | True 或 False 值。                                   |
| `list`      | Collection of items, mutable.                           | 项目的集合，可变。                                   |
| `tuple`     | Collection of items, immutable.                         | 项目的集合，不可变。                                 |
| `dict`      | Collection of key-value pairs.                          | 键值对的集合。                                       |
| `set`       | Collection of unique items, removes duplicates.         | 独特项目的集合，删除重复项。                         |

### Behind the Scenes Explanation

When you use these data types in Python, the interpreter handles the memory allocation and management for you. For instance:
- **Integers and floats** are typically stored in a fixed amount of memory, depending on their size.
- **Strings and lists** are more dynamic; Python allocates more memory as needed when you add elements or characters.
- **Dictionaries and sets** use hash tables behind the scenes, which allow for fast access to elements by using keys.

当您在 Python 中使用这些数据类型时，解释器会为您处理内存分配和管理。例如：
- **整数和浮点数** 通常存储在固定数量的内存中，具体取决于它们的大小。
- **字符串和列表** 更为动态；当您添加元素或字符时，Python 将根据需要分配更多内存。
- **字典和集合** 在幕后使用哈希表，这允许通过使用键快速访问元素。

These data types are essential for writing efficient Python code and are used in virtually every Python program. Understanding how and when to use them effectively can significantly impact the performance and scalability of your applications.

这些数据类型对于编写高效的 Python 代码至关重要，并且几乎在每个 Python 程序中都有使用。理解如何以及何时有效使用它们可以显著影响您的应用程序的性能和可扩展性。

Here's a comparison table that specifically outlines whether each of the common Python data types is mutable or immutable. This distinction is crucial for understanding how data types behave when they are modified in your code.

### Mutability Table

| Data Type   | Mutable / Immutable | Description in English                                       | Description in Chinese                                    |
|-------------|---------------------|--------------------------------------------------------------|-----------------------------------------------------------|
| `int`       | Immutable           | Cannot be changed after creation.                            | 创建后不能更改。                                            |
| `float`     | Immutable           | Cannot be changed after creation.                            | 创建后不能更改。                                            |
| `str`       | Immutable           | Cannot be changed after creation; a new string must be created. | 创建后不能更改；必须创建一个新字符串。                          |
| `bool`      | Immutable           | Cannot be changed after creation.                            | 创建后不能更改。                                            |
| `list`      | Mutable             | Can be changed after creation; items can be added or removed.  | 创建后可以更改；可以添加或删除项目。                          |
| `tuple`     | Immutable           | Cannot be changed after creation.                            | 创建后不能更改。                                            |
| `dict`      | Mutable             | Can be changed after creation; key-value pairs can be added or removed. | 创建后可以更改；可以添加或删除键值对。                          |
| `set`       | Mutable             | Can be changed after creation; elements can be added or removed, automatically handles duplicates. | 创建后可以更改；元素可以添加或删除，自动处理重复项。               |

### Behind the Scenes Explanation

- **Immutable types** like integers, floats, strings, tuples, and booleans are fixed once they are created. Any operations that seem to modify these data types actually create a new object and reassign the reference to this new object. For example, when you add two strings in Python, a new string is created, and the variable points to this new string.
  
  **不可变类型**，如整数、浮点数、字符串、元组和布尔值，一旦创建就固定了。任何看似修改这些数据类型的操作实际上都会创建一个新对象，并将引用重新分配给这个新对象。例如，在 Python 中添加两个字符串时，会创建一个新字符串，变量将指向这个新字符串。

- **Mutable types** like lists, dictionaries, and sets can be modified after their creation. This means you can add, remove, or change items directly in these objects without creating a new object each time. This mutability makes them very flexible, but it also means you need to be cautious when copying or passing them between functions to avoid unintended side effects.

  **可变类型**，如列表、字典和集合，可以在创建后修改。这意味着您可以在不每次都创建新对象的情况下直接添加、删除或更改这些对象中的项目。这种可变性使它们非常灵活，但也意味着在复制或在函数之间传递时需要小心，以避免意外的副作用。

Understanding the mutability of different data types helps in managing memory more efficiently and can influence how you structure data and algorithms in your programs.

了解不同数据类型的可变性有助于更有效地管理内存，并且可以影响您在程序中如何构建数据和算法。

In Python, there are several built-in data types that you'll frequently encounter. These data types are fundamental to handling various kinds of data in Python programs.

### None Type
- **NoneType**: Represents the NULL values in Python.
  - **NoneType**: 在 Python 中代表 NULL 值。

### Numeric Types
- **int**: Stores integer literals including hex, octal, and binary numbers as integers.
  - **int**: 存储整数，包括十六进制、八进制和二进制数。
- **float**: Stores literals containing decimal values and/or exponent signs as floating-point numbers.
  - **float**: 存储包含小数值和/或指数符号的浮点数。
- **complex**: Stores complex numbers in the form (A + Bj) and has attributes: real and imag.
  - **complex**: 存储复数形式 (A + Bj)，具有 real 和 imag 属性。
- **bool**: Stores boolean value (True or False).
  - **bool**: 存储布尔值（True 或 False）。

### Sequence Types
- **list**: Mutable sequence used to store a collection of items.
  - **list**: 可变序列，用于存储项目集合。
- **tuple**: Immutable sequence used to store a collection of items.
  - **tuple**: 不可变序列，用于存储项目集合。
- **range**: Represents an immutable sequence of numbers generated during execution.
  - **range**: 表示执行期间生成的不可变数字序列。
- **str**: Immutable sequence of Unicode code points to store textual data.
  - **str**: 不可变的 Unicode 码点序列，用于存储文本数据。

### Mapping Types
- **dict**: Stores a comma-separated list of key-value pairs.
  - **dict**: 存储键值对的逗号分隔列表。

### Set Types
- **set**: Mutable unordered collection of distinct hashable objects.
  - **set**: 可变的无序集合，包含不同的可哈希对象。
- **frozenset**: Immutable collection of distinct hashable objects.
  - **frozenset**: 不可变的独特可哈希对象集合。

### Modules
- Modules are containers for Python code, which can define functions, classes, and variables. Modules allow you to organize related code into a manageable and reusable manner.
  - 模块是 Python 代码的容器，可以定义函数、类和变量。模块允许您以可管理和可重用的方式组织相关代码。

### Callable Types
- Callable types include user-defined functions, instance methods, generator functions, and some other built-in functions and methods.
  - 可调用类型包括用户定义的函数、实例方法、生成器函数和一些其他内置函数和方法。

These data types are essential for writing efficient Python code and are used in virtually every Python program. Understanding how and when to use them effectively can significantly impact the performance and scalability of your applications.

这些数据类型对于编写高效的 Python 代码至关重要，并且几乎在每个 Python 程序中都有使用。理解如何以及何时有效使用它们可以显著影响您的应用程序的性能和可扩展性。
