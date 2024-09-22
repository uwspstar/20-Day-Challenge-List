# 101-160 Interview Questions

### Question 101: Explain Association?

#### English Explanation:

**Association** is a relationship between two classes where one class is connected to another without ownership. It describes a general relationship where one class uses or communicates with another. Unlike composition or aggregation, association doesn’t imply a HAS-A relationship. It can be **unidirectional** or **bidirectional**.

#### Code Example:

```csharp
public class Teacher
{
    public string Name { get; set; }

    public Teacher(string name)
    {
        Name = name;
    }

    public void Teach()
    {
        Console.WriteLine(Name + " is teaching.");
    }
}

public class Student
{
    public string Name { get; set; }

    public Student(string name)
    {
        Name = name;
    }

    public void Learn()
    {
        Console.WriteLine(Name + " is learning.");
    }

    // Association: Student can have a Teacher, but no ownership.
    public void AskQuestion(Teacher teacher)
    {
        Console.WriteLine(Name + " asks " + teacher.Name + " a question.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Teacher teacher = new Teacher("Mr. Smith");
        Student student = new Student("John");

        student.AskQuestion(teacher);
        teacher.Teach();
        student.Learn();
    }
}
```

In this example, `Student` and `Teacher` are associated, but neither has ownership over the other.

#### Chinese Explanation:

**关联（Association）** 是两个类之间的关系，一个类与另一个类相连，但没有所有权。它描述了一种一般关系，其中一个类使用或与另一个类通信。与组合或聚合不同，关联不暗示 HAS-A 关系。它可以是**单向**或**双向**的。

#### 代码示例：

```csharp
public class Teacher
{
    public string Name { get; set; }

    public Teacher(string name)
    {
        Name = name;
    }

    public void Teach()
    {
        Console.WriteLine(Name + " 在教学。");
    }
}

public class Student
{
    public string Name { get; set; }

    public Student(string name)
    {
        Name = name;
    }

    public void Learn()
    {
        Console.WriteLine(Name + " 在学习。");
    }

    // 关联：学生可以有一个老师，但没有所有权。
    public void AskQuestion(Teacher teacher)
    {
        Console.WriteLine(Name + " 问 " + teacher.Name + " 一个问题。");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Teacher teacher = new Teacher("Smith 老师");
        Student student = new Student("小明");

        student.AskQuestion(teacher);
        teacher.Teach();
        student.Learn();
    }
}
```

---

### Question 102: Differentiate between Composition vs Aggregation vs Association?

#### English Explanation:

| **Aspect**       | **Composition**                                  | **Aggregation**                                 | **Association**                                 |
|------------------|--------------------------------------------------|------------------------------------------------|------------------------------------------------|
| **Relationship** | Strong HAS-A (ownership)                         | Weak HAS-A (no ownership)                      | General relationship (no ownership)            |
| **Lifespan**     | Contained object cannot exist without the parent | Contained object can exist independently       | Objects can exist independently                |
| **Example**      | A car has an engine                              | A library contains books (but books exist independently) | A teacher and a student communicate            |

#### Chinese Explanation：

| **方面**       | **组合**                                         | **聚合**                                        | **关联**                                        |
|----------------|--------------------------------------------------|------------------------------------------------|------------------------------------------------|
| **关系**       | 强 HAS-A（所有权）                               | 弱 HAS-A（无所有权）                           | 一般关系（无所有权）                           |
| **生命周期**   | 包含的对象不能独立于父对象存在                   | 包含的对象可以独立存在                         | 对象可以独立存在                               |
| **示例**       | 汽车有引擎                                       | 图书馆包含书籍（但书籍独立存在）                | 老师和学生沟通                                 |

---

### Question 103: UML Symbols for Composition, Aggregation, and Association?

#### English Explanation:

In UML (Unified Modeling Language), relationships between objects are depicted using different symbols:
- **Composition**: Represented by a filled diamond at the parent class pointing to the child class.
- **Aggregation**: Represented by an unfilled diamond at the parent class pointing to the child class.
- **Association**: Represented by a simple line connecting two classes, optionally with arrowheads to show the direction of the association.

#### Chinese Explanation：

