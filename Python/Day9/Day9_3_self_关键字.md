# `self` keyword 
In Python, the `self` keyword is used in the context of class methods to refer to the instance of the class on which a method is being called. This mechanism allows each instance of a class to access its own attributes and methods using the same structure of code. The use of `self` makes it possible to manage instance-specific information and behaviors, supporting the fundamental principles of object-oriented programming, such as encapsulation and polymorphism.

在 Python 中，`self` 关键字用于类方法中，指代调用某个方法的类的实例。这种机制允许每个类的实例使用相同的代码结构访问其自身的属性和方法。使用 `self` 可以管理特定于实例的信息和行为，支持面向对象编程的基本原则，如封装和多态。

### 代码示例 (Code Example)

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # 使用 self 来保存实例特定的信息
        self.age = age

    def greet(self):
        # 使用 self 访问实例的属性
        print(f"Hello, my name is {self.name} and I am {self.age} years old.")

# 创建一个 Person 类的实例
john = Person("John", 30)

# 调用实例的方法
john.greet()
```

### 解释 (Explanation)

在这个例子中，`__init__` 和 `greet` 方法都使用了 `self` 关键字。在 `__init__` 方法中，`self` 被用来为每个新创建的对象设置 `name` 和 `age` 属性。当 `john.greet()` 被调用时，`self` 在 `greet` 方法中引用的是 `john` 这个实例，因此方法可以访问并显示 John 的名字和年龄。这展示了 `self` 如何使得实例能够访问和控制其自身的数据，这是面向对象编程中封装的核心概念之一。

In this example, both the `__init__` and `greet` methods use the `self` keyword. In the `__init__` method, `self` is used to set the `name` and `age` attributes for each newly created object. When `john.greet()` is called, `self` in the `greet` method refers to the `john` instance, allowing the method to access and display John's name and age. This demonstrates how `self` allows instances to access and control their own data, one of the core concepts of encapsulation in object-oriented programming.
