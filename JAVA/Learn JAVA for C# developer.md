# Learn JAVA for C# developer

Comparisons between Java and C# to help you understand the similarities and differences.

---

### 1. **What is the difference between `==` and `equals()` in Java?**
- **Java**: `==` compares references for objects, while `equals()` compares values.
- **C#**: Similar concept with `==` for reference comparison, but `Equals()` can be overridden for value comparison.

```java
// Java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b);        // false, compares memory locations
System.out.println(a.equals(b));   // true, compares actual content
```

```csharp
// C#
string a = new string("hello");
string b = new string("hello");

Console.WriteLine(a == b);        // true, compares content for string
Console.WriteLine(a.Equals(b));   // true, compares content
```

### 2. **Explain the concept of `final` keyword in Java.**
- **Java**: `final` ensures a variable, method, or class can’t be modified.
- **C#**: Use `readonly` for fields, `sealed` for classes.

```java
// Java
final int x = 10;
x = 20; // Error: cannot assign a value to a final variable
```

```csharp
// C#
readonly int x = 10;
x = 20; // Error: cannot modify readonly field
```

### 3. **What is a constructor in Java?**
- **Java**: Constructor is a special method used to initialize objects.
- **C#**: The concept of constructors is the same.

```java
// Java
class MyClass {
    int x;
    MyClass() {
        x = 5;
    }
}
```

```csharp
// C#
class MyClass {
    int x;
    public MyClass() {
        x = 5;
    }
}
```

### 4. **What is method overloading in Java?**
- **Java/C#**: Both languages support method overloading (same method name, different parameters).

```java
// Java
class MyClass {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

```csharp
// C#
class MyClass {
    int Add(int a, int b) {
        return a + b;
    }

    double Add(double a, double b) {
        return a + b;
    }
}
```

### 5. **What is method overriding in Java?**
- **Java/C#**: In both, method overriding allows a subclass to provide a specific implementation of a method already defined in its superclass.

```java
// Java
class Parent {
    void display() {
        System.out.println("Parent method");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child method");
    }
}
```

```csharp
// C#
class Parent {
    public virtual void Display() {
        Console.WriteLine("Parent method");
    }
}

class Child : Parent {
    public override void Display() {
        Console.WriteLine("Child method");
    }
}
```

### 6. **What is an abstract class in Java?**
- **Java/C#**: Abstract classes cannot be instantiated and can have both abstract and non-abstract methods.

```java
// Java
abstract class Animal {
    abstract void sound();
}
```

```csharp
// C#
abstract class Animal {
    public abstract void Sound();
}
```

### 7. **What is an interface in Java?**
- **Java/C#**: Both languages support interfaces, where all methods are abstract by default (Java 7 or earlier).

```java
// Java
interface Animal {
    void sound();
}
```

```csharp
// C#
interface IAnimal {
    void Sound();
}
```

### 8. **What is the difference between abstract class and interface?**
- **Java**: Interfaces cannot have concrete methods (before Java 8). Abstract classes can.
- **C#**: Interfaces cannot have concrete methods (before C# 8.0).

### 9. **What is a static method in Java?**
- **Java/C#**: A static method belongs to the class rather than any instance.

```java
// Java
class MyClass {
    static void myStaticMethod() {
        System.out.println("Static method");
    }
}
```

```csharp
// C#
class MyClass {
    public static void MyStaticMethod() {
        Console.WriteLine("Static method");
    }
}
```

### 10. **What is inheritance in Java?**
- **Java/C#**: Both support inheritance, allowing a class to inherit fields and methods from another class.

```java
// Java
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
}
```

```csharp
// C#
class Animal {
    public void Eat() {
        Console.WriteLine("Animal is eating");
    }
}

class Dog : Animal {
}
```

### 11. **What is polymorphism in Java?**
- **Java/C#**: Both support polymorphism, which allows one object to take many forms.

### 12. **What is encapsulation in Java?**
- **Java/C#**: Both languages use encapsulation to restrict direct access to fields.

```java
// Java
class MyClass {
    private int x;

    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }
}
```

```csharp
// C#
class MyClass {
    private int x;

