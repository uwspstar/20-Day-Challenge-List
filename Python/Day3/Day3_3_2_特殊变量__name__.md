In Python, the special variable `__name__` plays a crucial role in determining whether a script is being run as the main program or being imported as a module into another script. Here's how it works:

在Python中，特殊变量`__name__`在确定脚本是作为主程序运行还是作为模块被导入到另一个脚本中起着至关重要的作用。其工作原理如下：

### Purpose of `__name__`

The `__name__` variable is automatically set by Python. When a script is run directly, `__name__` is set to `'__main__'`. When the script is imported as a module, `__name__` is set to the module's name.

`__name__`变量是由Python自动设置的。当直接运行脚本时，`__name__`设置为`'__main__'`。当脚本作为模块导入时，`__name__`被设置为模块的名称。

### Example Usage

Here's a simple example to demonstrate its usage:

以下是一个简单的示例，以演示其用法：

```python
# mymodule.py
def function():
    print("Function called!")

if __name__ == '__main__':
    print("Script is running directly")
    function()
else:
    print("Script imported as a module")
```

When you run this script directly (e.g., `python mymodule.py`), Python sets `__name__` to `'__main__'`, and it prints "Script is running directly" followed by "Function called!".

当您直接运行此脚本（例如，`python mymodule.py`）时，Python将`__name__`设置为`'__main__'`，它会打印"Script is running directly"，然后是"Function called!"。

If you import this script into another Python script:

如果您将此脚本导入到另一个Python脚本中：

```python
# another_script.py
import mymodule
```

Python sets `__name__` to `'mymodule'`. When `mymodule` is imported, it prints "Script imported as a module", and it does not execute the code inside the `if` block.

Python将`__name__`设置为`'mymodule'`。当导入`mymodule`时，它会打印"Script imported as a module"，并且不执行`if`块内的代码。

### Practical Use

The use of `if __name__ == '__main__':` allows you to create Python files that can be both used as reusable modules and run as standalone programs, depending on the context in which they are used.

使用`if __name__ == '__main__':`允许您创建既可以作为可重用模块使用也可以作为独立程序运行的Python文件，具体取决于它们被使用的上下文。

------

### \_\_name\_\_ Variable
In Python, the special variable `__name__` plays a crucial role in determining whether a script is being run as the main program or being imported as a module into another script. Here's how it works:

#### 1. How does the `__name__` variable work in Python?
[English]
The `__name__` variable is automatically set by Python. When a script is run directly, `__name__` is set to `"__main__"`. When the script is imported as a module, `__name__` is set to the module's name.

```python
# my_script.py
def main():
    print("Running as the main program")

if __name__ == "__main__":
    main()
```

[Chinese]
`__name__` 变量由 Python 自动设置。当脚本直接运行时，`__name__` 被设置为 `"__main__"`；当脚本作为模块导入时，`__name__` 被设置为模块的名称。

```python
# my_script.py
def main():
    print("作为主程序运行")

if __name__ == "__main__":
    main()
```

#### 2. What happens when you run a script directly vs. importing it as a module?
[English]
When you run a script directly:
- `__name__` is set to `"__main__"`.
- The code block inside `if __name__ == "__main__":` is executed.

When you import the script as a module:
- `__name__` is set to the name of the module.
- The code block inside `if __name__ == "__main__":` is not executed.

```python
# test.py
import my_script
print("Importing my_script")
```

Running `my_script.py` directly:
```bash
$ python my_script.py
Running as the main program
```

Running `test.py`:
```bash
$ python test.py
Importing my_script
```

[Chinese]
直接运行脚本时：
- `__name__` 被设置为 `"__main__"`。
- `if __name__ == "__main__":` 内的代码块被执行。

将脚本作为模块导入时：
- `__name__` 被设置为模块的名称。
- `if __name__ == "__main__":` 内的代码块不会被执行。

```python
# test.py
import my_script
print("导入 my_script")
```

直接运行 `my_script.py`：
```bash
$ python my_script.py
作为主程序运行
```

运行 `test.py`：
```bash
$ python test.py
导入 my_script
```

#### 3. What are the benefits of using the `__name__` variable?
[English]
1. **Modularity**: Allows you to organize your code into reusable modules.
2. **Testing**: Enables running tests or main functions only when the script is executed directly.
3. **Readability**: Clarifies the entry point of the program for others reading the code.

```python
# utility.py
def useful_function():
    return "This is useful"

if __name__ == "__main__":
    print("utility.py is being run directly")
    print(useful_function())
else:
    print("utility.py has been imported")
```

[Chinese]
1. **模块化**：允许将代码组织成可重用的模块。
2. **测试**：仅在脚本直接执行时运行测试或主函数。
3. **可读性**：为阅读代码的人明确程序的入口点。

```python
# utility.py
def useful_function():
    return "这是有用的"

if __name__ == "__main__":
    print("utility.py 直接运行")
    print(useful_function())
else:
    print("utility.py 已被导入")
```

#### 4. What happens behind the scenes when `__name__` is used?
[English]
Behind the scenes, Python sets the `__name__` variable based on how the script is invoked. When you run a script directly, Python sets `__name__` to `"__main__"`. When the script is imported, Python sets `__name__` to the name of the module (typically the filename without the extension).

```python
# script.py
print(__name__)
```

Running `script.py` directly:
```bash
$ python script.py
__main__
```

Importing `script.py`:
```python
import script  # Outputs: script
```

[Chinese]
在幕后，Python 根据脚本的调用方式设置 `__name__` 变量。当直接运行脚本时，Python 将 `__name__` 设置为 `"__main__"`；当脚本被导入时，Python 将 `__name__` 设置为模块的名称（通常是文件名，不带扩展名）。

```python
# script.py
print(__name__)
```

直接运行 `script.py`：
```bash
$ python script.py
__main__
```

导入 `script.py`：
```python
import script  # 输出: script
```

#### 5. How do you use `__name__` to write testable code?
[English]
Using `__name__` to write testable code involves placing test cases or code that should only run when the script is executed directly inside the `if __name__ == "__main__":` block. This keeps the module clean and reusable while allowing direct execution for testing purposes.

```python
# calculator.py
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

if __name__ == "__main__":
    print("Testing calculator module")
    print(f"3 + 5 = {add(3, 5)}")
    print(f"10 - 4 = {subtract(10, 4)}")
```

[Chinese]
使用 `__name__` 编写可测试代码涉及将测试用例或仅在脚本直接执行时运行的代码放置在 `if __name__ == "__main__":` 块中。这保持了模块的干净和可重用性，同时允许为测试目的直接执行。

```python
# calculator.py
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

if __name__ == "__main__":
    print("测试计算器模块")
    print(f"3 + 5 = {add(3, 5)}")
    print(f"10 - 4 = {subtract(10, 4)}")
```

I hope this explanation helps in understanding the `__name__` variable in Python!

------

### Recommend Resources:
**Python Tutorial: if __name__ == '__main__' by Corey Schafer**
[![Python Tutorial: if __name__ == '__main__'](https://img.youtube.com/vi/sugvnHA7ElY/maxresdefault.jpg)](https://youtu.be/sugvnHA7ElY)




