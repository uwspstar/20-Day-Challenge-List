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

Sure! Let's continue with the rest of the questions.

---

### Q27. **What is the difference between “is” and “as” operators?**

- `is`: Checks if an object is of a specific type and returns a boolean.
- `as`: Tries to cast an object to a specific type and returns `null` if the cast fails.

```csharp
object obj = "Hello";
if (obj is string) {
    Console.WriteLine("obj is a string");
}

string str = obj as string;
if (str != null) {
    Console.WriteLine("obj was cast to string");
}
```

---

### Q28. **What is the difference between “Readonly” and “Constant” variables?**

| **Readonly** | **Constant** |
|--------------|--------------|
| Can be initialized either at the time of declaration or in a constructor. | Must be initialized at the time of declaration. |
| Value can be different for different objects. | Value is the same for all instances. |
| Evaluated at runtime. | Evaluated at compile-time. |

```csharp
public class Example {
    public const int ConstantValue = 10;
    public readonly int ReadonlyValue;

    public Example(int value) {
        ReadonlyValue = value;  // Can assign in constructor
    }
}
```

---

### Q29. **What is Boxing and Unboxing?**

- **Boxing**: Converting a value type to a reference type (like converting an `int` to `object`).
- **Unboxing**: Extracting the value type from the object.

```csharp
int x = 10;
object obj = x;  // Boxing
int y = (int)obj;  // Unboxing
```

---

### Q30. **What is the difference between “String” and “StringBuilder”? When to use what?**

- **String**: Immutable, meaning every modification creates a new string object.
- **StringBuilder**: Mutable, optimized for modifying the string content without creating new objects.

Use `StringBuilder` when you need to perform frequent modifications on the string.

```csharp
// Using String (Inefficient for multiple changes)
string s = "Hello";
s += " World";

// Using StringBuilder (Efficient)
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World");
```

---

### Q31. **What are Nullable types?**

Nullable types allow a value type (like `int`, `bool`) to hold a null value.

```csharp
int? nullableInt = null;
nullableInt = 10;
```

---

### Q32. **What are the important components of the .NET framework? What are their roles?**

- **CLR (Common Language Runtime)**: Manages execution of .NET programs.
- **BCL (Base Class Library)**: Provides basic libraries like collections, IO, threading, etc.
- **ASP.NET**: Framework for building web applications.
- **ADO.NET**: Data access framework.

---

### Q33. **What is an Assembly? What are the different types of assembly in .NET?**

An **Assembly** is a compiled code library used for deployment, versioning, and security.

Types of Assemblies:
- **Private Assembly**: Used by a single application.
- **Shared Assembly**: Stored in the Global Assembly Cache (GAC) and can be used by multiple applications.

---

### Q34. **What is GAC?**

GAC (Global Assembly Cache) is used to store shared assemblies that multiple .NET applications can use.

---

### Q35. **What is Garbage Collection(GC)?**

Garbage Collection in .NET is the process of automatically managing memory by reclaiming the memory occupied by objects that are no longer in use.

---

### Q36. **Can we force Garbage Collector to run?**

Yes, you can force it using `GC.Collect()`, but it's generally not recommended as the GC is optimized for performance.

```csharp
GC.Collect();
```

---

### Q37. **What is the difference between Process and Thread?**

- **Process**: An independent program with its own memory space.
- **Thread**: A unit of execution within a process, sharing memory with other threads of the same process.

---

### Q38. **Explain Multithreading.**

Multithreading allows multiple threads to run concurrently within a process, sharing the process's resources but executing independently.

```csharp
public class ThreadExample {
    public static void PrintNumbers() {
        for (int i = 1; i <= 5; i++) {
            Console.WriteLine(i);
            Thread.Sleep(1000); // Pause for 1 second
        }
    }

    public static void Main() {
        Thread t = new Thread(PrintNumbers);
        t.Start();
    }
}
```

---

### Q39. **What is Reflection?**

Reflection in C# allows inspecting metadata about types at runtime and dynamically invoking methods or accessing properties.

```csharp
Type type = typeof(string);
MethodInfo methodInfo = type.GetMethod("Substring");
Console.WriteLine(methodInfo.Invoke("Hello", new object[] { 2 }));
```

---

### Q40. **What is MVC (Model View Controller)? Explain MVC Life cycle.**

