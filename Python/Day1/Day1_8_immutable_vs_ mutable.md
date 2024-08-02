# "immutable" and "mutable"

- In programming, "immutable" and "mutable" are terms used to describe whether the state of an object can be changed after it is created.

在编程中，“不可变”和“可变”是用来描述对象创建后其状态是否可以改变的术语。

### Immutable
**Immutable** objects cannot be altered once they are created. This means that any changes to an object result in the creation of a new object. Examples in Python include tuples, strings, and frozensets.

### 不可变
**不可变**对象一旦创建就不能被修改。这意味着对对象的任何改变都会导致创建一个新对象。Python中的例子包括元组、字符串和冻结集。

### Mutable
**Mutable** objects can be changed after they are created. This allows modifications to the object without creating a new one. Examples in Python include lists, dictionaries, and sets.

### 可变
**可变**对象创建后可以改变。这允许对对象进行修改而不创建新对象。Python中的例子包括列表、字典和集合。

Here's a Python code example to demonstrate the concept:

这里有一个Python代码示例来演示这个概念：

```python
# Immutable example with a tuple
immutable_tuple = (1, 2, 3)
try:
    immutable_tuple[0] = 4  # Attempting to change an immutable tuple
except TypeError as e:
    print("Error:", e)

# Mutable example with a list
mutable_list = [1, 2, 3]
mutable_list[0] = 4  # Changing the first element of the list
print("Updated List:", mutable_list)
```

Here's a comparison table summarizing the differences:

这是一个总结差异的比较表：

| Aspect | Immutable | Mutable |
|--------|-----------|---------|
| Changeability | Cannot be changed after creation | Can be changed after creation |
| Examples | Tuple, String, Frozenset | List, Dictionary, Set |
| Performance | Generally faster to access | Slower to access but flexible |
| Use Case | Use when you need a constant data value | Use when you need to change the data over time |

| 方面     | 不可变       | 可变         |
|--------|-----------|---------|
| 可改变性 | 创建后不能改变 | 创建后可以改变 |
| 例子     | 元组、字符串、冻结集 | 列表、字典、集合 |
| 性能     | 通常访问更快 | 访问较慢但灵活 |
| 使用情况  | 需要常量数据值时使用 | 需要随时间改变数据时使用 |


### 与 immutable 字符串不同, 列表是 mutable 类型，其内容可以改变

In Python, data types are categorized into immutable and mutable types based on whether they can be modified after their creation. Here's a detailed look at which types are immutable and which are mutable:

在Python中，数据类型根据创建后是否可以修改分为不可变类型和可变类型。以下是哪些类型是不可变的，哪些类型是可变的详细介绍：

### Immutable Types (不可变类型)
Immutable types include:
不可变类型包括：

- **Integers (整数)**: Once an integer is created, its value cannot be changed.
- **Floating-point numbers (浮点数)**: Similar to integers, the value of a floating-point number is fixed upon creation.
- **Strings (字符串)**: Strings cannot be altered once they are created. Any operation that modifies a string actually creates a new string.
- **Tuples (元组)**: Tuples are collections that are ordered and unchangeable.
- **Frozensets (冻结集)**: These are just like sets but immutable.

### Mutable Types (可变类型)
Mutable types include:
可变类型包括：

- **Lists (列表)**: Lists can be modified in many ways — elements can be added, removed, or changed.
- **Dictionaries (字典)**: The contents of a dictionary can be altered at any time — elements can be added, removed, or modified.
- **Sets (集合)**: Sets are collections that can be modified by adding or removing items.

Here's a Python code example showing the immutability of a tuple and the mutability of a list:

这里有一个Python代码示例，展示了元组的不可变性和列表的可变性：

```python
# Immutable tuple
immutable_tuple = (1, 2, 3)
try:
    immutable_tuple[0] = 'a'  # Trying to change an immutable tuple
except TypeError as e:
    print("Immutable type error:", e)

# Mutable list
mutable_list = [1, 2, 3]
mutable_list[0] = 'a'  # Changing element of the list
print("Mutable list changed:", mutable_list)
```

And here is a comparison table:

这是一个比较表：

| Type | Mutable | Example | Modification Example |
|------|---------|---------|----------------------|
| Integer | No | `x = 5` | N/A |
| Float | No | `x = 5.5` | N/A |
| String | No | `x = "hello"` | N/A |
| Tuple | No | `x = (1, 2, 3)` | N/A |
| Frozenset | No | `x = frozenset([1, 2, 3])` | N/A |
| List | Yes | `x = [1, 2, 3]` | `x[0] = 'a'` |
| Dictionary | Yes | `x = {'key': 'value'}` | `x['new_key'] = 'new_value'` |
| Set | Yes | `x = {1, 2, 3}` | `x.add(4)` |

