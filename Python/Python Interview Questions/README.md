# Python Interview Questions

<details>
  <summary>1. What is `__init__`?</summary>

  1. **What is `__init__`?**

`__init__` is a special method in Python, known as a constructor in object-oriented terminology. This method is called when an object is created from a class and it allows the class to initialize the attributes of the class.

`__init__` 是 Python 中的一个特殊方法，被称为构造函数。当从一个类创建对象时，会调用这个方法，允许类初始化其属性。

```python
class Car:
    def __init__(self, make, model):
        self.make = make
        self.model = model

my_car = Car("Toyota", "Corolla")
print(my_car.make)  # Output: Toyota
print(my_car.model) # Output: Corolla
```

### Comparison Table: Constructor in Different Programming Languages

| Language  | Constructor Name     | Example                                      |
|-----------|----------------------|----------------------------------------------|
| Python    | `__init__`           | `def __init__(self, param): ...`             |
| Java      | Same as class name   | `public ClassName(param) { ... }`            |
| C++       | Same as class name   | `ClassName(param) { ... }`                   |
| JavaScript| `constructor`        | `constructor(param) { ... }`                 |

### Explanation Behind the Concept

Constructors like `__init__` in Python are fundamental for setting up initial conditions of an object. When you create an object, `__init__` sets the initial state by assigning the values of the object's properties. This method can take any number of parameters and typically is used to initialize the object's attributes based on those parameters.

构造函数如 Python 中的 `__init__` 对于设置对象的初始条件是基本的。当你创建一个对象时，`__init__` 通过分配对象属性的值来设置初始状态。这个方法可以接受任意数量的参数，并且通常用于根据这些参数初始化对象的属性。

</details>