在 UML（统一建模语言）中，对象之间的关系通过不同的符号表示：
- **组合**：用指向子类的实心菱形表示，位于父类旁。
- **聚合**：用指向子类的空心菱形表示，位于父类旁。
- **关联**：用连接两个类的简单线条表示，可以选择箭头表示关联的方向。

---

### Question 104: Explain stack and heap?

#### English Explanation:

In C# and most programming languages:
- **Stack**: Used for static memory allocation and stores value types (such as `int`, `float`, etc.), function calls, and local variables. Stack memory is managed automatically, following a **LIFO (Last In, First Out)** structure.
- **Heap**: Used for dynamic memory allocation and stores reference types (such as objects and arrays). Heap memory must be managed by the garbage collector.

#### Code Example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Stored on the stack
        int a = 10;
        
        // Stored on the heap
        object obj = new object();
    }
}
```

#### Chinese Explanation：

在 C# 和大多数编程语言中：
- **栈**：用于静态内存分配，存储值类型（如 `int`、`float` 等）、函数调用和局部变量。栈内存自动管理，遵循 **LIFO（后进先出）** 结构。
- **堆**：用于动态内存分配，存储引用类型（如对象和数组）。堆内存必须由垃圾回收器管理。

#### 代码示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        // 存储在栈上
        int a = 10;
        
        // 存储在堆上
        object obj = new object();
    }
}
```

---

### Question 105: Where are stack and heap stored?

#### English Explanation:

- **Stack**: Stored in a region of memory that is managed directly by the operating system. It is used for short-term memory management, mainly for function calls and local variables.
- **Heap**: Stored in a larger region of memory used for dynamic memory allocation. Objects in the heap have a longer lifespan than those in the stack, and they are managed by the garbage collector.

#### Chinese Explanation：

- **栈**：存储在由操作系统直接管理的内存区域中。主要用于函数调用和局部变量的短期内存管理。
- **堆**：存储在用于动态内存分配的较大内存区域中。堆中的对象的生命周期比栈中的长，并由垃圾回收器管理。

---

### Question 106: What goes on stack and what goes on heap?

#### English Explanation:

- **Stack**: Stores **value types** (such as `int`, `char`, etc.), function calls, and local variables.
- **Heap**: Stores **reference types** (such as objects, arrays, strings) and instances of classes.

#### Code Example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int value = 5;  // Stored on the stack (value type)
        string text = "Hello";  // Stored on the heap (reference type)
    }
}
```

#### Chinese Explanation：

- **栈**：存储**值类型**（如 `int`、`char` 等）、函数调用和局部变量。
- **堆**：存储**引用类型**（如对象、数组、字符串）和类的实例。

#### 代码示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        int value = 5;  // 存储在栈上（值类型）
        string text = "Hello";  // 存储在堆上（引用类型）
    }
}
```

---

### Question 107: How is the stack memory address arranged?

#### English Explanation:

Stack memory is arranged in a **LIFO (Last In, First Out)** order. When a function is called, its variables are pushed onto the stack, and when the function returns, those variables are popped off the stack. Each function call creates a new **stack frame**, and when the function exits, the stack frame is removed.

#### Chinese Explanation：

栈内存以 **LIFO（后进先出）** 顺序排列。当调用函数时，其变量被推送到栈中，当函数返回时，这些变量被从栈中弹出。每次函数调用都会创建一个新的**栈帧**，函数退出时栈帧被移除。

---

### Question 108: How is stack memory deallocated: LIFO or FIFO?

####

 English Explanation:

Stack memory is deallocated in a **LIFO (Last In, First Out)** order. When a function returns, its stack frame (containing local variables and function arguments) is removed from the stack in the reverse order of how they were added.

#### Chinese Explanation：

栈内存以 **LIFO（后进先出）** 的顺序释放。当一个函数返回时，其栈帧（包含局部变量和函数参数）按照与添加时相反的顺序从栈中移除。

---

### Question 109: How are primitive and objects stored in memory?

#### English Explanation:

- **Primitive types (value types)**: Stored directly in the stack memory.
- **Objects (reference types)**: The reference to the object is stored in the stack, while the actual object is stored in the heap.

