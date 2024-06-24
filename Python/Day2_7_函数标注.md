# 函数标注In Python, function annotations allow you to add arbitrary metadata to function parameters and return values. These annotations are stored in a dictionary called `__annotations__` within the function object, and they do not affect the execution of the function in any way.

在 Python 中，函数标注允许你为函数参数和返回值添加任意元数据。这些标注以字典的形式存放在函数对象的 `__annotations__` 属性中，它们不会以任何方式影响函数的执行。

### Key Concepts of Function Annotations

- **Parameter Annotations**: Defined by placing a colon after the parameter name, followed by an expression that evaluates to the annotation.
- **Return Value Annotations**: Defined using the arrow notation (`->`) followed by an expression for the annotation, placed before the colon that ends the `def` statement.

### 函数标注的关键概念

- **参数标注**：通过在参数名后加冒号，然后跟一个会被求值为标注的值的表达式来定义。
- **返回值标注**：使用箭头符号 (`->`) 后跟一个表达式来定义标注，这个表达式位于表示 `def` 语句结束的冒号之前。

### Example | 示例

#### A Function with Annotations

```python
def greet(name: str, greeting: str = "Hello") -> str:
    return f"{greeting}, {name}"

print(greet("Alice"))  # Outputs: Hello, Alice
print(greet("Bob", "Howdy"))  # Outputs: Howdy, Bob
print(greet.__annotations__)  # Outputs: {'name': <class 'str'>, 'greeting': <class 'str'>, 'return': <class 'str'>}
```

**一个带有标注的函数**

```python
def greet(name: str, greeting: str = "Hello") -> str:
    return f"{greeting}, {name}"

print(greet("Alice"))  # 输出：Hello, Alice
print(greet("Bob", "Howdy"))  # 输出：Howdy, Bob
print(greet.__annotations__)  # 输出：{'name': <class 'str'>, 'greeting': <class 'str'>, 'return': <class 'str'>}
```

### Explanation | 解释

- **Parameter Annotations**: `name: str` indicates that `name` is expected to be a string. `greeting: str = "Hello"` indicates that `greeting` is also expected to be a string and defaults to `"Hello"`.
- **Return Value Annotation**: `-> str` indicates that the function is expected to return a string.

- **参数标注**：`name: str` 表示预期 `name` 是一个字符串。`greeting: str = "Hello"` 表示 `greeting` 也预期是一个字符串，并默认为 `"Hello"`。
- **返回值标注**：`-> str` 表示函数预期返回一个字符串。

Function annotations can be particularly useful for documentation purposes or when using tools that enforce type checking, though they do not enforce any type checking themselves.

函数标注对于文档目的特别有用，或者在使用强制类型检查的工具时有用，尽管它们本身不强制执行任何类型检查。
