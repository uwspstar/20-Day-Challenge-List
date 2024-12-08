### **`<script src="_framework/blazor.web.js"></script>` 的作用**

在 **Blazor** 应用中，`blazor.web.js` 是一个核心的 JavaScript 文件，负责在浏览器中初始化和运行 Blazor 应用。它的作用因 Blazor 的模式（**Blazor Server** 或 **Blazor WebAssembly**）而有所不同。

以下是它在 Blazor 应用中的详细作用：

---

### **1. Blazor WebAssembly 中的作用**

在 **Blazor WebAssembly** 模式下，`blazor.web.js` 是 Blazor 应用的桥梁，负责：

1. **加载 WebAssembly 模块**：
   - 下载 Blazor 应用的 .NET 运行时（WebAssembly 形式）。
   - 下载应用的 DLL 文件和依赖项。
   - 初始化 .NET WebAssembly 运行时。

2. **启动 Blazor 应用**：
   - 加载 Razor 组件并渲染到 DOM 中。
   - 解析和处理应用的组件树。
   - 监听用户事件并将事件转发到 .NET 代码中处理。

3. **JavaScript 与 .NET 互操作**：
   - 提供 **JavaScript Interop** 功能，允许 .NET 调用 JavaScript 方法，或 JavaScript 调用 .NET 方法。
   - 示例：在前端调用浏览器 API（如 `window.alert`）。

4. **资源管理**：
   - 动态加载资源（CSS、JS 文件等）。
   - 管理 Blazor 应用的状态与生命周期。

---

### **2. Blazor Server 中的作用**

在 **Blazor Server** 模式下，`blazor.web.js` 的主要作用是建立客户端和服务器之间的实时通信。具体功能包括：

1. **建立 SignalR 连接**：
   - 使用 WebSocket 或其他 SignalR 协议，与服务器保持双向通信。
   - 在服务器端执行 Razor 组件的渲染逻辑，并将结果通过 SignalR 发送给客户端。

2. **同步 UI 与事件**：
   - 负责从服务器接收 UI 更新并在客户端渲染。
   - 将用户事件（如点击、输入）发送到服务器处理。

3. **管理连接状态**：
   - 监控 SignalR 的连接状态，并在断线时尝试重新连接。
   - 提供连接失败或状态变化的通知。

4. **JavaScript 与 .NET 互操作**：
   - 与 WebAssembly 模式类似，支持 .NET 与 JavaScript 的双向调用。

---

### **Blazor WebAssembly 与 Blazor Server 中的差异**

| **功能**                  | **Blazor WebAssembly**                                        | **Blazor Server**                                          |
|---------------------------|-------------------------------------------------------------|-----------------------------------------------------------|
| **运行环境**              | 在浏览器中运行 .NET WebAssembly 运行时。                     | 在服务器上运行 Razor 组件逻辑，通过 SignalR 同步到客户端。 |
| **`blazor.web.js` 作用**  | - 加载 WebAssembly 运行时<br>- 启动 .NET 应用<br>- 提供互操作 | - 建立 SignalR 连接<br>- 同步 UI 和事件<br>- 提供互操作    |
| **网络依赖**              | 独立运行，无需持续的网络连接。                                | 需要稳定的网络连接支持实时通信。                           |
| **性能**                  | 初次加载稍慢（需下载 WebAssembly）。                          | 初次加载快，但需依赖网络进行 UI 更新。                     |

---

### **JavaScript Interop 示例**

`blazor.web.js` 提供了 JavaScript 和 .NET 互操作的能力，例如：

#### **1. .NET 调用 JavaScript**
在 .NET 中调用浏览器的 `alert` 方法：
```csharp
@inject IJSRuntime JSRuntime

<button @onclick="CallJS">调用 JS</button>

@code {
    private async Task CallJS()
    {
        await JSRuntime.InvokeVoidAsync("alert", "Hello from .NET!");
    }
}
```

#### **2. JavaScript 调用 .NET**
在 JavaScript 中调用 .NET 方法：
```csharp
// wwwroot/site.js
function callDotNet() {
    DotNet.invokeMethodAsync('YourAssemblyName', 'SayHello')
        .then(result => console.log(result));
}
```

```csharp
// Blazor 组件
@code {
    [JSInvokable]
    public static string SayHello()
    {
        return "Hello from .NET!";
    }
}
```

---

### **总结**

`<script src="_framework/blazor.web.js"></script>` 是 Blazor 应用的基础脚本文件，主要负责：

1. **初始化和运行 Blazor 应用**：
   - 在 Blazor WebAssembly 模式中加载 WebAssembly 运行时。
   - 在 Blazor Server 模式中建立 SignalR 连接。

2. **支持 JavaScript 与 .NET 的互操作**。

3. **管理应用资源和通信**。

这个脚本文件是 Blazor 应用正常运行的关键组件，不同模式下功能侧重点不同，但都为现代化 Web 应用提供了高效的运行机制和交互能力。