#### Code Example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        int x = 10;  // Primitive, stored in stack
        object obj = new object();  // Object reference stored in stack, object stored in heap
    }
}
```

#### Chinese Explanation：

- **原始类型（值类型）**：直接存储在栈内存中。
- **对象（引用类型）**：对象的引用存储在栈中，而实际对象存储在堆中。

#### 代码示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        int x = 10;  // 原始类型，存储在栈中
        object obj = new object();  // 对象引用存储在栈中，对象存储在堆中
    }
}
```

---

### Question 110: Can primitive data types be stored in heap?

#### English Explanation:

Yes, **primitive data types** (value types) can be stored on the **heap** if they are part of a reference type, such as a field in an object. When a value type is included in an object, the value type is stored on the heap along with the object.

#### Code Example:

```csharp
public class MyClass
{
    public int Value;  // Value type stored on the heap because it is part of a reference type
}

class Program
{
    static void Main(string[] args)
    {
        MyClass myObject = new MyClass();
        myObject.Value = 42;  // Stored on heap with the object
    }
}
```

#### Chinese Explanation：

是的，如果**原始数据类型**（值类型）是引用类型的一部分（例如对象中的字段），它们可以存储在**堆**中。当值类型包含在对象中时，该值类型与对象一起存储在堆中。

#### 代码示例：

```csharp
public class MyClass
{
    public int Value;  // 值类型存储在堆中，因为它是引用类型的一部分
}

class Program
{
    static void Main(string[] args)
    {
        MyClass myObject = new MyClass();
        myObject.Value = 42;  // 与对象一起存储在堆中
    }
}
```

---
### Question 111: Explain value types and reference types?

#### English Explanation:

In C#, types are divided into **value types** and **reference types**:
- **Value types**: Store data directly in the memory location where the variable is declared. Common value types include `int`, `float`, `bool`, and `struct`. Value types are stored on the **stack**.
- **Reference types**: Store a reference to the memory location where the actual data is stored. Common reference types include `class`, `interface`, `delegate`, and `array`. Reference types are stored on the **heap**, and the reference itself is stored on the **stack**.

#### Code Example:

```csharp
public class MyClass
{
    public int Value;  // Reference type, object stored in heap
}

class Program
{
    static void Main(string[] args)
    {
        int a = 10;  // Value type, stored on the stack
        MyClass myObject = new MyClass();  // Reference type, reference stored on the stack, object on heap
        myObject.Value = 20;
    }
}
```

#### Chinese Explanation:

在 C# 中，类型分为**值类型**和**引用类型**：
- **值类型**：直接存储数据在变量声明的内存位置。常见的值类型包括 `int`、`float`、`bool` 和 `struct`。值类型存储在**栈**中。
- **引用类型**：存储对实际数据存储位置的引用。常见的引用类型包括 `class`、`interface`、`delegate` 和 `array`。引用类型存储在**堆**中，而引用本身存储在**栈**中。

#### 代码示例：

```csharp
public class MyClass
{
    public int Value;  // 引用类型，对象存储在堆中
}

class Program
{
    static void Main(string[] args)
    {
        int a = 10;  // 值类型，存储在栈上
        MyClass myObject = new MyClass();  // 引用类型，引用存储在栈上，对象存储在堆中
        myObject.Value = 20;
    }
}
```

---

### Question 112: Explain byval and byref?

#### English Explanation:

- **By Value (byval)**: When a value type is passed to a method **by value**, a copy of the actual data is passed. Changes made to the parameter inside the method do not affect the original value outside the method.
  
- **By Reference (byref)**: When a value type is passed to a method **by reference**, the reference to the actual data is passed. Changes made to the parameter inside the method affect the original value outside the method.

#### Code Example:

```csharp
public class Program
{
    static void ModifyByValue(int a)
    {
        a = 20;  // This change won't affect the original value
    }

    static void ModifyByReference(ref int a)
    {
        a = 20;  // This change will affect the original value
    }

    static void Main(string[] args)
    {
        int x = 10;

        // Passing by value
        ModifyByValue(x);
        Console.WriteLine(x);  // Output: 10

        // Passing by reference
        ModifyByReference(ref x);
        Console.WriteLine(x);  // Output: 20
    }
}
```

#### Chinese Explanation:

