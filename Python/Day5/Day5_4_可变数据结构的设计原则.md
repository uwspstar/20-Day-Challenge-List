# 可变数据结构的设计原则
In Python, methods that modify lists like `insert`, `remove`, or `sort` do not return any value; they return the default value `None`. This is a design principle for all mutable data structures in Python. 

在 Python 中，像 `insert`、`remove` 或 `sort` 这样修改列表的方法不会返回任何值；它们返回默认值 `None`。这是 Python 中所有可变数据结构的设计原则。

### Explanation | 解释

#### English
This behavior follows a common programming pattern called "Command-Query Separation" (CQS). According to this principle, methods that change the state of an object (commands) should return nothing (i.e., `None`) to signal that their primary operation is to perform a modification. This helps in preventing side effects during method chaining or unexpected behaviors in more complex data manipulations.

#### 中文
这种行为遵循一种常见的编程模式，称为“命令-查询分离”(CQS)。根据这一原则，改变对象状态的方法（命令）应该不返回任何东西（即 `None`），以表明它们的主要操作是进行修改。这有助于在方法链中防止副作用或在更复杂的数据操作中防止意外行为。

### Practical Examples | 实用示例

#### English
When you use the `sort()` method on a list, it rearranges the elements of the list in place and returns `None`. This indicates that the primary purpose of the method is to modify the list, not to produce a new value.

#### 中文
当你在列表上使用 `sort()` 方法时，它会就地重新排列列表的元素，并返回 `None`。这表明该方法的主要目的是修改列表，而不是产生一个新值。

```python
my_list = [3, 1, 2]
result = my_list.sort()
print(result)  # Outputs: None
print(my_list)  # Outputs: [1, 2, 3]
```

#### English
Similarly, the `remove()` method deletes an item from the list and returns `None`. This makes it clear that the function's role is to alter the list's content.

#### 中文
同样，`remove()` 方法从列表中删除一个项目并返回 `None`。这明确表明了函数的作用是更改列表的内容。

```python
my_list = ['a', 'b', 'c']
my_list.remove('b')
print(my_list)  # Outputs: ['a', 'c']
```

### Conclusion | 结论

Understanding that methods which modify Python's mutable data structures return `None` helps programmers avoid misusing return values and emphasizes the intent of these methods as operations that alter the state of the object rather than functions that compute and return new data values.

理解修改 Python 可变数据结构的方法返回 `None` 可以帮助程序员避免误用返回值，并强调这些方法的意图是改变对象状态的操作，而不是计算并返回新数据值的函数。

------

## Methods That Modify Lists in Python

In Python, methods that modify lists like `insert`, `remove`, or `sort` do not return any value; they return the default value `None`. This is a design principle for all mutable data structures in Python.

**在 Python 中，像 `insert`、`remove` 或 `sort` 这样修改列表的方法不会返回任何值；它们返回默认值 `None`。这是 Python 中所有可变数据结构的设计原则。**

### 1. **The Design Principle Behind Mutable Methods (可变方法背后的设计原则)**

[English] In Python, the design principle for mutable data structures like lists is that methods that modify the object in place do not return the object itself. Instead, they return `None`. This helps to prevent confusion and errors in code by making it clear that the object is being modified directly, rather than creating a new object.

**Example:**
```python
my_list = [3, 1, 2]
my_list.sort()
print(my_list)  # Output: [1, 2, 3]

result = my_list.sort()
print(result)  # Output: None
```

**What Happens:** The `sort()` method sorts the list in place and returns `None`, which reinforces that the operation modifies the original list rather than returning a new sorted list.

**Behind the Scenes:** By returning `None`, Python encourages developers to recognize that the object itself has changed. This design choice reduces the likelihood of mistakenly thinking that a new list is returned, which could lead to unexpected behavior or bugs.

**Chinese** 在 Python 中，像列表这样的可变数据结构的设计原则是，修改对象的方法不会返回对象本身，而是返回 `None`。这有助于避免代码中的混淆和错误，因为它明确表明对象是直接被修改的，而不是创建了一个新的对象。

**示例:**
```python
my_list = [3, 1, 2]
my_list.sort()
print(my_list)  # 输出: [1, 2, 3]

result = my_list.sort()
print(result)  # 输出: None
```

**What Happens:** `sort()` 方法对列表进行原地排序并返回 `None`，这强化了操作修改的是原始列表而不是返回新的排序列表的概念。

**Behind the Scenes:** 通过返回 `None`，Python 鼓励开发人员意识到对象本身已经改变。这种设计选择减少了错误地认为返回了新列表的可能性，这可能导致意外行为或错误。

### 2. **Examples of Common Mutable Methods (常见可变方法的示例)**

[English] Several methods in Python's list class are designed to modify the list in place and return `None`. These include `append`, `extend`, `insert`, `remove`, `pop`, `clear`, and `sort`. Understanding how these methods work can help you write more effective Python code.

**Examples:**
- **`append()`** adds an item to the end of the list:
    ```python
    my_list = [1, 2, 3]
    result = my_list.append(4)
    print(my_list)  # Output: [1, 2, 3, 4]
    print(result)  # Output: None
    ```
- **`remove()`** removes the first occurrence of a value:
    ```python
    my_list = [1, 2, 3, 2]
    result = my_list.remove(2)
    print(my_list)  # Output: [1, 3, 2]
    print(result)  # Output: None
    ```
- **`sort()`** sorts the list in ascending order:
    ```python
    my_list = [3, 1, 2]
    result = my_list.sort()
    print(my_list)  # Output: [1, 2, 3]
    print(result)  # Output: None
    ```

