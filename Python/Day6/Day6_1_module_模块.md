# 模块
In Python, a module is essentially a file containing Python definitions and statements. This allows you to organize your code logically, enabling reuse across different programs. Understanding how Python modules work is crucial for efficient programming and maintaining larger or multi-file projects.

在 Python 中，模块本质上是一个包含 Python 定义和语句的文件。这允许您逻辑地组织代码，使其可以在不同的程序之间重用。理解 Python 模块的工作原理对于高效编程和维护更大或多文件项目至关重要。

### Module Basics | 模块基础

#### English
Modules in Python are simply files with the `.py` extension containing Python code. Any Python file can be imported as a module into another Python script or interactive session. The file name (minus the `.py` extension) becomes the module name.

#### 中文
Python 中的模块只是包含 Python 代码的 `.py` 扩展名文件。任何 Python 文件都可以作为模块导入到另一个 Python 脚本或交互式会话中。文件名（去掉 `.py` 扩展名）成为模块名。

### How Modules are Used | 模块的使用方式

#### English
When you import a module, Python executes all of the code in the module file. This includes defining any functions, classes, and variables stated within the module. The `__name__` variable in the module is set to the module's name.

#### 中文
当您导入一个模块时，Python 会执行模块文件中的所有代码。这包括定义模块中声明的任何函数、类和变量。模块中的 `__name__` 变量被设置为模块的名字。

### Example of Creating and Using a Module | 创建和使用模块的示例

#### Creating a Module | 创建模块
Let's say you have a Python file named `mymodule.py` with the following content:

假设您有一个名为 `mymodule.py` 的 Python 文件，内容如下：

```python
# mymodule.py
def greet(name):
    print(f"Hello, {name}!")

if __name__ == "__main__":
    greet("Alice")
```

#### Using the Module | 使用模块
You can import and use this module in another Python script:

您可以在另一个 Python 脚本中导入并使用此模块：

```python
# another_script.py
import mymodule

mymodule.greet("Bob")
```

This will output:
这将输出：

```
Hello, Bob!
```

### The `__name__` Variable | `__name__` 变量

#### English
In Python, `__name__` is a special variable that Python sets to `"__main__"` when the module is run directly. If the module is imported from another module, `__name__` is set to the module's name. This allows for certain parts of the code to only execute when the module is run directly, not when it is imported.

#### 中文
在 Python 中，`__name__` 是 Python 设置的一个特殊变量，当直接运行模块时将其设置为 `"__main__"`。如果从另一个模块导入模块，`__name__` 被设置为模块的名字。这允许代码的某些部分仅在直接运行模块时执行，而不是在导入时执行。

### Conclusion | 结论

Modules are a key concept in Python that facilitates code reuse and organization. By creating files for different tasks and importing them as needed, you can keep your code base manageable and maintainable.

模块是 Python 中促进代码重用和组织的一个关键概念。通过为不同任务创建文件并根据需要导入它们，您可以保持代码库的可管理性和可维护性。
