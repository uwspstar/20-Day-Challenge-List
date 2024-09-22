
### Question 150: What are design patterns?

#### English Explanation:

**Design patterns** are proven solutions to common software design problems. They provide templates for how to structure and design your code to solve specific problems in a flexible and reusable way. Design patterns are typically categorized into:
1. **Creational Patterns**: Deal with object creation (e.g., Singleton, Factory).
2. **Structural Patterns**: Deal with object composition (e.g., Adapter, Decorator).
3. **Behavioral Patterns**: Deal with object interaction and communication (e.g., Observer, Strategy).

#### Chinese Explanation：

**设计模式**是针对常见软件设计问题的解决方案。它们提供了如何构建和设计代码的模板，以灵活和可重用的方式解决特定问题。设计模式通常分为：
1. **创建型模式**：处理对象创建（例如，单例模式，工厂模式）。
2. **结构型模式**：处理对象组合（例如，适配器模式，装饰器模式）。
3. **行为型模式**：处理对象之间的交互和通信（例如，观察者模式，策略模式）。

---

### Question 151: What are the different types of design patterns?

#### English Explanation:

Design patterns are categorized into three main types:
1. **Creational Patterns**: Focus on the creation of objects in a way that suits the situation. Examples include:
   - **Singleton**: Ensures only one instance of a class is created.
   - **Factory Method**: Creates objects without specifying the exact class.
   - **Abstract Factory**: Provides an interface for creating families of related or dependent objects.

2. **Structural Patterns**: Deal with object composition to form larger structures. Examples include:
   - **Adapter**: Allows incompatible interfaces to work together.
   - **Decorator**: Dynamically adds behavior to objects.

3. **Behavioral Patterns**: Focus on object interaction and communication. Examples include:
   - **Observer**: Allows a subject to notify its observers of state changes.
   - **Strategy**: Enables a family of algorithms to be defined and interchanged.

#### Chinese Explanation:

设计模式主要分为三种类型：
1. **创建型模式**：关注对象的创建方式，适应特定情境。示例包括：
   - **单例模式**：确保一个类只创建一个实例。
   - **工厂方法**：创建对象而无需指定确切的类。
   - **抽象工厂**：提供创建相关或依赖对象家族的接口。

2. **结构型模式**：处理对象组合以形成更大的结构。示例包括：
   - **适配器模式**：允许不兼容的接口协同工作。
   - **装饰器模式**：动态地为对象添加行为。

3. **行为型模式**：专注于对象之间的交互和通信。示例包括：
   - **观察者模式**：允许主题通知观察者状态变化。
   - **策略模式**：定义并可互换一系列算法。

---

### Question 152: Explain structural, behavioral, and creational design patterns?

#### English Explanation:

1. **Creational Design Patterns**: These patterns deal with object creation and provide solutions to instantiate objects in a manner suitable for the given situation.
   - Examples: Singleton, Factory, Builder.

2. **Structural Design Patterns**: These patterns focus on class and object composition to form larger structures. They help ensure that classes work together without being tightly coupled.
   - Examples: Adapter, Decorator, Composite.

3. **Behavioral Design Patterns**: These patterns focus on object interaction and responsibility distribution. They help manage algorithms, communication between objects, and responsibility.
   - Examples: Observer, Strategy, Command.

#### Chinese Explanation：

1. **创建型设计模式**：这些模式处理对象的创建，提供解决方案以适应给定场景实例化对象。
   - 示例：单例模式，工厂模式，建造者模式。

2. **结构型设计模式**：这些模式专注于类和对象的组合，形成更大的结构。它们帮助确保类之间的协作而不紧密耦合。
   - 示例：适配器模式，装饰器模式，组合模式。

3. **行为型设计模式**：这些模式专注于对象之间的交互和责任分配。它们帮助管理算法、对象间的通信和责任划分。
   - 示例：观察者模式，策略模式，命令模式。

---

### Question 153: Explain Singleton Pattern and the use of it?

#### English Explanation:

The **Singleton Pattern** ensures that a class has only one instance and provides a global point of access to that instance. It is commonly used when:
- You need exactly one instance of a class to control access to a resource (like a database connection).
- You want to ensure that a global state or configuration is consistent across the application.

#### Code Example:

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

#### Chinese Explanation：

**单例模式**确保一个类只有一个实例，并提供对该实例的全局访问点。它通常用于：
- 你需要类的唯一实例来控制对资源（如数据库连接）的访问时。
- 你希望确保全局状态或配置在整个应用程序中保持一致时。