| 类型     | 可变性 | 示例                  | 修改示例                       |
|------|------|---------------------|-------------------------------|
| 整数     | 否   | `x = 5`             | 不适用                         |
| 浮点数    | 否   | `x = 5.5`           | 不适用                         |
| 字符串    | 否   | `x = "hello"`       | 不适用                         |
| 元组     | 否   | `x = (1, 2, 3)`     | 不适用                         |
| 冻结集    | 否   | `x = frozenset([1, 2, 3])` | 不适用                 |
| 列表     | 是   | `x = [1, 2, 3]`     | `x[0] = 'a'`                  |
| 字典     | 是   | `x = {'key': 'value'}` | `x['new_key'] = 'new_value'` |
| 集合     | 是   | `x = {1, 2, 3}`     | `x.add(4)`                    |

That's correct! In Python, when you assign a list to a new variable, you're not actually creating a new independent copy of the list. Instead, the new variable refers to the same list. Changes made through any variable referencing this list will be visible through all variables referencing the same list.

没错！在Python中，当你将一个列表赋值给一个新变量时，你实际上并没有创建一个新的独立的列表副本。相反，新变量引用了相同的列表。通过引用这个列表的任何变量所做的更改都会通过所有引用同一个列表的变量看到。

Here's a Python code example to demonstrate this behavior:

这里有一个Python代码示例来演示这种行为：

```python
original_list = [1, 2, 3]
assigned_list = original_list  # Assigning the original list to a new variable

assigned_list[0] = 99  # Changing an element via the assigned variable

print("Original List:", original_list)  # Output will show the changed list
print("Assigned List:", assigned_list)  # Output will be the same as the original list
```

The output of this code will show that both `original_list` and `assigned_list` have been updated to `[99, 2, 3]`. This is because both variables refer to the same list object in memory.

这段代码的输出将显示`original_list`和`assigned_list`都被更新为`[99, 2, 3]`。这是因为两个变量都引用了内存中同一个列表对象。

In Python, when you assign a list to another variable, you're not creating a new list but instead creating a new reference to the original list. This means that any changes made to the new list will affect the original list as well, because they both refer to the same address in memory.

在Python中，当你将一个列表赋值给另一个变量时，你并没有创建一个新的列表，而是创建了一个指向原始列表的新引用。这意味着对新列表的任何更改也会影响原始列表，因为它们都指向内存中的同一个地址。

Here's an example to illustrate this:

下面是一个例子来说明这一点：

```python
list1 = [1, 2, 3]
list2 = list1
list2.append(4)

print("List1:", list1)
print("List2:", list2)
```

This code will output:

这段代码的输出将是：

```
List1: [1, 2, 3, 4]
List2: [1, 2, 3, 4]
```

As you can see, adding an element to `list2` also adds it to `list1`.

如你所见，向`list2`添加元素也会添加到`list1`。

The comparison of different list operations is shown in the table below:

不同列表操作的比较如下表所示：

| Operation | Description in English | Description in Chinese |
|-----------|------------------------|------------------------|
| Assignment | Creates a new reference to the same list. | 创建一个指向同一个列表的新引用。 |
| Copy (`list.copy()`) | Creates a shallow copy of the list, which is a new list with the same elements. | 创建列表的浅拷贝，这是一个具有相同元素的新列表。 |
| Deep copy (`copy.deepcopy()`) | Creates a deep copy of the list, which is a completely new list with copies of the original elements. | 创建列表的深拷贝，这是一个包含原始元素副本的完全新列表。 |

Understanding these differences is crucial when working with lists in Python to avoid unintended side effects.

理解这些差异在使用Python处理列表时至关重要，以避免意外的副作用。

#### Immutable and Mutable Objects in Python

In Python, objects are categorized as either **mutable** or **immutable**. Understanding the distinction between these two types of objects is crucial for efficient programming and can profoundly influence your decision when choosing which data type to use in solving a given programming problem.

**Immutable Objects:**
- Immutable objects do not allow their value or data to be changed in place without affecting the object's identity.
- When you modify an immutable object, a new object of the same type with different values is created.
- Examples of immutable objects in Python include strings, tuples, and numbers.

**Mutable Objects:**
- Mutable objects allow you to change their value or data in place without affecting the object's identity.
- They are easier to change but are slower to access and more expensive to change because it involves the creation of a copy.
- Examples of mutable objects in Python include lists, dictionaries, and sets.

#### Practical Implications
Understanding the concepts of mutability and immutability is crucial, especially when working with Python. By comprehending the concepts of mutability and immutability, developers can write more efficient, reliable, and bug-free code. The choice between mutable and immutable objects can profoundly influence your decision when choosing which data type to use in solving a given programming problem.

