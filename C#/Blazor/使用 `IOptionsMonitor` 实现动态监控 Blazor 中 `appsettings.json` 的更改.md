### **使用 `IOptionsMonitor` 实现动态监控 Blazor 中 `appsettings.json` 的更改**

在 Blazor 应用中，可以通过 `IOptionsMonitor` 实现对 `appsettings.json` 配置文件的动态监控。`IOptionsMonitor` 提供了实时监听和更新的能力，允许在不重启应用的情况下应用新的配置。

---

### **实现步骤**

#### **1. 配置 `appsettings.json`**
定义一个简单的配置文件 `appsettings.json`，包含一个可变配置。

```json
{
  "AppSettings": {
    "Title": "My Blazor App",
    "RefreshInterval": 30
  }
}
```

---

#### **2. 定义配置类**
创建一个对应的 C# 配置类，用于映射 `appsettings.json` 中的数据。

```csharp
public class AppSettings
{
    public string Title { get; set; }
    public int RefreshInterval { get; set; }
}
```

---

#### **3. 注册配置和监控服务**
在 `Program.cs` 中配置服务，将 `AppSettings` 映射为可监控的配置。

```csharp
var builder = WebApplication.CreateBuilder(args);

// 添加对 appsettings.json 的支持，并启用动态监控
builder.Services.Configure<AppSettings>(builder.Configuration.GetSection("AppSettings"));
builder.Services.AddSingleton<IOptionsMonitor<AppSettings>>(sp => sp.GetRequiredService<IOptionsMonitor<AppSettings>>());

var app = builder.Build();

app.MapBlazorHub();
app.MapFallbackToPage("/_Host");

app.Run();
```

---

#### **4. 在 Blazor 组件中使用 `IOptionsMonitor`**
在 Blazor 组件中注入 `IOptionsMonitor<AppSettings>` 并动态获取配置。

**示例：`Pages/Index.razor`**

```razor
@inject IOptionsMonitor<AppSettings> AppSettingsMonitor

<h1>@AppSettings.Title</h1>
<p>Refresh Interval: @AppSettings.RefreshInterval seconds</p>

<button @onclick="RefreshSettings">Refresh Settings</button>

@code {
    private AppSettings AppSettings;

    protected override void OnInitialized()
    {
        // 订阅配置更改事件
        AppSettingsMonitor.OnChange(settings =>
        {
            AppSettings = settings;
            StateHasChanged(); // 通知组件重新渲染
        });

        // 初始化时加载配置
        AppSettings = AppSettingsMonitor.CurrentValue;
    }

    private void RefreshSettings()
    {
        // 模拟刷新操作，实际场景中配置文件需要手动修改
        Console.WriteLine("Current Title: " + AppSettings.Title);
    }
}
```

---

#### **5. 修改配置并测试**
当运行应用时：
1. 打开 `appsettings.json` 文件，修改 `AppSettings` 中的值，例如更改 `Title` 或 `RefreshInterval`。
2. 保存文件后，应用会自动加载新的配置，无需重启应用。

---

### **完整解决方案的代码结构**

#### **appsettings.json**
```json
{
  "AppSettings": {
    "Title": "Dynamic Blazor App",
    "RefreshInterval": 60
  }
}
```

#### **AppSettings.cs**
```csharp
public class AppSettings
{
    public string Title { get; set; }
    public int RefreshInterval { get; set; }
}
```

#### **Program.cs**
```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.Configure<AppSettings>(builder.Configuration.GetSection("AppSettings"));
builder.Services.AddSingleton<IOptionsMonitor<AppSettings>>(sp => sp.GetRequiredService<IOptionsMonitor<AppSettings>>());

var app = builder.Build();

app.MapBlazorHub();
app.MapFallbackToPage("/_Host");

app.Run();
```

#### **Index.razor**
```razor
@inject IOptionsMonitor<AppSettings> AppSettingsMonitor

<h1>@AppSettings.Title</h1>
<p>Refresh Interval: @AppSettings.RefreshInterval seconds</p>

<button @onclick="RefreshSettings">Refresh Settings</button>

@code {
    private AppSettings AppSettings;

    protected override void OnInitialized()
    {
        AppSettingsMonitor.OnChange(settings =>
        {
            AppSettings = settings;
            StateHasChanged();
        });

        AppSettings = AppSettingsMonitor.CurrentValue;
    }

    private void RefreshSettings()
    {
        Console.WriteLine("Current Title: " + AppSettings.Title);
    }
}
```

---

### **总结**
1. **动态监控能力**：
   - 使用 `IOptionsMonitor` 可以实现动态加载 `appsettings.json` 的更改，无需重启应用。
   - 通过 `OnChange` 方法订阅配置更新事件，并及时通知 UI 重新渲染。

2. **适用场景**：
   - 适用于需要实时更新的 Blazor Server 应用，例如动态调整刷新间隔或修改应用标题。

3. **优点**：
   - 避免硬编码配置。
   - 支持动态更新和热加载，提升开发和运维效率。
