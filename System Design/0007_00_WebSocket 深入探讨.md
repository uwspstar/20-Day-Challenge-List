### WebSocket 深入探讨

在这节课中，我们将深入了解**应用层协议**，如 **HTTP**、**WebSocket**、**FTP**、**SMTP**、**SSH** 和 **WebRTC**。这些协议中的大多数使用 **TCP** 进行通信，除了 **WebRTC** 使用 **UDP**。我们已经了解了 **TCP** 和 **UDP** 之间的区别以及它们的应用场景。

### 问题背景

让我们以构建一个**聊天应用程序**为例。在这种情况下，**HTTP** 在处理无状态数据时表现良好。它遵循请求-响应协议，客户端请求页面，服务器返回页面。然而，HTTP 的这种单向通信模式无法满足实时通信的需求。客户端需要不断向服务器发送请求（轮询）以获取最新消息，这种方式会产生大量开销，尤其是在需要实时接收消息的群聊场景中。

例如，客户端每分钟向服务器请求一次消息，这在群聊中非常低效。如果客户端每分钟检查一次消息更新，用户会遇到明显的延迟。如果每秒检查一次，这将导致大量请求，增加服务器负载，浪费系统资源。

因此，虽然 **HTTP** 在某些方面有效，但在实时聊天应用中，它的轮询机制存在局限性，难以平衡效率和系统负载。

### WebSocket 作为解决方案

**WebSocket** 提供了双向通信能力，使客户端和服务器能够持续交换数据，适用于需要实时更新的场景，如**聊天应用**、**视频直播**、**实时游戏**等。

#### 建立 WebSocket 连接

WebSocket 的连接过程从 HTTP 请求开始，然后通过 HTTP 升级请求（Upgrade Request）转换为 WebSocket 连接。这个过程允许客户端和服务器进行持续的双向通信。

主要的现代浏览器（如 Chrome、Firefox、Edge）都内置了对 WebSocket 的支持，流行的服务端框架（如 Node.js、Django、ASP.NET）也支持 WebSocket。这使开发者能够轻松利用 WebSocket 的优势来实现实时的双向通信。

**WebSocket 连接步骤**：

1. **客户端发送 WebSocket 握手请求**：客户端发起一个 WebSocket 握手请求。这是一个 HTTP 升级请求，包含一些特殊的头部字段。
2. **服务器响应握手请求**：如果服务器支持 WebSocket 协议并愿意接受连接，它会返回状态码 101，表示服务器理解 Upgrade 请求并同意切换协议。
3. **数据传输**：握手完成后，客户端和服务器之间可以实时传输数据，这比不断打开和关闭 HTTP 连接高效得多。WebSocket 是真正的双向通信，客户端无需不断检查服务器的状态。

- 默认情况下，WebSocket 使用 **端口 80**，类似于 HTTP。
- WebSocket Secure (WSS) 使用 **端口 443**，类似于 HTTPS。

需要注意的是，虽然大多数设备和浏览器支持 WebSocket，但网络本身必须允许 WebSocket 连接。有些防火墙可能会阻止 WebSocket 连接。

尽管 **HTTP/2** 引入了多路复用功能，可以在单一的 TCP 连接上并行处理多个请求，但它并不能完全取代 WebSocket，因此 WebSocket 在很多实时应用中仍然非常流行。

### 用例：Twitch.com 的实时聊天

以一个实时流媒体网站（如 Twitch.com）为例，实时更新的聊天功能很可能使用 WebSocket 协议，而不是 HTTP。如果我们通过浏览器开发者工具的网络选项卡，过滤 `ws`，可以看到 WebSocket 的相关请求和响应，证明其确实使用 WebSocket 来实现实时聊天功能。

### 比较表：WebSocket vs HTTP/2 vs HTTP

| **协议**         | **传输模式**      | **连接方式**  | **性能**          | **典型用例**               | **缺点**                                 |
|------------------|-------------------|---------------|-------------------|----------------------------|------------------------------------------|
| **HTTP/1.1**     | 单向请求-响应     | 每次请求单独连接 | 传输速度较慢，无法多路复用 | 浏览静态网页、API 调用         | 每个请求都需要建立和关闭连接，开销大    |
| **HTTP/2**       | 多路复用          | 持久连接        | 性能优化，减少延迟  | 现代 Web 应用，资源密集型网站 | 需要服务器和客户端的支持                 |
| **WebSocket**    | 双向通信          | 长连接          | 实时性极高        | 聊天应用、股票行情、在线游戏 | 适用于实时应用，但处理逻辑复杂           |

### 代码示例：使用 FastAPI 实现 WebSocket

以下是一个简单的 **WebSocket** 实现，通过 WebSocket 实现实时双向通信：

```python
from fastapi import FastAPI, WebSocket

app = FastAPI()

# WebSocket 双向通信
@app.websocket("/ws/{client_id}")
async def websocket_endpoint(websocket: WebSocket, client_id: int):
    await websocket.accept()
    await websocket.send_text(f"欢迎, 客户端 {client_id}!")
    while True:
        data = await websocket.receive_text()
        await websocket.send_text(f"客户端 {client_id} 说: {data}")

# 使用 WebSocket 客户端连接 ws://localhost:8000/ws/1
```

### HTTP/2 多路复用示例（FastAPI）

FastAPI 支持 **HTTP/2**，以下是配置示例：

```python
import uvicorn
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id, "name": f"User {user_id}"}

# 使用 HTTP/2 启动服务器
if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000, http="h2")
```

### 总结

- **WebSocket** 适用于需要实时双向通信的场景，如聊天应用、在线游戏、实时流媒体等。
- **HTTP/1.1** 适合静态网页浏览和简单的请求-响应操作，但性能较低。
- **HTTP/2** 通过多路复用提升了并发处理能力，适用于现代 Web 应用和高流量场景，但不具备实时双向通信的能力。

WebSocket 在实时性要求较高的应用中表现优异，而 HTTP 和 HTTP/2 则在资源请求和响应中更为常见。
