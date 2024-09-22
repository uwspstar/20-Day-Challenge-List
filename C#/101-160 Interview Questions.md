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
