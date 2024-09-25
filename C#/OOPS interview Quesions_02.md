# OOPS interview Quesions

### 1. **What are the main concepts of OOPS? What are classes and objects?**

**Explanation**:  
- **Classes** define the blueprint for creating objects, encapsulating data for the object and the methods to manipulate that data.  
- **Objects** are instances of classes.

```csharp
// Example of a class and object in C#
public class Car
{
    public string model;
    public int year;

    public void DisplayInfo()
    {
        Console.WriteLine("Car: " + model + ", Year: " + year);
    }
}

// Creating an object from the class
Car myCar = new Car();
myCar.model = "Toyota";
myCar.year = 2020;
myCar.DisplayInfo();  // Output: Car: Toyota, Year: 2020
```

### 2. **What is Inheritance? Why is Inheritance important?**

**Explanation**:  
Inheritance allows a class to inherit fields and methods from another class. It promotes reusability and the creation of hierarchical relationships.

```csharp
// Example of Inheritance
public class Vehicle
{
    public string brand = "Ford";
}

public class Car : Vehicle  // Car inherits from Vehicle
{
    public string model = "Mustang";
}

Car myCar = new Car();
Console.WriteLine(myCar.brand + " " + myCar.model);  // Output: Ford Mustang
```

### 3. **What are the different types of Inheritance?**

