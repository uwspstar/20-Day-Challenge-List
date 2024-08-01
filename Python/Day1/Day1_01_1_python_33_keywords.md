# Python 3.8 的 35 个 Python 关键字的表格
Python keywords are reserved words that cannot be used as identifiers (like variable names, function names, class names, etc.) because they are used to define the syntax and structure of the Python language. Here’s a table of the 33 Python keywords as of Python 3.8, along with a brief explanation and example for each. This table and the explanations will be presented in both English and Chinese.

```python
import keyword

print(keyword.kwlist)  # Output: List of Python keywords ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

print(len(keyword.kwlist))  # Output: List of Python keywords 35

```

Python 关键字是不能用作标识符（如变量名、函数名、类名等）的保留字，因为它们用于定义 Python 语言的语法和结构。以下是截至 Python 3.8 的 35 个 Python 关键字的表格，每个关键字都附有简短的解释和示例。这个表格和解释将以英文和中文呈现。

### Python Keywords Table | Python 关键字表

| Keyword    | Description | Example |
|------------|-------------|---------|
| `False`    | Represents the boolean value false. | `is_valid = False` |
| `None`     | Represents the absence of a value. | `result = None` |
| `True`     | Represents the boolean value true. | `is_valid = True` |
| `and`      | A logical operator for conjunction. | `if a and b:` |
| `as`       | Used in aliasing modules or with `with` as a context manager. | `import math as m` |
| `assert`   | For debugging, to test if a condition is true. | `assert x > 0` |
| `async`    | Used to define asynchronous functions. | `async def fetch():` |
| `await`    | Used to wait for a result within an asynchronous function. | `data = await fetch()` |
| `break`    | Breaks out of the current loop. | `while True: break` |
| `class`    | Used to define a new user-defined class. | `class Dog:` |
| `continue` | Continues to the next iteration of the loop. | `for i in range(5): continue` |
| `def`      | Used to define a function. | `def my_function():` |
| `del`      | Used to delete an object. | `del my_var` |
| `elif`     | Else if condition in an if statement. | `if x > 10: elif x == 10:` |
| `else`     | Else part of an if statement. | `if x > 10: else:` |
| `except`   | Used in exception handling. | `try: except ValueError:` |
| `finally`  | Always executed in the end, used with try. | `try: finally:` |
| `for`      | Used for looping generally over a sequence. | `for i in range(5):` |
| `from`     | Used to import specific parts of a module. | `from math import pi` |
| `global`   | Declares a global variable. | `global x` |
| `if`       | Used for conditional execution. | `if x > 10:` |
| `import`   | Used to import a module. | `import os` |
| `in`       | Checks if a value is in a sequence. | `if 'a' in list:` |
| `is`       | Tests object identity. | `if a is None:` |
| `lambda`   | Creates an anonymous function. | `multiply = lambda x, y: x * y` |
| `nonlocal` | Declares a non-local variable. | `def outer(): nonlocal x` |
| `not`      | A logical negation. | `if not x:` |
| `or`       | A logical operator for disjunction. | `if a or b:` |
| `pass`     | A null operation or placeholder. | `def function(): pass` |
| `raise`    | Used to raise an exception. | `raise ValueError("error")` |
| `return`   | Returns a value from a function. | `def sum(a, b): return a + b` |
| `try`      | Begins a block for exception handling. | `try: x = int('foo')` |
| `while`    | Used for looping while a condition is true. | `while x < 10:` |
| `with`     | Used to wrap the execution of a block with methods. | `with open('file.txt') as f:` |
| `yield`    | Used to return from a generator. | `def count(): yield i` |

### Explanation and Use | 解释和使用

These keywords are fundamental to programming in Python and are used to define the flow and operation of code. Each keyword has a specific purpose:

这些关键字是 Python 编程的基础，用于定义代码的流程和操作。每个关键字都有特定的用途：

- **Control Flow Keywords**: `if`, `elif`, `else`, `for`, `while` help in branching and looping.
- **Function/Class Definition Keywords**: `def`, `class`, `lambda` are used to define functions, classes, and anonymous functions.
- **Exception Handling Keywords**: `try`, `except`, `finally`, `raise` manage exceptions.
- **Other Utilities**: `with`, `as`, `pass`, `yield` provide various utilities for context management, null operations, and generator functions.

