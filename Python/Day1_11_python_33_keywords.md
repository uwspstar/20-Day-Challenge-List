# Python 3.8 的 33 个 Python 关键字的表格
Python keywords are reserved words that cannot be used as identifiers (like variable names, function names, class names, etc.) because they are used to define the syntax and structure of the Python language. Here’s a table of the 33 Python keywords as of Python 3.8, along with a brief explanation and example for each. This table and the explanations will be presented in both English and Chinese.

Python 关键字是不能用作标识符（如变量名、函数名、类名等）的保留字，因为它们用于定义 Python 语言的语法和结构。以下是截至 Python 3.8 的 33 个 Python 关键字的表格，每个关键字都附有简短的解释和示例。这个表格和解释将以英文和中文呈现。

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

These keywords are fundamental to programming in Python and

 are used to define the flow and operation of code. Each keyword has a specific purpose:

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
