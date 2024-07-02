# Scope in Python

**Scope** in Python refers to the region of a program where a defined variable can be accessed. Understanding scope is crucial for managing variable visibility and lifecycle across different parts of your code.

**作用域**在Python中指的是程序中定义的变量可以被访问的区域。理解作用域对于管理代码不同部分的变量可见性和生命周期至关重要。

#### Types of Scopes

1. **Local Scope**: Variables defined within a function are in the local scope of that function. They are only accessible from within the function.
   
   **局部作用域**：在函数内定义的变量处于该函数的局部作用域中。它们仅在函数内部可访问。

2. **Global Scope**: Variables defined at the top level of a script or module are in the global scope. They are accessible from any part of the code in the same module.
   
   **全局作用域**：在脚本或模块的顶层定义的变量处于全局作用域中。它们可以从同一模块的任何部分访问。

3. **Module-level Scope**: Similar to global scope, but restricted to the module where the variable is defined.
   
   **模块级作用域**：类似于全局作用域，但限于定义变量的模块。

4. **Built-in Scope**: This includes names pre-defined in the built-in namespace of Python, accessible from any part of your program.
   
   **内置作用域**：这包括在Python的内置命名空间中预定义的名称，可从程序的任何部分访问。

#### Syncing Scopes

Using the `global` keyword, variables from the global scope can be modified within a local scope.

使用`global`关键字，可以在局部作用域内修改全局作用域的变量。

#### Example Code

```python
x = "global"

def example():
    global x
    x = "modified global"
    y = "local"
    print("Inside function:", x, y)

example()
print("Outside function:", x)
```

This example demonstrates how modifying a global variable affects it both inside and outside the function. The variable `y` remains local and is not accessible outside the function.

此示例演示了修改全局变量如何在函数内外影响它。变量`y`保持局部状态，不能在函数外访问。

#### Comparison Table

| Scope Type     | Description                                                  | Example            |
|----------------|--------------------------------------------------------------|--------------------|
| Local Scope    | Variables created inside functions; not accessible elsewhere | Variables in `example()` function |
| Global Scope   | Variables defined outside any function; accessible globally  | `x` in the example |
| Module-level   | Variables global within a module                             | Same as global in single-module scripts |
| Built-in Scope | Names pre-defined by Python; accessible everywhere           | `print`, `int`     |

The table summarizes the different types of scopes in Python and provides examples for better understanding.

表格总结了Python中不同类型的作用域，并提供了例子以便更好地理解。
