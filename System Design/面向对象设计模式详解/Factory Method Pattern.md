# Factory Method Pattern

### 工厂方法模式 (Factory Method Pattern) - 详解

#### 1. 定义 (Definition)

工厂方法模式 (Factory Method Pattern) 是一种创建型设计模式，它定义了一个用于创建对象的接口，但由子类决定实例化哪一个具体类。工厂方法将类的实例化延迟到子类，从而使得父类不需要关心要创建的对象类型是什么，达到对象创建与使用的解耦。

#### 2. 使用场景 (Usage Scenarios)

工厂方法模式适用于以下场景：
1. **当对象的创建过程复杂且有多个分支时**：例如根据不同参数或环境条件创建不同的对象。
2. **当系统需要屏蔽具体产品类的创建逻辑时**：例如在不同操作系统平台上创建不同的 GUI 元素（按钮、文本框）。
3. **当类的实例化过程可能变化时**：在不修改客户端代码的情况下增加新的产品类，保证了系统的可扩展性。

#### 3. 结构 (Structure)

工厂方法模式包含以下几个关键角色：
1. **抽象产品 (Product)**：定义所有产品的共同接口。
2. **具体产品 (Concrete Product)**：实现 `Product` 接口的具体类，是被创建的对象类型。
3. **抽象工厂 (Creator)**：定义了一个用于创建 `Product` 对象的抽象方法 `factoryMethod()`，并且可以包含通用的业务逻辑（如对产品的管理）。
4. **具体工厂 (Concrete Creator)**：实现 `Creator` 中的 `factoryMethod()` 方法，用于创建 `Concrete Product` 的实例。

