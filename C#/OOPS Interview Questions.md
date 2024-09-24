# Top 60 OOPS Interview Questions

### Q1. **What are the advantages of OOPS?**

- Encapsulation: Bundling data and methods that operate on the data within one unit (class).
- Abstraction: Hiding complex implementation details.
- Inheritance: Reusing existing code by inheriting properties from another class.
- Polymorphism: Ability to process objects differently based on their class types.

### Q2. **What are the limitations of OOPS?**

- OOP concepts can lead to overly complex designs if not handled properly.
- Slower performance compared to procedural programming due to abstraction and overhead.
- Not always suitable for small problems or simple tasks.

---

### Q3. **What are the different types of Inheritance?**

- Single Inheritance
- Multilevel Inheritance
- Hierarchical Inheritance
- Multiple Inheritance (C# supports this via Interfaces)

```csharp
// Example of Single Inheritance
public class Parent {
    public void ParentMethod() {
        Console.WriteLine("This is the parent method.");
    }
}

public class Child : Parent {
    public void ChildMethod() {
        Console.WriteLine("This is the child method.");
    }
}
```

---

### Q4. **How to prevent a class from being Inherited?**

Use the `sealed` keyword.

```csharp
public sealed class FinalClass {
    public void Method() {
        Console.WriteLine("This class cannot be inherited.");
    }
}
```

---

### Q5. **What is Polymorphism and what are its types?**

Polymorphism allows objects of different classes to be treated as objects of a common base class.

- **Compile-time Polymorphism** (Method Overloading)
- **Run-time Polymorphism** (Method Overriding)

```csharp
// Method Overloading (Compile-time Polymorphism)
public class Example {
    public void Show(int x) {
        Console.WriteLine("Int method: " + x);
    }

    public void Show(string s) {
        Console.WriteLine("String method: " + s);
    }
}
```

---

### Q6. **What is Method Overloading?**

Method Overloading allows multiple methods in the same class with the same name but different parameters.

Ways to overload:
1. Change the number of parameters.
2. Change the type of parameters.

```csharp
public class OverloadingExample {
    public void Add(int a, int b) {
        Console.WriteLine(a + b);
    }

    public void Add(double a, double b) {
        Console.WriteLine(a + b);
    }
}
```

---

### Q7. **What is the difference between Overloading and Overriding?**

- **Overloading**: Same method name with different parameter types in the same class.
- **Overriding**: Redefining a method from the parent class in the child class.

```csharp
// Overriding Example
public class Parent {
    public virtual void Show() {
        Console.WriteLine("Parent Show");
    }
}

public class Child : Parent {
    public override void Show() {
        Console.WriteLine("Child Show");
    }
}
```

---

### Q8. **What is the difference between an Abstract class and an Interface?**

| Abstract Class | Interface |
|----------------|-----------|
| Can have method implementations | Cannot have method implementations |
| Can have fields | Cannot have fields |
| Single inheritance allowed | Multiple inheritance allowed |
| Can have access modifiers | All members are public by default |

---

### Q9. **When to use Interface and when Abstract class?**

- Use **Interface** when you need multiple inheritance or when you need to define a contract that multiple classes must follow.
- Use **Abstract Class** when you want to provide a base class with some shared functionality.

---

### Q10. **Why create Interfaces?**

Interfaces define a contract. They ensure that all implementing classes provide certain functionality, promoting loose coupling.

---

### Q11. **Do Interfaces have a Constructor?**

No, interfaces cannot have constructors because they cannot hold state.

---

### Q12. **Can you create an instance of an Abstract class or an Interface?**

No, you cannot instantiate an abstract class or interface directly.

---

### Q13. **What is the difference between “out” and “ref” parameters?**

- **ref**: The variable must be initialized before passing.
- **out**: The variable does not need to be initialized before passing, but it must be initialized inside the method.

```csharp
public void Example(ref int a, out int b) {
    a += 10;
    b = 20;
}
```

---

### Q14. **What is the purpose of “params” keyword?**

The `params` keyword allows passing a variable number of arguments.

```csharp
public void PrintNumbers(params int[] numbers) {
    foreach (int number in numbers) {
        Console.WriteLine(number);
    }
}
```

---

### Q15. **What are Access Specifiers? What is the default access modifier in a class?**

- **Access Specifiers** define the accessibility of a class or its members (public, private, protected, internal).
- Default access modifier for a class is `internal`.

---

### Q16. **How to implement Exception Handling in C#?**

Use `try`, `catch`, and `finally`.

```csharp
try {
    int result = 10 / 0;
} catch (DivideByZeroException ex) {
    Console.WriteLine("Cannot divide by zero.");
} finally {
    Console.WriteLine("Cleanup code.");
}
```

---

### Q17. **Can we execute multiple Catch blocks?**

Yes, you can have multiple catch blocks for different exception types.

---

### Q18. **What is a Finally block and give an example when to use it?**

The `finally` block is used for cleanup code that must be executed regardless of whether an exception occurred.

---

### Q19. **Can we have only “Try” block without “Catch” block?**

Yes, but you must have a `finally` block.

---

### Q20. **What is the difference between “throw ex” and “throw”?**

- `throw ex`: Re-throws the original exception but resets the stack trace.
- `throw`: Re-throws the original exception without resetting the stack trace.

---

### Q21. **What are the Loop types in C#?**

- `for`
- `foreach`
- `while`
- `do-while`

---

### Q22. **What is the difference between “continue” and “break” statement?**

- `continue`: Skips the current iteration and moves to the next iteration.
- `break`: Exits the loop immediately.

---

### Q23. **What is the difference between Array and ArrayList?**

- Array: Fixed size, can hold elements of a specific type.
- ArrayList: Dynamic size, can hold elements of any type.

---

### Q24. **What is the difference between ArrayList and Hashtable?**

- ArrayList: Holds a collection of items in sequence.
- Hashtable: Holds key-value pairs.

---

### Q25. **What is “this” keyword in C#? When to use it?**

The `this` keyword refers to the current instance of the class.

---

### Q26. **What is the purpose of “using” keyword in C#?**

- **using**: Ensures the disposal of resources like file handles or database connections after use.

```csharp
using (StreamReader sr = new StreamReader("file.txt")) {
    string content = sr.ReadToEnd();
}
```

---

Would you like me to continue with the rest of the questions or focus on a specific area?
