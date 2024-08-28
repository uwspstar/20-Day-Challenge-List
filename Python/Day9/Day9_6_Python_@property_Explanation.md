### Detailed Explanation of `@property` in Python
- [Python 解释器内置了很多函数和类型，任何时候都能使用](https://docs.python.org/zh-cn/3/library/functions.html#property)

#### 1. What is `@property`?

**English:**
`@property` is a built-in decorator in Python that allows you to define a method in a class and access it like an attribute. This makes the code more intuitive and readable.

**中文:**
`@property` 是 Python 中的一个内置装饰器，允许您在类中定义一个方法，并像属性一样访问它。这使得代码更直观和可读。

#### 2. Why Use `@property`?

**English:**
Using `@property` allows you to encapsulate and control access to an attribute while maintaining a clean and simple interface. It also lets you add logic when getting, setting, or deleting an attribute without changing how the attribute is accessed.

**中文:**
使用 `@property` 允许您封装和控制对属性的访问，同时保持干净简洁的接口。它还允许您在获取、设置或删除属性时添加逻辑，而无需更改访问属性的方式。

#### 3. How to Define a Property

**English:**
You define a property by decorating a method with `@property`. Here’s a simple example:

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius
```

In this example, the `radius` method is decorated with `@property`, so it can be accessed as an attribute, like `circle.radius`, instead of calling it as a method.

**中文:**
您可以通过用 `@property` 装饰一个方法来定义一个属性。以下是一个简单的例子：

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius
```

在这个例子中，`radius` 方法用 `@property` 装饰，因此可以像属性一样访问，例如 `circle.radius`，而不是将其作为方法调用。

#### 4. Adding Setter and Deleter

**English:**
To add a setter or deleter, use `@property_name.setter` or `@property_name.deleter` decorators. This lets you control how the attribute is modified or deleted:

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value

    @radius.deleter
    def radius(self):
        del self._radius
```

Now, `circle.radius` can be set or deleted like a regular attribute, but with additional logic.

**中文:**
要添加 setter 或 deleter，可以使用 `@property_name.setter` 或 `@property_name.deleter` 装饰器。这允许您控制属性的修改或删除方式：

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self._radius = value

    @radius.deleter
    def radius(self):
        del self._radius
```

现在，`circle.radius` 可以像常规属性一样设置或删除，但带有额外的逻辑。

#### 5. Comparison: Attribute vs. Method

| Aspect                   | Attribute (with `@property`)                   | Method                                    |
|--------------------------|------------------------------------------------|-------------------------------------------|
| **Access**               | `object.attribute`                             | `object.method()`                         |
| **Readability**          | High, especially when encapsulating logic      | Medium, since parentheses indicate method |
| **Encapsulation**        | Good, hides implementation details             | Good, but less intuitive for simple access|
| **Setter/Deleter**       | Possible using `@setter` and `@deleter`        | Managed through separate methods          |

### 6. Tips & Warnings

**Tip:**  
Use `@property` when you want to make accessing a method appear like accessing a simple attribute. This is particularly useful when you want to compute a value on the fly but still want the interface to remain clean and intuitive.

**提示：**  
当您希望方法的访问看起来像访问一个简单的属性时，请使用 `@property`。这在您希望动态计算一个值但仍希望接口保持干净和直观时特别有用。

**Warning:**  
Avoid overusing `@property` for complex logic or expensive operations, as this can make the code harder to understand and can lead to performance issues.

**警告：**  
避免对复杂逻辑或耗时操作过度使用 `@property`，因为这可能会使代码难以理解并导致性能问题。

### 7. 5Ws (Who, What, When, Where, Why)

- **Who:**  
  Python developers who want to create a clean, user-friendly interface for their classes.

  **谁：**  
  希望为其类创建干净、用户友好接口的 Python 开发人员。

- **What:**  
  The `@property` decorator, which allows methods to be accessed as attributes.

  **什么：**  
  `@property` 装饰器，允许方法以属性的形式访问。

- **When:**  
  When you need to control access to an attribute while keeping the interface simple.

  **何时：**  
  当您需要控制对属性的访问，同时保持接口简洁时。

- **Where:**  
  In any Python class where encapsulation and simplicity of access are important.

  **在哪里：**  
  在任何需要封装和简便访问的 Python 类中。

- **Why:**  
  To improve code readability and maintainability by providing a clean interface for attribute access while encapsulating logic.

  **为什么：**  
  通过为属性访问提供干净的接口，同时封装逻辑来提高代码的可读性和可维护性。

### 8. Recommended Resources

1. **[Python Documentation on `@property`](https://docs.python.org/3/library/functions.html#property)**  
   A comprehensive guide on how to use the `@property` decorator in Python.

   **[Python 官方文档中的 `@property`](https://docs.python.org/3/library/functions.html#property)**  
   关于如何在 Python 中使用 `@property` 装饰器的全面指南。

2. **[Real Python's Guide on `@property`](https://realpython.com/python-property/)**  
   An in-depth tutorial on how and when to use `@property` in your Python classes.

   **[Real Python 的 `@property` 指南](https://realpython.com/python-property/)**  
   关于如何以及何时在 Python 类中使用 `@property` 的深入教程。

3. **[Python OOP Tutorial](https://realpython.com/python3-object-oriented-programming/)**  
   A broader tutorial that covers object-oriented programming in Python, including the use of `@property`.

   **[Python 面向对象编程教程](https://realpython.com/python3-object-oriented-programming/)**  
   涵盖 Python 中面向对象编程的更广泛教程，包括 `@property` 的使用。

By understanding and effectively using `@property`, you can create Python classes that are both powerful and easy to use.

通过理解和有效使用 `@property`，您可以创建既强大又易于使用的 Python 类。