- **按值传递（byval）**：当值类型按值传递到方法时，会传递数据的副本。方法内部对参数的更改不会影响方法外部的原始值。
  
- **按引用传递（byref）**：当值类型按引用传递到方法时，会传递对实际数据的引用。方法内部对参数的更改会影响方法外部的原始值。

#### 代码示例：

```csharp
public class Program
{
    static void ModifyByValue(int a)
    {
        a = 20;  // 此更改不会影响原始值
    }

    static void ModifyByReference(ref int a)
    {
        a = 20;  // 此更改将影响原始值
    }

    static void Main(string[] args)
    {
        int x = 10;

        // 按值传递
        ModifyByValue(x);
        Console.WriteLine(x);  // 输出：10

        // 按引用传递
        ModifyByReference(ref x);
        Console.WriteLine(x);  // 输出：20
    }
}
```

---

### Question 113: Differentiate between copy by value and copy by reference?

#### English Explanation:

- **Copy by Value**: When a value type is copied, only the value itself is copied. Modifications to the copied value do not affect the original value.
  
- **Copy by Reference**: When a reference type is copied, only the reference (or pointer) is copied, not the actual data. Changes made to the copied reference affect the original object, as both references point to the same object in memory.

#### Code Example:

```csharp
public class MyClass
{
    public int Value;
}

class Program
{
    static void ModifyValue(MyClass obj)
    {
        obj.Value = 20;  // Modifies the original object, as reference is passed
    }

    static void Main(string[] args)
    {
        MyClass obj1 = new MyClass();
        obj1.Value = 10;

        MyClass obj2 = obj1;  // Copy by reference, both point to the same object

        ModifyValue(obj2);
        Console.WriteLine(obj1.Value);  // Output: 20 (as both obj1 and obj2 reference the same object)
    }
}
```

#### Chinese Explanation：

- **按值复制**：当值类型被复制时，只复制值本身。对复制值的修改不会影响原始值。
  
- **按引用复制**：当引用类型被复制时，只复制引用（或指针），而不是实际数据。对复制引用的更改会影响原始对象，因为两个引用都指向内存中的同一个对象。

#### 代码示例：

```csharp
public class MyClass
{
    public int Value;
}

class Program
{
    static void ModifyValue(MyClass obj)
    {
        obj.Value = 20;  // 修改原始对象，因为传递的是引用
    }

    static void Main(string[] args)
    {
        MyClass obj1 = new MyClass();
        obj1.Value = 10;

        MyClass obj2 = obj1;  // 按引用复制，两个引用指向同一个对象

        ModifyValue(obj2);
        Console.WriteLine(obj1.Value);  // 输出：20（因为 obj1 和 obj2 都引用相同的对象）
    }
}
```

---

### Question 114: What is boxing and unboxing?

#### English Explanation:

- **Boxing**: The process of converting a value type (like `int`) into a reference type (like `object`). The value type is stored in a new object on the heap.
  
- **Unboxing**: The process of converting a reference type back to a value type. The value is extracted from the object and placed back into a value type variable.

#### Code Example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Boxing
        int a = 10;
        object obj = a;  // Value type a is boxed into a reference type obj

        // Unboxing
        int b = (int)obj;  // Reference type obj is unboxed back into a value type b

        Console.WriteLine(b);  // Output: 10
    }
}
```

#### Chinese Explanation：

- **装箱（Boxing）**：将值类型（如 `int`）转换为引用类型（如 `object`）的过程。值类型存储在堆上的新对象中。
  
- **拆箱（Unboxing）**：将引用类型转换回值类型的过程。值从对象中提取并放回值类型变量中。

#### 代码示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        // 装箱
        int a = 10;
        object obj = a;  // 值类型 a 装箱为引用类型 obj

        // 拆箱
        int b = (int)obj;  // 引用类型 obj 拆箱回值类型 b

        Console.WriteLine(b);  // 输出：10
    }
}
```

---

### Question 115: Is boxing/unboxing good or bad?

#### English Explanation:

Boxing and unboxing are generally considered **bad practices** in performance-critical applications because:
1. **Performance overhead**: Boxing and unboxing involve additional memory allocation on the heap and memory copying, which can slow down the application.
2. **Increased garbage collection**: Frequent boxing leads to more objects on the heap, which can increase the workload of the garbage collector.

