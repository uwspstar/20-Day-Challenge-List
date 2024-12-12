### 集成 SSRS REST API 的详细步骤（新手指南)

通过 SSRS 的 REST API，可以在 Blazor 应用中动态获取报表数据，并进行灵活渲染。以下是新手友好的详细步骤，帮助你从零开始实现。

---

#### **1. 什么是 SSRS REST API？**
SSRS REST API 是 SQL Server Reporting Services 提供的一组 HTTP 接口，可以用来：
- 列出报表或资源
- 执行报表并获取结果
- 导出报表为不同的格式（PDF、HTML、Excel 等）

优点：
- 支持动态获取数据，适合现代化应用场景。
- 支持多种报表格式，灵活适配不同需求。

---

#### **2. 准备工作**

**步骤**：
1. 确保你使用的是 **SSRS 2017 或更高版本**，因为 REST API 仅在这些版本中提供。
2. 确认你的 SSRS 服务器已配置正确，并启用了 **Web 服务 URL**。
   - 打开 **Reporting Services 配置管理器**。
   - 检查 “Web 服务 URL” 是否可以通过浏览器访问。例如：`http://your-ssrs-server/reports/api/v1.0/`

3. 创建一个 SSRS 报表，发布到服务器。
   - 在 SQL Server Data Tools (SSDT) 中创建报表并部署。
   - 假设报表路径为 `/YourFolder/YourReportName.rdl`。

4. 检查你的身份验证机制：
   - 如果 SSRS 使用的是 **Windows 身份验证**，需要在代码中处理凭据。
   - 如果使用 **自定义身份验证**，需要提供 Token。

---

#### **3. 在 Blazor 应用中集成 SSRS REST API**

**步骤 1：安装 HttpClient**

Blazor 已内置 `HttpClient`，确保你已经在项目中注入了 `HttpClient`。

**步骤 2：创建一个服务类**

在 Blazor 项目中添加一个服务，用于调用 SSRS REST API。

**代码示例**：
```csharp
using System.Net.Http.Headers;

public class SSRSService
{
    private readonly HttpClient _httpClient;

    public SSRSService(HttpClient httpClient)
    {
        _httpClient = httpClient;
    }

    // 获取报表数据
    public async Task<byte[]> GetReportAsPdfAsync(string reportPath)
    {
        var baseUrl = "http://your-ssrs-server/reports/api/v1.0";
        var requestUrl = $"{baseUrl}/Reports({reportPath})/Export";

        // 设置身份验证
        _httpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Basic", Convert.ToBase64String(
                System.Text.Encoding.ASCII.GetBytes("username:password")));

        var response = await _httpClient.GetAsync(requestUrl);
        if (response.IsSuccessStatusCode)
        {
            return await response.Content.ReadAsByteArrayAsync();
        }

        throw new Exception($"获取报表失败，状态码：{response.StatusCode}");
    }
}
```

**步骤 3：注册服务**

在 `Program.cs` 中注册服务：
```csharp
builder.Services.AddScoped<SSRSService>();
```

**步骤 4：在页面中调用服务**

创建一个页面，例如 `FetchReport.razor`：
```csharp
@inject SSRSService SSRSService
@inject NavigationManager Navigation

<h3>获取报表</h3>
<button @onclick="DownloadReport">下载 PDF 报表</button>

@code {
    private async Task DownloadReport()
    {
        try
        {
            var reportPath = "/YourFolder/YourReportName";
            var pdfBytes = await SSRSService.GetReportAsPdfAsync(reportPath);

            // 将 PDF 文件提供下载
            var base64 = Convert.ToBase64String(pdfBytes);
            var blobUrl = $"data:application/pdf;base64,{base64}";
            Navigation.NavigateTo(blobUrl, forceLoad: true);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"报表下载失败：{ex.Message}");
        }
    }
}
```

---

#### **4. 核心 REST API 说明**

1. **获取报表列表**：
   - URL: `http://your-ssrs-server/reports/api/v1.0/Folders('YourFolder')/Reports`
   - 方法：GET
   - 返回：JSON 格式的报表列表

2. **导出报表**：
   - URL: `http://your-ssrs-server/reports/api/v1.0/Reports('YourReportPath')/Export`
   - 方法：GET
   - 参数：
     - `format`: 导出格式（如 `PDF`、`HTML`）

3. **报表结果示例**：
   - 如果请求 `PDF`，返回的内容是二进制文件。
   - 如果请求 `HTML`，返回的内容是 HTML 格式，适合嵌入到页面中。

---

#### **5. 使用 REST API 的注意事项**

1. **身份验证**
   - 确保你的应用有权限访问 SSRS 服务器。
   - 如果使用 Windows 身份验证，可以使用 `HttpClientHandler` 提供凭据：
     ```csharp
     var handler = new HttpClientHandler
     {
         Credentials = new NetworkCredential("username", "password", "domain")
     };
     var httpClient = new HttpClient(handler);
     ```

2. **报表路径**
   - 报表路径必须以 SSRS 部署中的路径为准，例如 `/YourFolder/YourReportName.rdl`。

3. **报表格式**
   - 确认 API 支持的格式是否符合需求。

---

#### **6. 新手易错点总结**

1. **CORS 问题**：
   - 如果直接在前端调用 SSRS API，可能会遇到 CORS 问题。建议通过后端代理解决。

2. **路径错误**：
   - 报表路径需要完整且正确，例如 `/FolderName/ReportName`。

3. **身份验证问题**：
   - 确认你的 SSRS 服务器是否启用了身份验证机制（如 Windows 身份验证或 Token）。

---

通过以上步骤，你可以成功集成 SSRS REST API，并在 Blazor 应用中展示动态报表。如果还有疑问，可以继续沟通！
