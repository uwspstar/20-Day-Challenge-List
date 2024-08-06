# 函数参数的传递
在 Python 中，函数参数的传递行为有时会导致混淆，尤其是关于“按值传递”和“按引用传递”的术语。Python 的参数传递实际上是“按共享传递”（pass-by-sharing），这意味着函数接收的参数是实际数据（或对象）的引用，而不是它们的副本。这种方式有时被非正式地称为“按对象引用传递”。

### 关键概念

1. **实际参数的传递**: 当函数被调用时，实际使用的参数（或称为实参）会被传入到函数的局部符号表中。这些参数是对象的引用，而不是对象本身的副本。

2. **局部符号表**: 每当一个函数被调用时，Python 会为该函数创建一个新的局部符号表。这个符号表包含函数内的变量名和它们对应的值（实际上是引用）。

3. **按共享传递的含义**: 这意味着如果你在函数内修改了作为参数传入的可变对象（如列表或字典），那么这些修改会反映到调用者的环境中。但如果尝试重新绑定一个参数（例如，将一个整数参数设置为一个新的值），这将仅仅改变局部符号表中的引用，而不会影响外部的对象。

### 示例

下面的例子将帮助阐明这些概念：

#### 示例 1：修改可变对象

```python
def modify_list(lst):
    lst.append(3)  # 修改传入的列表

my_list = [1, 2]
modify_list(my_list)
print(my_list)  # 输出: [1, 2, 3]
```

**解释**:
- `modify_list` 函数接收一个列表，并向其中添加一个元素。因为列表是可变的，所以传入的是引用，列表的修改在函数外也可见。

#### 示例 2：尝试修改不可变对象

```python
def modify_number(x):
    x = 10  # 尝试修改传入的数字

num = 5
modify_number(num)
print(num)  # 输出: 5
```

**解释**:
- 尽管函数内部的 `x` 被重新赋值为 10，这种修改只影响函数的局部符号表中的 `x`。外部的 `num` 仍然是 5，因为整数是不可变的，并且重新赋值创建了一个新的局部引用，而不是修改原始对象。

### 解释 | 解释

Python 中的函数参数传递通常是按引用传递的，但这种引用是对象引用的副本。这意味着对可变对象的修改在函数外部是可见的，但直接对参数变量重新赋值（即更改引用）不会影响原始外部变量。理解这一点对于编写有效和预期的行为一致的 Python 代码至关重要。
在 Python 中使用可变对象作为函数参数的默认值时，确实需要小心。这个行为通常会导致初学者和经验丰富的开发者都感到困惑。函数的默认值是在函数定义时计算一次并且只计算一次。这意味着如果默认值是可变的（如列表、字典等），并且你在函数执行时修改了这个对象，那么这个修改将在函数的后续调用中保持有效。

### 示例详解

在你提供的例子中，函数 `f` 使用了一个列表作为默认参数。当列表在函数调用中被修改时（通过 `append` 方法），这个修改影响的是同一个列表对象，因此每次调用该函数时，都会看到之前调用的累积效果：

```python
def f(a, L=[]):
    L.append(a)
    return L

print(f(1))  # 输出: [1]
print(f(2))  # 输出: [1, 2]
print(f(3))  # 输出: [1, 2, 3]
```

### 为什么会这样？

这种行为的根本原因在于 `L=[]` 只在函数定义时执行一次，这样 `L` 就被创建了一次，并且在每次函数调用时都不会重新初始化。所有的 `append` 操作都在同一个列表对象上执行。

### 推荐的解决方法

为了避免这种由默认可变参数引起的潜在问题，建议使用 `None` 作为默认参数，并在函数体内检查它：

```python
def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L

print(f(1))  # 输出: [1]
print(f(2))  # 输出: [2]  (预期是 [2], 且这里确实是 [2])
print(f(3))  # 输出: [3]  (预期是 [3], 且这里确实是 [3])
```

在这种修改后的版本中，每次调用 `f` 时，如果未提供 `L`，将创建一个新的空列表。这样，每次函数调用都是独立的，避免了意外共享数据的问题。

### 总结 | 解释

使用默认可变参数时应格外小心，因为它们可能导致难以发现的错误和不一致的行为。通过使用 `None` 作为默认值并在函数内部初始化可变对象，可以保持函数的纯净性和预测性，这是编写清晰、可维护代码的重要方面。

The difference between the two function definitions you've provided hinges on how Python handles mutable default arguments like lists. Let's explore each function and understand the implications of using one over the other:

### Function with `L=None`

```python
def f(a, L=None):
    if L is None:
        L = []
    L.append(a)
    return L
```

**Key Characteristics**:
- **Immutable Default**: The default value of `L` is `None`, which is immutable.
- **Initialization Inside Function**: Each time the function is called without a specific `L` provided, a new list `L` is created inside the function. This ensures that `L` is always a new list for each function call unless a list is explicitly passed.
- **No Side Effects**: Since a new list is created each time the function is invoked with `L` as `None`, subsequent calls to the function do not affect the outcome of previous calls. Each call is independent.

