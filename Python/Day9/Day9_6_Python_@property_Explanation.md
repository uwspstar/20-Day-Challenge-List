### Detailed Explanation of `@property` in Python

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

| 方面                     | 属性 (使用 `@property`)                         | 方法                                      |
|--------------------------|------------------------------------------------|-------------------------------------------|
| **访问方式**             | `object.attribute`                             | `object.method()`                         |
| **可读性**               | 高，尤其是在封装逻辑时                          | 中等，因为括号表示方法                   |
| **封装性**               | 好，隐藏实现细节                               | 好，但对于简单访问不太直观                |
| **设置/删除器**          | 使用 `@
