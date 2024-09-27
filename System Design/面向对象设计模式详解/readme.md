### 面向对象设计模式详解 (Object-Oriented Design Patterns Detailed Explanation)

面向对象设计模式是一种用于解决常见软件设计问题的可重用解决方案。它们可以帮助开发者设计出灵活、可扩展和易维护的代码结构。
经典的设计模式主要分为三大类：**创建型模式 (Creational Patterns)**、**结构型模式 (Structural Patterns)** 和 **行为型模式 (Behavioral Patterns)**。
在面向对象设计中，设计模式用于提供解决常见软件设计问题的可重用方案，帮助开发者创建灵活、可扩展和易维护的代码结构。经典的设计模式主要分为 **三大类，共 23 种**，具体如下：

---

1. **创建型模式 (Creational Patterns)** - **5 种**  
   创建型模式主要用于对象的创建，能够使系统更灵活地控制对象的实例化过程，避免直接使用 `new` 操作符。
   - **单例模式 (Singleton Pattern)**：确保一个类只有一个实例，并提供全局访问点。
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
   - **观察者模式 (Observer Pattern)**：定义对象之间一对多的依赖关系，当一个对象的状态发生变化时，所有依赖它的对象都会被通知。
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

---

### 1. 创建型模式 (Creational Patterns)

创建型模式主要用于创建对象，能够帮助系统在面对复杂对象创建时更灵活地管理和控制对象的实例化过程。常见的创建型模式包括：

#### 1.1 单例模式 (Singleton Pattern)

- **定义**：确保一个类只有一个实例，并提供全局访问点。
- **使用场景**：适用于需要全局唯一访问点的场景，例如数据库连接池、配置管理器等。
- **优点**：
  - 提供对唯一实例的全局访问。
  - 控制实例化数量，减少内存开销。
- **缺点**：
  - 增加了类之间的依赖性，违背了单一职责原则。
  - 在多线程环境中需要额外处理线程安全问题。

- **Java 示例代码**：

  ```java
  public class Singleton {
      private static Singleton instance;

      private Singleton() {} // 私有构造函数，防止外部实例化

      public static synchronized Singleton getInstance() {
          if (instance == null) {
              instance = new Singleton();
          }
          return instance;
      }
  }

  // 示例用法
  Singleton singleton1 = Singleton.getInstance();
  Singleton singleton2 = Singleton.getInstance();
  System.out.println(singleton1 == singleton2); // 输出: true
  ```

- **C# 示例代码**：

  ```csharp
  public class Singleton
  {
      private static Singleton instance;

      private Singleton() {} // 私有构造函数

      public static Singleton Instance
      {
          get
          {
              if (instance == null)
              {
                  instance = new Singleton();
              }
              return instance;
          }
      }
  }

  // 示例用法
  Singleton singleton1 = Singleton.Instance;
  Singleton singleton2 = Singleton.Instance;
  Console.WriteLine(singleton1 == singleton2); // 输出: true
  ```

#### 1.2 工厂方法模式 (Factory Method Pattern)

- **定义**：定义一个用于创建对象的接口，让子类决定实例化哪一个类。
- **使用场景**：用于当需要创建的对象具有复杂创建过程时，或者对象类型在运行时才确定的场景。
- **优点**：
  - 客户端不需要知道具体产品类的细节，实现了解耦。
- **缺点**：
  - 随着产品类的增加，子类数量会增加，系统复杂度也随之增加。

- **Java 示例代码**：

  ```java
  // 抽象产品类
  abstract class Shape {
      abstract void draw();
  }

  // 具体产品类
  class Circle extends Shape {
      void draw() {
          System.out.println("Drawing a Circle");
      }
  }

  class Square extends Shape {
      void draw() {
          System.out.println("Drawing a Square");
      }
  }

  // 工厂类
  class ShapeFactory {
      public static Shape createShape(String type) {
          if (type.equalsIgnoreCase("circle")) {
              return new Circle();
          } else if (type.equalsIgnoreCase("square")) {
              return new Square();
          }
          return null;
      }
  }

  // 示例用法
  Shape shape = ShapeFactory.createShape("circle");
  shape.draw(); // 输出: Drawing a Circle
  ```

