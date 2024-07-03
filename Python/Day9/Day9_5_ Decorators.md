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
