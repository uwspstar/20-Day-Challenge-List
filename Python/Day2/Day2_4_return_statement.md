# `return` statement

The `return` statement in Python is a fundamental part of defining the behavior of functions. It determines the value that a function hands back to its caller. Understanding the different ways `return` can be used is crucial for effective Python programming.

### Key Points About the `return` Statement

1. **Returning a Value**: When a `return` statement includes an expression, the function will exit immediately, and the expression's value will be returned to the caller.
   
   **返回值**：当 `return` 语句包含一个表达式时，函数将立即退出，并将表达式的值返回给调用者。

2. **Implicit Return of None**: If a `return` statement is used without an expression, or if no `return` statement is used at all, the function returns `None` by default when it completes.

   **隐式返回 None**：如果使用了不带表达式的 `return` 语句，或者根本没有使用 `return` 语句，函数在完成时默认返回 `None`。

3. **Immediate Function Exit**: A `return` statement terminates the function execution immediately, which means any code following the `return` statement within the same function block will not be executed.

   **立即退出函数**：`return` 语句立即终止函数执行，这意味着在同一函数块内跟随 `return` 语句的任何代码都不会被执行。

### Examples

Here are some examples that illustrate these points:

#### Example 1: Returning a Specific Value

```python
def calculate_sum(a, b):
    return a + b

result = calculate_sum(5, 3)
print(result)  # Outputs: 8
```

**解释**:
- The function `calculate_sum` takes two parameters, calculates their sum, and returns the result. The `return` statement includes the expression `a + b`.

#### Example 2: Implicit Return of None

```python
def print_message(message):
    print(message)

result = print_message("Hello, world!")
print(result)  # Outputs: None
```

**解释**:
- The function `print_message` prints a message but does not explicitly return a value. Thus, it returns `None`, which is printed.

#### Example 3: Immediate Exit from a Function

```python
def check_number(num):
    if num == 0:
        return "Zero"
    return "Not zero"

print(check_number(0))  # Outputs: Zero
print(check_number(5))  # Outputs: Not zero
```

**解释**:
- The function `check_number` checks if the number is zero. If so, it immediately returns "Zero" and exits. Otherwise, it proceeds to return "Not zero".

### Explanation | 解释

Using `return` effectively allows you to control the flow of your program by managing how and when values are returned from functions. This makes your functions versatile in their interactions with the rest of your code, supporting both actions (like printing) and calculations that need to pass back data.

Understanding when to use `return`, and when it's appropriate to allow a function to return `None`, can help in designing clear and efficient functions in Python.

------

#### 1. What is the purpose of the `return` statement in Python?
[English]
The `return` statement is used to exit a function and pass a value back to the caller. It can be used to return any Python object, such as numbers, strings, lists, tuples, dictionaries, and even other functions or objects.

```python
def add(a, b):
    return a + b

result = add(3, 4)
print(result)  # Output: 7
```

[Chinese]
`return` 语句用于退出函数并将一个值传递回调用者。它可以用于返回任何 Python 对象，例如数字、字符串、列表、元组、字典，甚至其他函数或对象。

```python
def add(a, b):
    return a + b

result = add(3, 4)
print(result)  # 输出: 7
```

#### 2. How do you use the `return` statement to return multiple values?
[English]
In Python, you can return multiple values from a function by returning a tuple. This allows the caller to unpack the values into separate variables.

```python
def get_coordinates():
    return 10, 20

x, y = get_coordinates()
print(f"x: {x}, y: {y}")
```

[Chinese]
在 Python 中，可以通过返回元组从函数返回多个值。这允许调用者将这些值解包到单独的变量中。

```python
def get_coordinates():
    return 10, 20

x, y = get_coordinates()
print(f"x: {x}, y: {y}")
```

#### 3. What happens if you use `return` without a value?
[English]
If you use the `return` statement without a value, or omit the `return` statement entirely, the function returns `None` by default. This is useful when a function performs an action but does not need to return a value.

```python
def greet(name):
    print(f"Hello, {name}")

result = greet("Alice")
print(result)  # Output: None
```

[Chinese]
如果使用不带值的 `return` 语句，或者完全省略 `return` 语句，函数将默认返回 `None`。这在函数执行操作但不需要返回值时非常有用。

```python
def greet(name):
    print(f"Hello, {name}")

result = greet("Alice")
print(result)  # 输出: None
```

#### How do you use the `return` statement to exit a function early?
[English]
You can use the `return` statement to exit a function early based on a condition. This is useful for stopping the function execution when a specific condition is met.

```python
def find_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            return num
    return None

result = find_even([1, 3, 5, 7, 8, 10])
print(result)  # Output: 8
```

[Chinese]
可以使用 `return` 语句根据条件提前退出函数。这在满足特定条件时停止函数执行非常有用。

```python
def find_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            return num
    return None

result = find_even([1, 3, 5, 7, 8, 10])
print(result)  # 输出: 8
```

#### 4. How do you use `return` with recursion?
[English]
In recursive functions, the `return` statement is used to pass the result of a recursive call back to the previous level. This allows the function to build up the final result through multiple recursive calls.

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

result = factorial(5)
print(result)  # Output: 120
```

[Chinese]
在递归函数中，`return` 语句用于将递归调用的结果传递回上一层。这允许函数通过多次递归调用构建最终结果。

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

result = factorial(5)
print(result)  # 输出: 120
```

#### Practical Applications
[English]
1. **Conditional Returns**: Use `return` to exit a function when specific conditions are met.
2. **Multiple Returns**: Return multiple values using tuples for cleaner and more informative function outputs.
3. **Recursive Functions**: Utilize `return` to correctly propagate results in recursive algorithms.

[Chinese]
1. **条件返回**：在满足特定条件时使用 `return` 退出函数。
2. **多重返回**：使用元组返回多个值，以获得更清晰和信息更丰富的函数输出。
3. **递归函数**：利用 `return` 正确传播递归算法中的结果。

#### Tips and Tricks
[English]
- Use `return` to simplify complex conditional logic by exiting the function early.
- Remember that returning multiple values as a tuple can simplify function interfaces.
- Ensure that recursive functions have a clear base case and use `return` to handle it appropriately.

[Chinese]
- 使用 `return` 通过提前退出函数简化复杂的条件逻辑。
- 记住以元组形式返回多个值可以简化函数接口。
- 确保递归函数具有明确的基准情况，并使用 `return` 适当地处理它。

I hope this explanation helps in understanding the `return` statement in Python!