- **控制流关键字**：`if`、`elif`、`else`、`for`、`while` 用于分支和循环。
- **函数/类定义关键字**：`def`、`class`、`lambda` 用于定义函数、类和匿名函数。
- **异常处理关键字**：`try`、`except`、`finally`、`raise` 管理异常。
- **其他实用工具**：`with`、`as`、`pass`、`yield` 提供上下文管理、空操作和生成器函数的各种实用工具。

Understanding and using these keywords correctly is crucial for effective Python programming and can significantly impact the readability, maintainability, and functionality of your code.

### Python 3.9 keywords
| **Keyword**   | **Definition**                                                                                                                                       | **Code Example**                                                                                                                                                 | **Tips**                                                                                                                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `False`       | Boolean value indicating false.                                                                                                                       | `is_student = False`                                                                                                                                             | Use in conditional statements to represent a false state.                                                                                                                             |
| `None`        | Represents the absence of a value or a null value.                                                                                                    | `result = None`                                                                                                                                                  | Commonly used to initialize variables or indicate no result.                                                                                                                          |
| `True`        | Boolean value indicating true.                                                                                                                        | `is_student = True`                                                                                                                                              | Use in conditional statements to represent a true state.                                                                                                                              |
| `and`         | Logical AND operator.                                                                                                                                | `if is_student and is_enrolled:`                                                                                                                                 | Used to combine multiple conditions in a single `if` statement.                                                                                                                       |
| `as`          | Used to create an alias.                                                                                                                             | `import numpy as np`                                                                                                                                             | Commonly used with imports to give a module a different name.                                                                                                                         |
| `assert`      | Used for debugging purposes, to test if a condition in your code returns True, if not, the program will raise an AssertionError.                      | `assert x > 0, "x should be greater than 0"`                                                                                                                     | Useful for checking conditions and throwing errors when conditions are not met.                                                                                                       |
| `async`       | Declares an asynchronous function or coroutine.                                                                                                      | `async def fetch_data():`                                                                                                                                        | Use with `await` to handle asynchronous operations.                                                                                                                                  |
| `await`       | Pauses the execution of async function until the awaited coroutine completes.                                                                        | `await fetch_data()`                                                                                                                                             | Only used within `async` functions.                                                                                                                                                   |
| `break`       | Terminates the nearest enclosing loop.                                                                                                               | `for i in range(10): if i == 5: break`                                                                                                                           | Use to exit loops early based on a condition.                                                                                                                                         |
| `class`       | Used to define a new user-defined class.                                                                                                             | `class MyClass:`                                                                                                                                                | Classes are blueprints for creating objects.                                                                                                                                          |
| `continue`    | Skips the rest of the code inside the current loop iteration and goes to the next iteration.                                                         | `for i in range(10): if i % 2 == 0: continue`                                                                                                                    | Useful for skipping certain iterations in a loop.                                                                                                                                     |
| `def`         | Used to define a new function.                                                                                                                       | `def my_function():`                                                                                                                                             | Functions encapsulate reusable code.                                                                                                                                                   |
| `del`         | Used to delete objects.                                                                                                                              | `del my_list[0]`                                                                                                                                                 | Can be used to delete variables, list items, or object attributes.                                                                                                                     |
| `elif`        | Used in conditional statements, same as else if.                                                                                                     | `if x > 0: pass elif x < 0: pass`                                                                                                                                | Use to add multiple conditions in an `if` statement.                                                                                                                                  |
| `else`        | Used in conditional statements.                                                                                                                      | `if x > 0: pass else: pass`                                                                                                                                      | Executes a block of code if all preceding conditions are false.                                                                                                                        |
| `except`      | Used with exceptions, what to do when an exception occurs.                                                                                           | `try: pass except ValueError: pass`                                                                                                                              | Catches and handles exceptions raised in the `try` block.                                                                                                                              |
| `finally`     | Used with exceptions, a block of code that will be executed no matter if there is an exception or not.                                               | `try: pass except: pass finally: pass`                                                                                                                           | Ensures execution of cleanup code regardless of exceptions.                                                                                                                            |
| `for`         | Used to create a for loop.                                                                                                                           | `for i in range(10): pass`                                                                                                                                       | Iterates over sequences like lists, tuples, or strings.                                                                                                                                |
| `from`        | Used to import specific parts of a module.                                                                                                           | `from math import sqrt`                                                                                                                                          | Use to import only the required functions or classes.                                                                                                                                  |
| `global`      | Used to declare a global variable inside a function.                                                                                                 | `global x`                                                                                                                                                       | Allows modification of a global variable inside a function.                                                                                                                            |
| `if`          | Used to make a conditional statement.                                                                                                                | `if x > 0: pass`                                                                                                                                                 | Executes a block of code if the condition is true.                                                                                                                                     |
| `import`      | Used to import a module.                                                                                                                             | `import math`                                                                                                                                                    | Allows access to functions, classes, and variables defined in a module.                                                                                                                |
| `in`          | Used to check if a value is present in a sequence (lists, tuples, strings, etc.).                                                                    | `if x in my_list:`                                                                                                                                               | Checks for membership in sequences.                                                                                                                                                    |
| `is`          | Tests for object identity.                                                                                                                           | `if x is None:`                                                                                                                                                  | Use to check if two variables refer to the same object.                                                                                                                                |
| `lambda`      | Used to create an anonymous function.                                                                                                                | `f = lambda x: x + 1`                                                                                                                                            | Useful for short, throwaway functions.                                                                                                                                                |
| `nonlocal`    | Used to declare a non-local variable.                                                                                                                | `nonlocal x`                                                                                                                                                     | Used in nested functions to modify a variable defined in an enclosing scope.                                                                                                          |
| `not`         | Logical NOT operator.                                                                                                                                | `if not x:`                                                                                                                                                      | Negates a boolean value.                                                                                                                                                              |
| `or`          | Logical OR operator.                                                                                                                                 | `if x or y:`                                                                                                                                                     | Used to combine multiple conditions in an `if` statement.                                                                                                                             |
| `pass`        | Null statement, a statement that will do nothing.                                                                                                    | `if x > 0: pass`                                                                                                                                                 | Useful as a placeholder for future code.                                                                                                                                               |
| `raise`       | Used to raise an exception.                                                                                                                          | `raise ValueError("error message")`                                                                                                                              | Allows manual raising of exceptions.                                                                                                                                                   |
| `return`      | Exits a function and returns a value.                                                                                                                | `def func(): return x`                                                                                                                                           | Ends function execution and optionally returns a value.                                                                                                                                |
| `try`         | Used to catch exceptions.                                                                                                                            | `try: pass except: pass`                                                                                                                                        | Wraps code that may throw exceptions.                                                                                                                                                  |
| `while`       | Used to create a while loop.                                                                                                                         | `while x > 0: pass`                                                                                                                                              | Repeatedly executes a block of code as long as the condition is true.                                                                                                                  |
| `with`        | Used to simplify exception handling.                                                                                                                 | `with open('file.txt') as f:`                                                                                                                                    | Ensures proper acquisition and release of resources.                                                                                                                                  |
| `yield`       | Ends the execution of a function, returns a generator.                                                                                               | `def generator(): yield x`                                                                                                                                       | Used in functions to return an iterator instead of a single value.                                                                                                                     |


