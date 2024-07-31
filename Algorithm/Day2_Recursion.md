# Recursion

### 1: Introduction to Recursion
- **Definition of Recursion:** A technique where a function calls itself to solve subproblems of a larger problem.
- **Basic Principles of Recursive Functions:**
  - **Example:** Computing the factorial of a number.
  - **Python Code:**
    ```python
    def factorial(n):
        if n == 0:
            return 1
        else:
            return n * factorial(n - 1)
    ```
  - **Call Stack Illustration:**
    ```
    factorial(3)
      ↳ factorial(2)
        ↳ factorial(1)
          ↳ factorial(0)
              returns 1
          returns 1*1 = 1
        returns 2*1 = 2
      returns 3*2 = 6
    ```

### 2: Understanding Recursive Functions
- **Mechanics of Recursion:**
  - **Explanation of Stack Use:** Each recursive call adds a layer to the call stack.
  - **Tracing Recursive Calls:**
    - **Python Code for Fibonacci Numbers:**
      ```python
      def fibonacci(n):
          if n <= 1:
              return n
          else:
              return fibonacci(n-1) + fibonacci(n-2)
      ```
    - **Call Stack for `fibonacci(3)`:**
      ```
      fibonacci(3)
        ↳ fibonacci(2)
            ↳ fibonacci(1)
                returns 1
            ↳ fibonacci(0)
                returns 0
            returns 1 + 0 = 1
        ↳ fibonacci(1)
            returns 1
        returns 1 + 1 = 2
      ```

### 3: Implementing Recursion in Programming
- **Recursive Programming Examples:**
  - **Example: Reverse a string using recursion**
  - **Python Code:**
    ```python
    def reverse_string(s):
        if len(s) == 0:
            return s
        else:
            return reverse_string(s[1:]) + s[0]
    ```
  - **Call Stack Illustration:**
    ```
    reverse_string("hello")
      ↳ reverse_string("ello") + "h"
        ↳ reverse_string("llo") + "e"
          ↳ reverse_string("lo") + "l"
            ↳ reverse_string("o") + "l"
              ↳ reverse_string("") + "o"
                  returns ""
              returns "o"
            returns "ol"
          returns "oll"
        returns "olle"
      returns "olleh"
    ```

### 4: Advanced Recursive Techniques
- **Tail Recursion:** Discusses how tail recursion is optimized in some languages.
  - **Python Code for Tail Recursive Factorial:**
    ```python
    def factorial(n, acc=1):
        if n == 0:
            return acc
        else:
            return factorial(n-1, n*acc)
    ```
  - **Call Stack:**
    ```
    factorial(3)
      ↳ factorial(2, 3)
        ↳ factorial(1, 6)
          ↳ factorial(0, 6)
              returns 6
    ```

### 5: Recursion vs. Iteration
- **Converting Recursive Functions to Iterative Functions:**
  - **Example: Iterative vs. Recursive Factorial**
  - **Iterative Python Code:**
    ```python
    def factorial_iterative(n):
        result = 1
        for i in range(2, n+1):
            result *= i
        return result
    ```
  - **Comparative Call Flow:** No call stack for the iterative version, demonstrating the difference in memory usage.

### 6: Practical Applications and Limitations of Recursion
- **Real-world Applications:** Sorting algorithms like QuickSort and MergeSort.
- **Limitations of Recursion:**
  - **Python Code Example for Deep Recursion:**
    ```python
    def deep_recursion(n):
        if n == 0:
            return "Base case"
        else:
            return deep_recursion(n-1)
    ```
  - **Call Stack Overflow Example:** Explanation of how deep recursion can lead to stack overflow errors, especially if the base case is not reached or recursion is too deep.

This detailed breakdown with code examples and visual call stacks in markdown should help new programmers better understand how recursion works, how to implement it, and how to trace it effectively.

-----

### Recommend Resources:
**Recursion Full course BY ABDUL BARI from RAKIB**
[![Recursion Full course BY ABDUL BARI from RAKIB](https://img.youtube.com/vi/ETiZpSajasI/maxresdefault.jpg)](https://youtu.be/ETiZpSajasI)

