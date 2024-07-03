# Decorators
Decorators in Python are a very powerful and useful tool that allow you to modify the behavior of a function or class. They are often used to extend or modify the behavior of functions and methods without permanently modifying them.

Python 中的装饰器是一种非常强大且有用的工具，允许你修改函数或类的行为。它们通常用于扩展或修改函数和方法的行为，而无需永久修改它们。

### Example Code 示例代码

Here's a simple example of a decorator that adds a simple logging before and after the execution of a function:

下面是一个装饰器的简单示例，该装饰器在函数执行前后添加了简单的日志记录：

```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

### Comparison Table 比较表

| Feature 特征                  | Without Decorator 无装饰器 | With Decorator 使用装饰器  |
| -------------------------- | ---------------------- | --------------------- |
| Code Reusability 代码重用性     | Low 低                     | High 高                 |
| Complexity 复杂性            | Low 低                     | Moderate 中等           |
| Functionality 功能性         | Basic 基本                 | Enhanced 增强            |

### Explanation 解释

Decorators allow you to inject or modify code before and after a function runs, without changing the function's code. This is particularly useful for logging, access control, memoization, and other aspects where you want to add functionality without modifying the actual code of your functions.

装饰器允许你在函数运行前后注入或修改代码，而无需更改函数的代码。这对于日志记录、访问控制、记忆化以及其他你希望在不修改函数实际代码的情况下添加功能的方面特别有用。 

Decorators in Python are a powerful tool that allow you to modify the behavior of a function or a method without changing its code. They are particularly useful for logging, access control, memoization, and other aspects where you want to add functionality without altering the actual code of the function.

在Python中，装饰器是一种强大的工具，可以让你在不改变函数代码的情况下修改函数或方法的行为。它们在日志记录、访问控制、记忆化以及你希望在不修改函数实际代码的情况下添加功能的其他方面特别有用。

Here's a basic example of each use case:

这里是每个用例的基本示例：

### 1. Logging Decorator Example (日志记录装饰器示例)

```python
def logger(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@logger
def add(x, y):
    return x + y

add(5, 3)
```

### 2. Access Control Decorator Example (访问控制装饰器示例)

```python
def check_permission(func):
    def wrapper(*args, **kwargs):
        if not user_has_permission():
            raise Exception("You do not have the right permissions.")
        return func(*args, **kwargs)
    return wrapper

@check_permission
def delete_something():
    print("Deleting something...")

def user_has_permission():
    return False  # Example: User does not have permission

delete_something()
```

### 3. Memoization Decorator Example (记忆化装饰器示例)

```python
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper

@memoize
def fibonacci(n):
    if n in (0, 1):
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(10))
```

| Feature | Description | Example |
|---------|-------------|---------|
| Logging | Adds logging to functions to trace their results | Logging the return values of a function |
| Access Control | Adds a security layer to functions to control access | Checking permissions before executing a function |
| Memoization | Caches the results of expensive function calls | Storing results of the Fibonacci function |

| 功能 | 描述 | 示例 |
|---------|-------------|---------|
| 日志记录 | 为函数添加日志记录以追踪其结果 | 记录函数的返回值 |
| 访问控制 | 为函数添加安全层以控制访问 | 在执行函数前检查权限 |
| 记忆化 | 缓存昂贵函数调用的结果 | 存储Fibonacci函数的结果 |

These decorators demonstrate how to enhance functions with additional functionality in Python without modifying the original function's code.

这些装饰器展示了如何在不修改原始函数代码的情况下，使用Python增强函数的附加功能。

When the logging functionality is in a different class or module, you can import the required class or module and apply its methods as decorators. This is common in larger applications where logging logic is kept separate to maintain cleaner and more modular code.

当日志功能位于不同的类或模块中时，可以导入所需的类或模块并应用其方法作为装饰器。在更大的应用程序中，这种做法很常见，日志逻辑保持独立以维持更清晰、更模块化的代码。

Here's an example where we define a logging decorator in a separate module or class, and then use it in our main application code:

这里有一个示例，我们在一个单独的模块或类中定义一个日志记录装饰器，然后在我们的主应用程序代码中使用它：

### Logging Module (日志模块)

Create a Python file named `logger.py`:

创建一个名为 `logger.py` 的Python文件：

```python
class Logger:
    @staticmethod
    def log(func):
        def wrapper(*args, **kwargs):
            result = func(*args, **kwargs)
            print(f"{func.__name__} returned {result} with args {args} and kwargs {kwargs}")
            return result
        return wrapper
```

### Main Application (主应用程序)

In your main application, import the `Logger` from `logger.py` and use its `log` method as a decorator:

在您的主应用程序中，从 `logger.py` 导入 `Logger` 并使用其 `log` 方法作为装饰器：

```python
from logger import Logger

@Logger.log
def multiply(x, y):
    return x * y

print(multiply(4, 5))
```

This setup keeps your logging logic encapsulated in the `Logger` class, and your main application code remains clean and focused on its core functionality.

这种设置使您的日志逻辑封装在 `Logger` 类中，而您的主应用程序代码保持干净并专注于其核心功能。

Here's a comparison table illustrating the approach:

这里是一个比较表，说明了这种方法：

| Approach | Benefits | Use Case |
|---------|-------------|---------|
| External Logging | Separates concerns, enhances modularity | Large applications where separate logging is beneficial |
| Internal Logging | Simplifies deployment and debugging | Smaller scripts or applications where logging is minimal |

| 方法 | 优点 | 用例 |
|---------|-------------|---------|
| 外部日志记录 | 分离关注点，增强模块性 | 在分离日志记录有益的大型应用程序中 |
| 内部日志记录 | 简化部署和调试 | 在日志记录较少的小型脚本或应用程序中 |

This approach to decorators demonstrates the flexibility of Python in structuring applications in a way that is both functional and maintainable.

这种对装饰器的方法展示了Python在构建应用程序方面的灵活性，既功能强大又易于维护。

```python
def memoize(func):
    """
    A decorator to store the results of function calls in order to speed up future calls.
    This is useful for optimizing functions with expensive or frequent calls with the same arguments.

    Parameters:
    func (callable): The function to be memoized.

    Returns:
    callable: A wrapper function that checks the cache before calling the original function.
    """
    cache = {}  # Initializes an empty dictionary to store function results based on arguments.
    
    def wrapper(*args):
        """
        A wrapper function that checks if the function has been called with the given arguments.
        If yes, it returns the cached result; otherwise, it computes, caches, and returns the result.

        Parameters:
        *args: Variable length argument list for the function.

        Returns:
        The result of the function either from the cache or computed.
        """
        if args in cache:
            return cache[args]  # Return the cached result if available.
        result = func(*args)  # Call the function if not found in cache and get the result.
        cache[args] = result  # Store the new result in the cache.
        return result  # Return the newly computed result.
    
    return wrapper  # Return the wrapper function to be used as a decorator.

@memoize
def fibonacci(n):
    """
    Calculates the nth number in the Fibonacci sequence using recursion and memoization.
    The sequence starts with Fibonacci(0) = 0 and Fibonacci(1) = 1. 

    Parameters:
    n (int): The position in the Fibonacci sequence to calculate.

    Returns:
    int: The nth Fibonacci number.
    """
    if n in (0, 1):
        return n  # Return 0 or 1 if n is 0 or 1 respectively.
    return fibonacci(n-1) + fibonacci(n-2)  # Recursively calculate the Fibonacci number using the memoized function.

print(fibonacci(10))  # Output the 10th Fibonacci number, which is 55.
`1``