MVC is a design pattern for developing web applications:
- **Model**: Represents the data.
- **View**: UI representation of the data.
- **Controller**: Handles user input and updates the model and view accordingly.

---

### Q41. **What are the advantages of MVC over Web Forms?**

1. Separation of concerns (Model, View, and Controller).
2. More control over HTML, JavaScript, and CSS.
3. Support for Test-Driven Development (TDD).

---

### Q42. **What are the different return types of a controller Action method?**

- `View()`
- `PartialView()`
- `Json()`
- `RedirectToAction()`
- `File()`
- `Content()`

---

### Q43. **What are Filters and their types in MVC?**

Filters are used to execute code before or after specific stages in the request processing pipeline.

Types:
- **Authorization Filter**
- **Action Filter**
- **Result Filter**
- **Exception Filter**

---

### Q44. **What is Authentication and Authorization in ASP.NET MVC?**

- **Authentication**: Verifying the user's identity.
- **Authorization**: Checking if the authenticated user has access to specific resources.

---

### Q45. **What are the types of Authentication in ASP.NET MVC?**

- **Forms Authentication**
- **Windows Authentication**
- **OAuth/OpenID Authentication**
- **Token-Based Authentication**

---

### Q46. **What is Output Caching in MVC? How to implement it?**

Output Caching stores the generated output of a controller action to serve subsequent requests from the cache instead of executing the action again.

```csharp
[OutputCache(Duration = 60)]
public ActionResult Index() {
    return View();
}
```

---

### Q47. **What is the difference between ViewData, ViewBag, and TempData?**

| **ViewData** | **ViewBag** | **TempData** |
|--------------|-------------|--------------|
| Dictionary-based | Dynamic property | Dictionary-based |
| Available for the current request only | Available for the current request only | Available across requests |
| Requires casting | No casting required | Requires casting |

---

### Q48. **How can we pass data from the controller to the view in MVC?**

You can pass data using `ViewData`, `ViewBag`, `TempData`, or model binding.

---

### Q49. **What is Partial View?**

A Partial View is a reusable view component that can be embedded inside other views.

```csharp
@Html.Partial("_PartialViewName")
```

---

### Q50. **What are Areas in MVC?**

Areas allow you to divide large applications into smaller functional units, with each area containing its own controllers, views, and models.

---

### Q51. **How does Validation work in MVC?**

Validation can be implemented using Data Annotations or custom validation logic in the Model. It ensures that the data submitted by the user meets the defined criteria.

```csharp
public class UserModel {
    [Required]
    public string Name { get; set; }
}
```

---

### Q52. **Explain the concept of MVC Scaffolding.**

Scaffolding is a code generation framework for automatically generating code for CRUD operations based on the model.

---

### Q53. **What is Bundling and Minification in MVC?**

Bundling and Minification improve the performance of web applications by combining multiple files into one (bundling) and reducing their size (minification).

---

### Q54. **How to implement Security in web applications in MVC?**

Implement security by:
- Using HTTPS
- Applying Authorization filters
- Implementing input validation
- Using Anti-Forgery tokens

```csharp
@Html.AntiForgeryToken()
```

---

### Q55. **What are the events in Page Life Cycle? In which event are the controls fully loaded?**

Key Events:
1. `PreInit`
2. `Init`
3. `InitComplete`
4. `Load`
5. `LoadComplete`
6. `PreRender`
7. `Unload`

Controls are fully loaded in the `Load` event.

---

### Q56. **What is the difference between Server.Transfer() and Response.Redirect()?**

- **Server.Transfer()**: Transfers the execution to another page on the server without changing the URL.
- **Response.Redirect()**: Redirects the user to another page by making a new request to the server, changing the URL.

---

### Q57. **Where is the ViewState stored after the page postback?**

ViewState is stored in a hidden field in

 the page.

---

### Q58. **What are the different types of Caching?**

- **Output Caching**
- **Data Caching**
- **Object Caching**

---

### Q59. **What are the different Session state management options available in ASP.NET?**

- **In-Process**
- **State Server**
- **SQL Server**
- **Custom Session State Provider**

---

### Q60. **What are the main components of ADO.NET?**

- **Connection**: Represents a connection to the database.
- **Command**: Used to execute commands on the database.
- **DataReader**: Reads data in a forward-only stream.
- **DataAdapter**: Fills a DataSet and updates the database.
