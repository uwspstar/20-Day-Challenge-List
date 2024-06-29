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
