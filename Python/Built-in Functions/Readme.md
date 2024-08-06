# Python 57 Built-in Functions

Here is a table listing all 57 Python built-in functions along with code examples.

| Function   | Description | Code Example |
|------------|-------------|--------------|
| `abs()`    | Returns the absolute value of a number | `abs(-5)  # Output: 5` |
| `all()`    | Returns True if all elements in an iterable are true | `all([True, True, False])  # Output: False` |
| `any()`    | Returns True if any element in an iterable is true | `any([False, False, True])  # Output: True` |
| `ascii()`  | Returns a readable version of an object. Replaces non-ASCII characters with escape characters | `ascii('æ')  # Output: '\\xe6'` |
| `bin()`    | Returns the binary version of a number | `bin(5)  # Output: '0b101'` |
| `bool()`   | Converts a value to a Boolean | `bool(0)  # Output: False` |
| `bytearray()` | Returns an array of bytes | `bytearray(4)  # Output: bytearray(b'\x00\x00\x00\x00')` |
| `bytes()`  | Returns a bytes object | `bytes(4)  # Output: b'\x00\x00\x00\x00'` |
| `callable()` | Returns True if the specified object is callable | `callable(len)  # Output: True` |
| `chr()`    | Returns a character from the specified Unicode code | `chr(97)  # Output: 'a'` |
| `classmethod()` | Converts a method into a class method | `class C: @classmethod def method(cls): pass` |
| `compile()` | Returns a Python code object from a source (string) | `compile('print(5)', '<string>', 'exec')` |
| `complex()` | Returns a complex number | `complex(1, 2)  # Output: (1+2j)` |
| `delattr()` | Deletes the specified attribute from an object | `class C: pass; c = C(); c.attr = 10; delattr(c, 'attr')` |
| `dict()`   | Creates a dictionary | `dict(a=1, b=2)  # Output: {'a': 1, 'b': 2}` |
| `dir()`    | Returns a list of the specified object's properties and methods | `dir([])  # Output: ['append', 'clear', ...]` |
| `divmod()` | Returns a tuple containing the quotient and remainder | `divmod(5, 2)  # Output: (2, 1)` |
| `enumerate()` | Takes a collection and returns it as an enumerate object | `enumerate(['a', 'b', 'c'])` |
| `eval()`   | Evaluates and executes an expression | `eval('5 + 5')  # Output: 10` |
| `exec()`   | Executes the specified code (or object) | `exec('print(5)')` |
| `filter()` | Use a filter function to exclude items in an iterable object | `list(filter(lambda x: x > 0, [-1, 0, 1, 2]))  # Output: [1, 2]` |
| `float()`  | Returns a floating-point number | `float('3.14')  # Output: 3.14` |
| `format()` | Formats a specified value | `format(8, 'b')  # Output: '1000'` |
| `frozenset()` | Returns a frozenset object | `frozenset([1, 2, 3])` |
| `getattr()` | Returns the value of the specified attribute (property or method) | `class C: attr = 10; getattr(C, 'attr')  # Output: 10` |
| `globals()` | Returns the current global symbol table as a dictionary | `globals()` |
| `hasattr()` | Returns True if the specified object has the specified attribute (property/method) | `hasattr(object, 'attribute')` |
| `hash()`   | Returns the hash value of a specified object | `hash('test')` |
| `help()`   | Executes the built-in help system | `help(str)` |
| `hex()`    | Converts a number into a hexadecimal string | `hex(255)  # Output: '0xff'` |
| `id()`     | Returns the id of an object | `id(object)` |
| `input()`  | Allows user input | `input('Enter: ')` |
| `int()`    | Returns an integer number | `int('10')  # Output: 10` |
| `isinstance()` | Returns True if a specified object is an instance of a specified object | `isinstance(5, int)  # Output: True` |
| `issubclass()` | Returns True if a specified class is a subclass of a specified object | `issubclass(bool, int)  # Output: True` |
| `iter()`   | Returns an iterator object | `iter([1, 2, 3])` |
| `len()`    | Returns the length of an object | `len('abc')  # Output: 3` |
| `list()`   | Returns a list | `list('abc')  # Output: ['a', 'b', 'c']` |
| `locals()` | Updates and returns a dictionary of the current local symbol table | `locals()` |
| `map()`    | Returns the specified iterator with the specified function applied to each item | `list(map(lambda x: x**2, [1, 2, 3]))  # Output: [1, 4, 9]` |
| `max()`    | Returns the largest item in an iterable | `max([1, 2, 3])  # Output: 3` |
| `memoryview()` | Returns a memory view object | `memoryview(b'abc')` |
| `min()`    | Returns the smallest item in an iterable | `min([1, 2, 3])  # Output: 1` |
| `next()`   | Returns the next item in an iterator | `next(iter([1, 2, 3]))  # Output: 1` |
| `object()` | Returns a new object | `object()` |
| `oct()`    | Converts a number into an octal | `oct(8)  # Output: '0o10'` |
| `open()`   | Opens a file and returns a file object | `open('file.txt', 'r')` |
| `ord()`    | Convert an integer representing the Unicode of the specified character | `ord('a')  # Output: 97` |
| `pow()`    | Returns the value of x to the power of y | `pow(2, 3)  # Output: 8` |
| `print()`  | Prints to the standard output device | `print('Hello, World!')` |
| `property()` | Gets, sets, deletes a property | `class C: def __init__(self): self._x = None; def getx(self): return self._x; def setx(self, value): self._x = value; def delx(self): del self._x; x = property(getx, setx, delx)` |
| `range()`  | Returns a sequence of numbers | `range(5)` |
| `repr()`   | Returns a readable version of an object | `repr('Hello')  # Output: "'Hello'"` |
| `reversed()` | Returns a reversed iterator | `reversed([1, 2, 3])` |
| `round()`  | Rounds a numbers | `round(3.14159, 2)  # Output: 3.14` |
| `set()`    | Returns a new set object | `set([1, 2, 3])  # Output: {1, 2, 3}` |
| `setattr()` | Sets an attribute (property/method) | `class C: pass; c = C(); setattr(c, 'attr', 10)` |
| `slice()`  | Returns a slice object | `slice(1, 5)` |
| `sorted()` | Returns a sorted list | `sorted([3, 1, 2])  # Output: [1, 2, 3]` |
| `staticmethod()` | Converts a method into a static method | `class C: @staticmethod def method(): pass` |
| `str()`    | Returns a string object | `str(10)  # Output: '10'` |
| `sum()`    | Sums the items of an iterable | `sum([1, 2, 3])  # Output: 6` |
| `super()`  | Returns an object that represents the parent class | `class B: pass; class C(B): def method(self): super().method()` |
| `tuple()`  | Returns a tuple | `tuple([1, 2, 3])  # Output: (1, 2, 3)` |
| `type()`   | Returns the type of an object | `type(5)  # Output: <class 'int'>` |
| `vars()`   | Returns the __dict__ attribute of an object | `class C: pass; c = C(); vars(c)` |
| `zip()`    | Returns an iterator of tuples | `zip([1, 2, 3], ['a', 'b', 'c'])` |

These examples demonstrate how to use each built-in function in Python. For more detailed information, you can refer to the [Python official documentation](https://docs.python.org/3/library/functions.html).

- [Built-in Functions](https://docs.python.org/3/library/functions.html)
