### **C# 依赖注入（Dependency Injection, DI）**

依赖注入是 **C#** 中一种常见的设计模式，通过控制反转 (**Inversion of Control, IoC**) 实现组件之间的松耦合。在 **ASP.NET Core** 中，依赖注入是框架的核心特性之一，默认内置支持。

---

### **依赖注入的核心概念**

#### 1. **依赖（Dependency）**
- 一个类需要依赖另一个类的实例才能完成其功能。
- 例如，`OrderService` 依赖于 `ILogger` 来记录日志。

#### 2. **注入（Injection）**
- 将依赖的实例通过构造函数、属性或方法传递给需要的类。

#### 3. **IoC 容器**
- IoC 容器管理对象的生命周期，并负责将依赖对象注入到目标类中。

---

### **C# DI 的优点**
1. **松耦合**：提高模块的独立性，方便测试和维护。
2. **可测试性**：通过依赖注入，可以轻松使用 Mock 对象进行单元测试。
3. **生命周期管理**：IoC 容器帮助开发者管理对象的创建和销毁。

---

### **依赖注入的实现方式**

#### **1. 构造函数注入**
通过构造函数将依赖传递给目标类。
```csharp
public class OrderService
{
    private readonly ILogger _logger;

    // 构造函数注入
    public OrderService(ILogger logger)
    {
        _logger = logger;
    }

    public void ProcessOrder()
    {
        _logger.Log("Processing order...");
    }
}
```

#### **2. 属性注入**
通过设置类的属性来注入依赖。
```csharp
public class OrderService
{
    public ILogger Logger { get; set; }

    public void ProcessOrder()
    {
        Logger.Log("Processing order...");
    }
}
```

#### **3. 方法注入**
通过方法参数将依赖传递给类的方法。
```csharp
public class OrderService
{
    public void ProcessOrder(ILogger logger)
    {
        logger.Log("Processing order...");
    }
}
```

---

### **ASP.NET Core 中的依赖注入**

#### **1. 配置服务容器**
在 `Program.cs` 或 `Startup.cs` 中，通过 `IServiceCollection` 注册依赖。
```csharp
var builder = WebApplication.CreateBuilder(args);

// 注册服务
builder.Services.AddSingleton<ILogger, ConsoleLogger>();
builder.Services.AddScoped<IOrderService, OrderService>();

var app = builder.Build();
```

#### **2. 使用依赖注入**
通过构造函数注入已注册的依赖。

**示例**：
```csharp
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}

public interface IOrderService
{
    void ProcessOrder();
}

public class OrderService : IOrderService
{
    private readonly ILogger _logger;

    public OrderService(ILogger logger)
    {
        _logger = logger;
    }

    public void ProcessOrder()
    {
        _logger.Log("Order processed.");
    }
}

var builder = WebApplication.CreateBuilder(args);

// 注册服务
builder.Services.AddSingleton<ILogger, ConsoleLogger>();
builder.Services.AddScoped<IOrderService, OrderService>();

var app = builder.Build();

// 配置终端点
app.MapGet("/", (IOrderService orderService) =>
{
    orderService.ProcessOrder();
    return "Order processed!";
});

app.Run();
```

---

### **服务生命周期**

ASP.NET Core 提供了三种服务生命周期管理方式：

| **生命周期**   | **描述**                                                                                                                                                         | **示例**                                |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------|
| **Transient**  | 每次请求都会创建一个新的实例，适用于轻量级、无状态的服务。                                                                                                         | `builder.Services.AddTransient<IMyService, MyService>();` |
| **Scoped**     | 在每个 HTTP 请求中只创建一个实例，适用于需要在整个请求生命周期内共享的服务。                                                                                         | `builder.Services.AddScoped<IMyService, MyService>();`    |
| **Singleton**  | 在应用程序的整个生命周期内只创建一个实例，适用于全局共享的服务。                                                                                                   | `builder.Services.AddSingleton<IMyService, MyService>();` |

---

### **常见问题与解决**

#### **1. 服务未注册**
**错误**：未注册的服务会导致运行时异常。
**解决**：确保在 `Program.cs` 中正确注册依赖。

#### **2. 循环依赖**
**错误**：两个或多个服务直接或间接依赖彼此。
**解决**：
- 考虑重构代码以消除循环依赖。
- 使用 `IServiceProvider` 手动解析依赖。