**Usage Example**:
```python
print(f(1))  # Outputs: [1]
print(f(2))  # Outputs: [2]
print(f(3))  # Outputs: [3]
```
Each call to `f` returns a new list containing only the provided element `a`, as `L` is initialized to a new list each time.

### Function with `L=[]`

```python
def f(a, L=[]):
    L.append(a)
    return L
```

**Key Characteristics**:
- **Mutable Default**: The default value of `L` is a mutable list (`[]`).
- **Single Initialization**: The list `L` is created only once when the function is defined, not each time it is called. Therefore, this same list is used in every call where `L` is not explicitly provided.
- **Side Effects**: Because the same list `L` is used for every default call to `f`, the list retains elements added in previous calls, leading to potentially unintended accumulation of data across function calls.

**Usage Example**:
```python
print(f(1))  # Outputs: [1]
print(f(2))  # Outputs: [1, 2]
print(f(3))  # Outputs: [1, 2, 3]
```
Each call to `f` without a specific list provided appends to the same default list, accumulating results across calls.

### Summary of Differences

| Feature                         | `L=None`                        | `L=[]`                            |
|---------------------------------|---------------------------------|-----------------------------------|
| Default Argument Type           | Immutable (`None`)              | Mutable (list `[]`)               |
| Behavior on Subsequent Calls    | Independent (no side effects)   | Cumulative (shared state)         |
| Safety in Concurrent/Reusable Code | Safer (avoids shared state bugs) | Risky (prone to bugs from shared state) |

### Conclusion

The use of `L=None` with the conditional initialization inside the function (`if L is None: L = []`) is a common Python idiom to avoid the pitfalls associated with mutable default arguments. This pattern prevents unexpected behavior due to shared state across function calls and is especially important in larger and more complex software systems where such side effects can lead to bugs that are difficult to trace and fix.

------

### 函数参数的传递
在 Python 中，函数参数的传递行为有时会导致混淆，尤其是关于“按值传递”和“按引用传递”的术语。Python 的参数传递实际上是“按共享传递”（pass-by-sharing），这意味着函数接收的参数是实际数据（或对象）的引用，而不是它们的副本。这种方式有时被非正式地称为“按对象引用传递”。

#### 1. What does "pass-by-sharing" mean in Python?
[English]
"Pass-by-sharing" means that when you pass an argument to a function, the function receives a reference to the same object, not a copy. Therefore, changes to mutable objects within the function can affect the original object outside the function.

```python
def modify_list(lst):
    lst.append(4)

my_list = [1, 2, 3]
modify_list(my_list)
print(my_list)  # Output: [1, 2, 3, 4]
```

**What Happens:**
The `modify_list` function appends `4` to `lst`, which is a reference to `my_list`. The change is reflected in `my_list` outside the function.

**Behind the Scenes:**
When `my_list` is passed to `modify_list`, both `my_list` and `lst` refer to the same list object in memory. The `append` operation modifies this shared object.

[Chinese]
“按共享传递”意味着当你将一个参数传递给函数时，函数接收到的是同一个对象的引用，而不是它的副本。因此，对可变对象的更改会影响到函数外的原始对象。

```python
def modify_list(lst):
    lst.append(4)

my_list = [1, 2, 3]
modify_list(my_list)
print(my_list)  # 输出: [1, 2, 3, 4]
```

**What Happens:**
`modify_list` 函数将 `4` 添加到 `lst`，即 `my_list` 的引用。更改反映在函数外的 `my_list` 中。

**Behind the Scenes:**
当 `my_list` 被传递给 `modify_list` 时，`my_list` 和 `lst` 都指向内存中的同一个列表对象。`append` 操作修改了这个共享对象。

#### 2. How does "pass-by-sharing" differ for mutable and immutable objects?
[English]
For mutable objects (like lists and dictionaries), changes within the function affect the original object. For immutable objects (like integers, strings, and tuples), changes within the function do not affect the original object because a new object is created.

```python
def modify_number(num):
    num += 10

my_number = 5
modify_number(my_number)
print(my_number)  # Output: 5
```

**What Happens:**
The `modify_number` function attempts to change `num`, but this does not affect `my_number` because integers are immutable.

**Behind the Scenes:**
When `my_number` is passed to `modify_number`, `num` is a reference to the same integer object. However, `num += 10` creates a new integer object and assigns it to `num`, leaving `my_number` unchanged.

[Chinese]
对于可变对象（如列表和字典），函数内的更改会影响原始对象。对于不可变对象（如整数、字符串和元组），函数内的更改不会影响原始对象，因为会创建一个新对象。

```python
def modify_number(num):
    num += 10

my_number = 5
modify_number(my_number)
print(my_number)  # 输出: 5
```

