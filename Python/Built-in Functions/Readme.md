# Python 71 Built-in Functions

Here is a table listing all [71 Python built-in functions](https://docs.python.org/zh-cn/3/library/functions.html) along with code example.

"内置函数" means "built-in functions" in Chinese. These are functions that are provided by Python and are available for use without needing to import any additional modules. They are integral parts of the Python language, offering a wide range of functionality for various tasks.

| **内置函数**       | **示例代码**                                           | **描述**                                           |
|-------------------|------------------------------------------------------|----------------------------------------------------|
| [abs()](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Python/Built-in%20Functions/abs(x)_function.md)    | `abs(-5)` => `5`                                      | 返回数字的绝对值                                    |
| aiter()           | `async for x in aiter(iterable):` => `Async iteration`| 返回异步迭代器                                      |
| [all()](https://github.com/uwspstar/20-Day-Challenge-List/tree/main/Python/Built-in%20Functions)             | `all([True, False])` => `False`                       | 如果所有元素都为真，返回 `True`  [Comparison: any([]) vs all([])](https://codebitwave.com/python-101-comparison-any-vs-all/)                     |
| anext()           | `await anext(async_iterator)` => `Get next item`      | 异步地获取下一个元素                                |
| [any()](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Python/Built-in%20Functions/any(iterable)_function.md)             | `any([True, False])` => `True`                        | 如果任一元素为真，返回 `True` [Comparison: any([]) vs all([])](https://codebitwave.com/python-101-comparison-any-vs-all/)                       |
| ascii()           | `ascii('ñ')` => `'\\xf1'`                             | 返回对象的可打印ASCII表示形式                         |
| bin()             | `bin(10)` => `'0b1010'`                               | 将整数转换为二进制字符串                             |
| bool()            | `bool(1)` => `True`                                   | 将值转换为布尔类型                                  |
| breakpoint()      | `breakpoint()` => `Enter debugging mode`              | 进入调试模式                                        |
| bytearray()       | `bytearray('abc', 'utf-8')` => `bytearray(b'abc')`    | 返回字节数组                                        |
| bytes()           | `bytes('abc', 'utf-8')` => `b'abc'`                   | 返回字节对象                                        |
| callable()        | `callable(abs)` => `True`                             | 检查对象是否可调用                                  |
| chr()             | `chr(97)` => `'a'`                                    | 返回对应ASCII值的字符                                |
| classmethod()     | `classmethod(func)` => `Class method wrapper`         | 将函数转换为类方法                                  |
| compile()         | `compile('print(1)', '', 'exec')` => `Compile code`   | 编译代码并返回代码对象                              |
| complex()         | `complex(1, 2)` => `(1+2j)`                           | 创建一个复数                                        |
| delattr()         | `delattr(obj, 'attr')` => `Deletes attribute`         | 删除对象的属性                                      |
| dict()            | `dict(a=1, b=2)` => `{'a': 1, 'b': 2}`                | 创建字典对象                                        |
| dir()             | `dir()` => `['__class__', ...]`                       | 列出对象的属性和方法                                |
| divmod()          | `divmod(9, 4)` => `(2, 1)`                            | 返回商和余数                                        |
| enumerate()       | `enumerate(['a', 'b'])` => `[(0, 'a'), (1, 'b')]`     | 返回枚举对象                                        |
| eval()            | `eval('1 + 2')` => `3`                                | 计算表达式并返回结果                                |
| exec()            | `exec('print(1)')` => `Executes code`                 | 执行动态Python代码                                  |
| filter()          | `filter(lambda x: x > 0, [-1, 1, 2])` => `[1, 2]`     | 过滤序列中的元素                                    |
| float()           | `float(2)` => `2.0`                                   | 将值转换为浮点数                                    |
| format()          | `format(2, '04d')` => `'0002'`                        | 格式化值为指定格式                                  |
| frozenset()       | `frozenset([1, 2, 3])` => `frozenset({1, 2, 3})`      | 创建不可变集合                                      |
| getattr()         | `getattr(obj, 'attr', 'default')` => `default`        | 获取对象的属性值                                    |
| globals()         | `globals()` => `{'__name__': '__main__', ...}`        | 返回全局符号表                                      |
| hasattr()         | `hasattr(obj, 'attr')` => `True`                      | 检查对象是否有指定属性                              |
| hash()            | `hash('abc')` => `-1100007589`                        | 返回对象的哈希值                                    |
| [help()](https://github.com/uwspstar/20-Day-Challenge-List/tree/main/Python/Built-in%20Functions)            | `help(print)` => `Displays help for print`            | 显示帮助信息                                        |
| hex()             | `hex(255)` => `'0xff'`                                | 将整数转换为十六进制字符串                           |
| id()              | `id(obj)` => `140152140012544`                        | 返回对象的唯一标识符                                |
| input()           | `input('Enter: ')` => `User input`                    | 从用户获取输入                                      |
| int()             | `int('10')` => `10`                                   | 将值转换为整数                                      |
| isinstance()      | `isinstance(1, int)` => `True`                        | 检查对象是否为指定类型的实例                         |
| issubclass()      | `issubclass(bool, int)` => `True`                     | 检查类是否为指定类的子类                             |
| iter()            | `iter([1, 2, 3])` => `<list_iterator>`                | 返回对象的迭代器                                    |
| len()             | `len('abc')` => `3`                                   | 返回对象的长度                                      |
| list()            | `list(range(3))` => `[0, 1, 2]`                       | 创建列表对象                                        |
| locals()          | `locals()` => `{'var': 'value', ...}`                 | 返回局部符号表                                      |
| map()             | `map(str, [1, 2, 3])` => `['1', '2', '3']`            | 对序列中的每一项应用函数                            |
| max()             | `max(1, 2)` => `2`                                    | 返回最大值                                          |
| memoryview()      | `memoryview(b'abc')` => `<memory at 0x7f3d700fc100>`  | 返回内存视图对象                                    |
| min()             | `min(1, 2)` => `1`                                    | 返回最小值                                          |
| next()            | `next(iter([1, 2, 3]))` => `1`                        | 返回迭代器的下一个元素                              |
| object()          | `object()` => `New object`                            | 创建一个新对象                                      |
| oct()             | `oct(8)` => `'0o10'`                                  | 将整数转换为八进制字符串                             |
| open()            | `open('file.txt')` => `<_io.TextIOWrapper ...>`       | 打开文件并返回文件对象                              |
| ord()             | `ord('a')` => `97`                                    | 返回字符的ASCII值                                   |
| pow()             | `pow(2, 3)` => `8`                                    | 返回x的y次幂                                        |
| print()           | `print('Hello')` => `Hello`                           | 打印输出                                            |
| property()        | `property(fget=None)` => `<property object>`          | 返回属性                                            |
| range()           | `range(3)` => `range(0, 3)`                           | 返回不可变序列                                      |
| repr()            | `repr(1.5)` => `'1.5'`                                | 返回对象的字符串表示                                |
| reversed()        | `reversed([1, 2, 3])` => `[3, 2, 1]`                  | 返回序列的反向迭代器                                |
| round()           | `round(1.2345, 2)` => `1.23`                          | 对浮点数进行四舍五入                                |
| set()             | `set([1, 2, 3])` => `{1, 2, 3}`                       | 创建一个新的集合                                    |
| setattr()         | `setattr(obj, 'attr', value)` => `Sets attribute`     | 设置对象的属性                                      |
| slice()           | `slice(1, 5, 2)` => `slice(1, 5, 2)`                  | 返回一个切片对象                                    |
| sorted()          | `sorted([3, 1, 2])` => `[1, 2, 3]`                    | 返回排序后的列表                                    |
| staticmethod()    | `staticmethod(func)` => `Static method wrapper`       | 将函数转换为静态方法                                |
| str()             | `str(123)` => `'123'`                                 | 将值转换为字符串                                    |
| sum()             | `sum([1, 2, 3])` => `6`                               | 返回序列中元素的总和                                |
| super()           | `super()` => `<super object>`                         | 返回父类对象                                        |
| tuple()           | `tuple([1, 2, 3])` => `(1, 2, 3)`                     | 创建一个新的元组                                    |
| type()            | `type(123)` => `<class 'int'>`                        | 返回对象的类型                                      |
| vars()            | `vars()` => `{'var': 'value', ...}`                   | 返回对象的__dict__属性                              |
| zip()             | `zip([1, 2], ['a', 'b'])` => `[(1, 'a'), (2, 'b')]`   | 将多个序列压缩成一个元组列表                        |
| `__import__()`      | `__import__('math')` => `<module 'math' (built-in)>`  | 动态加载模块                                        |
 



These examples demonstrate how to use each built-in function in Python. For more detailed information, you can refer to the [Python official documentation](https://docs.python.org/3/library/functions.html).

- [Built-in Functions](https://docs.python.org/3/library/functions.html)