#### **3. 多个实现**
**问题**：多个实现会导致 IoC 容器无法确定注入哪个。
**解决**：通过命名约定或 `IEnumerable<T>` 注入多个实现。

---

### **总结**

- **DI 的核心**：通过 IoC 容器管理依赖，提升代码的松耦合性和可维护性。
- **ASP.NET Core 的内置支持**：无需额外工具即可实现依赖注入。
- **三种生命周期管理**：`Transient`、`Scoped` 和 `Singleton` 满足不同场景需求。
- **最佳实践**：尽量使用构造函数注入，避免属性注入和方法注入，确保依赖清晰。

依赖注入是现代开发中的重要工具，掌握其用法可以极大提高代码质量和开发效率！

---

### **生命周期对比总结表**

以下是 **Transient**、**Scoped** 和 **Singleton** 的详细比较，包含 **创建时机**、**适用场景** 和 **特点**。

| **生命周期类型**  | **创建时机**                    | **适用场景**                                | **特点**                                                                                       |
|-------------------|---------------------------------|--------------------------------------------|----------------------------------------------------------------------------------------------|
| **Transient**     | 每次注入时创建新实例            | - 无状态的服务<br>- 工具类，如字符串操作、日志格式化 | - 每次调用都会创建新的实例。<br>- 实例轻量，适合无状态任务。<br>- 实例之间互不干扰。            |
| **Scoped**        | 每个 HTTP 请求生命周期内共享     | - 数据访问层，如 `DbContext`<br>- 需要在同一请求内共享数据的服务 | - 每个请求中共享同一实例。<br>- 请求完成后，实例会被销毁。<br>- 避免实例在不同请求间共享数据。   |
| **Singleton**     | 应用程序生命周期内共享一个实例   | - 全局状态服务，如配置管理器、缓存服务<br>- 大型单例，如第三方 API 客户端 | - 整个应用程序中共享一个实例。<br>- 减少实例创建的开销。<br>- 需要注意线程安全问题。           |

---

### **详细说明**

#### **1. Transient（瞬时服务）**
- **适用场景**：
  - 适用于无状态的任务或工具类服务。
  - 每次使用都需要新实例，例如日志格式化服务。
- **特点**：
  - 每次调用都会创建新的实例。
  - 实例之间相互独立，无需保存状态。
  - 实例轻量，创建开销较低。

#### **2. Scoped（作用域服务）**
- **适用场景**：
  - 适合与请求生命周期相关的服务，如数据库上下文 `DbContext`。
  - 需要在同一请求中共享状态的服务。
- **特点**：
  - 每个 HTTP 请求内共享一个实例。
  - 实例在请求完成后自动销毁，避免资源泄漏。
  - 不同请求之间不会共享实例，数据隔离性强。

#### **3. Singleton（单例服务）**
- **适用场景**：
  - 全局共享的服务，例如缓存管理器、配置加载器。
  - 重型对象（如第三方 API 客户端）避免多次创建。
- **特点**：
  - 整个应用程序生命周期内只创建一个实例。
  - 减少重复实例创建的开销。
  - 需要注意线程安全问题，避免状态被多线程同时修改。

---

### **代码示例**

#### **Transient 示例**
```csharp
builder.Services.AddTransient<IMyService, MyService>();
```
- 每次注入时创建一个新实例。
- 适用于：轻量工具类服务，无状态任务。

#### **Scoped 示例**
```csharp
builder.Services.AddScoped<IMyService, MyService>();
```
- 每个请求中共享一个实例。
- 适用于：数据访问层服务，需在同一请求中共享状态。

#### **Singleton 示例**
```csharp
builder.Services.AddSingleton<IMyService, MyService>();
```
- 整个应用程序共享一个实例。
- 适用于：全局服务，配置管理，线程安全服务。

---

### **选择指南**

| **使用场景**                 | **推荐生命周期**      |
|------------------------------|-----------------------|
| 工具类服务、无状态任务         | **Transient**         |
| 数据库访问、请求范围服务       | **Scoped**            |
| 配置管理、全局共享服务         | **Singleton**         |

通过正确选择生命周期，可以提高服务性能、优化资源利用，并避免潜在的线程安全问题。