#### 代码示例：

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

---

### Question 154: How did you implement Singleton Pattern?

#### English Explanation:

To implement the **Singleton Pattern**, follow these steps:
1. **Private Constructor**: Prevents the creation of an object using the `new` keyword.
2. **Static Field**: Holds the single instance of the class.
3. **Thread-Safe Access**: Use a locking mechanism to ensure the singleton instance is created safely when accessed by multiple threads.

#### Code Example:

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

#### Chinese Explanation：

要实现**单例模式**，遵循以下步骤：
1. **私有构造函数**：防止使用 `new` 关键字创建对象。
2. **静态字段**：保存类的唯一实例。
3. **线程安全访问**：使用锁机制确保单例实例在多线程访问时安全创建。

#### 代码示例：

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

---

### Question 155: Can we use a static class instead of Singleton?

#### English Explanation:

Yes, you can use a **static class** instead of a **Singleton**, but they differ:
- **Singleton**: Can implement interfaces, inherit from other classes, and can be lazily instantiated.
- **Static class**: Cannot implement interfaces or inherit from other classes, and its members are always initialized as soon as the program starts.

**Use Singleton** when you need more control over the instantiation process or need to follow OOP principles (like inheritance).

#### Chinese Explanation：

是的，可以使用**静态类**代替**单例模式**，但它们有区别：
- **单例模式**：可以实现接口，继承其他类，并且可以延迟实例化。
- **静态类**：不能实现接口或继承其他类，并且其成员在程序启动时立即初始化。

当你需要更多控制实例化过程或需要遵循面向对象原则（如继承）时，**使用单例模式**。

---

### Question 156: Static vs Singleton pattern?

#### English Explanation:

| **Aspect**         | **Static Class**                               | **Singleton Pattern**                             |
|--------------------|------------------------------------------------|--------------------------------------------------|
| **Instance**       | No instance; accessed directly by class name   | Only one instance; accessed via instance property |
| **Inheritance**    | Cannot inherit or implement interfaces         | Can inherit and implement interfaces              |
| **Instantiation**  | Initialized when program starts                | Can be lazily initialized (created when needed)   |
| **Thread-Safety**  | No built-in thread safety                      | Can implement thread safety in instance creation  |

#### Chinese Explanation：

| **方面**           | **静态类**                                      | **单例模式**                                       |
|--------------------|------------------------------------------------|--------------------------------------------------|
| **实例**           | 没有实例；直接通过类名访问                       | 只有一个实例；通过实例属性访问                     |
| **继承**           | 不能继承或实现接口                               | 可以继承并实现接口                                 |
| **实例化**         | 在程序启动时初始化                               | 可以延迟实例化（按需创建）                         |
| **线程安全**       | 没有内置的线程安全                               | 可以在实例创建中实现线程安全                       |

---

### Question 157: How did you implement thread safety in Singleton?

#### English Explanation:

To implement **thread safety** in a Singleton, you can use the **`lock`** keyword to ensure that only one thread can access the critical section of code that creates the Singleton instance.

#### Code Example:

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

#### Chinese Explanation：

要在单例

模式中实现**线程安全**，你可以使用 **`lock`** 关键字，确保只有一个线程可以访问创建单例实例的关键代码段。

#### 代码示例：

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (padlock)
            {
                if (instance == null)
                {
                    instance = new Singleton();
                }
                return instance;
            }
        }
    }
}
```

---

### Question 158: What is double-check locking in Singleton?

#### English Explanation:

**Double-check locking** is an optimization in Singleton pattern where the `lock` is only used when necessary. This reduces the overhead of acquiring a lock every time the `Instance` property is accessed.

#### Code Example:

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (instance == null) // First check (without locking)
            {
                lock (padlock)
                {
                    if (instance == null) // Second check (with locking)
                    {
                        instance = new Singleton();
                    }
                }
            }
            return instance;
        }
    }
}
```

#### Chinese Explanation：

**双重检查锁定**是在单例模式中的一种优化，只有在必要时才使用 `lock`。这样可以减少每次访问 `Instance` 属性时获取锁的开销。

#### 代码示例：

```csharp
public class Singleton
{
    private static Singleton instance = null;
    private static readonly object padlock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            if (instance == null) // 第一次检查（不加锁）
            {
                lock (padlock)
                {
                    if (instance == null) // 第二次检查（加锁）
                    {
                        instance = new Singleton();
                    }
                }
            }
            return instance;
        }
    }
}
```

---

### Question 159: Can Singleton pattern code be simplified with the `Lazy<T>` keyword?

