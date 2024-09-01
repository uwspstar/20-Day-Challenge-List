### `Optional`

```python
from typing import Optional

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2:Optional[ListNode]):
```

The `Optional` type hint is part of the `typing` module in Python and is used to indicate that a value could either be of a specific type or `None`. It provides a way to specify that a parameter or return value can be either a specific type or `None`, making the code more expressive and easier to understand.

1. **Purpose**: 
   - `Optional[X]` is a shorthand for `Union[X, None]`. It indicates that a variable can be of type `X` or it can be `None`.

2. **Usage**:
   - It’s commonly used in function signatures and class attributes to explicitly declare that a value may not always be present (i.e., it could be `None`).

### Syntax and Examples

Here’s a deeper look into how `Optional` works with examples:

1. **Basic Example**:
   ```python
   from typing import Optional

   def find_item(index: int) -> Optional[str]:
       items = ["apple", "banana", "cherry"]
       if 0 <= index < len(items):
           return items[index]
       else:
           return None
   ```

   In this example, the function `find_item` returns a `str` if the index is valid; otherwise, it returns `None`. The type hint `Optional[str]` specifies that the return type could either be a string or `None`.

2. **Class Example**:
   ```python
   from typing import Optional

   class Person:
       def __init__(self, name: str, age: Optional[int] = None):
           self.name = name
           self.age = age
   ```

   In this `Person` class, the `age` attribute is type-hinted as `Optional[int]`, meaning `age` can be an integer or `None`. This is useful for cases where an age might not be provided.

### Detailed Explanation

- **`Union`**:
  - `Optional[X]` is essentially a convenience for `Union[X, None]`. The `Union` type hint allows for specifying multiple possible types. For example, `Union[int, None]` means a value could be an integer or `None`.

- **Practical Use Cases**:
  - **Function Parameters**: When a function parameter can be optionally provided or might be absent.
  - **Function Return Types**: When a function might return a value of a certain type or `None` if the value is not available.
  - **Class Attributes**: When attributes in a class might be assigned a certain type or remain `None` if not yet set.

### More Examples

**Function with `Optional` Parameter**:
```python
from typing import Optional

def greet(name: Optional[str] = None) -> str:
    if name is None:
        return "Hello, Guest!"
    else:
        return f"Hello, {name}!"
```

In this function, `name` is optional. If `name` is not provided (i.e., `None`), it defaults to a generic greeting.

**Optional with Custom Types**:
```python
from typing import Optional

class ListNode:
    def __init__(self, val=0, next: Optional['ListNode'] = None):
        self.val = val
        self.next = next
```

Here, `next` is an optional parameter of type `ListNode`, allowing it to be `None` if there is no subsequent node.

### Summary

- **`Optional[X]`**: A shorthand for `Union[X, None]`, used to denote that a value could be of type `X` or `None`.
- **Enhances Code Readability**: Makes it clear that a value might not be present.
- **Helps with Type Checking**: Useful for static type checkers like `mypy` to ensure that functions and methods handle cases where a value could be `None`.

By using `Optional`, you make your code more robust and self-documenting, making it clear that certain values may be absent or not initialized.
