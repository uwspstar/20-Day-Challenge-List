# exception handling

In Python, the `try...except` block is used for exception handling, allowing you to catch and respond to errors or exceptions that occur during the execution of your program. This mechanism helps to make the program more robust and prevents it from crashing unexpectedly.

### Basic Structure

The basic structure of a `try...except` block is as follows:

```python
try:
    # Code that might cause an exception
    risky_operation()
except SomeException as e:
    # Code that runs if an exception occurs
    print("An error occurred:", e)
```

1. **`try` Block**: You put the code that might cause an exception inside the `try` block.
   
   **`try` 块**：你将可能引发异常的代码放在 `try` 块中。

2. **`except` Block**: Code inside the `except` block runs if an exception of the matching type is thrown in the `try` block.
   
   **`except` 块**：如果 `try` 块中抛出匹配类型的异常，则 `except` 块中的代码将运行。

### Common Python Exceptions

Here is a list of some common exceptions in Python along with their typical causes:

| Exception              | Description (EN)                                      | Description (CN)                              |
|------------------------|-------------------------------------------------------|-----------------------------------------------|
| `Exception`            | Base class for all built-in exceptions                | 所有内置异常的基类                            |
| `AttributeError`       | Raised when an attribute reference or assignment fails| 当属性引用或赋值失败时引发                     |
| `IOError`              | Raised when an I/O operation fails                    | 当 I/O 操作失败时引发                         |
| `ImportError`          | Raised when an import statement fails                 | 当导入语句失败时引发                          |
| `IndexError`           | Raised when a sequence subscript is out of range      | 当序列下标超出范围时引发                      |
| `KeyError`             | Raised when a dictionary key is not found             | 当字典键找不到时引发                          |
| `KeyboardInterrupt`    | Raised when the user hits the interrupt key (Ctrl+C)  | 当用户按下中断键（Ctrl+C）时引发              |
| `NameError`            | Raised when a local or global name is not found       | 当找不到本地或全局名称时引发                  |
| `SyntaxError`          | Raised when there is an error in Python syntax        | 当 Python 语法错误时引发                      |
| `TypeError`            | Raised when an operation or function is applied to an object of inappropriate type | 当操作或函数应用于不适当类型的对象时引发      |
| `ValueError`           | Raised when a function gets an argument of correct type but improper value | 当函数获得正确类型但不当值的参数时引发        |
| `ZeroDivisionError`    | Raised when the second argument of a division or modulo operation is zero | 当除法或模运算的第二个参数为零时引发          |

### Example with Code

Here's a practical example demonstrating the use of `try...except`:

```python
try:
    # This will raise a ZeroDivisionError
    result = 10 / 0
except ZeroDivisionError as e:
    print("Caught an error:", e)
```

### Explanation | 解释

- The code attempts to divide 10 by zero, which raises a `ZeroDivisionError`.
  
  代码试图将10除以零，这会引发 `ZeroDivisionError`。

- The `except` block catches the error and prints a message.

  `except` 块捕获错误并打印消息。

Using `try...except` blocks appropriately can help in handling errors gracefully and maintaining a smooth user experience in your applications.

------

#### 1. How do you use a `try...except` block in Python?
[English]
A `try...except` block allows you to catch exceptions that occur in the `try` block and handle them in the `except` block. This prevents the program from terminating unexpectedly when an error occurs.

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You cannot divide by zero")
```

**What Happens:**
An attempt to divide by zero raises a `ZeroDivisionError`, which is caught by the `except` block, and the program prints a custom error message.

**Behind the Scenes:**
The `try` block executes the code that may raise an exception. If an exception occurs, the flow of control immediately jumps to the `except` block that matches the exception type.

[Chinese]
`try...except` 块允许你捕获 `try` 块中发生的异常并在 `except` 块中处理它们。这防止了程序在发生错误时意外终止。

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You cannot divide by zero")
```

**What Happens:**
尝试除以零会引发 `ZeroDivisionError`，`except` 块捕获此错误，并打印自定义错误消息。

**Behind the Scenes:**
`try` 块执行可能引发异常的代码。如果发生异常，控制流会立即跳转到匹配异常类型的 `except` 块。

#### 2. How do you catch multiple exceptions?
[English]
You can catch multiple exceptions by specifying multiple `except` blocks or by using a single `except` block with a tuple of exception types.

```python
try:
    value = int("abc")
except (ValueError, TypeError):
    print("Invalid input")
```

