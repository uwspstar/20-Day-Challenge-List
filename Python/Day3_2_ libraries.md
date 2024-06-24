# libraries

In Python, libraries (also known as modules) contain sets of tools including functions, classes, and variables that you can use to enhance the functionality of your Python scripts. Using `import` statements, you can access these libraries and utilize their features in your code.

### Import Styles in Python

1. **`import` Statement**: Used to import the whole module. You must prefix the module's functions, classes, or attributes with the module name.

   **`import` 语句**：用于导入整个模块。你必须在模块的函数、类或属性前加上模块名。

2. **`from ... import` Statement**: Allows you to import specific attributes from a module, which can be used directly without the module name prefix.

   **`from ... import` 语句**：允许你从模块中导入特定的属性，可以直接使用，无需模块名前缀。

### Code Examples

#### Example 1: Using `import`

```python
import math

# Use the sqrt function from the math module
result = math.sqrt(16)
print(result)  # Outputs: 4.0
```

**解释**:
- We import the entire `math` module and use its `sqrt` function by referring to it as `math.sqrt`.

  我们导入整个 `math` 模块并通过引用 `math.sqrt` 来使用它的 `sqrt` 函数。

#### Example 2: Using `from ... import`

```python
from math import sqrt

# Use the sqrt function directly
result = sqrt(16)
print(result)  # Outputs: 4.0
```

**解释**:
- We import only the `sqrt` function from the `math` module, so we can use it directly without prefixing it with `math`.

  我们只从 `math` 模块中导入 `sqrt` 函数，因此我们可以直接使用它，无需加上 `math` 前缀。

### Comparison Table | 比较表

| Import Style           | Usage                                   | Benefit                                         | Example               |
|------------------------|-----------------------------------------|-------------------------------------------------|-----------------------|
| `import module`        | Accesses the entire module              | Maintains namespace, avoiding naming conflicts  | `import math`         |
| `from module import x` | Imports specific functions or attributes| Directly use functions without module prefix    | `from math import sqrt`|

### Explanation | 解释

- **Namespace Management**: Using `import module` keeps the namespace clear, which helps in avoiding conflicts with functions or attributes having the same name from different modules.

  **命名空间管理**：使用 `import module` 保持命名空间清晰，这有助于避免不同模块中具有相同名称的函数或属性之间的冲突。

- **Code Clarity and Convenience**: `from module import x` can make the code cleaner and more readable by removing the need for repeated module references, which is especially useful if you are frequently using a specific function or attribute from a module.

  **代码清晰和便利性**：`from module import x` 通过去除重复的模块引用的需要，可以使代码更加清洁和可读，这在你频繁使用模块中的特定函数或属性时尤其有用。

By selecting the appropriate import style, you can write more readable and maintainable Python code.