#### English Explanation:

Yes, the Singleton pattern can be simplified using the **`Lazy<T>`** keyword in C#. `Lazy<T>` provides lazy initialization and ensures thread safety. It removes the need for explicit locking and double-check locking.

#### Code Example:

```csharp
public class Singleton
{
    private static readonly Lazy<Singleton> lazyInstance = new Lazy<Singleton>(() => new Singleton());

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            return lazyInstance.Value;
        }
    }
}
```

#### Chinese Explanation：

是的，使用 C# 中的 **`Lazy<T>`** 关键字可以简化单例模式。`Lazy<T>` 提供了延迟初始化，并确保线程安全。它不需要显式的锁定和双重检查锁定。

#### 代码示例：

```csharp
public class Singleton
{
    private static readonly Lazy<Singleton> lazyInstance = new Lazy<Singleton>(() => new Singleton());

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            return lazyInstance.Value;
        }
    }
}
```
### Question 160: Can we get rid of double-check locking in Singleton?

#### English Explanation:

Yes, you can eliminate **double-check locking** by using the **`Lazy<T>`** type in C#. This approach simplifies the Singleton pattern by ensuring thread-safe lazy initialization without the need for manual locking. With `Lazy<T>`, the Singleton instance is created only when it is first accessed, and it automatically handles thread safety.

#### Code Example:

```csharp
public class Singleton
{
    private static readonly Lazy<Singleton> instance = new Lazy<Singleton>(() => new Singleton());

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            return instance.Value;
        }
    }
}
```

#### Chinese Explanation:

是的，使用 C# 中的 **`Lazy<T>`** 类型可以消除**双重检查锁定**。这种方法通过确保线程安全的延迟初始化简化了单例模式，不需要手动加锁。使用 `Lazy<T>` 时，单例实例仅在首次访问时创建，并且自动处理线程安全问题。

#### 代码示例：

```csharp
public class Singleton
{
    private static readonly Lazy<Singleton> instance = new Lazy<Singleton>(() => new Singleton());

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            return instance.Value;
        }
    }
}
```

---

### Question 161: What is a Factory Method Pattern?

#### English Explanation:

The **Factory Method Pattern** defines an interface for creating objects but allows subclasses to alter the type of objects that will be created. This pattern lets a class delegate the responsibility of object creation to subclasses, promoting flexibility and scalability.

#### Code Example:

```csharp
// Product interface
public interface IProduct
{
    void Operation();
}

// Concrete Product A
public class ProductA : IProduct
{
    public void Operation()
    {
        Console.WriteLine("Operation of Product A");
    }
}

// Concrete Product B
public class ProductB : IProduct
{
    public void Operation()
    {
        Console.WriteLine("Operation of Product B");
    }
}

// Creator abstract class
public abstract class Creator
{
    public abstract IProduct FactoryMethod();

    public void AnOperation()
    {
        IProduct product = FactoryMethod();
        product.Operation();
    }
}

// Concrete Creator for Product A
public class ConcreteCreatorA : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ProductA();
    }
}

// Concrete Creator for Product B
public class ConcreteCreatorB : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ProductB();
    }
}

// Client code
class Program
{
    static void Main()
    {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.AnOperation();

        Creator creatorB = new ConcreteCreatorB();
        creatorB.AnOperation();
    }
}
```

#### Chinese Explanation：

**工厂方法模式**定义了一个用于创建对象的接口，但允许子类更改将要创建的对象类型。此模式将对象创建的责任委派给子类，促进了灵活性和可扩展性。

#### 代码示例：

```csharp
// 产品接口
public interface IProduct
{
    void Operation();
}

// 具体产品 A
public class ProductA : IProduct
{
    public void Operation()
    {
        Console.WriteLine("产品 A 的操作");
    }
}

// 具体产品 B
public class ProductB : IProduct
{
    public void Operation()
    {
        Console.WriteLine("产品 B 的操作");
    }
}

// 创建者抽象类
public abstract class Creator
{
    public abstract IProduct FactoryMethod();

    public void AnOperation()
    {
        IProduct product = FactoryMethod();
        product.Operation();
    }
}

// 具体创建者 A
public class ConcreteCreatorA : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ProductA();
    }
}

// 具体创建者 B
public class ConcreteCreatorB : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ProductB();
    }
}

// 客户端代码
class Program
{
    static void Main()
    {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.AnOperation();

        Creator creatorB = new ConcreteCreatorB();
        creatorB.AnOperation();
    }
}
```

---

