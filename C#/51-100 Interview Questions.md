# Question 51 - 100

### Question 51: Is it compulsory to implement Abstract methods?

#### English Explanation:

Yes, when a class inherits from an abstract class, it is **compulsory** for that class to provide an implementation for all the **abstract methods**. If the derived class does not implement all abstract methods, it must also be declared as abstract.

#### Chinese Explanation:

是的，当一个类继承自抽象类时，该类**必须**为所有的**抽象方法**提供实现。如果派生类没有实现所有抽象方法，它也必须被声明为抽象类。

---

### Question 52: Why use a simple base class instead of an Abstract class?

#### English Explanation:

A simple base class is used when all methods have full implementations, and no method is left abstract. An **Abstract class** is used when there is a need to enforce that some methods must be implemented by the derived classes. Use a simple base class when:
- All methods can have meaningful default implementations.
- You don't need to enforce any mandatory method implementation in derived classes.

#### Chinese Explanation：

当所有方法都有完整实现，并且没有方法是抽象的时，使用简单的基类。**抽象类**用于需要强制派生类实现某些方法的情况。当以下情况时使用简单的基类：
- 所有方法都可以有有意义的默认实现。
- 不需要强制派生类实现任何方法。

---

### Question 53: Explain Interfaces and why do we need them?

#### English Explanation:

An **Interface** in C# is a contract that defines a set of methods and properties without providing any implementation. Any class or struct that implements an interface must provide concrete implementations of its methods. Interfaces are used for:
- **Decoupling**: Interfaces allow flexibility by separating the definition of behaviors from their implementation.
- **Multiple Inheritance**: Unlike classes, interfaces support multiple inheritance, allowing a class to implement multiple interfaces.
- **Polymorphism**: Interfaces allow objects to be treated polymorphically if they implement the same interface.

#### Chinese Explanation:

C# 中的**接口**是一种约定，定义了一组方法和属性，但不提供任何实现。实现接口的任何类或结构都必须提供具体的实现。使用接口的原因包括：
- **解耦**：接口通过将行为的定义与实现分离来提供灵活性。
- **多继承**：与类不同，接口支持多继承，允许一个类实现多个接口。
- **多态**：接口允许对象以多态的方式进行处理，只要它们实现了相同的接口。

---

### Question 54: Can we write logic in an Interface?

#### English Explanation:

Before **C# 8.0**, interfaces in C# could only have method signatures without any logic (implementation). However, starting with C# 8.0, **default interface methods** allow interfaces to provide method implementations. This feature allows backward compatibility when modifying interfaces.

#### Chinese Explanation:

在 **C# 8.0** 之前，C# 中的接口只能有方法签名，不能包含任何逻辑（实现）。然而，从 C# 8.0 开始，**默认接口方法** 允许接口提供方法实现。这一特性允许在修改接口时保持向后兼容性。

---

### Question 55: Can we define methods as private in an Interface?

#### English Explanation:

No, in C# interfaces, methods cannot be marked as **private**. All methods in an interface are implicitly **public**, and an interface is meant to provide a contract for public behavior that other classes or structs will implement.

#### Chinese Explanation:

不，在 C# 的接口中，方法不能标记为 **private**。接口中的所有方法都是隐式的 **public**，并且接口旨在为其他类或结构体提供要实现的公共行为约定。

---

### Question 56: If I want to change an Interface, what's the best practice?

#### English Explanation:

Changing an interface can break existing implementations, so the best practice is to avoid changing existing interfaces directly. Instead:
- Create a new interface that extends the original one, adding new methods if necessary.
- Use **default interface methods** (available in C# 8.0 and later) to provide a default implementation for new methods, preventing the need for all implementers to change immediately.

#### Chinese Explanation:

更改接口可能会破坏现有的实现，因此最佳实践是避免直接更改现有接口。可以采用以下方式：
- 创建一个扩展原始接口的新接口，必要时添加新方法。
- 使用 **默认接口方法**（在 C# 8.0 及之后的版本中可用）为新方法提供默认实现，避免所有实现者立即进行更改。

---

### Question 57: Explain Multiple Inheritance in Interface?

#### English Explanation:

C# does not support **multiple inheritance** for classes, but it does allow a class to implement multiple interfaces. This allows for **multiple inheritance of behavior** (methods and properties) via interfaces, without inheriting from multiple base classes.

#### Example:

```csharp
public interface IAnimal
{
    void Eat();
}

public interface IMammal
{
    void GiveBirth();
}

public class Dog : IAnimal, IMammal
{
    public void Eat()
    {
        Console.WriteLine("Dog is eating");
    }

    public void GiveBirth()
    {
        Console.WriteLine("Dog gives birth to puppies");
    }
}
```

#### Chinese Explanation：

C# 不支持类的**多重继承**，但允许类实现多个接口。通过接口，C# 允许行为的**多重继承**（方法和属性），而无需从多个基类继承。

#### 例子：

```csharp
public interface IAnimal
{
    void Eat();
}

public interface IMammal
{
    void GiveBirth();
}

public class Dog : IAnimal, IMammal
{
    public void Eat()
    {
        Console.WriteLine("狗在吃东西");
    }

    public void GiveBirth()
    {
        Console.WriteLine("狗生小狗");
    }
}
```

---

### Question 58: Explain Interface Segregation Principle (ISP)?

#### English Explanation:

The **Interface Segregation Principle (ISP)** is one of the SOLID principles that states **"No client should be forced to depend on methods it does not use."** It suggests that larger interfaces should be broken down into smaller, more specific interfaces, so that clients only need to implement the methods they require.

**Key Points:**
- Avoid "fat" interfaces that include methods not relevant to all clients.
- Provide specific, narrowly defined interfaces for different use cases.

#### Chinese Explanation：

**接口隔离原则（ISP）** 是 SOLID 原则之一，指出**“不应该强迫客户端依赖它不使用的方法。”** 它建议将较大的接口拆分为更小、更具体的接口，以便客户端只需要实现它们所需的方法。

**主要要点：**
- 避免包含与所有客户端不相关方法的“肥”接口。
- 为不同的用例提供特定的、定义明确的接口。

---

### Question 59: Can we create an instance of Interface?

#### English Explanation:

No, you cannot create an instance of an **interface** directly in C#. An interface only defines a contract (method signatures and properties) but does not provide implementations. To create an instance, you need to implement the interface in a concrete class and instantiate the class.

#### Chinese Explanation：

不，不能直接在 C# 中创建**接口**的实例。接口只定义了契约（方法签名和属性），但不提供实现。要创建实例，您需要在具体类中实现该接口并实例化该类。

---

### Question 60: Can we do Multiple Inheritance with Abstract classes?

#### English Explanation:

No, C# does not support **multiple inheritance** with abstract classes (or any classes). A class can only inherit from a single base class, whether it's abstract or not. However, you can achieve multiple inheritance-like behavior using interfaces, as a class can implement multiple interfaces.

#### Chinese Explanation：

不，C# 不支持带有抽象类（或任何类）的**多重继承**。一个类只能继承一个基类，无论它是否是抽象的。但是，您可以使用接口实现类似多重继承的行为，因为一个类可以实现多个接口。

---

### Question 61: Abstract Class vs Interface?

#### English Explanation:

| **Feature**                | **Abstract Class**                        | **Interface**                                    |
|----------------------------|-------------------------------------------|-------------------------------------------------|
| **Method Implementation**   | Can have both implemented and abstract methods | Only method signatures (until C# 8.0, which allows default methods) |
| **Fields**                  | Can contain fields                       | Cannot contain fields                           |
| **Multiple Inheritance**     | Supports only single inheritance         | Supports multiple inheritance                   |
| **Use Case**                | Used when classes share common behavior   | Used to define behavior but not the implementation |

#### Chinese Explanation：

| **特性**                   | **抽象类**                               | **接口**                                        |
|----------------------------|------------------------------------------|------------------------------------------------|
| **方法实现**                | 可以有已实现和抽象方法                    | 仅有方法签名（C# 8.0 之后允许默认方法）         |
| **字段**                    | 可以包含字段                              | 不能包含字段                                    |
| **多重继承**                | 只支持单继承                             | 支持多重继承                                    |
| **使用场景**                | 当类共享通用行为时使用                    | 用于定义

行为，但不实现                          |

---

### Question 62: Why do we need Constructors?

#### English Explanation:

**Constructors** are special methods used to initialize an object when it is created. They allow you to set default values for the object's fields, allocate resources, or run any startup code when the object is instantiated. Constructors ensure that an object is in a valid state before it is used.

#### Chinese Explanation：

**构造函数**是用于在对象创建时初始化对象的特殊方法。它们允许您为对象的字段设置默认值、分配资源或在对象实例化时运行任何启动代码。构造函数确保对象在使用之前处于有效状态。

---

### Question 63: In parent-child inheritance, which constructor fires first?

#### English Explanation:

In C#, when a derived class (child class) is instantiated, the **constructor of the base class (parent class)** is called first, followed by the constructor of the derived class. This ensures that the base class is fully initialized before any initialization occurs in the derived class.

#### Chinese Explanation：

在 C# 中，当实例化派生类（子类）时，首先调用**基类（父类）的构造函数**，然后调用派生类的构造函数。这确保基类在派生类进行任何初始化之前已经完全初始化。

---

### Question 64: How are initializers executed?

#### English Explanation:

In C#, **field initializers** are executed before the constructor body. If an object is initialized with a constructor that takes parameters, the field initializers are executed first, followed by the base class constructor, and then the derived class constructor.

#### Chinese Explanation：

在 C# 中，**字段初始化器** 在构造函数体之前执行。如果对象使用带参数的构造函数初始化，则首先执行字段初始化器，然后是基类构造函数，最后是派生类构造函数。

---

### Question 65: How are static constructors executed in Parent-Child inheritance?

#### English Explanation:

In C#, **static constructors** are executed once per type and are executed before any static or instance members are accessed. In the case of inheritance, the **static constructor of the base class** is executed first, followed by the **static constructor of the derived class**.

#### Chinese Explanation：

在 C# 中，**静态构造函数** 每个类型只执行一次，并且在访问任何静态或实例成员之前执行。对于继承，**基类的静态构造函数** 先执行，然后执行 **派生类的静态构造函数**。

---

### Question 66: When does static constructor fire?

#### English Explanation:

A **static constructor** in C# is called automatically before the first instance of the class is created or any static members are accessed. It ensures that any static fields are initialized before they are used.

#### Chinese Explanation：

C# 中的**静态构造函数**在类的第一个实例创建之前或任何静态成员访问之前自动调用。它确保在使用静态字段之前对它们进行初始化。

---

### Question 67: What is Shadowing?

#### English Explanation:

**Shadowing** occurs when a derived class defines a member (method or field) that has the same name as a member in the base class. In C#, shadowing is achieved using the `new` keyword. Shadowing hides the base class member, but the base member can still be accessed using `base.`.

#### Chinese Explanation：

**隐藏（Shadowing）** 发生在派生类定义了与基类成员（方法或字段）同名的成员时。在 C# 中，使用 `new` 关键字实现隐藏。隐藏会覆盖基类成员，但可以使用 `base.` 访问基类成员。

---

### Question 68: Explain method hiding?

#### English Explanation:

**Method hiding** in C# occurs when a derived class defines a method with the same name as a method in the base class but uses the `new` keyword to hide the base class method. The base method is still available and can be called using the `base` keyword.

#### Code Example:

```csharp
public class BaseClass
{
    public void ShowMessage()
    {
        Console.WriteLine("Base class method");
    }
}

public class DerivedClass : BaseClass
{
    public new void ShowMessage()
    {
        Console.WriteLine("Derived class method");
    }
}

class Program
{
    static void Main(string[] args)
    {
        DerivedClass derived = new DerivedClass();
        derived.ShowMessage();   // Outputs: Derived class method

        BaseClass baseRef = new DerivedClass();
        baseRef.ShowMessage();   // Outputs: Base class method
    }
}
```

#### Chinese Explanation：

在 C# 中，**方法隐藏** 发生在派生类定义了与基类方法同名的方法时，但使用 `new` 关键字来隐藏基类方法。基类方法仍然可用，可以使用 `base` 关键字调用。

#### 代码示例：

```csharp
public class BaseClass
{
    public void ShowMessage()
    {
        Console.WriteLine("基类方法");
    }
}

public class DerivedClass : BaseClass
{
    public new void ShowMessage()
    {
        Console.WriteLine("派生类方法");
    }
}

class Program
{
    static void Main(string[] args)
    {
        DerivedClass derived = new DerivedClass();
        derived.ShowMessage();   // 输出: 派生类方法

        BaseClass baseRef = new DerivedClass();
        baseRef.ShowMessage();   // 输出: 基类方法
    }
}
```

---

### Question 69: Shadowing vs Overriding?

#### English Explanation:

- **Shadowing**: Hides a base class method by defining a new method with the same name in the derived class using the `new` keyword. The base class method is still accessible using `base.`.
- **Overriding**: Replaces the base class method with a new implementation in the derived class using the `override` keyword. The base class method cannot be called unless explicitly accessed using `base.`.

**Key Difference**:
- Shadowing is not polymorphic, while overriding is polymorphic and allows runtime binding.

#### Chinese Explanation：

- **隐藏（Shadowing）**：通过在派生类中使用 `new` 关键字定义一个与基类同名的新方法来隐藏基类方法。基类方法仍然可以通过 `base.` 访问。
- **重写（Overriding）**：使用 `override` 关键字在派生类中提供基类方法的新实现。基类方法不能被调用，除非通过 `base.` 明确访问。

**主要区别**：
- 隐藏不是多态的，而重写是多态的，并且允许运行时绑定。

---

### Question 70: When do we need Shadowing?

#### English Explanation:

**Shadowing** is useful when you want to provide a new implementation for a method in the derived class without modifying or affecting the base class's implementation. Shadowing is typically used when:
- You want to define a new behavior for a method that is not directly related to the base class's implementation.
- The base class method is not marked as `virtual`, so it cannot be overridden.

#### Chinese Explanation：

**隐藏（Shadowing）** 在派生类中提供新方法实现而不修改或影响基类的实现时非常有用。通常在以下情况下使用隐藏：
- 您想为一个方法定义新行为，而该行为与基类的实现无直接关系。
- 基类方法未标记为 `virtual`，因此无法重写。

---

### Question 71: Explain Sealed Classes?

#### English Explanation:

A **sealed class** in C# is a class that cannot be inherited. It is used to prevent other classes from extending its functionality. By marking a class as `sealed`, you are ensuring that no other class can derive from it, which can be useful when you want to maintain strict control over a class's implementation.

#### Code Example:

```csharp
public sealed class FinalClass
{
    public void DisplayMessage()
    {
        Console.WriteLine("This is a sealed class.");
    }
}

// The following will cause a compilation error because FinalClass is sealed.
// public class DerivedClass : FinalClass {}

class Program
{
    static void Main(string[] args)
    {
        FinalClass finalObj = new FinalClass();
        finalObj.DisplayMessage();
    }
}
```

#### Chinese Explanation:

C# 中的 **sealed 类** 是不能被继承的类。它用于防止其他类扩展其功能。通过将类标记为 `sealed`，您可以确保没有其他类可以从其派生，这在您想严格控制类的实现时非常有用。

#### 代码示例：

```csharp
public sealed class FinalClass
{
    public void DisplayMessage()
    {
        Console.WriteLine("这是一个 sealed 类。");
    }
}

// 以下代码将导致编译错误，因为 FinalClass 是 sealed 的。
// public class DerivedClass : FinalClass {}

class Program
{
    static void Main(string[] args)
    {
        FinalClass finalObj = new FinalClass();
        finalObj.DisplayMessage();
    }
}
```

---

### Question 72: Can we create an instance of Sealed classes?

#### English Explanation:

Yes, you can create an instance of a **sealed class** just like any other class. However, you cannot inherit from a sealed class. Sealed classes behave like regular classes except that they cannot be used as a base class for inheritance.

#### Chinese Explanation：

是的，您可以像创建任何其他类一样创建**sealed 类**的实例。但是，您不能继承 sealed 类。Sealed 类的行为与常规类相同，唯一的区别是它不能用作继承的基类。

---

### Question 73: What are nested classes, and when to use them?

#### English Explanation:

A **nested class** is a class defined inside another class. Nested classes are used when the inner class logically belongs only to the outer class. It provides better encapsulation and can access the private members of the containing (outer) class.

**When to use Nested Classes**:
- When a class is tightly coupled with another class and is not useful independently.
- To group logically related classes inside a single outer class for better organization.

#### Code Example:

```csharp
public class OuterClass
{
    private string outerField = "Outer field";

    public class NestedClass
    {
        public void Display()
        {
            OuterClass outer = new OuterClass();
            Console.WriteLine(outer.outerField); // Nested class can access outer class's private fields
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        OuterClass.NestedClass nested = new OuterClass.NestedClass();
        nested.Display();
    }
}
```

#### Chinese Explanation：

**嵌套类** 是在另一个类内部定义的类。嵌套类用于当内部类仅逻辑上属于外部类时。它提供了更好的封装，并且可以访问包含类（外部类）的私有成员。

**何时使用嵌套类**：
- 当一个类与另一个类紧密耦合且不能独立使用时。
- 将逻辑上相关的类分组到单个外部类中，以便更好地组织。

#### 代码示例：

```csharp
public class OuterClass
{
    private string outerField = "外部字段";

    public class NestedClass
    {
        public void Display()
        {
            OuterClass outer = new OuterClass();
            Console.WriteLine(outer.outerField); // 嵌套类可以访问外部类的私有字段
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        OuterClass.NestedClass nested = new OuterClass.NestedClass();
        nested.Display();
    }
}
```

---

### Question 74: Can Nested classes access outer class variables?

#### English Explanation:

Yes, nested classes in C# can access the private and public members of their outer class, as long as they have a reference to an instance of the outer class. If the nested class is static, it can only access static members of the outer class.

#### Chinese Explanation：

是的，C# 中的嵌套类可以访问它们外部类的私有和公共成员，只要它们有外部类实例的引用。如果嵌套类是静态的，它只能访问外部类的静态成员。

---

### Question 75: Can we have public, protected access modifiers in nested classes?

#### English Explanation:

Yes, nested classes in C# can have **public**, **private**, **protected**, **internal**, and **protected internal** access modifiers. The access level of the nested class is independent of the access level of the outer class.

- **public**: The nested class is accessible from any code.
- **protected**: The nested class is accessible only within its containing class and any derived classes.
- **private**: The nested class is only accessible within the containing class.

#### Chinese Explanation：

是的，C# 中的嵌套类可以有 **public**、**private**、**protected**、**internal** 和 **protected internal** 访问修饰符。嵌套类的访问级别与外部类的访问级别无关。

- **public**：嵌套类可从任何代码访问。
- **protected**：嵌套类只能在包含类及其派生类中访问。
- **private**：嵌套类只能在包含类中访问。

---

### Question 76: Explain Partial Classes?

#### English Explanation:

**Partial classes** in C# allow a class to be split across multiple files. All parts of a partial class are combined into a single class when the application is compiled. Partial classes are often used to separate automatically generated code from user-defined code, improving maintainability and clarity.

#### Code Example:

```csharp
// File 1: Part of the class
public partial class MyClass
{
    public void MethodA()
    {
        Console.WriteLine("Method A");
    }
}

// File 2: Another part of the class
public partial class MyClass
{
    public void MethodB()
    {
        Console.WriteLine("Method B");
    }
}

class Program
{
    static void Main(string[] args)
    {
        MyClass myClass = new MyClass();
        myClass.MethodA();
        myClass.MethodB();
    }
}
```

#### Chinese Explanation：

C# 中的**部分类**允许类分散在多个文件中。当应用程序编译时，部分类的所有部分都合并为一个类。部分类通常用于将自动生成的代码与用户定义的代码分开，以提高可维护性和清晰度。

#### 代码示例：

```csharp
// 文件 1：类的一部分
public partial class MyClass
{
    public void MethodA()
    {
        Console.WriteLine("方法 A");
    }
}

// 文件 2：类的另一部分
public partial class MyClass
{
    public void MethodB()
    {
        Console.WriteLine("方法 B");
    }
}

class Program
{
    static void Main(string[] args)
    {
        MyClass myClass = new MyClass();
        myClass.MethodA();
        myClass.MethodB();
    }
}
```

---

### Question 77: In what scenarios do we use partial classes?

#### English Explanation:

**Partial classes** are used in scenarios where:
1. **Separation of concerns**: Automatically generated code (e.g., from a designer or a tool) can be placed in one file, while the user’s code can be in another file.
2. **Large classes**: When a class is large and complex, splitting it across multiple files can improve readability and maintainability.
3. **Team collaboration**: Different team members can work on different parts of the same class simultaneously.

#### Chinese Explanation：

**部分类** 适用于以下场景：
1. **关注点分离**：自动生成的代码（如来自设计器或工具）可以放在一个文件中，而用户的代码可以放在另一个文件中。
2. **大型类**：当类庞大且复杂时，将其拆分为多个文件可以提高可读性和可维护性。
3. **团队协作**：不同的团队成员可以同时处理同一个类的不同部分。

---

### Question 78: What is SOLID?

#### English Explanation:

**SOLID** is an acronym for five design principles that help developers build more maintainable, understandable, and flexible software:
1. **S** - Single Responsibility Principle (SRP): A class should have only one reason to change.
2. **O** - Open/Closed Principle (OCP): Software entities should be open for extension but closed for modification.
3. **L** - Liskov Substitution Principle (LSP): Derived classes should be substitutable for their base classes.
4. **I** - Interface Segregation Principle (ISP): Clients should not be forced to depend on methods they do not use.
5. **D** - Dependency Inversion Principle (DIP): Depend on

 abstractions, not on concretions.

#### Chinese Explanation：

**SOLID** 是五个设计原则的缩写，这些原则帮助开发人员构建更易维护、理解和灵活的软件：
1. **S** - 单一职责原则（SRP）：一个类应该只有一个改变的理由。
2. **O** - 开闭原则（OCP）：软件实体应对扩展开放，对修改关闭。
3. **L** - 里氏替换原则（LSP）：派生类应可以替换基类。
4. **I** - 接口隔离原则（ISP）：客户端不应被迫依赖它们不使用的方法。
5. **D** - 依赖倒置原则（DIP）：依赖抽象，而不是依赖具体实现。

---

### Question 79: What is the full form of SOLID?

#### English Explanation:

The full form of **SOLID** is:
- **S** - Single Responsibility Principle (SRP)
- **O** - Open/Closed Principle (OCP)
- **L** - Liskov Substitution Principle (LSP)
- **I** - Interface Segregation Principle (ISP)
- **D** - Dependency Inversion Principle (DIP)

#### Chinese Explanation：

**SOLID** 的完整形式是：
- **S** - 单一职责原则（SRP）
- **O** - 开闭原则（OCP）
- **L** - 里氏替换原则（LSP）
- **I** - 接口隔离原则（ISP）
- **D** - 依赖倒置原则（DIP）

---

### Question 80: What is the goal of SOLID?

#### English Explanation:

The goal of the **SOLID** principles is to create software that is:
- **Easier to maintain**: By ensuring each class and module has a clear purpose and minimal dependencies.
- **More flexible**: By allowing code to be extended without modifying existing code.
- **More understandable**: By promoting clear, organized, and decoupled design.
- **Less prone to bugs**: By enforcing good practices that reduce complexity.

#### Chinese Explanation：

**SOLID** 原则的目标是创建：
- **更易维护的软件**：通过确保每个类和模块都有明确的目的和最小的依赖性。
- **更灵活的软件**：通过允许扩展代码而不修改现有代码。
- **更易理解的软件**：通过促进清晰、有组织和解耦的设计。
- **更少错误的软件**：通过实施减少复杂性的良好实践来降低错误的可能性。

---

### Question 81: Explain SRP with an example?

#### English Explanation:

**SRP (Single Responsibility Principle)** states that a class should have only one reason to change, meaning it should have only one job or responsibility. A class with multiple responsibilities is harder to maintain and test. SRP encourages developers to divide responsibilities among different classes.

#### Code Example:

```csharp
// Violation of SRP: The Report class is responsible for generating and printing reports
public class Report
{
    public string GenerateReport()
    {
        return "Report Content";
    }

    public void PrintReport()
    {
        Console.WriteLine("Printing Report...");
    }
}

// Applying SRP: Separate responsibilities into two classes
public class ReportGenerator
{
    public string GenerateReport()
    {
        return "Report Content";
    }
}

public class ReportPrinter
{
    public void PrintReport(string report)
    {
        Console.WriteLine("Printing: " + report);
    }
}

class Program
{
    static void Main(string[] args)
    {
        ReportGenerator generator = new ReportGenerator();
        ReportPrinter printer = new ReportPrinter();
        
        string report = generator.GenerateReport();
        printer.PrintReport(report);
    }
}
```

In the above example, the `Report` class originally had two responsibilities: generating and printing a report. By applying SRP, these responsibilities are split into two separate classes (`ReportGenerator` and `ReportPrinter`).

#### Chinese Explanation:

**单一职责原则（SRP）** 指出，一个类应该只有一个引起变化的原因，也就是说它应该只有一个职责。具有多重职责的类更难维护和测试。SRP 鼓励开发人员将职责分配到不同的类中。

#### 代码示例：

```csharp
// 违反 SRP：Report 类负责生成和打印报告
public class Report
{
    public string GenerateReport()
    {
        return "报告内容";
    }

    public void PrintReport()
    {
        Console.WriteLine("打印报告...");
    }
}

// 应用 SRP：将职责分配给两个类
public class ReportGenerator
{
    public string GenerateReport()
    {
        return "报告内容";
    }
}

public class ReportPrinter
{
    public void PrintReport(string report)
    {
        Console.WriteLine("打印: " + report);
    }
}

class Program
{
    static void Main(string[] args)
    {
        ReportGenerator generator = new ReportGenerator();
        ReportPrinter printer = new ReportPrinter();
        
        string report = generator.GenerateReport();
        printer.PrintReport(report);
    }
}
```

---

### Question 82: What is the benefit of SRP?

#### English Explanation:

The **Single Responsibility Principle (SRP)** offers several benefits:
1. **Improved Maintainability**: When a class has a single responsibility, changes are easier to manage and implement.
2. **Better Testability**: Smaller classes with fewer responsibilities are easier to test.
3. **Enhanced Reusability**: Classes with focused responsibilities are more likely to be reusable in other parts of the system.
4. **Clearer Design**: SRP leads to a cleaner, more understandable codebase, as each class has a clearly defined purpose.

#### Chinese Explanation:

**单一职责原则（SRP）** 提供了以下好处：
1. **提高可维护性**：当一个类只有一个职责时，更容易管理和实现变更。
2. **更好的可测试性**：职责较少的小类更容易测试。
3. **增强的可重用性**：职责集中的类更有可能在系统的其他部分中重用。
4. **更清晰的设计**：SRP 使代码库更加简洁易懂，因为每个类都有明确的目的。

---

### Question 83: Explain OCP with an example?

#### English Explanation:

**OCP (Open/Closed Principle)** states that software entities (such as classes, modules, functions) should be **open for extension but closed for modification**. This means that the behavior of a module should be extended without modifying its source code.

#### Code Example:

```csharp
// Without OCP: Modifying existing code to support new operations
public class Calculator
{
    public int Calculate(int a, int b, string operation)
    {
        if (operation == "add")
            return a + b;
        else if (operation == "subtract")
            return a - b;
        // New operation requires modifying existing code
        else if (operation == "multiply")
            return a * b;
        else
            throw new InvalidOperationException("Unsupported operation");
    }
}

// Applying OCP: Extending behavior without modifying existing code
public interface IOperation
{
    int Perform(int a, int b);
}

public class AddOperation : IOperation
{
    public int Perform(int a, int b)
    {
        return a + b;
    }
}

public class SubtractOperation : IOperation
{
    public int Perform(int a, int b)
    {
        return a - b;
    }
}

public class Calculator
{
    public int Calculate(int a, int b, IOperation operation)
    {
        return operation.Perform(a, b);
    }
}

class Program
{
    static void Main(string[] args)
    {
        Calculator calculator = new Calculator();
        
        IOperation addOperation = new AddOperation();
        Console.WriteLine("Addition: " + calculator.Calculate(5, 3, addOperation));

        IOperation subtractOperation = new SubtractOperation();
        Console.WriteLine("Subtraction: " + calculator.Calculate(5, 3, subtractOperation));
    }
}
```

In this example, the `Calculator` class is open for extension because new operations can be added without modifying the existing code by introducing new implementations of `IOperation`.

#### Chinese Explanation:

**开闭原则（OCP）** 指出，软件实体（如类、模块、函数）应该**对扩展开放，对修改关闭**。这意味着模块的行为应能通过扩展而不修改源代码来改变。

#### 代码示例：

```csharp
// 未应用 OCP：为支持新操作修改现有代码
public class Calculator
{
    public int Calculate(int a, int b, string operation)
    {
        if (operation == "add")
            return a + b;
        else if (operation == "subtract")
            return a - b;
        // 新操作需要修改现有代码
        else if (operation == "multiply")
            return a * b;
        else
            throw new InvalidOperationException("不支持的操作");
    }
}

// 应用 OCP：扩展行为而不修改现有代码
public interface IOperation
{
    int Perform(int a, int b);
}

public class AddOperation : IOperation
{
    public int Perform(int a, int b)
    {
        return a + b;
    }
}

public class SubtractOperation : IOperation
{
    public int Perform(int a, int b)
    {
        return a - b;
    }
}

public class Calculator
{
    public int Calculate(int a, int b, IOperation operation)
    {
        return operation.Perform(a, b);
    }
}

class Program
{
    static void Main(string[] args)
    {
        Calculator calculator = new Calculator();
        
        IOperation addOperation = new AddOperation();
        Console.WriteLine("加法: " + calculator.Calculate(5, 3, addOperation));

        IOperation subtractOperation = new SubtractOperation();
        Console.WriteLine("减法: " + calculator.Calculate(5, 3, subtractOperation));
    }
}
```

---

### Question 84: What is the benefit of OCP?

#### English Explanation:

The **Open/Closed Principle (OCP)** provides the following benefits:
1. **Improved Maintainability**: Changes can be made to a system by adding new functionality without altering existing code, reducing the likelihood of introducing bugs.
2. **Enhanced Flexibility**: It promotes a flexible system where new features or operations can be added easily.
3. **Reduced Risk**: Existing code is less likely to be impacted by new features, reducing the risk of unintended consequences.

#### Chinese Explanation:

**开闭原则（OCP）** 提供以下好处：
1. **提高可维护性**：通过添加新功能而不修改现有代码来对系统进行更改，减少引入错误的可能性。
2. **增强灵活性**：它促进了一个灵活的系统，能够轻松添加新功能或操作。
3. **降低风险**：现有代码不太可能受到新功能的影响，从而减少了意外后果的风险。

---

### Question 85: Explain Liskov Substitution Principle (LSP) with a violation example?

#### English Explanation:

The **Liskov Substitution Principle (LSP)** states that **subtypes must be substitutable for their base types**. This means that an instance of a derived class should be able to replace an instance of its base class without altering the desirable properties of the program.

**Violation Example**:

```csharp
public class Bird
{
    public virtual void Fly()
    {
        Console.WriteLine("Bird is flying");
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotSupportedException("Penguins can't fly");
    }
}
```

In this case, the `Penguin` class violates LSP because it cannot fly, but it overrides the `Fly` method from its base class, `Bird`. According to LSP, the derived class should not throw unexpected exceptions when substituting for the base class.

#### Chinese Explanation:

**里氏替换原则（LSP）** 指出，**子类型必须能够

替换其基类型**。这意味着派生类的实例应该能够替换其基类的实例，而不会改变程序的期望属性。

**违规示例**：

```csharp
public class Bird
{
    public virtual void Fly()
    {
        Console.WriteLine("鸟在飞");
    }
}

public class Penguin : Bird
{
    public override void Fly()
    {
        throw new NotSupportedException("企鹅不会飞");
    }
}
```

在这个例子中，`Penguin` 类违反了 LSP，因为它不能飞，但它重写了基类 `Bird` 的 `Fly` 方法。根据 LSP，派生类在替换基类时不应抛出意外的异常。

---

### Question 86: How can we fix the Liskov violation?

#### English Explanation:

To fix the **Liskov Substitution Principle (LSP)** violation in the previous example, we can refactor the design to ensure that only birds that can fly implement a method for flying. One possible solution is to introduce an interface that defines flying behavior, and only birds that can fly implement it.

#### Code Example:

```csharp
public interface IFlyable
{
    void Fly();
}

public class Bird
{
    public void Walk()
    {
        Console.WriteLine("Bird is walking");
    }
}

public class Sparrow : Bird, IFlyable
{
    public void Fly()
    {
        Console.WriteLine("Sparrow is flying");
    }
}

public class Penguin : Bird
{
    // No Fly method, Penguins don't fly
}
```

Now, `Sparrow` implements the `IFlyable` interface and can fly, while `Penguin` doesn't need to implement the `Fly` method.

#### Chinese Explanation:

要解决**里氏替换原则（LSP）**的违规问题，我们可以重新设计，确保只有能飞的鸟类实现飞行方法。一个可能的解决方案是引入一个定义飞行行为的接口，并且只有会飞的鸟类实现该接口。

#### 代码示例：

```csharp
public interface IFlyable
{
    void Fly();
}

public class Bird
{
    public void Walk()
    {
        Console.WriteLine("鸟在走路");
    }
}

public class Sparrow : Bird, IFlyable
{
    public void Fly()
    {
        Console.WriteLine("麻雀在飞");
    }
}

public class Penguin : Bird
{
    // 没有 Fly 方法，企鹅不会飞
}
```

---

### Question 87: Explain Interface Segregation Principle (ISP)?

#### English Explanation:

The **Interface Segregation Principle (ISP)** states that **no client should be forced to depend on methods it does not use**. This principle encourages the design of small, specific interfaces that only contain methods relevant to the client, instead of having large, "fat" interfaces with many methods.

#### Code Example:

```csharp
// Violating ISP: A single large interface with irrelevant methods
public interface IWorker
{
    void Work();
    void Eat();
}

public class Robot : IWorker
{
    public void Work()
    {
        Console.WriteLine("Robot is working.");
    }

    public void Eat()
    {
        // Robots don't eat, so this is unnecessary.
        throw new NotImplementedException();
    }
}

// Applying ISP: Separate the interfaces
public interface IWorkable
{
    void Work();
}

public interface IFeedable
{
    void Eat();
}

public class Robot : IWorkable
{
    public void Work()
    {
        Console.WriteLine("Robot is working.");
    }
}
```

In this example, the `Robot` class does not need to implement the `Eat` method, so we applied ISP by splitting the `IWorker` interface into `IWorkable` and `IFeedable`.

#### Chinese Explanation：

**接口隔离原则（ISP）** 指出，**不应该强迫客户端依赖它们不使用的方法**。该原则鼓励设计小型的、具体的接口，这些接口只包含与客户端相关的方法，而不是拥有许多方法的“大而全”接口。

#### 代码示例：

```csharp
// 违反 ISP：一个大的接口包含无关的方法
public interface IWorker
{
    void Work();
    void Eat();
}

public class Robot : IWorker
{
    public void Work()
    {
        Console.WriteLine("机器人在工作。");
    }

    public void Eat()
    {
        // 机器人不吃东西，所以这不必要。
        throw new NotImplementedException();
    }
}

// 应用 ISP：将接口分离
public interface IWorkable
{
    void Work();
}

public interface IFeedable
{
    void Eat();
}

public class Robot : IWorkable
{
    public void Work()
    {
        Console.WriteLine("机器人在工作。");
    }
}
```

---

### Question 88: Is there a connection between LSP and ISP?

#### English Explanation:

Yes, there is a connection between **Liskov Substitution Principle (LSP)** and **Interface Segregation Principle (ISP)**. Both principles emphasize the importance of **behavioral consistency**:
- **LSP** focuses on ensuring that derived classes can substitute base classes without altering the program's behavior.
- **ISP** focuses on ensuring that clients are not forced to implement or depend on irrelevant methods.

By adhering to both LSP and ISP, you can ensure that your system is more flexible, easier to extend, and less prone to errors due to behavioral inconsistencies.

#### Chinese Explanation：

是的，**里氏替换原则（LSP）** 和 **接口隔离原则（ISP）** 之间存在联系。两个原则都强调了**行为一致性**的重要性：
- **LSP** 关注确保派生类可以替换基类而不改变程序的行为。
- **ISP** 关注确保客户端不被强迫实现或依赖无关的方法。

通过遵循 LSP 和 ISP，可以确保系统更加灵活、易于扩展，并且由于行为不一致性导致的错误更少。

---

### Question 89: Define Dependency Inversion Principle (DIP)?

#### English Explanation:

The **Dependency Inversion Principle (DIP)** is one of the SOLID principles that states **high-level modules should not depend on low-level modules; both should depend on abstractions**. This means that:
- **Abstractions** (interfaces or abstract classes) should not depend on concrete implementations.
- **Concrete classes** should depend on abstractions.

#### Chinese Explanation：

**依赖倒置原则（DIP）** 是 SOLID 原则之一，指出**高层模块不应该依赖低层模块；二者都应该依赖抽象**。这意味着：
- **抽象**（接口或抽象类）不应该依赖具体实现。
- **具体类**应该依赖抽象。

---

### Question 90: What is higher-level module and lower-level module?

#### English Explanation:

- A **higher-level module** is responsible for complex or abstract logic, often involving decision-making and controlling the flow of the program.
- A **lower-level module** handles basic, concrete tasks, such as handling data input/output, networking, or database access.

In the context of **DIP**, higher-level modules should depend on abstractions rather than on the specific implementations of lower-level modules.

#### Chinese Explanation：

- **高层模块** 负责复杂或抽象逻辑，通常涉及决策和控制程序的流程。
- **低层模块** 处理基本的、具体的任务，例如处理数据输入/输出、网络或数据库访问。

在 **依赖倒置原则（DIP）** 的上下文中，高层模块应该依赖于抽象，而不是具体的低层模块实现。

---

### Question 91: How does Dependency Inversion benefit, show with an example?

#### English Explanation:

The **Dependency Inversion Principle (DIP)** helps in creating flexible and decoupled systems by ensuring that high-level modules depend on abstractions rather than on concrete implementations. This reduces the impact of changes in low-level modules on high-level modules, making the system more maintainable and testable.

#### Code Example:

Without DIP:

```csharp
public class FileLogger
{
    public void Log(string message)
    {
        Console.WriteLine("Logging to file: " + message);
    }
}

public class UserService
{
    private FileLogger logger = new FileLogger();

    public void RegisterUser(string username)
    {
        // Register user logic
        logger.Log("User registered: " + username);
    }
}
```

With DIP:

```csharp
public interface ILogger
{
    void Log(string message);
}

public class FileLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine("Logging to file: " + message);
    }
}

public class UserService
{
    private ILogger logger;

    public UserService(ILogger logger)
    {
        this.logger = logger;
    }

    public void RegisterUser(string username)
    {
        // Register user logic
        logger.Log("User registered: " + username);
    }
}

class Program
{
    static void Main(string[] args)
    {
        ILogger logger = new FileLogger();
        UserService service = new UserService(logger);
        service.RegisterUser("JohnDoe");
    }
}
```

In the second example, `UserService` depends on the `ILogger` abstraction, making it easier to swap out the logging mechanism without changing the `UserService` class.

#### Chinese Explanation:

**依赖倒置原则（DIP）** 通过确保高层模块依赖于抽象而不是具体实现，帮助创建灵活且解耦的系统。这减少了低层模块的更改对高层模块的影响，使系统更易维护和测试。

#### 代码示例：

不使用 DIP：

```csharp
public class FileLogger
{
    public void Log(string message)
    {
        Console.WriteLine("记录到文件：" + message);
    }
}

public class UserService
{
    private FileLogger logger = new FileLogger();

    public void RegisterUser(string username)
    {
        // 注册用户逻辑
        logger.Log("用户已注册：" + username);
    }
}
```

使用 DIP：

```csharp
public interface ILogger
{
    void Log(string message);
}

public class FileLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine("记录到文件：" + message);
    }
}

public class UserService
{
    private ILogger logger;

    public UserService(ILogger logger)
    {
        this.logger = logger;
    }

    public void RegisterUser(string username)
    {
        // 注册用户逻辑
        logger.Log("用户已注册：" + username);
    }
}

class Program
{
    static void Main(string[] args)
    {
        ILogger logger = new FileLogger();
        UserService service = new UserService(logger);
        service.RegisterUser("JohnDoe");
    }
}
```

---

### Question 92: Will only Dependency Inversion solve decoupling problems?

#### English Explanation:

No, **Dependency Inversion** alone cannot solve all decoupling problems. While it encourages high-level modules to depend on abstractions rather than concrete implementations, true decoupling requires a combination of principles like **Interface Segregation**, **Single Responsibility**, and **Open/Closed** principles. These principles work together to reduce dependencies and make the system more flexible.

#### Chinese Explanation：

不，**依赖倒置** 本身不能解决所有的解耦问题。虽然它鼓励高层模块依赖抽象而不是具体实现，但真正的解耦需要结合**接口隔离**、**单一职责** 和 **开闭原则** 等原则共同作用，减少依赖性并使系统更灵活。

---

### Question 93: Why do developers move object creation outside high-level modules?

#### English Explanation:

Developers move **object creation** outside high-level modules to adhere to the **Dependency Inversion Principle (DIP)** and reduce coupling. By outsourcing object creation to a **factory** or **dependency injection** mechanism, high-level modules depend on abstractions rather than concrete implementations. This allows for easier testing, maintenance, and flexibility in changing dependencies without modifying high-level logic.

#### Chinese Explanation：

开发人员将**对象创建**移到高层模块之外，以遵循**依赖倒置原则（DIP）** 并减少耦合。通过将对象创建委托给**工厂**或**依赖注入**机制，高层模块依赖于抽象而不是具体实现。这使得测试、维护更容易，并且在不修改高层逻辑的情况下可以灵活更改依赖关系。

---

### Question 94: Explain IOC (Inversion of Control)?

#### English Explanation:

**Inversion of Control (IOC)** is a design principle where the control of object creation and dependency management is transferred from the object itself to a **container** or **framework**. This is commonly achieved through **dependency injection** or **service locators**. It allows for better decoupling and more flexible code.

#### Code Example:

Using Dependency Injection (DI) in IOC:

```csharp
public interface IMessageService
{
    void SendMessage(string message);
}

public class EmailService : IMessageService
{
    public void SendMessage(string message)
    {
        Console.WriteLine("Email sent: " + message);
    }
}

public class Notification
{
    private IMessageService messageService;

    // Dependency Injection via constructor
    public Notification(IMessageService messageService)
    {
        this.messageService = messageService;
    }

    public void NotifyUser()
    {
        messageService.SendMessage("Hello User!");
    }
}

class Program
{
    static void Main(string[] args)
    {
        IMessageService service = new EmailService();
        Notification notification = new Notification(service);
        notification.NotifyUser();
    }
}
```

Here, **IOC** is applied by injecting `EmailService` into `Notification`, decoupling the `Notification` class from a specific implementation of the message service.

#### Chinese Explanation：

**控制反转（IOC）** 是一种设计原则，其中对象的创建和依赖管理的控制权从对象本身转移到**容器**或**框架**。通常通过**依赖注入**或**服务定位器**来实现。这种方式使代码更解耦且更灵活。

#### 代码示例：

使用依赖注入实现 IOC：

```csharp
public interface IMessageService
{
    void SendMessage(string message);
}

public class EmailService : IMessageService
{
    public void SendMessage(string message)
    {
        Console.WriteLine("发送邮件：" + message);
    }
}

public class Notification
{
    private IMessageService messageService;

    // 通过构造函数进行依赖注入
    public Notification(IMessageService messageService)
    {
        this.messageService = messageService;
    }

    public void NotifyUser()
    {
        messageService.SendMessage("你好，用户！");
    }
}

class Program
{
    static void Main(string[] args)
    {
        IMessageService service = new EmailService();
        Notification notification = new Notification(service);
        notification.NotifyUser();
    }
}
```

---

### Question 95: Explain Dependency Injection with an example?

#### English Explanation:

**Dependency Injection (DI)** is a design pattern where the dependencies of an object are injected into it rather than being created inside the object. This allows for better decoupling, making code easier to test and maintain. DI can be done via **constructor injection**, **property injection**, or **method injection**.

#### Code Example:

```csharp
public interface IDatabase
{
    void SaveData(string data);
}

public class SqlDatabase : IDatabase
{
    public void SaveData(string data)
    {
        Console.WriteLine("Saving data to SQL Database: " + data);
    }
}

public class DataService
{
    private IDatabase database;

    // Constructor Injection
    public DataService(IDatabase database)
    {
        this.database = database;
    }

    public void Save(string data)
    {
        database.SaveData(data);
    }
}

class Program
{
    static void Main(string[] args)
    {
        IDatabase db = new SqlDatabase();
        DataService dataService = new DataService(db);
        dataService.Save("Sample Data");
    }
}
```

Here, `DataService` doesn't create its dependency (`IDatabase`) directly. Instead, the dependency is injected through the constructor.

#### Chinese Explanation：

**依赖注入（DI）** 是一种设计模式，其中对象的依赖项被注入到对象中，而不是在对象内部创建。这种方式提高了解耦性，使代码更易于测试和维护。DI 可以通过**构造函数注入**、**属性注入**或**方法注入**来实现。

#### 代码示例：

```csharp
public interface IDatabase
{
    void SaveData(string data);
}

public class SqlDatabase : IDatabase
{
    public void SaveData(string data)
    {
        Console.WriteLine("将数据保存到 SQL 数据库：" + data);
    }
}

public class DataService
{
    private IDatabase database;

    // 构造函数注入
    public DataService(IDatabase database)
    {
        this.database = database;
    }

    public void Save(string data)
    {
        database.SaveData(data);
    }
}

class Program
{
    static void Main(string[] args)
   



 {
        IDatabase db = new SqlDatabase();
        DataService dataService = new DataService(db);
        dataService.Save("示例数据");
    }
}
```

---

### Question 96: Is SOLID, IOC, and DI design pattern or principle?

#### English Explanation:

- **SOLID**: These are **design principles** that guide how to design software systems for better maintainability and flexibility.
- **IOC (Inversion of Control)**: This is a **principle** that describes how control of object creation should be inverted.
- **DI (Dependency Injection)**: This is a **design pattern** used to implement IOC by injecting dependencies into objects.

In summary:
- **SOLID** = Design principles.
- **IOC** = Principle.
- **DI** = Design pattern.

#### Chinese Explanation：

- **SOLID**：这些是**设计原则**，指导如何设计软件系统以提高可维护性和灵活性。
- **IOC（控制反转）**：这是一种**原则**，描述了如何将对象创建的控制权反转。
- **DI（依赖注入）**：这是一种**设计模式**，用于通过将依赖项注入对象来实现 IOC。

总结：
- **SOLID** = 设计原则。
- **IOC** = 原则。
- **DI** = 设计模式。

---

### Question 97: Is only SOLID enough for good code/architecture?

#### English Explanation:

No, while **SOLID principles** are a great foundation for creating maintainable and flexible code, they are not sufficient on their own for a robust architecture. Other principles, patterns, and practices such as **DRY (Don't Repeat Yourself)**, **KISS (Keep It Simple, Stupid)**, **YAGNI (You Aren't Gonna Need It)**, and **Design Patterns** are also essential to creating well-structured and scalable systems.

#### Chinese Explanation：

不，尽管 **SOLID 原则** 是创建可维护和灵活代码的良好基础，但它们本身不足以构建健壮的架构。其他原则、模式和实践，如 **DRY（不要重复自己）**、**KISS（保持简单，愚蠢）**、**YAGNI（你不需要它）** 和 **设计模式** 对于创建结构良好且可扩展的系统也至关重要。

---

### Question 98: What are the different types of "HAS-A" relationships?

#### English Explanation:

A **HAS-A relationship** (also known as **composition**) describes how one class contains or is composed of another class. It is different from inheritance and can be expressed in the following ways:
1. **Composition**: One class owns another class's object. If the container object is destroyed, the contained object is also destroyed.
2. **Aggregation**: A weak relationship where one class contains another, but the contained object can exist independently of the container.

#### Chinese Explanation：

**HAS-A 关系**（也称为**组合关系**）描述了一个类包含或由另一个类组成的方式。它不同于继承，并可以通过以下方式表达：
1. **组合（Composition）**：一个类拥有另一个类的对象。如果容器对象被销毁，包含的对象也会被销毁。
2. **聚合（Aggregation）**：一种弱关系，一个类包含另一个类，但包含的对象可以独立于容器存在。

---

### Question 99: What is a composition relationship?

#### English Explanation:

**Composition** is a **strong HAS-A relationship** where one class contains another class as a part of itself. If the containing (parent) class is destroyed, the composed (child) object is also destroyed. Composition implies ownership, and the lifetime of the contained object is tightly coupled with the container class.

#### Code Example:

```csharp
public class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine started");
    }
}

public class Car
{
    private Engine engine;

    public Car()
    {
        engine = new Engine(); // Composition: Car owns the engine
    }

    public void StartCar()
    {
        engine.Start();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Car car = new Car();
        car.StartCar();
    }
}
```

In this example, `Car` has a composition relationship with `Engine`. If the `Car` object is destroyed, the `Engine` object is also destroyed.

#### Chinese Explanation：

**组合（Composition）** 是一种**强 HAS-A 关系**，其中一个类将另一个类作为自身的一部分。如果包含（父）类被销毁，组合的（子）对象也会被销毁。组合意味着所有权，包含对象的生命周期与容器类紧密耦合。

#### 代码示例：

```csharp
public class Engine
{
    public void Start()
    {
        Console.WriteLine("引擎启动");
    }
}

public class Car
{
    private Engine engine;

    public Car()
    {
        engine = new Engine(); // 组合关系：汽车拥有引擎
    }

    public void StartCar()
    {
        engine.Start();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Car car = new Car();
        car.StartCar();
    }
}
```

---

### Question 100: Explain Aggregation?

#### English Explanation:

**Aggregation** is a **weak HAS-A relationship** where one class contains another class, but the contained object can exist independently of the container. If the container object is destroyed, the contained object can still exist.

#### Code Example:

```csharp
public class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine started");
    }
}

public class Car
{
    private Engine engine;

    public Car(Engine engine)
    {
        this.engine = engine; // Aggregation: Car uses an existing engine
    }

    public void StartCar()
    {
        engine.Start();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Engine myEngine = new Engine();
        Car car = new Car(myEngine);
        car.StartCar();
    }
}
```

In this example, the `Engine` exists independently of `Car`, demonstrating aggregation.

#### Chinese Explanation：

**聚合（Aggregation）** 是一种**弱 HAS-A 关系**，其中一个类包含另一个类，但包含的对象可以独立于容器存在。如果容器对象被销毁，包含的对象仍然可以存在。

#### 代码示例：

```csharp
public class Engine
{
    public void Start()
    {
        Console.WriteLine("引擎启动");
    }
}

public class Car
{
    private Engine engine;

    public Car(Engine engine)
    {
        this.engine = engine; // 聚合关系：汽车使用现有的引擎
    }

    public void StartCar()
    {
        engine.Start();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Engine myEngine = new Engine();
        Car car = new Car(myEngine);
        car.StartCar();
    }
}
```

---

