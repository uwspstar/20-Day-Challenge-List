# Python 中方法调用与函数调用之间的关系

在 Python 中，当你调用一个对象的方法时，这个对象会自动作为第一个参数传递给该方法。这种机制是面向对象编程的一个重要特性，它让方法能够访问和操作实例对象的数据。

This paragraph describes the relationship between method calls and function calls in Python. In Python, when you call a method of an object, the object is automatically passed as the first argument to that method. This mechanism is an important feature of object-oriented programming, allowing methods to access and manipulate the data of the instance object.

### 代码示例 (Code Example)

```python
class MyClass:
    def show(self, msg):
        print(f"Message from {self}: {msg}")

# 实例化对象
obj = MyClass()

# 使用方法调用
obj.show("Hello!")

# 等效的函数调用
MyClass.show(obj, "Hello!")
```

### 比较 (Comparison)

| 调用类型 | 代码示例 | 说明 |
|--------|----------|-----|
| 方法调用 | `obj.show("Hello!")` | `obj` 作为 `show` 方法的第一个参数自动传递。 |
| 函数调用 | `MyClass.show(obj, "Hello!")` | 显式地将 `obj` 作为第一个参数传递给 `show` 函数。 |

### 解释 (Explanation)
当你使用 `obj.show("Hello!")` 时，Python 内部实际上会将它转化为 `MyClass.show(obj, "Hello!")`。这说明 `obj`（即 `self` 参数）自动成为方法的第一个参数，而其他参数如 `"Hello!"` 跟随其后。这种转换使得方法能够访问调用它的实例的属性和方法，这是面向对象编程中封装的一个体现。

When you use `obj.show("Hello!")`, Python internally converts it to `MyClass.show(obj, "Hello!")`. This shows that `obj` (i.e., the `self` parameter) automatically becomes the first parameter of the method, followed by other parameters like `"Hello!"`. This conversion allows the method to access the properties and methods of the instance that calls it, reflecting encapsulation in object-oriented programming.
