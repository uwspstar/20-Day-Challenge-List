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