#### 以下是关于 Python 关键字的 3 个面试问题及其答案

### 1. What are Python keywords? 什么是Python关键字？

Python keywords are reserved words that cannot be used as identifiers (like variable names, function names, class names, etc.) because they are used to define the syntax and structure of the Python language.

```python
import keyword
print(keyword.kwlist)  # Output: List of Python keywords
```

Python 关键字是不能用作标识符（如变量名、函数名、类名等）的保留字，因为它们用于定义 Python 语言的语法和结构。

```python
import keyword
print(keyword.kwlist)  # 输出: Python 关键字列表
```

### 2. Why can't Python keywords be used as identifiers? 为什么Python关键字不能用作标识符？

Python keywords are reserved for specific functions within the language and using them as identifiers would cause syntax errors and ambiguity in the code.

```python
def = 5  # SyntaxError: invalid syntax
```

Python 关键字是保留用于语言中的特定功能的，使用它们作为标识符会导致语法错误和代码中的歧义。

```python
def = 5  # 语法错误: 语法无效
```

### 3. How can you get a list of all Python keywords programmatically? 如何以编程方式获取所有Python关键字的列表？

You can use the `keyword` module in Python to get a list of all keywords.

```python
import keyword
print(keyword.kwlist)  # Output: List of Python keywords
```

可以使用Python中的`keyword`模块获取所有关键字的列表。

```python
import keyword
print(keyword.kwlist)  # 输出: Python 关键字列表
```



### Recommend Resources:
**All 39 Python Keywords Explained Indently**
[![All 39 Python Keywords Explained](https://img.youtube.com/vi/rKk8XPLysj8/maxresdefault.jpg)](https://youtu.be/rKk8XPLysj8)