**Explanation**:  
The different types of inheritance include:
- Single Inheritance
- Multilevel Inheritance
- Multiple Inheritance (not supported in C# directly but through interfaces)
- Hierarchical Inheritance

```csharp
// Multilevel Inheritance
public class Animal
{
    public void Eat() => Console.WriteLine("Eating");
}

public class Mammal : Animal
{
    public void Walk() => Console.WriteLine("Walking");
}

public class Human : Mammal
{
    public void Speak() => Console.WriteLine("Speaking");
}

Human person = new Human();
person.Eat();  // Inherited from Animal
person.Walk(); // Inherited from Mammal
person.Speak(); // Method of Human
```

### 4. **How to prevent a class from being inherited?**

**Explanation**:  
In C#, you can use the `sealed` keyword to prevent a class from being inherited.

```csharp
// Sealed class
public sealed class FinalClass
{
    public void Display() => Console.WriteLine("This class cannot be inherited.");
}

// The following would cause an error:
// public class DerivedClass : FinalClass { }
```

### 5. **What is Abstraction?**

**Explanation**:  
Abstraction hides implementation details and only shows the essential features of an object. It is achieved using abstract classes or interfaces.

```csharp
// Example of Abstraction
public abstract class Shape
{
    public abstract void Draw();  // Abstract method
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a circle.");
}

Shape myShape = new Circle();
myShape.Draw();  // Output: Drawing a circle
```

### 6. **What is Encapsulation?**

**Explanation**:  
Encapsulation is the concept of wrapping data (variables) and methods (functions) into a single unit. It restricts access to some of the object's components.

```csharp
// Example of Encapsulation
public class Account
{
    private double balance;  // private field

    public void SetBalance(double amount)  // public method to set value
    {
        if (amount > 0) balance = amount;
    }

    public double GetBalance() => balance;  // public method to get value
}

Account myAccount = new Account();
myAccount.SetBalance(500);
Console.WriteLine(myAccount.GetBalance());  // Output: 500
```

### 7. **What is Polymorphism and what are its types?**

**Explanation**:  
Polymorphism allows objects of different types to be treated as objects of a common base type. The two types are:
1. **Compile-time polymorphism** (method overloading)
2. **Runtime polymorphism** (method overriding)

```csharp
// Example of Runtime Polymorphism (Method Overriding)
public class Animal
{
    public virtual void Sound() => Console.WriteLine("Animal sound");
}

public class Dog : Animal
{
    public override void Sound() => Console.WriteLine("Bark");
}

Animal myDog = new Dog();
myDog.Sound();  // Output: Bark
```

### 8. **What is Method Overloading? In how many ways can a method be overloaded?**

**Explanation**:  
Method overloading allows you to have multiple methods in the same class with the same name but different parameters.

```csharp
// Example of Method Overloading
public class Calculator
{
    public int Add(int a, int b) => a + b;  // Method with two parameters
    public int Add(int a, int b, int c) => a + b + c;  // Method with three parameters
}

Calculator calc = new Calculator();
Console.WriteLine(calc.Add(2, 3));  // Output: 5
Console.WriteLine(calc.Add(2, 3, 4));  // Output: 9
```

### 9. **What is the difference between Overloading and Overriding?**

**Explanation**:  
- **Overloading** is when multiple methods have the same name but different signatures in the same class.
- **Overriding** is when a subclass provides a specific implementation of a method that is already defined in its superclass.

```csharp
// Overloading (same class, different signatures)
public class Printer
{
    public void Print(string msg) => Console.WriteLine(msg);
    public void Print(int msg) => Console.WriteLine(msg);
}

// Overriding (derived class overrides base class method)
public class BasePrinter
{
    public virtual void Print() => Console.WriteLine("Base Printer");
}

public class AdvancedPrinter : BasePrinter
{
    public override void Print() => Console.WriteLine("Advanced Printer");
}
```

Let me know if you would like me to continue explaining the other questions with more code examples!

### 10. **What is the difference between Method Overriding and Method Hiding?**

**Explanation**:  
- **Method Overriding**: Occurs when a derived class defines a method with the same name, return type, and parameters as a method in its base class using the `override` keyword.
- **Method Hiding**: Uses the `new` keyword to hide a base class method in a derived class.

```csharp
// Method Overriding
public class BaseClass
{
    public virtual void Display() => Console.WriteLine("BaseClass Display");
}

public class DerivedClass : BaseClass
{
    public override void Display() => Console.WriteLine("DerivedClass Display");
}

BaseClass obj = new DerivedClass();
obj.Display();  // Output: DerivedClass Display

// Method Hiding
public class AnotherDerivedClass : BaseClass
{
    public new void Display() => Console.WriteLine("AnotherDerivedClass Display");
}

BaseClass obj2 = new AnotherDerivedClass();
obj2.Display();  // Output: BaseClass Display (Base method is called)
```

### 11. **What are the advantages and limitations of OOPS?**

**Explanation**:  
**Advantages**:
- Reusability
- Modularity
- Encapsulation
- Easy to maintain and modify
- Inheritance and Polymorphism promote flexibility

**Limitations**:
- More complexity
- Larger memory footprint
- Slower execution compared to procedural programming for simple tasks

### 12. **What is the difference between an Abstract class and an Interface (at least 4)?**

**Explanation**:  
1. **Abstract class**: Can have method implementations, but an **Interface** cannot.
2. **Abstract class**: Can have fields, while an **Interface** cannot.
3. **Abstract class**: Supports access modifiers, but all members of an **Interface** are public.
4. **Abstract class**: Inherits using the `extends` keyword; **Interface** uses `implements`.

```csharp
// Abstract Class Example
public abstract class Animal
{
    public abstract void Speak();
    public void Walk() => Console.WriteLine("Walking");
}

// Interface Example
public interface IFlyable
{
    void Fly();
}
```

### 13. **When to use Interface and when Abstract class?**

**Explanation**:  
- **Interface**: Use when you need multiple classes to implement specific behavior that is unrelated (like flying or swimming).
- **Abstract class**: Use when multiple related classes need to share common behavior (like an Animal class where all animals have legs).

### 14. **Why even create Interfaces?**

**Explanation**:  
Interfaces allow different classes to implement the same set of methods, which promotes loose coupling and polymorphism.

### 15. **Can an Interface have a Constructor?**

**Explanation**:  
No, interfaces cannot have constructors because they cannot store state. Constructors are used to initialize objects, but an interface does not have any implementation.

### 16. **Can you create an instance of an Abstract class or an Interface?**

**Explanation**:  
No, you cannot create instances of either an abstract class or an interface directly. You can only instantiate concrete subclasses or implementors.

```csharp
// The following will cause an error:
// Animal animal = new Animal();  // Cannot instantiate abstract class
```

### 17. **What are Access Specifiers? What is the default access modifier in a class?**

**Explanation**:  
Access specifiers control the visibility of class members. In C#, the default access specifier is **`private`** for class members and **`internal`** for classes.

```csharp
public class MyClass
{
    private int privateField;  // Only accessible within the class
    public int publicField;    // Accessible everywhere
    protected int protectedField;  // Accessible in derived classes
}
```

### 18. **What is Boxing and Unboxing?**

**Explanation**:  
- **Boxing**: Converting a value type to a reference type.
- **Unboxing**: Extracting a value type from a reference type.

```csharp
int num = 123;
object obj = num;  // Boxing
int unboxedNum = (int)obj;  // Unboxing
```

### 19. **What is the difference between `String` and `StringBuilder`? When to use each?**

**Explanation**:  
- **String** is immutable, meaning once it’s created, its value cannot be changed.
- **StringBuilder** is mutable, meaning you can modify its content without creating new objects. Use `StringBuilder` when concatenating large numbers of strings.

```csharp
// String (Immutable)
string str = "Hello";
str += " World";  // Creates a new string object

// StringBuilder (Mutable)
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World");  // Modifies the same object
Console.WriteLine(sb);  // Output: Hello World
```

### 20. **What are the basic string operations in C#?**

**Explanation**:  
- **Length**: Gets the length of the string.
- **IndexOf()**: Finds the index of a substring.
- **Substring()**: Retrieves part of the string.
- **Replace()**: Replaces characters in a string.

```csharp
string text = "Hello, World!";
Console.WriteLine(text.Length);  // Output: 13
Console.WriteLine(text.IndexOf("World"));  // Output: 7
Console.WriteLine(text.Substring(0, 5));  // Output: Hello
Console.WriteLine(text.Replace("World", "C#"));  // Output: Hello, C#
```

### 21. **What are Nullable types?**

**Explanation**:  
Nullable types allow value types to represent `null`.

```csharp
int? nullableInt = null;
if (nullableInt.HasValue)
{
    Console.WriteLine(nullableInt.Value);
}
else
{
    Console.WriteLine("No value");
}
```

### 22. **Explain Generics in C#. When and why to use them?**

**Explanation**:  
Generics allow you to define a class or method with a placeholder for the data type. This promotes type safety and reusability.

```csharp
// Generic class example
public class GenericClass<T>
{
    public T value;
    public void Display(T item) => Console.WriteLine(item);
}

GenericClass<int> myInt = new GenericClass<int>();
myInt.Display(100);  // Output: 100

GenericClass<string> myString = new GenericClass<string>();
myString.Display("Hello Generics");  // Output: Hello Generics
```

### 23. **How to implement Exception Handling in C#?**

**Explanation**:  
Exception handling in C# is implemented using `try`, `catch`, `finally` blocks.

```csharp
try
{
    int x = 0;
    int y = 100 / x;  // Will throw a DivideByZeroException
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Cannot divide by zero!");
}
finally
{
    Console.WriteLine("This block always executes.");
}
```

### 24. **Can we execute multiple Catch blocks?**

**Explanation**:  
Yes, you can have multiple `catch` blocks to handle different exceptions.

```csharp
try
{
    // Some code that throws exceptions
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("DivideByZeroException caught!");
}
catch (Exception ex)
{
    Console.WriteLine("Generic exception caught!");
}
```

### 25. **What is a Finally block and give an example when to use it?**

**Explanation**:  
The `finally` block contains code that is always executed, regardless of whether an exception was thrown.

```csharp
try
{
    // Code that may throw an exception
}
catch
{
    // Handle exception
}
finally
{
    // Clean-up code (e.g., closing a file or releasing resources)
    Console.WriteLine("Finally block executed.");
}
```

### 26. **Can we have only a "Try" block without a "Catch" block?**

**Explanation**:  
Yes, but you must include a `finally` block if no `catch` is provided.

```csharp
try
{
    // Code that may throw an exception
}
finally
{
    // Clean-up code
}
```

### 27. **What is the difference between `throw ex` and `throw`?**

**Explanation**:  
- **`throw ex`**: Resets the stack trace, hiding the original error location.
- **`throw`**: Preserves the original stack trace, providing accurate error information.

```csharp
try
{
    throw new Exception("Something went wrong!");
}
catch (Exception ex)
{
    // throw ex;  // Resets the stack trace
    throw;  // Preserves the original exception
}
```

Let me know if you'd like me to continue with the rest of the questions!

### 28. **What are the Loop types in C#?**

**Explanation**:  
C# supports several types of loops:
- **`for` loop**: Repeats a block of code a specified number of times.
- **`foreach` loop**: Iterates over a collection or array.
- **`while` loop**: Repeats a block of code while a condition is true.
- **`do-while` loop**: Similar to the `while` loop but checks the condition after executing the loop body.

```csharp
// for loop example
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);  // Output: 0 1 2 3 4
}

// foreach loop example
int[] numbers = { 1, 2, 3, 4, 5 };
foreach (int number in numbers)
{
    Console.WriteLine(number);  // Output: 1 2 3 4 5
}

// while loop example
int count = 0;
while (count < 3)
{
    Console.WriteLine(count);  // Output: 0 1 2
    count++;
}

// do-while loop example
int num = 0;
do
{
    Console.WriteLine(num);  // Output: 0 1 2
    num++;
} while (num < 3);
```

### 29. **What is the difference between `continue` and `break` statements?**

**Explanation**:  
- **`break`**: Exits the loop immediately.
- **`continue`**: Skips the current iteration and moves to the next iteration of the loop.

```csharp
// break example
for (int i = 0; i < 5; i++)
{
    if (i == 3) break;
    Console.WriteLine(i);  // Output: 0 1 2
}

// continue example
for (int i = 0; i < 5; i++)
{
    if (i == 3) continue;
    Console.WriteLine(i);  // Output: 0 1 2 4
}
```

### 30. **What is the difference between Array and ArrayList (at least 2)?**

**Explanation**:
1. **Array**: Has a fixed size, meaning you cannot change its size once it's created.
2. **ArrayList**: Can dynamically resize, allowing you to add or remove items after creation.

```csharp
// Array Example (fixed size)
int[] arr = new int[3] { 1, 2, 3 };
// arr[3] = 4;  // This will throw an error (Index out of range)

// ArrayList Example (dynamic size)
ArrayList arrayList = new ArrayList();
arrayList.Add(1);
arrayList.Add(2);
arrayList.Add(3);
arrayList.Add(4);  // Dynamically grows
```

### 31. **What is the difference between ArrayList and Hashtable?**

**Explanation**:
- **ArrayList**: Stores a collection of objects that can be accessed by index.
- **Hashtable**: Stores key-value pairs and allows fast lookup by key.

```csharp
// ArrayList Example
ArrayList arrayList = new ArrayList();
arrayList.Add("Apple");
arrayList.Add("Banana");
Console.WriteLine(arrayList[0]);  // Output: Apple

// Hashtable Example
Hashtable hashtable = new Hashtable();
hashtable.Add(1, "Apple");
hashtable.Add(2, "Banana");
Console.WriteLine(hashtable[1]);  // Output: Apple
```

### 32. **What are Collections in C# and what are their types?**

**Explanation**:  
Collections in C# are classes for grouping objects. They can be broadly categorized into:
- **Non-generic collections** (like `ArrayList`, `Hashtable`)
- **Generic collections** (like `List<T>`, `Dictionary<TKey, TValue>`)
- **Concurrent collections** (like `ConcurrentDictionary`)

```csharp
// List<T> example (Generic Collection)
List<int> numbers = new List<int> { 1, 2, 3 };
numbers.Add(4);
Console.WriteLine(numbers[0]);  // Output: 1

// Dictionary<TKey, TValue> example
Dictionary<int, string> dictionary = new Dictionary<int, string>();
dictionary.Add(1, "Apple");
dictionary.Add(2, "Banana");
Console.WriteLine(dictionary[1]);  // Output: Apple
```

### 33. **What is IEnumerable in C#?**

**Explanation**:  
`IEnumerable` is an interface that defines a single method `GetEnumerator()` which returns an enumerator that can iterate through a collection.

```csharp
// Example of IEnumerable
public class MyCollection : IEnumerable<int>
{
    private int[] numbers = { 1, 2, 3 };

    public IEnumerator<int> GetEnumerator()
    {
        foreach (int number in numbers)
        {
            yield return number;
        }
    }

    IEnumerator IEnumerable.GetEnumerator() => GetEnumerator();
}

MyCollection collection = new MyCollection();
foreach (int number in collection)
{
    Console.WriteLine(number);  // Output: 1 2 3
}
```

### 34. **What is the difference between IEnumerable and IEnumerator in C#?**

**Explanation**:  
- **IEnumerable**: Represents a collection that can be enumerated.
- **IEnumerator**: Is used to iterate through the collection. It has methods like `MoveNext()`, `Reset()`, and a property `Current` to access the current item.

```csharp
// Example showing both IEnumerable and IEnumerator
public class MyEnumerator : IEnumerable<int>, IEnumerator<int>
{
    private int[] numbers = { 1, 2, 3 };
    private int position = -1;

    public int Current => numbers[position];

    object IEnumerator.Current => Current;

    public bool MoveNext()
    {
        position++;
        return (position < numbers.Length);
    }

    public void Reset() => position = -1;

    public void Dispose() { }

    public IEnumerator<int> GetEnumerator() => this;
    IEnumerator IEnumerable.GetEnumerator() => this;
}

MyEnumerator enumerator = new MyEnumerator();
while (enumerator.MoveNext())
{
    Console.WriteLine(enumerator.Current);  // Output: 1 2 3
}
```

### 35. **What is the difference between IEnumerable and IQueryable in C#? Why use IQueryable in SQL queries?**

**Explanation**:  
- **IEnumerable**: Executes queries in-memory and does not support lazy loading.
- **IQueryable**: Supports query execution on a data source, allowing for more optimized SQL queries by pushing operations to the database server.

```csharp
// IQueryable is used with Entity Framework for deferred execution
IQueryable<User> query = dbContext.Users.Where(u => u.Age > 18);
// SQL query is executed only when the result is accessed
List<User> users = query.ToList();  // Executes the SQL query
```

### 36. **What is the difference between `out` and `ref` parameters?**

**Explanation**:  
- **`out`**: The parameter must be assigned inside the method before use. It’s used to return multiple values from a method.
- **`ref`**: The parameter must be initialized before passing it to the method.

```csharp
// ref example
public void ModifyValue(ref int x)
{
    x += 10;
}
int a = 5;
ModifyValue(ref a);
Console.WriteLine(a);  // Output: 15

// out example
public void GetValues(out int x, out int y)
{
    x = 10;
    y = 20;
}
int val1, val2;
GetValues(out val1, out val2);
Console.WriteLine(val1 + " " + val2);  // Output: 10 20
```

### 37. **What is the purpose of the `params` keyword?**

**Explanation**:  
The `params` keyword allows a method to accept a variable number of arguments as an array.

```csharp
public void PrintNumbers(params int[] numbers)
{
    foreach (var num in numbers)
    {
        Console.WriteLine(num);
    }
}

PrintNumbers(1, 2, 3, 4);  // Output: 1 2 3 4
PrintNumbers(10);  // Output: 10
```

### 38. **What is a Constructor and what are its types?**

**Explanation**:  
A constructor is a special method that is invoked when an object of a class is created. Types of constructors include:
1. **Default constructor**: Provided by C# if no constructor is defined.
2. **Parameterized constructor**: Allows passing parameters during object creation.
3. **Static constructor**: Initializes static members of the class.

```csharp
// Parameterized Constructor
public class Car
{
    public string model;
    public Car(string modelName)
    {
        model = modelName;
    }
}

Car myCar = new Car("Toyota");
Console.WriteLine(myCar.model);  // Output: Toyota
```

### 39. **When to use a Private constructor?**

**Explanation**:  
Private constructors are used when you do not want instances of the class to be created outside the class. It's often used in singleton patterns.

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (

instance == null)
                instance = new Singleton();
            return instance;
        }
    }
}
```

### 40. **What are Extension Methods in C#? When to use them?**

**Explanation**:  
Extension methods allow you to add new methods to an existing class without modifying it. It’s commonly used to extend built-in types or third-party libraries.

```csharp
// Example of Extension Method
public static class StringExtensions
{
    public static int WordCount(this string str)
    {
        return str.Split(' ').Length;
    }
}