![Factory Method Pattern Diagram](https://refactoring.guru/images/patterns/diagrams/factory-method/structure.png)

#### 4. 实现方式 (Implementation)

工厂方法模式通常包括以下几个步骤：
1. 创建一个 `Product` 接口，用于定义所有产品的共同行为。
2. 创建多个 `Concrete Product` 类，实现 `Product` 接口，定义不同产品的具体行为。
3. 创建一个 `Creator` 抽象类，定义 `factoryMethod()` 抽象方法。
4. 创建 `Concrete Creator` 类，实现 `factoryMethod()` 方法，返回 `Concrete Product` 的实例。

#### 5. 实现代码 (Code Implementation)

##### 5.1 Java 实现代码 (Java Code)

```java
// 1. 抽象产品接口
interface Product {
    void use();
}

// 2. 具体产品类
class ConcreteProductA implements Product {
    @Override
    public void use() {
        System.out.println("Using ConcreteProductA");
    }
}

class ConcreteProductB implements Product {
    @Override
    public void use() {
        System.out.println("Using ConcreteProductB");
    }
}

// 3. 抽象工厂类
abstract class Creator {
    // 抽象工厂方法
    public abstract Product factoryMethod();

    // 其他通用的操作
    public void someOperation() {
        // 调用工厂方法创建产品
        Product product = factoryMethod();
        // 使用产品
        product.use();
    }
}

// 4. 具体工厂类
class ConcreteCreatorA extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductA(); // 创建 ConcreteProductA
    }
}

class ConcreteCreatorB extends Creator {
    @Override
    public Product factoryMethod() {
        return new ConcreteProductB(); // 创建 ConcreteProductB
    }
}

// 示例用法
public class Main {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        Creator creatorB = new ConcreteCreatorB();

        creatorA.someOperation(); // 输出: Using ConcreteProductA
        creatorB.someOperation(); // 输出: Using ConcreteProductB
    }
}
```

##### 5.2 C# 实现代码 (C# Code)

```csharp
using System;

// 1. 抽象产品接口
interface IProduct
{
    void Use();
}

// 2. 具体产品类
class ConcreteProductA : IProduct
{
    public void Use()
    {
        Console.WriteLine("Using ConcreteProductA");
    }
}

class ConcreteProductB : IProduct
{
    public void Use()
    {
        Console.WriteLine("Using ConcreteProductB");
    }
}

// 3. 抽象工厂类
abstract class Creator
{
    // 抽象工厂方法
    public abstract IProduct FactoryMethod();

    // 其他通用的操作
    public void SomeOperation()
    {
        // 调用工厂方法创建产品
        IProduct product = FactoryMethod();
        // 使用产品
        product.Use();
    }
}

// 4. 具体工厂类
class ConcreteCreatorA : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ConcreteProductA(); // 创建 ConcreteProductA
    }
}

class ConcreteCreatorB : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ConcreteProductB(); // 创建 ConcreteProductB
    }
}

// 示例用法
class Program
{
    static void Main(string[] args)
    {
        Creator creatorA = new ConcreteCreatorA();
        Creator creatorB = new ConcreteCreatorB();

        creatorA.SomeOperation(); // 输出: Using ConcreteProductA
        creatorB.SomeOperation(); // 输出: Using ConcreteProductB
    }
}
```

#### 6. 优缺点 (Pros and Cons)

**优点**：
1. **封装对象创建细节**：工厂方法将对象的创建封装在子类中，使得客户端不需要知道具体创建逻辑。
2. **遵循开放-封闭原则 (OCP)**：可以通过增加新的具体工厂类来扩展系统，而无需修改现有的代码。
3. **解耦产品和工厂类**：工厂方法提供了创建产品的接口，不同工厂类负责具体产品的创建，产品类和工厂类的解耦降低了耦合度。

**缺点**：
1. **增加系统复杂性**：每个具体工厂类都需要创建一个新的类，导致类的数量增加，系统变得更复杂。
2. **不适用于简单场景**：对于简单对象的创建，使用工厂方法可能显得过于复杂，增加了额外的抽象层。

#### 7. 应用场景分析 (Use Case Analysis)

工厂方法模式常用于以下应用场景：
1. **日志记录类 (Logging Class)**：可以根据不同平台（如文件日志、数据库日志）生成不同的日志记录器。
2. **数据库连接类 (Database Connection Class)**：可以根据不同数据库类型（如 MySQL、SQL Server）生成不同的数据库连接对象。
3. **文件解析类 (File Parser Class)**：根据不同文件格式（如 XML、JSON）生成不同的文件解析器。

#### 8. 注意事项 (Considerations)

- **选择适当的抽象级别**：在设计工厂方法模式时，要注意抽象工厂的抽象级别。如果抽象级别过高，系统会变得复杂难以理解；如果抽象级别过低，工厂方法可能失去其应有的作用。
- **避免滥用模式**：工厂方法模式非常灵活，但滥用可能会导致代码结构过于复杂，尤其在简单对象的创建场景下，可以考虑直接使用简单工厂或构造函数替代。

#### 9. 工厂方法模式 vs 简单工厂模式 (Factory Method Pattern vs Simple Factory Pattern)

| **比较维度**                 | **工厂方法模式 (Factory Method Pattern)**                                            | **简单工厂模式 (Simple Factory Pattern)**                                      |
|-----------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **创建对象的责任**           | 由具体工厂类来负责创建具体的产品对象。                                             | 由一个单一的工厂类负责创建所有产品对象。                                        |
| **是否符合开放-封闭原则 (OCP)** | 符合开放-封闭原则，新增产品时，只需增加新的工厂类，无需修改已有代码。                | 不符合开放-封闭原则，新增产品时，需要修改工厂类的代码，违反了 OCP 原则。        |
| **类的复杂度**               | 增加了抽象工厂类和多个具体工厂类，类的数量较多，系统复杂度较高。                     | 类的数量较少，系统简单，但产品和工厂类耦合度较高。                              |
| **灵活性**                   | 更加灵活，可以动态扩展新的产品和工厂类，而不会影响已有系统。                         | 灵活性较低，扩展新的产品需要修改已有的工厂类。                                  |
| **使用场景**                 | 当产品族复杂且需要考虑系统扩展性时使用。                                             | 当产品种类较少且对象创建过程简单时使用。                                        |

#### 10. 总结 (Conclusion)

工厂方法模式通过将对象的创建延迟到子类，解耦了产品类与工厂类，并且遵循了开放-封闭原则。它提供了一种灵活的设计方式，能够在不修改已有代码的情况下扩展新的产品类。但在实际应用中，应根据具体场景权衡其优缺点，避免过度设计导致系统复杂性增加

。在需要创建复杂对象的场景中，工厂方法模式是一种非常有效的设计模式，可以为系统带来良好的扩展性和灵活性。