### Question 162: What is the Abstract Factory Pattern?

#### English Explanation:

The **Abstract Factory Pattern** provides an interface for creating families of related or dependent objects without specifying their concrete classes. It allows you to produce objects from different factories interchangeably, ensuring consistency across the created objects.

#### Code Example:

```csharp
// Abstract Factory
public interface IAbstractFactory
{
    IProductA CreateProductA();
    IProductB CreateProductB();
}

// Concrete Factory 1
public class ConcreteFactory1 : IAbstractFactory
{
    public IProductA CreateProductA() => new ProductA1();
    public IProductB CreateProductB() => new ProductB1();
}

// Concrete Factory 2
public class ConcreteFactory2 : IAbstractFactory
{
    public IProductA CreateProductA() => new ProductA2();
    public IProductB CreateProductB() => new ProductB2();
}

// Abstract Product A
public interface IProductA
{
    void OperationA();
}

// Abstract Product B
public interface IProductB
{
    void OperationB();
}

// Concrete Product A1
public class ProductA1 : IProductA
{
    public void OperationA()
    {
        Console.WriteLine("Operation of Product A1");
    }
}

// Concrete Product A2
public class ProductA2 : IProductA
{
    public void OperationA()
    {
        Console.WriteLine("Operation of Product A2");
    }
}

// Concrete Product B1
public class ProductB1 : IProductB
{
    public void OperationB()
    {
        Console.WriteLine("Operation of Product B1");
    }
}

// Concrete Product B2
public class ProductB2 : IProductB
{
    public void OperationB()
    {
        Console.WriteLine("Operation of Product B2");
    }
}

// Client code
class Program
{
    static void Main()
    {
        IAbstractFactory factory1 = new ConcreteFactory1();
        IProductA productA1 = factory1.CreateProductA();
        IProductB productB1 = factory1.CreateProductB();
        productA1.OperationA();
        productB1.OperationB();

        IAbstractFactory factory2 = new ConcreteFactory2();
        IProductA productA2 = factory2.CreateProductA();
        IProductB productB2 = factory2.CreateProductB();
        productA2.OperationA();
        productB2.OperationB();
    }
}
```

#### Chinese Explanation：

**抽象工厂模式**提供了一个用于创建相关或依赖对象家族的接口，而无需指定它们的具体类。它允许你从不同的工厂生成对象，确保所创建对象之间的一致性。

#### 代码示例：

```csharp
// 抽象工厂
public interface IAbstractFactory
{
    IProductA CreateProductA();
    IProductB CreateProductB();
}

// 具体工厂 1
public class ConcreteFactory1 : IAbstractFactory
{
    public IProductA CreateProductA() => new ProductA1();
    public IProductB CreateProductB() => new ProductB1();
}

// 具体工厂 2
public class ConcreteFactory2 : IAbstractFactory
{
    public IProductA CreateProductA() => new ProductA2();
    public IProductB CreateProductB() => new ProductB2();
}

// 抽象产品 A
public interface IProductA
{
    void OperationA();
}

// 抽象产品 B
public interface IProductB
{
    void OperationB();
}

// 具体产品 A1
public class ProductA1 : IProductA
{
    public void OperationA()
    {
        Console.WriteLine("产品 A1 的操作");
    }
}

// 具体产品 A2
public class ProductA2 : IProductA
{
    public void OperationA()
    {
        Console.WriteLine("产品 A2 的操作");
    }
}

// 具体产品 B1
public class ProductB1 : IProductB
{
    public void OperationB()
    {
        Console.WriteLine("产品 B1 的操作");
    }
}

// 具体产品 B2
public class ProductB2 : IProductB
{
    public void OperationB()
    {
        Console.WriteLine("产品 B2 的操作");
    }
}

// 客户端代码
class Program
{
    static void Main()
    {
        IAbstractFactory factory1 = new ConcreteFactory1();
        IProductA productA1 = factory1.CreateProductA();
        IProductB productB1 = factory1.CreateProductB();
        productA1.OperationA();
        productB1.OperationB();

        IAbstractFactory factory2 = new ConcreteFactory2();
        IProductA productA2 = factory2.CreateProductA();
        IProductB productB2 = factory2.CreateProductB();
        productA2.OperationA();
        productB2.OperationB();
    }
}
```

---

### Question 163: What is the Adapter Pattern?

#### English Explanation:

The **Adapter Pattern** allows two incompatible interfaces to work together by converting the interface of a class into one that a client expects. This pattern is commonly used when you want to integrate a new component into an existing system without modifying the client code.