**What Happens:**
`modify_number` 函数尝试更改 `num`，但这不会影响 `my_number`，因为整数是不可变的。

**Behind the Scenes:**
当 `my_number` 被传递给 `modify_number` 时，`num` 是指向同一个整数对象的引用。然而，`num += 10` 创建了一个新的整数对象并将其分配给 `num`，而 `my_number` 保持不变。

#### 3. How can you avoid unintended side effects when passing mutable objects to a function?
[English]
To avoid unintended side effects, you can create a copy of the mutable object within the function. This way, modifications within the function do not affect the original object.

```python
def modify_list_safe(lst):
    lst_copy = lst.copy()
    lst_copy.append(4)
    return lst_copy

my_list = [1, 2, 3]
new_list = modify_list_safe(my_list)
print(my_list)  # Output: [1, 2, 3]
print(new_list)  # Output: [1, 2, 3, 4]
```

**What Happens:**
The `modify_list_safe` function creates a copy of `lst` and modifies the copy, leaving `my_list` unchanged.

**Behind the Scenes:**
The `lst.copy()` method creates a shallow copy of the list. The modifications are made to this new list object, which is then returned.

[Chinese]
为了避免意外的副作用，可以在函数内创建可变对象的副本。这样，函数内的修改不会影响原始对象。

```python
def modify_list_safe(lst):
    lst_copy = lst.copy()
    lst_copy.append(4)
    return lst_copy

my_list = [1, 2, 3]
new_list = modify_list_safe(my_list)
print(my_list)  # 输出: [1, 2, 3]
print(new_list)  # 输出: [1, 2, 3, 4]
```

**What Happens:**
`modify_list_safe` 函数创建 `lst` 的副本并修改该副本，使 `my_list` 保持不变。

**Behind the Scenes:**
`lst.copy()` 方法创建列表的浅拷贝。修改是在这个新列表对象上进行的，然后返回该对象。

#### 4. Can you illustrate "pass-by-sharing" with a custom class?
[English]
When you pass an instance of a custom class to a function, it behaves like any other mutable object. Changes to its attributes within the function will affect the original instance.

```python
class MyClass:
    def __init__(self, value):
        self.value = value

def modify_object(obj):
    obj.value += 10

my_obj = MyClass(5)
modify_object(my_obj)
print(my_obj.value)  # Output: 15
```

**What Happens:**
The `modify_object` function modifies the `value` attribute of `obj`, which is a reference to `my_obj`. The change is reflected in `my_obj` outside the function.

**Behind the Scenes:**
When `my_obj` is passed to `modify_object`, both `my_obj` and `obj` refer to the same instance of `MyClass`. Modifying `obj.value` directly changes the attribute of the shared object.

[Chinese]
当你将自定义类的实例传递给函数时，它的行为类似于其他可变对象。对其属性的更改将在函数内影响原始实例。

```python
class MyClass:
    def __init__(self, value):
        self.value = value

def modify_object(obj):
    obj.value += 10

my_obj = MyClass(5)
modify_object(my_obj)
print(my_obj.value)  # 输出: 15
```

**What Happens:**
`modify_object` 函数修改 `obj` 的 `value` 属性，即 `my_obj` 的引用。更改反映在函数外的 `my_obj` 中。

**Behind the Scenes:**
当 `my_obj` 被传递给 `modify_object` 时，`my_obj` 和 `obj` 都指向 `MyClass` 的同一个实例。修改 `obj.value` 直接更改了共享对象的属性。

#### 5. How does "pass-by-sharing" affect the use of default mutable arguments?
[English]
Using mutable objects as default arguments can lead to unexpected behavior because the default value is shared across all calls to the function. It's better to use `None` and create a new object inside the function.

```python
def add_to_list(value, lst=None):
    if lst is None:
        lst = []
    lst.append(value)
    return lst

list1 = add_to_list(1)
list2 = add_to_list(2)

print(list1)  # Output: [1]
print(list2)  # Output: [2]
```

**What Happens:**
The `add_to_list` function initializes `lst` to an empty list if no list is provided. This ensures each call to the function gets a new list.

**Behind the Scenes:**
Using `None` as a default value ensures that a new list is created each time the function is called, avoiding unintended sharing of the list between function calls.

[Chinese]
使用可变对象作为默认参数可能会导致意外行为，因为默认值在所有函数调用中共享。最好使用 `None` 并在函数内部创建新对象。

```python
def add_to_list(value, lst=None):
    if lst is None:
        lst = []
    lst.append(value)
    return lst

list1 = add_to_list(1)
list2 = add_to_list(2)

print(list1)  # 输出: [1]
print(list2)  # 输出: [2]
```

**What Happens:**
`add_to_list` 函数

在没有提供列表时将 `lst` 初始化为空列表。这确保每次调用函数时都获得一个新列表。

**Behind the Scenes:**
使用 `None` 作为默认值可确保每次调用函数时都会创建一个新列表，避免在函数调用之间意外共享列表。