- **C# 示例代码**：

  ```csharp
  // 抽象产品类
  abstract class Shape
  {
      public abstract void Draw();
  }

  // 具体产品类
  class Circle : Shape
  {
      public override void Draw()
      {
          Console.WriteLine("Drawing a Circle");
      }
  }

  class Square : Shape
  {
      public override void Draw()
      {
          Console.WriteLine("Drawing a Square");
      }
  }

  // 工厂类
  class ShapeFactory
  {
      public static Shape CreateShape(string type)
      {
          if (type.Equals("circle", StringComparison.OrdinalIgnoreCase))
          {
              return new Circle();
          }
          else if (type.Equals("square", StringComparison.OrdinalIgnoreCase))
          {
              return new Square();
          }
          return null;
      }
  }

  // 示例用法
  Shape shape = ShapeFactory.CreateShape("circle");
  shape.Draw(); // 输出: Drawing a Circle
  ```

#### 1.3 抽象工厂模式 (Abstract Factory Pattern)

- **定义**：提供一个接口，用于创建相关或依赖对象的家族，而不指定具体类。
- **使用场景**：用于系统中对象具有相互依赖关系且对象类型在运行时才确定的场景。
- **优点**：
  - 分离了具体类的实现，提高了系统的灵活性。
- **缺点**：
  - 增加了系统的抽象层次和复杂性。

- **Java 示例代码**：

  ```java
  // 抽象产品类
  interface Button {
      void render();
  }

  // 具体产品类
  class WindowsButton implements Button {
      public void render() {
          System.out.println("Render a Windows Button");
      }
  }

  class MacOSButton implements Button {
      public void render() {
          System.out.println("Render a MacOS Button");
      }
  }

  // 抽象工厂类
  interface GUIFactory {
      Button createButton();
  }

  // 具体工厂类
  class WindowsFactory implements GUIFactory {
      public Button createButton() {
          return new WindowsButton();
      }
  }

  class MacOSFactory implements GUIFactory {
      public Button createButton() {
          return new MacOSButton();
      }
  }

  // 示例用法
  GUIFactory factory = new WindowsFactory();
  Button button = factory.createButton();
  button.render(); // 输出: Render a Windows Button
  ```

- **C# 示例代码**：

  ```csharp
  // 抽象产品类
  interface Button
  {
      void Render();
  }

  // 具体产品类
  class WindowsButton : Button
  {
      public void Render()
      {
          Console.WriteLine("Render a Windows Button");
      }
  }

  class MacOSButton : Button
  {
      public void Render()
      {
          Console.WriteLine("Render a MacOS Button");
      }
  }

  // 抽象工厂类
  interface GUIFactory
  {
      Button CreateButton();
  }

  // 具体工厂类
  class WindowsFactory : GUIFactory
  {
      public Button CreateButton()
      {
          return new WindowsButton();
      }
  }

  class MacOSFactory : GUIFactory
  {
      public Button CreateButton()
      {
          return new MacOSButton();
      }
  }

  // 示例用法
  GUIFactory factory = new WindowsFactory();
  Button button = factory.CreateButton();
  button.Render(); // 输出: Render a Windows Button
  ```

#### 1.4 建造者模式 (Builder Pattern)

- **定义**：将对象的构建过程与其表示分离，使得同样的构建过程可以创建不同的表示。
- **使用场景**：用于创建复杂对象，尤其是多个属性需要一步步设置的对象。
- **优点**：
  - 允许一步步构建复杂对象，避免了构造函数过长的问题。
- **缺点**：
  - 增加了许多额外的类和代码，使得系统复杂性提高。

