### 什么是 Webhook？

#### 场景假设：
假设我们运行一个电子商务网站，客户通过 API 网关将订单发送到订单服务，订单服务再将请求转发给支付服务以完成支付交易。支付服务与一个外部支付服务提供商（PSP）进行通信以完成交易。

#### Webhook vs Polling 两种与外部支付服务提供商（PSP）通信的方式：

```mermaid
graph LR
    subgraph Webhook
        A1[用户] -->|通过API网关| A2[订单服务]
        A2 --> A3[支付服务]
        A3 -->|调用外部支付服务| A4[外部支付处理器 PSP]
        A4 -->|完成后回调通知| A3
        A3 -->|返回结果| A1
    end
```

```mermaid
sequenceDiagram
    participant 用户 as 用户
    participant API网关 as API网关
    participant 订单服务 as 订单服务
    participant 支付服务 as 支付服务
    participant PSP as 外部支付处理器（PSP）

    %% 流程开始
    用户->>+API网关: 1. 发送订单请求
    API网关->>+订单服务: 2. 转发订单请求
    订单服务->>+支付服务: 3. 调用支付服务
    支付服务->>+PSP: 4. 调用外部支付服务

    %% PSP处理完成后回调通知
    PSP->>+支付服务: 5. 回调通知支付完成
    支付服务-->>-订单服务: 6. 更新支付状态
    订单服务-->>-API网关: 7. 返回支付结果
    API网关-->>-用户: 8. 返回支付完成通知
```

### 说明：
1. **流程编号：** 每个交互都有对应的编号，清晰描述整个 Webhook 流程。
2. **步骤解释：**
   - **步骤 1-4：** 用户通过 API 网关发起订单，订单服务和支付服务协作，最终调用外部支付服务（PSP）。
   - **步骤 5：** PSP 完成支付处理后通过回调通知支付服务。
   - **步骤 6-8：** 支付服务更新状态，并通过订单服务和 API 网关将结果返回给用户。
3. **Webhook 的优势：** 
   - 减少支付服务的资源消耗，无需频繁轮询外部支付处理器。
   - 提升效率，支持异步回调通知。

---

```mermaid
graph LR
    subgraph Polling
        B1[用户] -->|通过API网关| B2[订单服务]
        B2 --> B3[支付服务]
        B3 -->|轮询支付状态| B4[外部支付处理器 PSP]
        B4 -->|支付未完成| B3
        B4 -->|支付完成| B3
        B3 -->|返回结果| B1
    end
```

```mermaid
sequenceDiagram
    participant 用户 as 用户
    participant API网关 as API网关
    participant 订单服务 as 订单服务
    participant 支付服务 as 支付服务
    participant PSP as 外部支付处理器（PSP）

    %% 流程开始
    用户->>+API网关: 1. 发送订单请求
    API网关->>+订单服务: 2. 转发订单请求
    订单服务->>+支付服务: 3. 调用支付服务
    支付服务->>+PSP: 4. 请求支付状态

    %% PSP处理状态
    alt 支付未完成
        PSP-->>支付服务: 5. 返回支付未完成状态
        支付服务->>PSP: 6. 继续轮询支付状态
    else 支付完成
        PSP-->>支付服务: 5. 返回支付完成状态
    end

    %% 返回结果
    支付服务-->>-订单服务: 7. 更新支付状态
    订单服务-->>-API网关: 8. 返回支付结果
    API网关-->>-用户: 9. 返回支付完成通知
```

### 说明：
1. **流程编号：** 每个交互明确标注，展示轮询模式的完整流程。
2. **步骤解释：**
   - **步骤 1-4：** 用户通过 API 网关发起订单，订单服务和支付服务协作，向外部支付服务（PSP）发送支付状态查询请求。
   - **步骤 5-6：** 支付服务以轮询方式多次向 PSP 查询支付状态，直到收到支付完成的确认。
   - **步骤 7-9：** 支付服务更新状态后，通过订单服务和 API 网关将支付结果返回给用户。