string sentence = "Hello World!";
Console.WriteLine(sentence.WordCount());  // Output: 2
```

Let me know if you'd like to proceed with the remaining questions!

### 41. **What do you mean by a Delegate? When to use them?**

**Explanation**:  
A **delegate** is a type that represents references to methods. Delegates are used to pass methods as arguments to other methods, enabling callback mechanisms and event handling.

```csharp
// Delegate declaration
public delegate void PrintDelegate(string message);

// Delegate usage
public class Printer
{
    public void PrintMessage(string message)
    {
        Console.WriteLine(message);
    }
}

PrintDelegate del = new PrintDelegate(new Printer().PrintMessage);
del("Hello Delegates!");  // Output: Hello Delegates!
```

### 42. **What are Multicast Delegates?**

**Explanation**:  
Multicast delegates can reference more than one method. When the delegate is invoked, all methods it references are called.

```csharp
// Multicast Delegate
public delegate void PrintDelegate(string message);

public class Printer
{
    public void PrintMessage1(string message) => Console.WriteLine("Printer1: " + message);
    public void PrintMessage2(string message) => Console.WriteLine("Printer2: " + message);
}

PrintDelegate del = new Printer().PrintMessage1;
del += new Printer().PrintMessage2;  // Multicast

del("Multicast");  
// Output:
// Printer1: Multicast
// Printer2: Multicast
```

### 43. **What are Anonymous Delegates in C#?**

**Explanation**:  
Anonymous delegates are methods without a name. They are used where the delegate needs to be passed as an argument without the need to declare a separate method.

```csharp
// Anonymous Delegate Example
public delegate void PrintDelegate(string message);