#### Chinese Explanation：

在性能关键的应用中，装箱和拆箱通常被认为是**不好的做法**，原因是：
1. **性能开销**：装箱和拆箱涉及堆上的额外内存分配和内存复制，这会降低应用程序的性能。
2. **增加垃圾回收**：频繁的装箱会导致堆上有更多对象，这会增加垃圾回收器的工作

量。

---

### Question 116: Can we avoid boxing and unboxing?

#### English Explanation:

Yes, boxing and unboxing can be avoided by:
1. Using **generics**: Generics allow you to work with types without boxing/unboxing by maintaining the actual type instead of converting it to `object`.
2. Avoiding operations that require boxing, like passing value types to methods that expect `object`.

#### Code Example:

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Without boxing, using generics
        List<int> numbers = new List<int>();
        numbers.Add(10);  // No boxing involved

        foreach (int number in numbers)
        {
            Console.WriteLine(number);  // No unboxing needed
        }
    }
}
```

#### Chinese Explanation：

是的，可以通过以下方式避免装箱和拆箱：
1. 使用**泛型**：泛型允许你在不进行装箱/拆箱的情况下处理类型，因为它保留了实际类型而不是将其转换为 `object`。
2. 避免需要装箱的操作，例如将值类型传递给期望 `object` 类型的方法。

#### 代码示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        // 无装箱，使用泛型
        List<int> numbers = new List<int>();
        numbers.Add(10);  // 不涉及装箱

        foreach (int number in numbers)
        {
            Console.WriteLine(number);  // 不需要拆箱
        }
    }
}
```

---

### Question 117: What effect does boxing and unboxing have on performance?

#### English Explanation:

Boxing and unboxing negatively affect performance because:
1. **Memory allocation**: Boxing allocates memory on the heap for the value type, which is slower than stack allocation.
2. **Garbage collection**: More heap allocations lead to more frequent garbage collections, which can slow down the application.
3. **Memory copying**: Boxing involves copying the value type's data into a heap-allocated object, and unboxing requires copying it back to the stack.

#### Chinese Explanation：

装箱和拆箱对性能有负面影响，原因包括：
1. **内存分配**：装箱在堆上为值类型分配内存，这比栈分配更慢。
2. **垃圾回收**：更多的堆分配会导致更频繁的垃圾回收，从而降低应用程序的速度。
3. **内存复制**：装箱涉及将值类型的数据复制到堆分配的对象中，拆箱需要将其复制回栈中。

---

### Question 118: Are strings allocated on the stack or heap?

#### English Explanation:

In C#, **strings** are **reference types**, so they are allocated on the **heap**. However, string literals are **interned** by the .NET runtime, meaning they are stored in a special memory pool to avoid duplication and save memory.

#### Chinese Explanation：

在 C# 中，**字符串**是**引用类型**，因此它们分配在**堆**上。然而，字符串字面量由 .NET 运行时**驻留**，这意味着它们存储在一个特殊的内存池中，以避免重复并节省内存。

---

### Question 119: How many stack and heaps are created for an application?

#### English Explanation:

In a typical C# application:
- **Stack**: Each thread has its own **stack**, so for every thread in your application, there is a separate stack.
- **Heap**: There is only **one heap** for the entire application, shared by all threads. Objects created on the heap are managed by the garbage collector.

#### Chinese Explanation：

在典型的 C# 应用程序中：
- **栈**：每个线程都有自己的**栈**，因此在应用程序中的每个线程都有一个单独的栈。
- **堆**：整个应用程序只有一个**堆**，由所有线程共享。堆上的对象由垃圾回收器管理。

---

### Question 120: How are stack and heap memory deallocated?

#### English Explanation:

- **Stack**: Stack memory is deallocated automatically when a function call or method returns, following a **LIFO (Last In, First Out)** order.
- **Heap**: Heap memory is deallocated by the **garbage collector**, which automatically identifies and frees objects that are no longer in use.

#### Chinese Explanation：

- **栈**：栈内存在函数调用或方法返回时自动释放，遵循**LIFO（后进先出）**顺序。
- **堆**：堆内存由**垃圾回收器**释放，垃圾回收器会自动识别并释放不再使用的对象。

---