- **Java 示例代码**：

  ```java
  class Computer {
      private String cpu;
      private int ram;
      private int storage;

      public Computer(String cpu, int ram, int storage) {
          this.cpu = cpu;
          this.ram = ram;
          this.storage = storage;
      }

      @Override
      public String toString() {
          return "Computer: CPU=" + cpu + ", RAM=" + ram + "GB, Storage=" + storage + "GB";
      }
  }

  class ComputerBuilder {
      private String cpu;
      private int ram;
      private int storage;

      public ComputerBuilder setCpu(String cpu) {
          this.cpu = cpu;
          return this;
      }

      public ComputerBuilder setRam(int ram) {
          this.ram = ram;
          return this;
      }

      public ComputerBuilder setStorage(int storage) {
          this.storage = storage;
          return this;
      }

      public Computer build() {
          return new Computer(cpu, ram, storage);
      }
  }

  // 示例用法
  Computer computer = new ComputerBuilder()
                      .setCpu("Intel i9")
                      .setRam(32)
                      .setStorage(1024)
                      .build();
  System.out.println(computer); // 输出: Computer: CPU=Intel i9, RAM=32GB, Storage=1024GB
  ```

- **C# 示例代码**：

  ```csharp
  class Computer
  {
      public string CPU { get; }
      public int RAM { get; }
      public int Storage { get; }

      public Computer(string cpu, int ram, int```csharp
      storage)
      {
          CPU = cpu;
          RAM = ram;
          Storage = storage;
      }

      public override string ToString()
      {
          return $"Computer: CPU={CPU}, RAM={RAM}GB, Storage={Storage}GB";
      }
  }

  class ComputerBuilder
  {
      private string cpu;
      private int ram;
      private int storage;

      public ComputerBuilder SetCpu(string cpu)
      {
          this.cpu = cpu;
          return this;
      }

      public ComputerBuilder SetRam(int ram)
      {
          this.ram = ram;
          return this;
      }

      public ComputerBuilder SetStorage(int storage)
      {
          this.storage = storage;
          return this;
      }

      public Computer Build()
      {
          return new Computer(cpu, ram, storage);
      }
  }

  // 示例用法
  Computer computer = new ComputerBuilder()
                      .SetCpu("Intel i9")
                      .SetRam(32)
                      .SetStorage(1024)
                      .Build();
  Console.WriteLine(computer); // 输出: Computer: CPU=Intel i9, RAM=32GB, Storage=1024GB
  ```

#### 1.5 原型模式 (Prototype Pattern)

- **定义**：使用原型实例指定创建对象的种类，并通过复制这些原型创建新的对象。
- **使用场景**：在创建开销较大的对象时（如数据库操作、网络请求等），通过复制现有对象来创建新对象。
- **优点**：
  - 提供了创建对象的简单方法，并避免了类的多层次复杂继承。
- **缺点**：
  - 深复制和浅复制的问题可能导致不易发现的错误。

- **Java 示例代码**：

  ```java
  import java.util.Objects;

  abstract class Prototype implements Cloneable {
      public Prototype clone() throws CloneNotSupportedException {
          return (Prototype) super.clone();
      }
  }

  class ConcretePrototype extends Prototype {
      private int value;

      public ConcretePrototype(int value) {
          this.value = value;
      }

      public int getValue() {
          return value;
      }

      public void setValue(int value) {
          this.value = value;
      }

      @Override
      public String toString() {
          return "ConcretePrototype: " + value;
      }
  }

  // 示例用法
  ConcretePrototype prototype = new ConcretePrototype(10);
  try {
      ConcretePrototype clonedPrototype = (ConcretePrototype) prototype.clone();
      System.out.println(clonedPrototype); // 输出: ConcretePrototype: 10
  } catch (CloneNotSupportedException e) {
      e.printStackTrace();
  }
  ```

- **C# 示例代码**：

  ```csharp
  using System;

  abstract class Prototype
  {
      public abstract Prototype Clone();
  }

  class ConcretePrototype : Prototype
  {
      public int Value { get; set; }

      public ConcretePrototype(int value)
      {
          Value = value;
      }

      public override Prototype Clone()
      {
          return (Prototype)this.MemberwiseClone();
      }

      public override string ToString()
      {
          return $"ConcretePrototype: {Value}";
      }
  }

  // 示例用法
  ConcretePrototype prototype = new ConcretePrototype(10);
  ConcretePrototype clonedPrototype = (ConcretePrototype)prototype.Clone();
  Console.WriteLine(clonedPrototype); // 输出: ConcretePrototype: 10
  ```

---

### 2. 结构型模式 (Structural Patterns)

结构型模式关注类和对象的组合，如何将对象和类组装成更大的结构来实现新的功能。常见的结构型模式包括适配器模式、桥接模式、组合模式、装饰模式、外观模式、享元模式和代理模式。

#### 2.1 适配器模式 (Adapter Pattern)

- **定义**：将一个类的接口转换成客户希望的另一个接口，适配器模式使原本接口不兼容的类可以一起工作。
- **使用场景**：当需要将已有的类改造成不同接口使用时，或者现有系统中引入了新的模块需要适配老接口时。
- **优点**：
  - 可以使得两个不兼容的接口相互协作。
- **缺点**：
  - 增加了系统的复杂性，因为增加了额外的适配层。

- **Java 示例代码**：

  ```java
  // 现有的老系统类
  class OldSystem {
      public String specificRequest() {
          return "Old System Response";
      }
  }

  // 目标接口
  interface Target {
      String request();
  }

  // 适配器类
  class Adapter implements Target {
      private OldSystem oldSystem;

      public Adapter(OldSystem oldSystem) {
          this.oldSystem = oldSystem;
      }

      @Override
      public String request() {
          return oldSystem.specificRequest();
      }
  }

  // 示例用法
  OldSystem oldSystem = new OldSystem();
  Target adapter = new Adapter(oldSystem);
  System.out.println(adapter.request()); // 输出: Old System Response
  ```

- **C# 示例代码**：

  ```csharp
  // 现有的老系统类
  class OldSystem
  {
      public string SpecificRequest()
      {
          return "Old System Response";
      }
  }

  // 目标接口
  interface ITarget
  {
      string Request();
  }

  // 适配器类
  class Adapter : ITarget
  {
      private OldSystem oldSystem;

      public Adapter(OldSystem oldSystem)
      {
          this.oldSystem = oldSystem;
      }

      public string Request()
      {
          return oldSystem.SpecificRequest();
      }
  }

  // 示例用法
  OldSystem oldSystem = new OldSystem();
  ITarget adapter = new Adapter(oldSystem);
  Console.WriteLine(adapter.Request()); // 输出: Old System Response
  ```

#### 2.2 桥接模式 (Bridge Pattern)

- **定义**：将抽象部分与实现部分分离，使它们可以独立地变化。
- **使用场景**：适用于实现系统中存在多维度变化的场景，如不同设备上的不同接口实现。
- **优点**：
  - 分离了抽象与实现，使它们可以独立地变化。
- **缺点**：
  - 增加了系统的复杂性。

- **Java 示例代码**：

  ```java
  // 实现接口
  interface Color {
      String fill();
  }

  class RedColor implements Color {
      public String fill() {
          return "Color is Red";
      }
  }

  class GreenColor implements Color {
      public String fill() {
          return "Color is Green";
      }
  }

  // 抽象类
  abstract class Shape {
      protected Color color;

      protected Shape(Color color) {
          this.color = color;
      }

      abstract void draw();
  }

  class Circle extends Shape {
      public Circle(Color color) {
          super(color);
      }

      public void draw() {
          System.out.println("Circle drawn with " + color.fill());
      }
  }

  // 示例用法
  Shape redCircle = new Circle(new RedColor());
  redCircle.draw(); // 输出: Circle drawn with Color is Red
  ```

- **C# 示例代码**：

  ```csharp
  // 实现接口
  interface IColor
  {
      string Fill();
  }

  class RedColor : IColor
  {
      public string Fill()
      {
          return "Color is Red";
      }
  }

  class GreenColor : IColor
  {
      public string Fill()
      {
          return "Color is Green";
      }
  }

  // 抽象类
  abstract class Shape
  {
      protected IColor color;

      protected Shape(IColor color)
      {
          this.color = color;
      }

      public abstract void Draw();
  }

  class Circle : Shape
  {
      public Circle(IColor color) : base(color) { }

      public override void Draw()
      {
          Console.WriteLine($"Circle drawn with {color.Fill()}");
      }
  }

  // 示例用法
  Shape redCircle = new Circle(new RedColor());
  redCircle.Draw(); // 输出: Circle drawn with Color is Red
  ```

---

### 2. 结构型模式 (Structural Patterns) 续篇

#### 2.3 组合模式 (Composite Pattern)

- **定义**：将对象组合成树形结构以表示“部分-整体”的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性。
- **使用场景**：当需要表示对象的部分和整体层次结构时，例如文件系统目录、UI 元素层次结构。
- **优点**：
  - 可以清晰地定义复杂的树形结构，客户端可以以相同的方式处理组合对象和单个对象。
- **缺点**：
  - 使得设计变得更为复杂，并且在添加新的组件时可能需要修改已有的类。

- **Java 示例代码**：

  ```java
  import java.util.ArrayList;
  import java.util.List;

  // 组件接口
  interface Component {
      void showDetails();
  }

  // 叶子组件
  class Leaf implements Component {
      private String name;

      public Leaf(String name) {
          this.name = name;
      }

      @Override
      public void showDetails() {
          System.out.println("Leaf: " + name);
      }
  }

  // 组合组件
  class Composite implements Component {
      private List<Component> components = new ArrayList<>();

      public void addComponent(Component component) {
          components.add(component);
      }

      @Override
      public void showDetails() {
          for (Component component : components) {
              component.showDetails();
          }
      }
  }

  // 示例用法
  Composite tree = new Composite();
  tree.addComponent(new Leaf("Leaf A"));
  tree.addComponent(new Leaf("Leaf B"));
  Composite subtree = new Composite();
  subtree.addComponent(new Leaf("Leaf C"));
  tree.addComponent(subtree);
  tree.showDetails();
  ```

- **C# 示例代码**：

  ```csharp
  using System;
  using System.Collections.Generic;

  // 组件接口
  interface IComponent
  {
      void ShowDetails();
  }

  // 叶子组件
  class Leaf : IComponent
  {
      private string name;

      public Leaf(string name)
      {
          this.name = name;
      }

      public void ShowDetails()
      {
          Console.WriteLine("Leaf: " + name);
      }
  }

  // 组合组件
  class Composite : IComponent
  {
      private List<IComponent> components = new List<IComponent>();

      public void AddComponent(IComponent component)
      {
          components.Add(component);
      }

      public void ShowDetails()
      {
          foreach (var component in components)
          {
              component.ShowDetails();
          }
      }
  }

  // 示例用法
  Composite tree = new Composite();
  tree.AddComponent(new Leaf("Leaf A"));
  tree.AddComponent(new Leaf("Leaf B"));
  Composite subtree = new Composite();
  subtree.AddComponent(new Leaf("Leaf C"));
  tree.AddComponent(subtree);
  tree.ShowDetails();
  ```

#### 2.4 装饰模式 (Decorator Pattern)

- **定义**：动态地给对象增加新的功能，并且这种功能扩展不影响其他对象。
- **使用场景**：在不改变原有类的基础上，为对象动态添加职责。例如，为文本框组件增加滚动功能。
- **优点**：
  - 通过组合而非继承的方式动态扩展对象的功能，降低类的复杂度。
- **缺点**：
  - 增加了许多小的类，系统变得更加复杂。

- **Java 示例代码**：

  ```java
  // 基础组件接口
  interface Coffee {
      String getDescription();
      double cost();
  }

  // 具体组件类
  class SimpleCoffee implements Coffee {
      public String getDescription() {
          return "Simple Coffee";
      }

      public double cost() {
          return 5.0;
      }
  }

  // 装饰器基类
  abstract class CoffeeDecorator implements Coffee {
      protected Coffee decoratedCoffee;

      public CoffeeDecorator(Coffee coffee) {
          this.decoratedCoffee = coffee;
      }

      public String getDescription() {
          return decoratedCoffee.getDescription();
      }

      public double cost() {
          return decoratedCoffee.cost();
      }
  }

  // 具体装饰器类
  class MilkDecorator extends CoffeeDecorator {
      public MilkDecorator(Coffee coffee) {
          super(coffee);
      }

      public String getDescription() {
          return decoratedCoffee.getDescription() + ", Milk";
      }

      public double cost() {
          return decoratedCoffee.cost() + 1.5;
      }
  }

  class SugarDecorator extends CoffeeDecorator {
      public SugarDecorator(Coffee coffee) {
          super(coffee);
      }

      public String getDescription() {
          return decoratedCoffee.getDescription() + ", Sugar";
      }

      public double cost() {
          return decoratedCoffee.cost() + 0.5;
      }
  }

  // 示例用法
  Coffee coffee = new SimpleCoffee();
  coffee = new MilkDecorator(coffee);
  coffee = new SugarDecorator(coffee);
  System.out.println(coffee.getDescription() + " costs $" + coffee.cost());
  ```

- **C# 示例代码**：

  ```csharp
  // 基础组件接口
  interface ICoffee
  {
      string GetDescription();
      double Cost();
  }

  // 具体组件类
  class SimpleCoffee : ICoffee
  {
      public string GetDescription()
      {
          return "Simple Coffee";
      }

      public double Cost()
      {
          return 5.0;
      }
  }

  // 装饰器基类
  abstract class CoffeeDecorator : ICoffee
  {
      protected ICoffee decoratedCoffee;

      public CoffeeDecorator(ICoffee coffee)
      {
          this.decoratedCoffee = coffee;
      }

      public virtual string GetDescription()
      {
          return decoratedCoffee.GetDescription();
      }

      public virtual double Cost()
      {
          return decoratedCoffee.Cost();
      }
  }

  // 具体装饰器类
  class MilkDecorator : CoffeeDecorator
  {
      public MilkDecorator(ICoffee coffee) : base(coffee) {}

      public override string GetDescription()
      {
          return base.GetDescription() + ", Milk";
      }

      public override double Cost()
      {
          return base.Cost() + 1.5;
      }
  }

  class SugarDecorator : CoffeeDecorator
  {
      public SugarDecorator(ICoffee coffee) : base(coffee) {}

      public override string GetDescription()
      {
          return base.GetDescription() + ", Sugar";
      }

      public override double Cost()
      {
          return base.Cost() + 0.5;
      }
  }

  // 示例用法
  ICoffee coffee = new SimpleCoffee();
  coffee = new MilkDecorator(coffee);
  coffee = new SugarDecorator(coffee);
  Console.WriteLine($"{coffee.GetDescription()} costs ${coffee.Cost()}");
  ```

#### 2.5 外观模式 (Facade Pattern)

- **定义**：为子系统中的一组接口提供一个一致的界面，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。
- **使用场景**：用于简化复杂子系统的接口，使得子系统更容易使用和访问。
- **优点**：
  - 减少系统与客户端的耦合，隐藏了子系统的复杂性。
- **缺点**：
  - 不符合开闭原则，如果需要添加子系统，则可能需要修改外观类。

- **Java 示例代码**：

  ```java
  class CPU {
      public void start() {
          System.out.println("CPU started");
      }
  }

  class Memory {
      public void load() {
          System.out.println("Memory loaded");
      }
  }

  class HardDrive {
      public void read() {
          System.out.println("Hard Drive reading data");
      }
  }

  // 外观类
  class ComputerFacade {
      private CPU cpu;
      private Memory memory;
      private HardDrive hardDrive;

      public ComputerFacade() {
          this.cpu = new CPU();
          this.memory = new Memory();
          this.hardDrive = new HardDrive();
      }

      public void startComputer() {
          cpu.start();
          memory.load();
          hardDrive.read();
          System.out.println("Computer started");
      }
  }

  // 示例用法
  ComputerFacade computer = new ComputerFacade();
  computer.startComputer();
  ```

- **C# 示例代码**：

  ```csharp
  class CPU
  {
      public void Start()
      {
          Console.WriteLine("CPU started");
      }
  }

  class Memory
  {
      public void Load()
      {
          Console.WriteLine("Memory loaded");
      }
  }

  class HardDrive
  {
      public void Read()
      {
          Console.WriteLine("Hard Drive reading data");
      }
  }

  // 外观类
  class ComputerFacade
  {
      private CPU cpu;
      private Memory memory;
      private HardDrive hardDrive;

      public ComputerFacade()
      {
          this.cpu = new CPU();
          this.memory = new Memory();
          this.hardDrive = new HardDrive();
      }

      public void StartComputer()
      {
          cpu.Start();
          memory.Load();
          hardDrive.Read();
          Console.WriteLine("Computer started");
      }
  }

  // 示例用法
  ComputerFacade computer = new ComputerFacade();
  computer.StartComputer();
  ```

---

### 3. 行为型模式 (Behavioral Patterns)

行为型模式关注对象之间的通信与职责分配。常见的

行为型模式包括策略模式、观察者模式、命令模式、责任链模式、模板方法模式等。

#### 3.1 策略模式 (Strategy Pattern)

- **定义**：定义一组算法，将每个算法封装起来，并使它们可以相互替换。
- **使用场景**：用于算法的动态选择，如不同排序算法、不同的支付方式等。
- **优点**：
  - 消除了算法类之间的耦合，每个算法独立实现，可以方便地替换或添加新的算法。
- **缺点**：
  - 客户端必须了解所有策略类的实现，以决定使用哪种策略。

- **Java 示例代码**：

  ```java
  // 策略接口
  interface Strategy {
      int execute(int a, int b);
  }

  // 具体策略类
  class Addition implements Strategy {
      public int execute(int a, int b) {
          return a + b;
      }
  }

  class Subtraction implements Strategy {
      public int execute(int a, int b) {
          return a - b;
      }
  }

  // 上下文类
  class Context {
      private Strategy strategy;

      public Context(Strategy strategy) {
          this.strategy = strategy;
      }

      public int executeStrategy(int a, int b) {
          return strategy.execute(a, b);
      }
  }

  // 示例用法
  Context context = new Context(new Addition());
  System.out.println("10 + 5 = " + context.executeStrategy(10, 5)); // 输出: 10 + 5 = 15

  context = new Context(new Subtraction());
  System.out.println("10 - 5 = " + context.executeStrategy(10, 5)); // 输出: 10 - 5 = 5
  ```

- **C# 示例代码**：

  ```csharp
  // 策略接口
  interface IStrategy
  {
      int Execute(int a, int b);
  }

  // 具体策略类
  class Addition : IStrategy
  {
      public int Execute(int a, int b)
      {
          return a + b;
      }
  }

  class Subtraction : IStrategy
  {
      public int Execute(int a, int b)
      {
          return a - b;
      }
  }

  // 上下文类
  class Context
  {
      private IStrategy strategy;

      public Context(IStrategy strategy)
      {
          this.strategy = strategy;
      }

      public int ExecuteStrategy(int a, int b)
      {
          return strategy.Execute(a, b);
      }
  }

  // 示例用法
  Context context = new Context(new Addition());
  Console.WriteLine("10 + 5 = " + context.ExecuteStrategy(10, 5)); // 输出: 10 + 5 = 15

  context = new Context(new Subtraction());
  Console.WriteLine("10 - 5 = " + context.ExecuteStrategy(10, 5)); // 输出: 10 - 5 = 5
  ```

### 总结

以上涵盖了常见的创建型、结构型和行为型设计模式的定义、适用场景、优缺点以及 Java 和 C# 的代码实现。掌握这些模式有助于设计灵活、可扩展、可维护的系统架构。设计模式的选择应该基于具体的业务需求和系统的复杂性，避免过度设计。希望这些模式能够帮助您在实际项目中更好地应用面向对象设计原则。


