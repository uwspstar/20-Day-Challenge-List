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
```

In Python, `*args` and `**kwargs` are special syntax elements used in function definitions to handle variable numbers of arguments. They are particularly useful when defining wrapper functions in decorators, where the wrapper must work with any arguments that the original function expects.

在Python中，`*args` 和 `**kwargs` 是在函数定义中用来处理可变数量参数的特殊语法元素。它们在定义装饰器中的包装函数时特别有用，因为包装函数必须能够处理原始函数期望的任何参数。

### `*args`

- `*args` allows a function to accept any number of positional arguments (arguments that are not named).
- `*args` 允许函数接受任何数量的位置参数（未命名的参数）。
- It is typically used when you are not sure how many arguments might be passed to your function, or if you want to accept a list or tuple of arguments.
- 当你不确定可能会传递给你的函数多少个参数，或者如果你想接受一个列表或元组的参数时，通常会使用它。
- Inside the function, `args` is accessible as a tuple.
- 在函数内部，`args` 可以作为元组访问。

### `**kwargs`

- `**kwargs` allows a function to accept any number of keyword arguments (arguments that are provided by name).
- `**kwargs` 允许函数接受任何数量的关键字参数（通过名称提供的参数）。
- This is useful for functions that need to handle named arguments not explicitly defined in the function signature.
- 这对于需要处理在函数签名中未明确定义的命名参数的函数非常有用。
- Inside the function, `kwargs` is accessible as a dictionary.
- 在函数内部，`kwargs` 可以作为字典访问。

### Example Usage in a Decorator

Here’s how `*args` and `**kwargs` might be used in a decorator to ensure that any function with any type of arguments can be wrapped:

以下是如何在装饰器中使用 `*args` 和 `**kwargs`，以确保可以包装任何类型参数的任何函数：

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before calling the function")
        result = func(*args, **kwargs)  # Pass all received arguments to the original function.
        print("After calling the function")
        return result
    return wrapper

@my_decorator
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice", greeting="Hi")
```

This example shows how `*args` and `**kwargs` enable the `wrapper` function to accept and pass along any combination of positional and keyword arguments to the function it decorates, making the decorator flexible and applicable to a wide variety of functions.

这个示例展示了如何通过 `*args` 和 `**kwargs`，使 `wrapper` 函数能够接受并传递任何组合的位置参数和关键字参数给它装饰的函数，使装饰器灵活且适用于多种函数。

Yes, access control decorators can indeed be used to manage API access, and this technique is especially relevant in web frameworks like FastAPI. These decorators help enforce security measures by controlling who can access specific functions or endpoints based on predefined criteria such as user roles, permissions, or authentication status.

是的，访问控制装饰器确实可以用来管理API访问，这种技术在FastAPI等Web框架中尤其相关。这些装饰器通过根据预定义的标准（如用户角色、权限或认证状态）控制谁可以访问特定的函数或端点来帮助执行安全措施。

Here's a step-by-step example of how you might implement an access control decorator in FastAPI:

这里是在FastAPI中实现访问控制装饰器的逐步示例：

### Step 1: Define the Access Control Decorator

First, we define a decorator that checks if the user has the required permission to access a specific endpoint.

首先，我们定义一个装饰器，用于检查用户是否具有访问特定端点的所需权限。

```python
from fastapi import HTTPException, Depends, status
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

def has_permission(required_permission: str):
    def decorator(func):
        async def wrapper(*args, **kwargs):
            token = kwargs.get('token') or (await oauth2_scheme(kwargs['request']))
            user_permissions = decode_token(token)  # This should implement the logic to extract user details from the token
            if required_permission not in user_permissions:
                raise HTTPException(
                    status_code=status.HTTP_401_UNAUTHORIZED,
                    detail="You don't have permission to access this resource."
                )
            return await func(*args, **kwargs)
        return wrapper
    return decorator
```

### Step 2: Use the Decorator in FastAPI Routes

Apply the decorator to FastAPI routes to protect them. This example assumes you have some way to decode and verify tokens to extract user permissions.

在FastAPI路由中应用装饰器以保护它们。此示例假设您有某种方法来解码和验证令牌以提取用户权限。

```python
from fastapi import FastAPI, Depends

app = FastAPI()

@app.get("/protected-data")
@has_permission("admin")  # Only users with 'admin' permission can access this endpoint
async def read_protected_data(token: str = Depends(oauth2_scheme)):
    return {"data": "This is protected data"}
```

### Step 3: Handling Authentication and Permissions

In this setup, you will need a way to handle user authentication and token management. FastAPI works well with tools like OAuth2 and JWT for managing security tokens.

在此设置中，您需要一种处理用户身份验证和令牌管理的方法。FastAPI可以很好地与OAuth2和JWT等工具配合使用，以管理安全令牌。

### Summary

This example shows how to create a simple access control decorator in FastAPI. The decorator uses a security scheme to extract the token from the request, decode it to verify the user's permissions, and either proceed with the request or deny access based on those permissions.

此示例展示了如何在FastAPI中创建一个简单的访问控制装饰器。装饰器使用安全方案从请求中提取令牌，解码它以验证用户的权限，并根据这些权限继续请求或拒绝访问。
