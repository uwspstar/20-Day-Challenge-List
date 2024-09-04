### What are Python Decorators and How Do They Work?

#### English Explanation:
Python decorators are a powerful tool to modify or extend the behavior of functions or methods. They are often used in scenarios such as:
- **Logging**: Automatically log calls to functions.
- **Access Control**: Restrict access to certain functions based on roles.
- **Instrumentation**: Measure the time a function takes to execute.
- **Caching**: Cache the result of function calls for optimization.

A decorator is simply a function that takes another function as an argument, adds some functionality before or after the execution of that function, and then returns a new function that wraps the original one.

**Basic Example:**
```python
def my_decorator(func):
    def wrapper():
        print("Something before the function is called.")
        func()
        print("Something after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

- **Output:**
```
Something before the function is called.
Hello!
Something after the function is called.
```

In this example, the decorator `my_decorator` adds behavior before and after the `say_hello` function is called.

#### Chinese Explanation:
Python装饰器是一种修改或扩展函数或方法行为的强大工具。它们常用于以下场景：
- **日志记录**: 自动记录函数调用。
- **访问控制**: 基于角色限制对某些函数的访问。
- **检测**: 测量函数执行的时间。
- **缓存**: 缓存函数调用结果以优化性能。

装饰器本质上是一个函数，它接受另一个函数作为参数，在该函数执行之前或之后添加一些功能，然后返回一个包装原始函数的新函数。

**基础示例：**
```python
def my_decorator(func):
    def wrapper():
        print("在函数调用之前执行一些操作")
        func()
        print("在函数调用之后执行一些操作")
    return wrapper

@my_decorator
def say_hello():
    print("你好!")

say_hello()
```

- **输出：**
```
在函数调用之前执行一些操作
你好!
在函数调用之后执行一些操作
```

在这个例子中，装饰器 `my_decorator` 在 `say_hello` 函数调用之前和之后添加了行为。

#### Warning:
- **English**: Be careful with decorators that change the function's signature (number of arguments). Always use `functools.wraps` to preserve the metadata (like the name and docstring) of the original function.
- **Chinese**: 当使用装饰器时，要注意不要更改函数的签名（参数数量）。使用 `functools.wraps` 来保留原始函数的元数据（如名称和文档字符串）。

#### Key Points:
1. **English:** Decorators are functions that modify other functions.
2. **Chinese:** 装饰器是修改其他函数的函数。

Let me know if you'd like a more advanced example or more explanation on any specific part!