    public int X {
        get { return x; }
        set { x = value; }
    }
}
```

### 13. **What is the `super` keyword in Java?**
- **Java**: Used to refer to the immediate parent class object.
- **C#**: `base` keyword is equivalent.

```java
// Java
class Parent {
    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    void display() {
        super.display();
        System.out.println("Child");
    }
}
```

```csharp
// C#
class Parent {
    public void Display() {
        Console.WriteLine("Parent");
    }
}

class Child : Parent {
    public void Display() {
        base.Display();
        Console.WriteLine("Child");
    }
}
```

### 14. **What is `this` keyword in Java?**
- **Java/C#**: Refers to the current instance of the class.

```java
// Java
class MyClass {
    int x;
    MyClass(int x) {
        this.x = x;
    }
}
```

```csharp
// C#
class MyClass {
    int x;
    public MyClass(int x) {
        this.x = x;
    }
}
```

### 15. **What are the different types of loops in Java?**
- **Java/C#**: Both support `for`, `while`, and `do-while` loops.

### 16. **What is the `break` and `continue` statement in Java?**
- **Java/C#**: Both support `break` to exit loops and `continue` to skip iterations.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    if (i == 3) continue;
}
```

```csharp
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    if (i == 3) continue;
}
```

### 17. **What is the difference between `ArrayList` and `LinkedList` in Java?**
- **Java**: `ArrayList` is backed by an array, while `LinkedList` is backed by a doubly linked list.
- **C#**: Similar structure with `List<T>` (like `ArrayList`) and `LinkedList<T>`.

```java
ArrayList<Integer> list = new ArrayList<>();
LinkedList<Integer> linkedList = new LinkedList<>();
```

```csharp
List<int> list = new List<int>();
LinkedList<int> linkedList = new LinkedList<int>();
```

---

This comparison covers just the first 17 questions, and the structure is kept consistent for easier understanding between Java and C#. If you'd like, I can continue the rest with this comparison format. Let me know if you would prefer additional details or more questions.

### 18. **What is exception handling in Java?**
- **Java/C#**: Both use `try-catch` blocks for exception handling, and both support `finally` for cleanup code.

```java
// Java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Can't divide by zero");
} finally {
    System.out.println("Cleanup code");
}
```

```csharp
// C#
try {
    int result = 10 / 0;
} catch (DivideByZeroException e) {
    Console.WriteLine("Can't divide by zero");
} finally {
    Console.WriteLine("Cleanup code");
}
```

### 19. **What are checked and unchecked exceptions in Java?**
- **Java**: Checked exceptions must be handled during compilation; unchecked exceptions occur at runtime.
- **C#**: All exceptions in C# are unchecked.

### 20. **What is the `finalize()` method in Java?**
- **Java**: `finalize()` is called before garbage collection.
- **C#**: The equivalent is the destructor (`~ClassName()`), but garbage collection is automatic.

```java
// Java
protected void finalize() {
    System.out.println("Object is being garbage collected");
}
```

```csharp
// C#
~MyClass() {
    Console.WriteLine("Object is being garbage collected");
}
```

### 21. **What is the difference between `String`, `StringBuilder`, and `StringBuffer`?**
- **Java**:
  - `String`: Immutable.
  - `StringBuilder`: Mutable, not thread-safe.
  - `StringBuffer`: Mutable, thread-safe.
- **C#**:
  - `String`: Immutable.
  - `StringBuilder`: Mutable, not thread-safe by default.

```java
// Java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
```

```csharp
// C#
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World");
```

### 22. **What is the `enum` type in Java?**
- **Java/C#**: Both languages have enums for representing fixed sets of constants.

```java
// Java
enum Direction { NORTH, EAST, SOUTH, WEST }
```

```csharp
// C#
enum Direction { North, East, South, West }
```

### 23. **What is a singleton class in Java?**
- **Java/C#**: Both use singleton patterns to ensure only one instance of a class is created.

```java
// Java
class Singleton {
    private static Singleton instance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

```csharp
// C#
class Singleton {
    private static Singleton instance;
    
    private Singleton() {}
    