In summary, the distinction between mutable and immutable objects in Python is essential for crafting error-free code and can significantly impact your coding approach. It's important to use immutable objects for values that should not be modified and mutable objects for when you need to modify the object's state or contents.

---

### 1. **What is the difference between immutable and mutable objects in programming?**

**Answer:**
- **Immutable Objects**: Once created, the state of an immutable object cannot be changed. Any operation that seems to modify the object actually creates a new object. Examples in Python include integers, floats, strings, and tuples.

- **Mutable Objects**: The state of a mutable object can be changed after it is created. Operations like adding, removing, or modifying elements can affect the same object. Examples in Python include lists, dictionaries, and sets.

**中文回答:**
- **不可变对象**：一旦创建，不可变对象的状态无法改变。任何看似修改对象的操作实际上都会创建一个新对象。Python 中的示例包括整数、浮点数、字符串和元组。

- **可变对象**：可变对象的状态可以在创建后改变。像添加、删除或修改元素等操作可以影响同一个对象。Python 中的示例包括列表、字典和集合。

### 2. **Why might you choose an immutable type over a mutable type?**

**Answer:**
Choosing an immutable type over a mutable type can offer several benefits:
- **Predictability**: Immutable objects provide a guarantee that their state cannot be changed, which can make code easier to reason about and debug.
- **Hashability**: Immutable objects can be used as keys in dictionaries or elements in sets, as their hash values do not change.
- **Thread Safety**: Immutable objects are inherently thread-safe, as their state cannot be modified by different threads.

**中文回答:**
选择不可变类型而非可变类型可以带来几个好处：
- **可预测性**：不可变对象提供了其状态无法改变的保证，这可以使代码更易于理解和调试。
- **可哈希性**：不可变对象可以作为字典中的键或集合中的元素，因为它们的哈希值不会改变。
- **线程安全**：不可变对象本质上是线程安全的，因为它们的状态不能被不同线程修改。

### 3. **How does immutability affect performance in Python?**

**Answer:**
- **Memory Efficiency**: Immutable objects can be more memory-efficient because they can be shared across different parts of a program. For example, small integers and strings are often cached and reused.
- **Speed**: Operations on immutable objects can be faster in some cases because their state does not change, leading to fewer synchronization issues. However, operations that involve creating new immutable objects can involve additional overhead.

**中文回答:**
- **内存效率**：不可变对象可能具有更好的内存效率，因为它们可以在程序的不同部分之间共享。例如，小整数和字符串通常会被缓存和重用。
- **速度**：在某些情况下，对不可变对象的操作可能会更快，因为其状态不会改变，导致较少的同步问题。然而，涉及创建新不可变对象的操作可能会带来额外的开销。

### 4. **Can you modify an immutable object directly? What happens if you try?**

**Answer:**
You cannot modify an immutable object directly. Any attempt to alter the object will result in an error or create a new object. For example, trying to change a character in a string or an element in a tuple will raise a `TypeError`.

For example:
```python
s = "hello"
s[0] = "H"  # Raises TypeError: 'str' object does not support item assignment
```

**中文回答:**
你不能直接修改不可变对象。任何试图改变对象的操作都会导致错误或创建一个新对象。例如，尝试更改字符串中的字符或元组中的元素将引发 `TypeError`。

例如：
```python
s = "hello"
s[0] = "H"  # 引发 TypeError: 'str' object does not support item assignment
```

### 5. **How does the immutability of tuples compare to the mutability of lists in Python?**

**Answer:**
- **Tuples**: Tuples are immutable sequences. Once a tuple is created, its contents cannot be changed. However, if a tuple contains mutable objects (e.g., lists), those objects can still be modified.
  
- **Lists**: Lists are mutable sequences. Their contents can be changed after creation, including adding, removing, or modifying elements.

For example:
```python
t = (1, [2, 3])
t[1][0] = 4  # This is allowed because the list inside the tuple is mutable
# t[1] = [5, 6]  # This would raise a TypeError because the tuple is immutable
```

**中文回答:**
- **元组**：元组是不可变的序列。一旦创建了元组，其内容无法改变。然而，如果元组包含可变对象（例如列表），这些对象仍然可以被修改。
  
- **列表**：列表是可变的序列。它们的内容可以在创建后改变，包括添加、删除或修改元素。

例如：
```python
t = (1, [2, 3])
t[1][0] = 4  # 这是允许的，因为元组中的列表是可变的
# t[1] = [5, 6]  # 这将引发 TypeError，因为元组是不可变的
```

---

### Recommend Resources:
**Programming Terms: Mutable vs Immutable  by Corey Schafer**
[![Programming Terms: Mutable vs Immutable  by Corey Schafer](https://img.youtube.com/vi/5qQQ3yzbKp8/maxresdefault.jpg)](https://youtu.be/5qQQ3yzbKp8)