**What Happens:**
An attempt to convert a non-numeric string to an integer raises a `ValueError`, which is caught by the `except` block, and the program prints "Invalid input".

**Behind the Scenes:**
The `except` block checks if the raised exception matches any of the specified types in the tuple. If a match is found, the corresponding code block is executed.

[Chinese]
你可以通过指定多个 `except` 块或使用包含异常类型元组的单个 `except` 块来捕获多个异常。

```python
try:
    value = int("abc")
except (ValueError, TypeError):
    print("Invalid input")
```

**What Happens:**
尝试将非数字字符串转换为整数会引发 `ValueError`，`except` 块捕获此错误，程序打印 "Invalid input"。

**Behind the Scenes:**
`except` 块检查引发的异常是否与元组中的任何指定类型匹配。如果找到匹配，则执行相应的代码块。

#### 3. What is the purpose of the `finally` block?
[English]
The `finally` block is used to specify cleanup actions that must be executed under all circumstances, whether an exception is raised or not. It ensures that important code runs regardless of whether an exception occurs.

```python
try:
    file = open('example.txt', 'r')
    data = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    file.close()
    print("File closed")
```

**What Happens:**
If the file is not found, a `FileNotFoundError` is caught, and the error message is printed. Regardless of the outcome, the `finally` block ensures the file is closed.

**Behind the Scenes:**
The `finally` block executes after the `try` and `except` blocks, ensuring that cleanup code runs no matter what, making it ideal for resource management tasks like closing files or releasing locks.

[Chinese]
`finally` 块用于指定在任何情况下都必须执行的清理操作，无论是否引发异常。它确保重要代码无论是否发生异常都会运行。

```python
try:
    file = open('example.txt', 'r')
    data = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    file.close()
    print("File closed")
```

**What Happens:**
如果未找到文件，则会捕获 `FileNotFoundError` 并打印错误消息。无论结果如何，`finally` 块都确保文件关闭。

**Behind the Scenes:**
`finally` 块在 `try` 和 `except` 块之后执行，确保无论发生什么情况，清理代码都会运行，这使其成为资源管理任务（如关闭文件或释放锁）的理想选择。

#### 4. How do you use the `else` block in exception handling?
[English]
The `else` block can be used to specify code that should run only if no exceptions were raised in the `try` block. It helps in distinguishing between code that should run in the normal case and code that handles exceptions.

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("You cannot divide by zero")
else:
    print("Division successful, result is:", result)
```

**What Happens:**
Since no exception is raised, the `else` block executes and prints the result of the division.

**Behind the Scenes:**
The `else` block executes only if the `try` block completes without raising any exceptions. It provides a place to put code that should only run if no exceptions occur.

[Chinese]
`else` 块可用于指定只有在 `try` 块中未引发任何异常时才应运行的代码。它有助于区分应在正常情况下运行的代码和处理异常的代码。

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("You cannot divide by zero")
else:
    print("Division successful, result is:", result)
```

**What Happens:**
由于没有引发异常，`else` 块执行并打印除法结果。

**Behind the Scenes:**
`else` 块仅在 `try` 块完成且未引发任何异常时执行。它提供了一个仅在未发生任何异常时才应运行的代码位置。

#### 5. How do you raise exceptions manually in Python?
[English]
You can raise exceptions manually in Python using the `raise` statement. This is useful when you need to trigger an exception under specific conditions in your code.

```python
def check_positive(number):
    if number < 0:
        raise ValueError("Number must be positive")
    return number

try:
    print(check_positive(-5))
except ValueError as e:
    print(e)
```

**What Happens:**
The `check_positive` function raises a `ValueError` if the input number is negative. The `except` block catches this exception and prints the error message.

**Behind the Scenes:**
The `raise` statement creates a new exception object and raises it. The flow of control is transferred to the nearest matching `except` block.

[Chinese]
可以使用 `raise` 语句在 Python 中手动引发异常。当你需要在代码中特定条件下触发异常时，这很有用。

```python
def check_positive(number):
    if number < 0:
        raise ValueError("Number must be positive")
    return number

try:
    print(check_positive(-5))
except ValueError as e:
    print(e)
```

**What Happens:**
如果输入的数字为负，`check_positive` 函数会引发 `ValueError`。`except` 块捕获此异常并打印错误消息。

**Behind the Scenes:**
`raise` 语句创建一个新的异常对象并引发它。控制流转移到最近的匹配 `except` 块。
