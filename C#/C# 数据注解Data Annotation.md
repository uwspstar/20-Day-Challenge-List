### C# 数据注解（Data Annotation）

C# 数据注解是一个强大的工具，主要用于对类和属性进行验证、格式化或数据库映射。它通常被用于 **ASP.NET Core** 应用程序中，尤其是模型绑定和验证场景。以下是详细介绍及示例。

---

| **注解**             | **描述**                                                                                           | **示例**                                                                                      |
|-----------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| `[Required]`          | 指定属性为必填字段。                                                                               | ```csharp<br>[Required]<br>public string Name { get; set; }```                              |
| `[StringLength]`      | 限制字符串的最小长度和最大长度。                                                                   | ```csharp<br>[StringLength(100, MinimumLength = 10)]<br>public string Description { get; set; }``` |
| `[Range]`             | 指定数值或日期范围。                                                                               | ```csharp<br>[Range(18, 60)]<br>public int Age { get; set; }```                             |
| `[MaxLength]`         | 指定字符串的最大长度。                                                                             | ```csharp<br>[MaxLength(50)]<br>public string Title { get; set; }```                        |
| `[MinLength]`         | 指定字符串的最小长度。                                                                             | ```csharp<br>[MinLength(5)]<br>public string ShortDescription { get; set; }```             |
| `[EmailAddress]`      | 验证属性是否是有效的电子邮件地址格式。                                                             | ```csharp<br>[EmailAddress]<br>public string Email { get; set; }```                         |
| `[Phone]`             | 验证属性是否是有效的电话号码格式。                                                                 | ```csharp<br>[Phone]<br>public string PhoneNumber { get; set; }```                          |
| `[Url]`               | 验证属性是否是有效的 URL 格式。                                                                    | ```csharp<br>[Url]<br>public string Website { get; set; }```                                |
| `[Compare]`           | 验证两个属性的值是否相等，常用于密码确认场景。                                                     | ```csharp<br>[Compare("Password")]<br>public string ConfirmPassword { get; set; }```        |
| `[CreditCard]`        | 验证属性是否是有效的信用卡格式。                                                                   | ```csharp<br>[CreditCard]<br>public string CreditCardNumber { get; set; }```                |
| `[RegularExpression]` | 验证属性是否符合指定的正则表达式格式。                                                             | ```csharp<br>[RegularExpression(@"^[a-zA-Z]+$", ErrorMessage = "仅支持字母。")]<br>public string Username { get; set; }``` |
| `[Key]`               | 指定属性为主键（通常在 **Entity Framework** 中使用）。                                              | ```csharp<br>[Key]<br>public int Id { get; set; }```                                        |
| `[Timestamp]`         | 用于并发控制，表示该属性是一个时间戳字段。                                                         | ```csharp<br>[Timestamp]<br>public byte[] RowVersion { get; set; }```                       |
| `[ForeignKey]`        | 指定外键字段，通常用于数据库关系映射。                                                             | ```csharp<br>[ForeignKey("UserId")]<br>public User User { get; set; }```                    |

---

### 示例：完整模型和验证

#### 模型定义
```csharp
using System.ComponentModel.DataAnnotations;

public class UserModel
{
    [Key]
    public int Id { get; set; }

    [Required(ErrorMessage = "姓名是必填项。")]
    [StringLength(50, ErrorMessage = "姓名不能超过 50 个字符。")]
    public string Name { get; set; }

    [Range(18, 100, ErrorMessage = "年龄必须在 18 到 100 之间。")]
    public int Age { get; set; }

    [EmailAddress(ErrorMessage = "无效的电子邮件格式。")]
    public string Email { get; set; }

    [Compare("Password", ErrorMessage = "密码和确认密码不一致。")]
    public string ConfirmPassword { get; set; }

    [RegularExpression(@"^[0-9]{10}$", ErrorMessage = "电话号码必须为 10 位数字。")]
    public string PhoneNumber { get; set; }
}
```

#### 验证示例
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

public class Program
{
    public static void Main()
    {
        var user = new UserModel
        {
            Name = "",
            Age = 17,
            Email = "invalid-email",
            ConfirmPassword = "123456",
            PhoneNumber = "123"
        };

        var validationResults = new List<ValidationResult>();
        var validationContext = new ValidationContext(user);

        if (!Validator.TryValidateObject(user, validationContext, validationResults, true))
        {
            foreach (var validationResult in validationResults)
            {
                Console.WriteLine(validationResult.ErrorMessage);
            }
        }
        else
        {
            Console.WriteLine("验证通过！");
        }
    }
}
```

---

### 输出结果
```
姓名是必填项。
年龄必须在 18 到 100 之间。
无效的电子邮件格式。
电话号码必须为 10 位数字。
```

---

### 总结

数据注解的优点：
1. **简洁性**：直接通过属性进行验证，无需额外的代码。
2. **灵活性**：可以通过属性参数指定验证规则，也可以自定义错误信息。
3. **集成性**：与 ASP.NET Core 模型绑定、EF Core 映射无缝集成。

**提示**：
- 在大规模项目中，可能需要结合自定义验证属性以实现更复杂的业务规则。
- 确保测试所有验证规则的覆盖性，避免潜在的验证漏洞。