    public static Singleton GetInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 24. **What is the `default` keyword in interfaces in Java?**
- **Java**: Allows methods with default implementations in interfaces (from Java 8).
- **C#**: Default interface methods are available in C# 8.0.

```java
// Java
interface MyInterface {
    default void myMethod() {
        System.out.println("Default method");
    }
}
```

```csharp
// C#
interface IMyInterface {
    public void MyMethod() {
        Console.WriteLine("Default method");
    }
}
```

### 25. **What is the difference between `throw` and `throws` in Java?**
- **Java**:
  - `throw`: Used to explicitly throw an exception.
  - `throws`: Declares that a method can throw exceptions.
- **C#**: Only `throw` is used.

```java
// Java
void method() throws IOException {
    throw new IOException("IO error");
}
```

```csharp
// C#
void Method() {
    throw new IOException("IO error");
}
```

### 26. **What is garbage collection in Java?**
- **Java/C#**: Both Java and C# provide automatic garbage collection to free up memory by destroying unused objects.

### 27. **What is a package in Java?**
- **Java**: A package is used to group related classes.
- **C#**: The equivalent is the `namespace`.

```java
// Java
package mypackage;
```

```csharp
// C#
namespace MyNamespace;
```

### 28. **What is the `static` keyword in Java?**
- **Java/C#**: Both use `static` to declare class-level methods and fields.

### 29. **What is an anonymous inner class in Java?**
- **Java**: An anonymous class is a local class without a name.
- **C#**: Anonymous methods or lambda expressions can be used in similar situations.

```java
// Java
new Thread(new Runnable() {
    public void run() {
        System.out.println("Anonymous class");
    }
}).start();
```

```csharp
// C#
new Thread(() => {
    Console.WriteLine("Lambda expression");
}).Start();
```

### 30. **What is a lambda expression in Java?**
- **Java/C#**: Both languages support lambda expressions for functional programming.

```java
// Java
Runnable r = () -> System.out.println("Lambda expression");
r.run();
```

```csharp
// C#
Action r = () => Console.WriteLine("Lambda expression");
r();
```

### 31. **What is `List` in Java?**
- **Java**: `List` is an interface; `ArrayList` is a common implementation.
- **C#**: `List<T>` is a generic collection type.

```java
// Java
List<Integer> list = new ArrayList<>();
list.add(1);
```

```csharp
// C#
List<int> list = new List<int>();
list.Add(1);
```

### 32. **What is a `Set` in Java?**
- **Java/C#**: Both support sets, but `HashSet` is the most common implementation.

```java
// Java
Set<String> set = new HashSet<>();
set.add("a");
```

```csharp
// C#
HashSet<string> set = new HashSet<string>();
set.Add("a");
```

### 33. **What is the `HashMap` in Java?**
- **Java/C#**: `HashMap` in Java is equivalent to `Dictionary<TKey, TValue>` in C#.

```java
// Java
Map<String, Integer> map = new HashMap<>();
map.put("key", 1);
```

```csharp
// C#
Dictionary<string, int> map = new Dictionary<string, int>();
map.Add("key", 1);
```

### 34. **What is the difference between `HashMap` and `Hashtable`?**
- **Java**:
  - `HashMap`: Not synchronized, allows null keys/values.
  - `Hashtable`: Synchronized, does not allow null keys/values.
- **C#**:
  - `Dictionary`: Similar to `HashMap`.
  - `Hashtable`: Similar to Java's `Hashtable`, but it's rarely used in modern C#.

### 35. **What is `Iterator` in Java?**
- **Java/C#**: Both languages provide `Iterator` or `Enumerator` to traverse collections.

```java
// Java
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

```csharp
// C#
IEnumerator<string> it = list.GetEnumerator();
while (it.MoveNext()) {
    Console.WriteLine(it.Current);
}
```

### 36. **What is the `Optional` class in Java?**
- **Java**: `Optional` is used to avoid null checks.
- **C#**: `Nullable<T>` is the closest equivalent, but only for value types.

```java
// Java
Optional<String> opt = Optional.ofNullable("Hello");
System.out.println(opt.orElse("Default"));
```

```csharp
// C#
string? opt = "Hello";
Console.WriteLine(opt ?? "Default");
```

### 37. **What is the `Stream` API in Java?**
- **Java**: `Stream` API is used for functional-style operations on collections.
- **C#**: LINQ is the equivalent for querying and manipulating collections.

```java
// Java
List<String> list = Arrays.asList("a", "b", "c");
list.stream().forEach(System.out::println);
```

```csharp
// C#
List<string> list = new List<string> { "a", "b", "c" };
list.ForEach(Console.WriteLine);
```

### 38. **What is the use of `synchronized` keyword in Java?**
- **Java**: `synchronized` is used to control thread access.
- **C#**: `lock` is used for the same purpose.

```java
// Java
synchronized (this) {
    // critical section
}
```

```csharp
// C#
lock (this) {
    // critical section
}
```

### 39. **What is multithreading in Java?**
- **Java/C#**: Both support multithreading to allow concurrent execution of multiple threads.

### 40. **

What is the `volatile` keyword in Java?**
- **Java/C#**: `volatile` ensures changes to a variable are visible to all threads.

### 41. **What is `Comparable` interface in Java?**
- **Java**: `Comparable` is used to define natural ordering.
- **C#**: The equivalent is `IComparable<T>`.

```java
// Java
class MyClass implements Comparable<MyClass> {
    int x;
    public int compareTo(MyClass o) {
        return this.x - o.x;
    }
}
```

```csharp
// C#
class MyClass : IComparable<MyClass> {
    public int x;
    public int CompareTo(MyClass o) {
        return this.x - o.x;
    }
}
```

### 42. **What is `Comparator` interface in Java?**
- **Java**: `Comparator` provides custom ordering.
- **C#**: The equivalent is `IComparer<T>`.

```java
// Java
Comparator<MyClass> comp = new Comparator<MyClass>() {
    public int compare(MyClass o1, MyClass o2) {
        return o1.x - o2.x;
    }
};
```

```csharp
// C#
IComparer<MyClass> comp = new MyClassComparer();

class MyClassComparer : IComparer<MyClass> {
    public int Compare(MyClass o1, MyClass o2) {
        return o1.x - o2.x;
    }
}
```

### 43. **What is the difference between `wait()` and `sleep()` in Java?**
- **Java/C#**: 
  - `wait()`: Releases the lock and waits until notified.
  - `sleep()`: Pauses execution without releasing the lock.

```java
// Java
synchronized (this) {
    wait();
    Thread.sleep(1000);
}
```

```csharp
// C#
lock (this) {
    Monitor.Wait(this);
    Thread.Sleep(1000);
}
```

### 44. **What is a `deadlock` in Java?**
- **Java/C#**: A deadlock occurs when two or more threads are blocked forever, waiting for each other.

### 45. **What are the four access modifiers in Java?**
- **Java/C#**: Both have four main access modifiers:
  - `public`
  - `private`
  - `protected`
  - Default (package-private in Java, internal in C#).

### 46. **What is `try-with-resources` in Java?**
- **Java**: Automatically closes resources.
- **C#**: `using` block serves the same purpose.

```java
// Java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // Use BufferedReader
}
```

```csharp
// C#
using (var br = new StreamReader("file.txt")) {
    // Use StreamReader
}
```

### 47. **What is the `transient` keyword in Java?**
- **Java**: `transient` prevents a field from being serialized.
- **C#**: The equivalent is `[NonSerialized]` attribute.

```java
// Java
transient int x;
```

```csharp
// C#
[NonSerialized]
int x;
```

### 48. **What is the `instanceof` operator in Java?**
- **Java**: Used to check object type.
- **C#**: Use `is` for type checking.

```java
// Java
if (obj instanceof String) {
    System.out.println("Object is a String");
}
```

```csharp
// C#
if (obj is string) {
    Console.WriteLine("Object is a string");
}
```

### 49. **What is the use of `assert` keyword in Java?**
- **Java/C#**: Both have `assert` for debugging purposes.

```java
// Java
assert x >= 0 : "x is negative";
```

```csharp
// C#
Debug.Assert(x >= 0, "x is negative");
```

### 50. **What are the default values of primitive data types in Java?**
- **Java/C#**: Default values are the same for both languages:
  - `int`: 0
  - `char`: '\u0000'
  - `boolean`: false
  - `float`: 0.0f
  - `double`: 0.0

---

This completes the list of 50 Java entry-level interview questions with a comparison to C#. This should help bridge the gap between the two languages as you learn Java, given your background in C#. Let me know if you need further clarification or additional examples.