PrintDelegate del = delegate (string msg)
{
    Console.WriteLine("Anonymous: " + msg);
};

del("Hello");  // Output: Anonymous: Hello
```

### 44. **What are the differences between Events and Delegates?**

**Explanation**:
- **Events** are a type of delegate that provide a way for objects to communicate. Events are triggered when an action occurs, and other parts of the program can subscribe to be notified when the event occurs.
- **Delegates** are simply function pointers used to call methods.

```csharp
// Event Example
public class Button
{
    public event Action Clicked;

    public void OnClick()
    {
        if (Clicked != null)
        {
            Clicked();  // Raise event
        }
    }
}

public class Program
{
    public static void Main()
    {
        Button button = new Button();
        button.Clicked += () => Console.WriteLine("Button clicked!");

        button.OnClick();  // Output: Button clicked!
    }
}
```

### 45. **What is the `this` keyword in C#? When to use it?**

**Explanation**:  
The `this` keyword refers to the current instance of the class. It is used to avoid naming conflicts between class fields and method parameters or to refer to the current object within instance methods.

```csharp
// Example of 'this' keyword
public class Person
{
    private string name;

    public Person(string name)
    {
        this.name = name;  // 'this' is used to distinguish between the field and parameter
    }

    public void PrintName() => Console.WriteLine("Name: " + this.name);
}

