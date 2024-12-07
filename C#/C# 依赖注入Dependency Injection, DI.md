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
