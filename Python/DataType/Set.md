
#### Python Sets
- https://www.w3schools.com/python/python_sets.asp

- In Python, a set is a collection of unique elements, and it is an unordered and unindexed collection of items. 
- `Set` is one of 4 built-in data types in Python used to store collections of data, the other 3 are List, Tuple, and Dictionary, all with different qualities and usage.

**A set is a collection which is unordered, unchangeable*, and unindexed.**
- `Unordered` means that the items in a set do not have a defined order. Set items can appear in a different order every time you use them, and cannot be referred to by index or key.
- Set items are `unchangeable`, meaning that we cannot change the items after the set has been created. Once a set is created, you cannot change its items, but you can remove items and add new items.
- The values True and 1 are considered the same value in sets, and are treated as duplicates. The values False and 0 are considered the same value in sets, and are treated as duplicates.

#### Definition and Creation
**Definition:** 
- A set is defined by placing all the elements inside curly braces `{}`, separated by commas.
- Sets can store all forms of data, such as strings, integers, floats, and even a combination of different data types.
- It's important to note that sets do not allow duplicate elements.

**Example:**
```python
# Creating a set
my_set = {1, 2, 3, 4, 5}
print(my_set)  # Output: {1, 2, 3, 4, 5}
```

#### Operations and Methods
**Operations:**
- Sets can be used to perform various set operations such as union, intersection, difference, and more.
- These operations are useful for comparing and manipulating sets.

**Example:**
```python
# Set operations
set1 = {1, 2, 3}
set2 = {3, 4, 5}
print(set1.union(set2))  # Output: {1, 2, 3, 4, 5}
print(set1.intersection(set2))  # Output: {3}
print(set1.difference(set2))  # Output: {1, 2}
```


**Methods:**
- Python provides built-in methods for sets, such as `add()`, `remove()`, `clear()`, and more, to manipulate and perform operations on sets.

**Example:**
```python
# Set methods
my_set.add(6)  # Adds an element to the set
my_set.remove(3)  # Removes a specific element from the set
print(my_set)  # Output: {1, 2, 4, 5, 6}
```


#### Advantages and Comparison
**Advantages:**
- Sets internally make use of a data structure called a hash table, which provides highly optimized methods for checking whether a specific element is contained in the set or not.
- Sets are unordered and do not allow duplicate elements, making them efficient for certain operations.

**Comparison:**
- Compared to other data structures like lists and tuples, sets have the advantage of faster element lookup due to their internal implementation using hash tables.

**Example:**
```python
# Set advantage and comparison
# Faster element lookup in sets compared to lists
my_list = [1, 2, 3, 4, 5]
my_set = {1, 2, 3, 4, 5}
print(3 in my_list)  # Output: True
print(3 in my_set)  # Output: True

# Creating sets
set_a = {1, 2, 3, 4}
set_b = {3, 4, 5, 6}

# Adding an element
set_a.add(5)

# Removing an element
set_b.remove(6)

# Union of two sets
union_set = set_a | set_b  # or set_a.union(set_b)

# Intersection of two sets
intersection_set = set_a & set_b  # or set_a.intersection(set_b)

# Difference of two sets
difference_set = set_a - set_b  # or set_a.difference(set_b)

print("Set A:", set_a)
print("Set B:", set_b)
print("Union:", union_set)
print("Intersection:", intersection_set)
print("Difference:", difference_set)
```

| Method                     | Shortcut | Description                                                       |
|----------------------------|----------|-------------------------------------------------------------------|
| `add()`                    |          | Adds an element to the set                                        |
| `clear()`                  |          | Removes all the elements from the set                             |
| `copy()`                   |          | Returns a copy of the set                                        |
| `difference()`             | -        | Returns a set containing the difference between two or more sets |
| `difference_update()`      | -=       | Removes the items in this set that are also included in another, specified set |
| `discard()`                |          | Removes the specified item                                        |
| `intersection()`           | &        | Returns a set that is the intersection of two other sets        |
| `intersection_update()`    | &=       | Removes the items in this set that are not present in other, specified set(s) |
| `isdisjoint()`            |          | Returns whether two sets have an intersection or not             |
| `issubset()`              | <=       | Returns whether another set contains this set or not             |
|                            | <        | Returns whether all items in this set are present in other, specified set(s) |
| `issuperset()`            | >=       | Returns whether this set contains another set or not             |
|                            | >        | Returns whether all items in other, specified set(s) are present in this set |
| `pop()`                    |          | Removes an element from the set                                   |
| `remove()`                 |          | Removes the specified element                                      |
| `symmetric_difference()`   | ^        | Returns a set with the symmetric differences of two sets        |
| `symmetric_difference_update()` | ^=   | Inserts the symmetric differences from this set and another      |
| `union()`                  | |        | Returns a set containing the union of sets                       |
| `update()`                 | |=       | Updates the set with the union of this set and others           |

#### Python Collections (Arrays)
There are four collection data types in the Python programming language:

- `List` is a collection which is ordered and changeable. Allows duplicate members.
- `Tuple` is a collection which is ordered and unchangeable. Allows duplicate members.
- `Set` is a collection which is unordered, unchangeable*, and unindexed. No duplicate members.
- `Dictionary` is a collection which is ordered** and changeable. No duplicate members.
