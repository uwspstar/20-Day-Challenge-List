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

