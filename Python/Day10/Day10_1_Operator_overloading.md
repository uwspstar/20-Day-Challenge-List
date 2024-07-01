# Operator overloading
Operator overloading in Python allows custom objects to interact with built-in operators. For instance, using operators like `+`, `-`, `*`, or `/` can be defined for your own class objects so they can be used in ways that are intuitive and natural to the specific context of your application.

在 Python 中，运算符重载允许自定义对象与内置运算符进行交互。例如，可以为你自己的类对象定义像 `+`、`-`、`*` 或 `/` 这样的运算符，使它们能够以直观和自然的方式用于你应用程序的特定上下文中。

### Key Points (关键点)
- **Pythonic Feature**: Python supports operator overloading, making it possible to define or change the meaning of operators based on the objects they are operating on.
- **Methods**: Special methods in Python, called "magic methods" or "dunder methods" (because they start and end with double underscores, e.g., `__add__`), are used for operator overloading.

- **Python 特性**：Python 支持运算符重载，使得可以根据运算符操作的对象定义或改变运算符的含义。
- **方法**：Python 中的特殊方法，称为“魔术方法”或“双下方法”（因为它们以双下划线开始和结束，例如 `__add__`），用于运算符重载。

### Commonly Overloaded Operators and Their Methods

| Operator | Method           | Description (描述)                           |
|----------|------------------|---------------------------------------------|
| `+`      | `__add__(self, other)`      | Adds two objects together (将两个对象相加) |
| `-`      | `__sub__(self, other)`      | Subtracts one object from another (从一个对象中减去另一个对象) |
| `*`      | `__mul__(self, other)`      | Multiplies two objects (将两个对象相乘) |
| `/`      | `__truediv__(self, other)` | Divides one object by another (将一个对象除以另一个对象) |
| `==`     | `__eq__(self, other)`      | Checks if two objects are equal (检查两个对象是否相等) |

### Example (例子)

Let's define a class `Vector` and overload the `+` operator to add two vector objects:

让我们定义一个类 `Vector` 并重载 `+` 运算符来添加两个向量对象：

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented

# Creating two vectors
v1 = Vector(2, 4)
v2 = Vector(5, -2)

# Using the overloaded + operator
print(v1 + v2)  # Output: Vector(7, 2)
```

### Explanation (解释)

In the example above, the `__add__` method is defined to allow two `Vector` instances to be added together using the `+` operator. When `v1 + v2` is executed, Python calls `v1.__add__(v2)`.

在上面的例子中，定义了 `__add__` 方法，允许使用 `+` 运算符将两个 `Vector` 实例相加。当执行 `v1 + v2` 时，Python 调用 `v1.__add__(v2)`。

This feature enhances the flexibility and readability of your code, making it closer to natural language and intuitive understanding.

这个功能增强了代码的灵活性和可读性，使其更接近自然语言和直观理解。
