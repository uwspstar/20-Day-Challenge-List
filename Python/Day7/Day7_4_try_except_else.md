# try except else
The `try ... except` statement in Python can include an optional `else` clause, which, if present, must be placed after all `except` clauses. The `else` clause is executed if the `try` block does not raise an exception. Using the `else` clause can be advantageous because it helps ensure that certain code runs only if no exceptions were raised in the `try` block, thereby avoiding the accidental capture of exceptions that are not intended to be handled by the `except` clauses.

Python中的`try ... except`语句可以包含一个可选的`else`子句，如果存在，必须放在所有`except`子句之后。如果`try`块没有引发异常，则执行`else`子句。使用`else`子句具有优势，因为它有助于确保只有在`try`块中没有引发异常时才运行某些代码，从而避免意外捕获未打算由`except`子句处理的异常。

The example you provided demonstrates how to use the `else` clause effectively:

你提供的示例演示了如何有效使用`else`子句：

```python
import sys

# Assume sys.argv contains the script name and any filenames as arguments
for arg in sys.argv[1:]:
    try:
        f = open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()
```

### Explanation:

1. **Try Block**: Attempts to open a file. If the file cannot be opened (e.g., it does not exist or the user lacks the necessary permissions), an `OSError` is raised.

1. **Try块**：尝试打开一个文件。如果无法打开文件（例如，文件不存在或用户缺乏必要的权限），则会引发`OSError`。

2. **Except Block**: Handles the case where an `OSError` occurs by printing a message indicating that the file cannot be opened.

2. **Except块**：通过打印一条消息来处理发生`OSError`的情况，指出无法打开文件。

3. **Else Block**: This block is executed only if no exceptions were raised in the `try` block. It prints the number of lines in the file and then closes the file. Using `else` here is beneficial because it clearly separates the error handling code from the normal operation code, which only runs when the file opening succeeds.

3. **Else块**：只有在`try`块中没有引发异常时，才执行此块。它打印文件中的行数，然后关闭文件。在这里使用`else`是有益的，因为它清楚地将错误处理代码与正常操作代码分开，后者仅在文件打开成功时运行。

The use of the `else` clause makes the code more readable and maintains a clear separation between the handling of exceptions and the execution of code that should only run when no exceptions occur. This practice enhances the maintainability and clarity of the code.
