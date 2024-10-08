# Design Patterns

### 面向对象设计模式详解 (Object-Oriented Design Patterns Detailed Explanation)

面向对象设计模式是一种用于解决常见软件设计问题的可重用解决方案。它们可以帮助开发者设计出灵活、可扩展和易维护的代码结构。
经典的设计模式主要分为**三大类，共 23 种**：**创建型模式 (Creational Patterns)**、**结构型模式 (Structural Patterns)** 和 **行为型模式 (Behavioral Patterns)**。
具体如下：

---

1. **创建型模式 (Creational Patterns)** - **5 种**  
   创建型模式主要用于对象的创建，能够使系统更灵活地控制对象的实例化过程，避免直接使用 `new` 操作符。
   - [**单例模式 (Singleton Pattern)**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E8%AF%A6%E8%A7%A3/Singleton%20Pattern.md)：确保一个类只有一个实例，并提供全局访问点。
   - **工厂方法模式 (Factory Method Pattern)**：定义创建对象的接口，让子类决定实例化哪一个类。
   - **抽象工厂模式 (Abstract Factory Pattern)**：提供一个接口创建相关对象家族，而不指定具体类。
   - **建造者模式 (Builder Pattern)**：将对象的构建过程与其表示分离，使得同样的构建过程可以创建不同的表示。
   - **原型模式 (Prototype Pattern)**：使用原型实例指定创建对象的种类，并通过复制这些原型创建新的对象。

2. **结构型模式 (Structural Patterns)** - **7 种**  
   结构型模式主要关注对象和类的组合，如何将对象和类组装成更大的结构来实现新的功能。
   - **适配器模式 (Adapter Pattern)**：将一个类的接口转换成客户端期望的另一种接口，适配器模式使得原本接口不兼容的类可以一起工作。
   - **桥接模式 (Bridge Pattern)**：将抽象部分与实现部分分离，使它们可以独立地变化。
   - **组合模式 (Composite Pattern)**：将对象组合成树形结构以表示“部分-整体”的层次结构，使得客户端对单个对象和组合对象的使用具有一致性。
   - **装饰模式 (Decorator Pattern)**：动态地给对象增加新的功能，并且这种功能扩展不影响其他对象。
   - **外观模式 (Facade Pattern)**：为子系统中的一组接口提供一个一致的界面，简化客户端对子系统的访问。
   - **享元模式 (Flyweight Pattern)**：通过共享相似对象来减少内存使用量，适用于大量细粒度对象的场景。
   - **代理模式 (Proxy Pattern)**：为其他对象提供一种代理以控制对这个对象的访问，适用于在访问对象前后执行特定操作的场景。

3. **行为型模式 (Behavioral Patterns)** - **11 种**  
   行为型模式侧重于对象和类之间的通信方式和职责分配，帮助对象有效地协作。
   - **策略模式 (Strategy Pattern)**：定义一组算法，将每个算法封装起来，并使它们可以相互替换。
   - [**观察者模式 (Observer Pattern)**](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E8%AF%A6%E8%A7%A3/Observer%20Pattern.md)：定义对象之间一对多的依赖关系，当一个对象的状态发生变化时，所有依赖它的对象都会被通知。
   - **命令模式 (Command Pattern)**：将请求封装成对象，从而使得可以用不同的请求对客户进行参数化。
   - **责任链模式 (Chain of Responsibility Pattern)**：将多个处理器连接成一条链，沿着链传递请求，直到某个处理器处理请求。
   - **模板方法模式 (Template Method Pattern)**：定义一个算法的框架，而将一些步骤的实现延迟到子类。
   - **状态模式 (State Pattern)**：允许对象在内部状态改变时改变其行为，看起来就像改变了它的类。
   - **中介者模式 (Mediator Pattern)**：用一个中介对象来封装一组对象之间的交互关系，简化对象之间的通信。
   - **迭代器模式 (Iterator Pattern)**：提供一种方法顺序访问聚合对象的各个元素，而又不暴露该对象的内部表示。
   - **访问者模式 (Visitor Pattern)**：将操作与对象结构分离，使得可以在不改变对象类的前提下定义作用于这些对象的新操作。
   - **备忘录模式 (Memento Pattern)**：在不破坏封装的前提下，捕获并保存对象的内部状态，以便稍后恢复。
   - **解释器模式 (Interpreter Pattern)**：为语言中的每一个符号定义一个解释器，使得可以解释语言中的句子。

### 设计模式的分类总结 (Summary of Design Patterns)

| **设计模式类别**        | **模式数量** | **具体模式**                                                                                                                                               |
|------------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| **创建型模式 (Creational Patterns)** | 5           | 单例模式 (Singleton)、工厂方法模式 (Factory Method)、抽象工厂模式 (Abstract Factory)、建造者模式 (Builder)、原型模式 (Prototype)                                                                 |
| **结构型模式 (Structural Patterns)** | 7           | 适配器模式 (Adapter)、桥接模式 (Bridge)、组合模式 (Composite)、装饰模式 (Decorator)、外观模式 (Facade)、享元模式 (Flyweight)、代理模式 (Proxy)                                                |
| **行为型模式 (Behavioral Patterns)** | 11          | 策略模式 (Strategy)、观察者模式 (Observer)、命令模式 (Command)、责任链模式 (Chain of Responsibility)、模板方法模式 (Template Method)、状态模式 (State)、中介者模式 (Mediator)、迭代器模式 (Iterator)、访问者模式 (Visitor)、备忘录模式 (Memento)、解释器模式 (Interpreter) |

### 总结 (Conclusion)

总计 **23 种设计模式**，被划分为三大类：**创建型模式 (5 种)**、**结构型模式 (7 种)** 和 **行为型模式 (11 种)**。设计模式的选择应基于项目需求和系统的复杂性，避免过度设计。通过合理使用这些模式，可以设计出更加灵活、可扩展、易维护的系统架构。希望通过本总结，能帮助您在实际项目中更好地理解和应用面向对象设计模式。

以上涵盖了常见的创建型、结构型和行为型设计模式的定义、适用场景、优缺点以及 Java 和 C# 的代码实现。掌握这些模式有助于设计灵活、可扩展、可维护的系统架构。设计模式的选择应该基于具体的业务需求和系统的复杂性，避免过度设计。希望这些模式能够帮助您在实际项目中更好地应用面向对象设计原则。