3. **Polling 的劣势：**
   - 高资源消耗：支付服务需要频繁调用 PSP。
   - 时效性问题：支付结果的更新延迟可能影响用户体验。

---

### 说明：
1. **Webhook：**
   - 用户通过 API 网关发送订单请求。
   - 订单服务调用支付服务，支付服务与外部支付处理器（PSP）通信。
   - 当 PSP 完成支付处理时，会通过回调通知支付服务（如调用指定的 URL）。
   - 支付服务收到通知后返回结果给用户。

2. **Polling：**
   - 用户通过 API 网关发送订单请求。
   - 订单服务调用支付服务，支付服务通过轮询方式向 PSP 查询支付状态。
   - 每次查询都需要消耗资源，直到支付状态更新。
   - 支付完成后，支付服务返回结果给用户。

这种表示清晰展示了两种模式的主要区别，Webhook 减少了资源消耗和不必要的轮询，适合高效异步通信的场景。

---


#### 1. **短轮询（Short Polling）**

支付服务向 PSP 发送支付请求后，会不断向 PSP 询问支付状态。经过多轮询问后，PSP 最终返回支付状态。

**短轮询的缺点**：
- **资源消耗**：支付服务需要不断轮询 PSP 状态，这需要消耗大量资源。
- **安全问题**：外部服务直接与支付服务通信，可能带来安全漏洞。

---

#### 2. **Webhook**

通过使用 Webhook，我们可以向外部服务注册一个回调（Webhook）。这意味着：**当外部服务（PSP）有更新时，会在指定的 URL 回调我们的服务**。当 PSP 完成支付处理后，它将调用 HTTP 请求来更新支付状态。

**Webhook 的优势**：
- 编程范式发生了变化，支付服务不需要浪费资源轮询支付状态。
- 降低了服务的复杂性和资源使用量。

---

#### Webhook 的潜在问题：
- **PSP 不回调怎么办？**  
我们可以设置一个定时任务，例如每小时检查一次支付状态，以确保系统的状态一致性。

---

#### 为什么称为 "反向 API" 或 "推送 API"？
Webhook 经常被称为 **反向 API（Reverse API）** 或 **推送 API（Push API）**，因为它是由服务器向客户端发送 HTTP 请求。

---

#### 使用 Webhook 需要注意的 3 个关键点：
1. **设计合适的 API**  
   我们需要为外部服务调用设计一个适当的 API。
2. **设置适当的安全规则**  
   在 API 网关中设置安全规则，例如验证外部服务的来源 IP 或请求签名。
3. **注册正确的 URL**  
   确保在外部服务中正确注册回调的 URL。

---

#### 总结：
Webhook 的使用改变了传统的轮询模型，通过事件驱动的回调方式显著提高了系统的性能和效率。然而，为了保证安全性和可靠性，我们需要在设计和实现时关注以上关键点。

--- 

### 示例代码：
**Webhook 的简单实现：**

```csharp
// Webhook 接收端的实现
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/webhook")]
public class WebhookController : ControllerBase
{
    [HttpPost("payment-status")]
    public IActionResult UpdatePaymentStatus([FromBody] PaymentStatusUpdate statusUpdate)
    {
        Console.WriteLine($"Received payment update: {statusUpdate.Status}");
        // 处理状态更新逻辑
        return Ok();
    }
}

public class PaymentStatusUpdate
{
    public string PaymentId { get; set; }
    public string Status { get; set; }
}
```

**Webhook 注册示例（模拟）：**
```bash
# 模拟向 PSP 注册 Webhook 回调 URL
curl -X POST https://psp.example.com/api/webhook/register \
    -H "Content-Type: application/json" \
    -d '{
        "callbackUrl": "https://your-ecommerce-site.com/api/webhook/payment-status"
    }'
```

**定时任务（备选方案）：**
```bash
# 每小时检查未完成的支付状态
*/60 * * * * curl -X GET https://your-ecommerce-site.com/api/payment/status-check
```

---

通过 Webhook，支付服务的架构更具弹性，同时大幅减少了不必要的资源消耗。