#### Code Example:

```csharp
// Target interface
public interface ITarget
{
    void Request();
}

// Adaptee class with an incompatible interface
public class Adaptee
{
    public void SpecificRequest()
    {
        Console

.WriteLine("Specific request in Adaptee");
    }
}

// Adapter class that makes Adaptee compatible with ITarget
public class Adapter : ITarget
{
    private readonly Adaptee _adaptee;

    public Adapter(Adaptee adaptee)
    {
        _adaptee = adaptee;
    }

    public void Request()
    {
        _adaptee.SpecificRequest();
    }
}

// Client code
class Program
{
    static void Main()
    {
        Adaptee adaptee = new Adaptee();
        ITarget target = new Adapter(adaptee);
        target.Request();
    }
}
```

#### Chinese Explanation：

**适配器模式**通过将类的接口转换为客户端期望的接口，使两个不兼容的接口能够一起工作。这种模式通常用于将新组件集成到现有系统中，而无需修改客户端代码。

#### 代码示例：

```csharp
// 目标接口
public interface ITarget
{
    void Request();
}

// 适配者类，具有不兼容的接口
public class Adaptee
{
    public void SpecificRequest()
    {
        Console.WriteLine("适配者的具体请求");
    }
}

// 适配器类，使适配者与 ITarget 兼容
public class Adapter : ITarget
{
    private readonly Adaptee _adaptee;

    public Adapter(Adaptee adaptee)
    {
        _adaptee = adaptee;
    }

    public void Request()
    {
        _adaptee.SpecificRequest();
    }
}

// 客户端代码
class Program
{
    static void Main()
    {
        Adaptee adaptee = new Adaptee();
        ITarget target = new Adapter(adaptee);
        target.Request();
    }
}
```

---

### Question 164: What is the Observer Pattern?

#### English Explanation:

The **Observer Pattern** defines a one-to-many dependency between objects, so that when one object (the subject) changes state, all its dependents (observers) are notified and updated automatically. This pattern is commonly used for implementing event handling and notification systems.

#### Code Example:

```csharp
// Subject interface
public interface ISubject
{
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}

// Concrete Subject
public class ConcreteSubject : ISubject
{
    private List<IObserver> observers = new List<IObserver>();
    public string State { get; set; }

    public void Attach(IObserver observer)
    {
        observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in observers)
        {
            observer.Update();
        }
    }
}

// Observer interface
public interface IObserver
{
    void Update();
}

// Concrete Observer
public class ConcreteObserver : IObserver
{
    private readonly string _name;
    private readonly ConcreteSubject _subject;

    public ConcreteObserver(string name, ConcreteSubject subject)
    {
        _name = name;
        _subject = subject;
    }

    public void Update()
    {
        Console.WriteLine($"{_name} received update: {_subject.State}");
    }
}

// Client code
class Program
{
    static void Main()
    {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer1 = new ConcreteObserver("Observer1", subject);
        ConcreteObserver observer2 = new ConcreteObserver("Observer2", subject);

        subject.Attach(observer1);
        subject.Attach(observer2);

        subject.State = "New State";
        subject.Notify();
    }
}
```

#### Chinese Explanation：

**观察者模式**定义了对象之间的**一对多**依赖关系，当一个对象（主题）状态发生变化时，所有依赖于它的对象（观察者）会被通知并自动更新。该模式通常用于实现事件处理和通知系统。

#### 代码示例：

```csharp
// 主题接口
public interface ISubject
{
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}

// 具体主题
public class ConcreteSubject : ISubject
{
    private List<IObserver> observers = new List<IObserver>();
    public string State { get; set; }

    public void Attach(IObserver observer)
    {
        observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in observers)
        {
            observer.Update();
        }
    }
}

// 观察者接口
public interface IObserver
{
    void Update();
}

// 具体观察者
public class ConcreteObserver : IObserver
{
    private readonly string _name;
    private readonly ConcreteSubject _subject;

    public ConcreteObserver(string name, ConcreteSubject subject)
    {
        _name = name;
        _subject = subject;
    }

    public void Update()
    {
        Console.WriteLine($"{_name} 收到更新：{_subject.State}");
    }
}

// 客户端代码
class Program
{
    static void Main()
    {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer1 = new ConcreteObserver("观察者1", subject);
        ConcreteObserver observer2 = new ConcreteObserver("观察者2", subject);

        subject.Attach(observer1);
        subject.Attach(observer2);

        subject.State = "新状态";
        subject.Notify();
    }
}
```