**What Happens:** In each of these cases, the list is modified in place, and the method returns `None`, reinforcing the idea that the list itself is being altered.

**Behind the Scenes:** The decision to return `None` helps prevent accidental chaining of methods that modify the list, which could lead to misunderstandings about the state of the list after the operation.

**Chinese** Python 列表类中的一些方法设计为原地修改列表并返回 `None`。这些方法包括 `append`、`extend`、`insert`、`remove`、`pop`、`clear` 和 `sort`。理解这些方法的工作原理可以帮助你编写更有效的 Python 代码。

**示例:**
- **`append()`** 将一个项目添加到列表末尾：
    ```python
    my_list = [1, 2, 3]
    result = my_list.append(4)
    print(my_list)  # 输出: [1, 2, 3, 4]
    print(result)  # 输出: None
    ```
- **`remove()`** 删除值的第一次出现：
    ```python
    my_list = [1, 2, 3, 2]
    result = my_list.remove(2)
    print(my_list)  # 输出: [1, 3, 2]
    print(result)  # 输出: None
    ```
- **`sort()`** 按升序排序列表：
    ```python
    my_list = [3, 1, 2]
    result = my_list.sort()
    print(my_list)  # 输出: [1, 2, 3]
    print(result)  # 输出: None
    ```

**What Happens:** 在每种情况下，列表都会原地修改，方法返回 `None`，强化了列表本身被更改的概念。

**Behind the Scenes:** 决定返回 `None` 有助于防止意外地链接修改列表的方法，这可能会导致对操作后列表状态的误解。

### 3. **Comparison with Immutable Methods (与不可变方法的比较)**

[English] In contrast to methods that modify the list in place, immutable methods create a new object and return it. For example, string methods like `replace` or `upper` return a new string without modifying the original string. This distinction is important for understanding how Python handles mutable and immutable objects.

**Example:**
```python
original_string = "hello"
new_string = original_string.replace("h", "j")
print(original_string)  # Output: hello
print(new_string)  # Output: jello
```

**What Happens:** The `replace()` method returns a new string, leaving the original string unchanged.

**Behind the Scenes:** Python’s handling of immutable objects like strings emphasizes that operations on these objects do not modify the original data but rather produce new data, in contrast to mutable objects like lists.

**Chinese** 与原地修改列表的方法相比，不可变方法创建一个新对象并返回它。例如，像 `replace` 或 `upper` 这样的字符串方法返回一个新字符串，而不修改原始字符串。理解这一区别对于理解 Python 如何处理可变和不可变对象非常重要。

**示例:**
```python
original_string = "hello"
new_string = original_string.replace("h", "j")
print(original_string)  # 输出: hello
print(new_string)  # 输出: jello
```

**What Happens:** `replace()` 方法返回一个新字符串，原始字符串保持不变。

**Behind the Scenes:** Python 对不可变对象（如字符串）的处理强调了这些对象上的操作不会修改原始数据，而是生成新数据，这与可变对象（如列表）形成对比。

### 4. **Best Practices for Using Mutable Methods (使用可变方法的最佳实践)**

[English] Understanding that methods like `insert`, `remove`, and `sort` return `None` is crucial for avoiding common pitfalls in Python programming. Here are some best practices:

- **Avoid Chaining Mutating Methods:** Since these methods return `None`, chaining them can lead to `NoneType` errors.
    ```python
    my_list = [3, 1, 2]
    # Incorrect: my_list.sort().reverse()  # This raises an AttributeError
    my_list.sort()
    my_list.reverse()  # Correct
    ```
- **Use the Return Value Appropriately:** Remember that if you assign the result of a mutating method to a variable, that variable will be `None`.
    ```python
    my_list = [1, 2, 3]
    result = my_list.append(4)
    print(result)  # Output: None
    ```

**What Happens:** These practices ensure that you correctly handle the behavior of mutable methods, preventing bugs related to unexpected `None` values.

**Behind the Scenes:** By adhering to these practices, you can write clearer and more reliable Python code, avoiding common errors associated with mutable objects.

**Chinese** 理解像 `insert`、`remove` 和 `sort` 这样的方法返回 `None` 对于避免 Python 编程中的常见陷阱至关重要。以下是一些最佳实践：

- **避免链接变异方法：** 由于这些方法返回 `None`，链接它们可能会导致 `NoneType` 错误。
    ```python
    my_list = [3, 1, 2]
    # 不正确: my_list.sort().reverse()  # 这会引发 AttributeError
    my_list.sort()
    my_list.reverse()  # 正确
    ```
- **适当地使用返回值：** 请

记住，如果将变异方法的结果分配给变量，该变量将为 `None`。
    ```python
    my_list = [1, 2, 3]
    result = my_list.append(4)
    print(result)  # 输出: None
    ```

**What Happens:** 这些实践确保你正确处理可变方法的行为，防止与意外的 `None` 值相关的错误。

**Behind the Scenes:** 通过遵循这些实践，你可以编写更清晰和更可靠的 Python 代码，避免与可变对象相关的常见错误。

### **Summary (总结)**

[English] Methods that modify lists in Python, such as `insert`, `remove`, and `sort`, return `None` by design. This design choice ensures that the operations are understood as modifying the list in place rather than returning a new list. Understanding this principle helps prevent common mistakes in Python programming and encourages better practices when working with mutable data structures.

**Chinese** Python 中修改列表的方法，如 `insert`、`remove` 和 `sort`，按照设计返回 `None`。这种设计选择确保这些操作被理解为在原地修改列表，而不是返回一个新列表。理解这一原则有助于防止 Python 编程中的常见错误，并鼓励在处理可变数据结构时采用更好的实践。