Person person = new Person("Alice");
person.PrintName();  // Output: Name: Alice
```

### 46. **What is the purpose of the `using` keyword in C#?**

**Explanation**:  
The `using` keyword is used for two purposes:
1. **Namespace inclusion**: Allows you to include namespaces.
2. **Resource management**: Provides a mechanism to automatically dispose of resources like files or database connections after they are no longer needed.

```csharp
// Using for resource management
using (StreamWriter writer = new StreamWriter("file.txt"))
{
    writer.WriteLine("Hello, world!");
}  // StreamWriter is automatically disposed of when it goes out of scope
```

### 47. **What is the difference between the `is` and `as` operators?**

**Explanation**:  
- **`is`**: Checks if an object is of a certain type and returns `true` or `false`.
- **`as`**: Attempts to cast an object to a specified type and returns `null` if the cast fails.

```csharp
// 'is' operator example
object obj = "Hello";
if (obj is string)
{
    Console.WriteLine("It is a string");  // Output: It is a string
}

// 'as' operator example
object obj2 = "World";
string str = obj2 as string;
Console.WriteLine(str);  // Output: World
```

### 48. **What is the difference between `Readonly` and `Constant` variables (at least 3)?**

**Explanation**:
1. **`const`**: Must be initialized at the time of declaration and cannot be changed afterward.
2. **`readonly`**: Can be initialized either at declaration or in the constructor and cannot be changed afterward.
3. **Scope**: `const` is implicitly static, while `readonly` can have instance-level scope.

```csharp
public class MyClass
{
    public const int constantValue = 10;  // Must be initialized here
    public readonly int readonlyValue;

