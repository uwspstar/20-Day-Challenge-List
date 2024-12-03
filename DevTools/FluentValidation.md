### FluentValidation 在 .NET 中的使用

**FluentValidation** 是一个用于 .NET 的强大验证库，它通过流式接口提供简洁、易读的代码来验证对象属性和业务规则。相比手写验证逻辑，FluentValidation 提高了代码的可维护性和可测试性。

---

### **1. 为什么使用 FluentValidation？**

#### **优势**：
1. **简洁的语法**：通过流式接口定义验证规则，代码更直观。
2. **强大的功能**：
   - 支持复杂验证规则。
   - 提供条件验证和自定义规则。
   - 支持本地化错误消息。
3. **易于测试**：验证逻辑与业务逻辑分离，便于单元测试。
4. **集成支持**：与 ASP.NET Core 的模型验证无缝集成。

---

### **2. 安装 FluentValidation**

#### **通过 NuGet 安装**：
运行以下命令安装 FluentValidation 和 ASP.NET Core 集成包：

```bash
dotnet add package FluentValidation
dotnet add package FluentValidation.AspNetCore
```

---

### **3. 基本使用**

以下是使用 FluentValidation 的示例，包括定义验证器和执行验证。

#### **示例：定义模型和验证规则**

```csharp
using FluentValidation;

// 定义数据模型
public class User
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}

// 定义验证器
public class UserValidator : AbstractValidator<User>
{
    public UserValidator()
    {
        // 验证 Name 非空，且长度在 2 到 50 之间
        RuleFor(user => user.Name)
            .NotEmpty().WithMessage("Name 不能为空")
            .Length(2, 50).WithMessage("Name 长度必须在 2 到 50 之间");

        // 验证 Age 在 18 到 60 之间
        RuleFor(user => user.Age)
            .InclusiveBetween(18, 60).WithMessage("Age 必须在 18 到 60 之间");

        // 验证 Email 格式
        RuleFor(user => user.Email)
            .EmailAddress().WithMessage("Email 格式无效");
    }
}
```

#### **执行验证**

```csharp
class Program
{
    static void Main()
    {
        // 创建用户对象
        var user = new User
        {
            Name = "Xing",
            Age = 25,
            Email = "test@example.com"
        };

        // 创建验证器
        var validator = new UserValidator();

        // 执行验证
        var result = validator.Validate(user);

        if (result.IsValid)
        {
            Console.WriteLine("验证通过！");
        }
        else
        {
            foreach (var error in result.Errors)
            {
                Console.WriteLine($"错误：{error.ErrorMessage}");
            }
        }
    }
}
```

---

### **4. 在 ASP.NET Core 中集成**

#### **配置 FluentValidation**

在 ASP.NET Core 项目中，可以将 FluentValidation 与模型绑定集成，自动处理模型验证。

```csharp
// 在 Program.cs 中配置 FluentValidation
builder.Services.AddControllers();
builder.Services.AddFluentValidationAutoValidation();
builder.Services.AddValidatorsFromAssemblyContaining<UserValidator>(); // 自动注册验证器
```

#### **控制器使用**

```csharp
[ApiController]
[Route("api/[controller]")]
public class UserController : ControllerBase
{
    [HttpPost]
    public IActionResult CreateUser([FromBody] User user)
    {
        // 如果模型验证失败，FluentValidation 会自动返回 400 响应
        return Ok("用户创建成功");
    }
}
```

---

### **5. 高级功能**

#### **1. 条件验证**
根据条件动态应用规则。

```csharp
RuleFor(user => user.Email)
    .NotEmpty().When(user => user.Age > 18).WithMessage("成人用户必须提供 Email");
```

#### **2. 自定义验证规则**
添加复杂的自定义逻辑。

```csharp
RuleFor(user => user.Name).Custom((name, context) =>
{
    if (name == "Admin")
    {
        context.AddFailure("Name 不能为 'Admin'");
    }
});
```

#### **3. 验证集合**
验证嵌套对象或集合。

```csharp
RuleForEach(user => user.Addresses)
    .SetValidator(new AddressValidator());
```

#### **4. 本地化错误消息**
支持多语言错误消息。

```csharp
RuleFor(user => user.Name)
    .NotEmpty().WithMessage("Name 是必填项"); // 可替换为资源文件中的本地化字符串
```

---

### **6. 注意事项**

1. **性能优化**：
   - 避免在 `Validate` 方法中进行数据库查询或耗时操作。
2. **错误处理**：
   - 在 ASP.NET Core 中，可以自定义错误响应格式。
3. **与原生模型验证冲突**：
   - 如果同时使用 DataAnnotations 和 FluentValidation，需要注意规则的优先级问题。

---

### **总结**

| **功能**              | **描述**                             |
|----------------------|------------------------------------|
| **简单验证**          | 使用流式接口定义规则，代码简洁直观。          |
| **复杂验证**          | 支持条件验证、自定义规则和集合验证。          |
| **ASP.NET Core 集成**  | 自动处理模型验证，支持本地化错误消息。         |
| **性能和安全**         | 规则应尽量避免耗时操作，使用有效错误处理策略。   |

FluentValidation 是 .NET 应用中一个灵活、高效的验证工具。它适用于复杂业务规则的验证场景，尤其是在需要简洁代码和高可维护性的项目中。
