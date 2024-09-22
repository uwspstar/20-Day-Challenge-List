# Commonly Used Design Patterns in Software Development

### 软件开发中的常用设计模式

In software development, design patterns provide standardized solutions to commonly occurring problems. They improve code reusability, clarity, and maintainability. Here, we’ll go over some of the most commonly used design patterns, categorized into **Creational**, **Structural**, and **Behavioral** patterns.

在软件开发中，设计模式为常见问题提供了标准化的解决方案。它们提高了代码的可重用性、清晰度和可维护性。本文将介绍一些最常用的设计模式，分类为 **创建型**、**结构型** 和 **行为型** 模式。

---

### 1. **Creational Patterns**

### 1. **创建型模式**

Creational patterns are concerned with the way objects are created. These patterns abstract the instantiation process, making a system independent of how its objects are created, composed, and represented.

创建型模式与对象的创建方式有关。这些模式抽象了实例化过程，使系统独立于对象的创建、组合和表示方式。

#### **Singleton Pattern (单例模式)**

The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This pattern is commonly used in scenarios such as database connections, where having multiple connections might cause problems.

单例模式确保一个类只有一个实例，并提供对它的全局访问点。该模式常用于数据库连接等场景，因为多个连接可能会导致问题。

**Example:**
```csharp
public class Database
{
    private static Database instance;

    private Database() {}

    public static Database GetInstance()
    {
        if (instance == null)
        {
            instance = new Database();
        }
        return instance;
    }
}
```

**场景：**
```csharp
public class Database
{
    private static Database instance;

    private Database() {}

    public static Database GetInstance()
    {
        if (instance == null)
        {
            instance = new Database();
        }
        return instance;
    }
}
```

---

#### **Factory Method Pattern (工厂方法模式)**

This pattern defines an interface for creating objects but allows subclasses to alter the type of objects that will be created. It decouples the client code from the object creation process, enhancing flexibility.

工厂方法模式定义了一个创建对象的接口，但允许子类改变将要创建的对象类型。它将客户端代码与对象创建过程解耦，增强了灵活性。

**Example:**
```csharp
public abstract class AnimalFactory
{
    public abstract IAnimal CreateAnimal();
}

public class DogFactory : AnimalFactory
{
    public override IAnimal CreateAnimal() => new Dog();
}

public class CatFactory : AnimalFactory
{
    public override IAnimal CreateAnimal() => new Cat();
}
```

**场景：**
```csharp
public abstract class AnimalFactory
{
    public abstract IAnimal CreateAnimal();
}

public class DogFactory : AnimalFactory
{
    public override IAnimal CreateAnimal() => new Dog();
}

public class CatFactory : AnimalFactory
{
    public override IAnimal CreateAnimal() => new Cat();
}
```

---

### 2. **Structural Patterns**

### 2. **结构型模式**

Structural patterns deal with object composition and aim to simplify relationships between entities. These patterns help ensure that if one part of a system changes, it doesn’t require the whole system to change.

结构型模式处理对象的组成，并旨在简化实体之间的关系。这些模式有助于确保系统的某部分发生变化时，不会影响整个系统。

#### **Adapter Pattern (适配器模式)**

The Adapter pattern allows two incompatible interfaces to work together. It acts as a bridge between two objects that otherwise wouldn't be able to interact.

适配器模式允许两个不兼容的接口一起工作。它充当两个对象之间的桥梁，否则它们将无法交互。

**Example:**
```csharp
public class USPowerSocket
{
    public string GetPower() => "110V";
}

public interface IEuropeanSocket
{
    string GetEuropeanPower();
}

public class Adapter : IEuropeanSocket
{
    private USPowerSocket _usSocket;

    public Adapter(USPowerSocket usSocket)
    {
        _usSocket = usSocket;
    }

    public string GetEuropeanPower() => _usSocket.GetPower();
}
```

**场景：**
```csharp
public class USPowerSocket
{
    public string GetPower() => "110V";
}

public interface IEuropeanSocket
{
    string GetEuropeanPower();
}

public class Adapter : IEuropeanSocket
{
    private USPowerSocket _usSocket;

    public Adapter(USPowerSocket usSocket)
    {
        _usSocket = usSocket;
    }

    public string GetEuropeanPower() => _usSocket.GetPower();
}
```

---

#### **Facade Pattern (外观模式)**

The Facade pattern provides a simplified interface to a complex subsystem. It shields clients from the complexities of the subsystem by providing an easier-to-use interface.

外观模式为复杂子系统提供了一个简化的接口。它通过提供一个易于使用的接口屏蔽了子系统的复杂性。

**Example:**
```csharp
public class Computer
{
    public void Start() => Console.WriteLine("Computer starting...");
}

public class Projector
{
    public void On() => Console.WriteLine("Projector on...");
}

public class HomeTheaterFacade
{
    private Computer _computer;
    private Projector _projector;

    public HomeTheaterFacade(Computer computer, Projector projector)
    {
        _computer = computer;
        _projector = projector;
    }

    public void StartMovie()
    {
        _computer.Start();
        _projector.On();
    }
}
```

**场景：**
```csharp
public class Computer
{
    public void Start() => Console.WriteLine("Computer starting...");
}

public class Projector
{
    public void On() => Console.WriteLine("Projector on...");
}

public class HomeTheaterFacade
{
    private Computer _computer;
    private Projector _projector;

    public HomeTheaterFacade(Computer computer, Projector projector)
    {
        _computer = computer;
        _projector = projector;
    }

    public void StartMovie()
    {
        _computer.Start();
        _projector.On();
    }
}
```

---

### 3. **Behavioral Patterns**

### 3. **行为型模式**

Behavioral patterns deal with how objects communicate with one another. These patterns define how to manage interactions between entities.

行为型模式处理对象之间如何通信。这些模式定义了如何管理实体之间的交互。

#### **Observer Pattern (观察者模式)**

The Observer pattern is a subscription model where objects (observers) can register to be notified when the state of another object (subject) changes. It is often used in event handling systems.

观察者模式是一种订阅模型，观察者可以注册以便在其他对象（主体）状态发生变化时收到通知。它通常用于事件处理系统。

**Example:**
```csharp
public class NewsPublisher
{
    private List<IObserver> observers = new List<IObserver>();

    public void AddObserver(IObserver observer) => observers.Add(observer);
    public void NotifyObservers() => observers.ForEach(observer => observer.Update());
}

public interface IObserver
{
    void Update();
}

public class NewsReader : IObserver
{
    public void Update() => Console.WriteLine("NewsReader got the update.");
}
```

**场景：**
```csharp
public class NewsPublisher
{
    private List<IObserver> observers = new List<IObserver>();

    public void AddObserver(IObserver observer) => observers.Add(observer);
    public void NotifyObservers() => observers.ForEach(observer => observer.Update());
}

public interface IObserver
{
    void Update();
}

public class NewsReader : IObserver
{
    public void Update() => Console.WriteLine("NewsReader got the update.");
}
```

---

### Conclusion

### 结论

Understanding and using design patterns is essential for building scalable, maintainable, and flexible software systems. Whether it's creating objects, structuring your code, or managing behavior between components, design patterns help improve software quality by promoting reusability and best practices.

理解并使用设计模式对于构建可扩展、可维护和灵活的软件系统至关重要。无论是创建对象、结构化代码，还是管理组件之间的行为，设计模式通过促进代码重用和最佳实践来帮助提高软件质量。