    public MyClass(int val)
    {
        readonlyValue = val;  // Can be initialized in the constructor
    }
}
```

### 49. **What is a `Static` class? When to use it?**

**Explanation**:  
A **static class** is a class that cannot be instantiated. It can contain only static members and methods. Use static classes for utility functions or when no object instance is required.

```csharp
// Static class example
public static class MathUtils
{
    public static int Add(int a, int b) => a + b;
}

int result = MathUtils.Add(5, 10);  // Static method call
Console.WriteLine(result);  // Output: 15
```

### 50. **What is the difference between `var` and `dynamic` in C#?**

**Explanation**:
- **`var`**: The type is determined at compile-time, meaning the compiler knows the type at the time of writing the code.
- **`dynamic`**: The type is determined at runtime, allowing more flexibility but less safety (as errors may occur at runtime).

```csharp
// var (compile-time type inference)
var number = 10;  // number is of type int
Console.WriteLine(number);  // Output: 10

// dynamic (runtime type determination)
dynamic dyn = 10;
Console.WriteLine(dyn);  // Output: 10

dyn = "Hello";
Console.WriteLine(dyn);  // Output: Hello
```

### 51. **What is the purpose of the `Enum` keyword?**

**Explanation**:  
An **enum** is a special value type that defines a set of named constants. It’s used to assign meaningful names to numeric values for better code readability.

```csharp
// Enum example
public enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }

Days today = Days.Wednesday;
Console.WriteLine(today);  // Output: Wednesday
Console.WriteLine((int)today);  // Output: 3 (zero-based index)
```

### Summary

The concepts and examples provided above give you a solid understanding of core C# features, OOP principles, and practical usage of essential keywords. These are important to help you write clean, maintainable, and efficient code in C#. Feel free to ask for further clarification on any of the topics!

Let me know if you'd like further assistance with other questions!
