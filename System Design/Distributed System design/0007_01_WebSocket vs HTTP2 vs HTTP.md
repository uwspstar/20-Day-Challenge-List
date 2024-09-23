### WebSocket vs HTTP/2 vs HTTP

在系统设计中，选择合适的通信协议至关重要，尤其是在设计高效的、可扩展的网络应用时。**WebSocket**、**HTTP/2** 和 **HTTP/1.1** 是三种常见的协议，每种协议都有其优缺点和适用场景。我们将对这三者进行比较，并通过实际用例、比较表和代码示例来深入理解它们的区别和使用场景。

### 1. **协议简介**

- **HTTP/1.1**: 标准的超文本传输协议，用于客户端-服务器之间的单向通信。每次请求都需要单独建立连接。
- **HTTP/2**: 是 HTTP/1.1 的改进版本，支持多路复用和二进制传输，优化了数据传输的效率和速度。
- **WebSocket**: 全双工协议，允许客户端和服务器之间建立持久的双向通信。它特别适合需要实时更新的应用，如聊天系统和在线游戏。

### 2. **实际用例**

#### **HTTP/1.1 用例**
- **Alice 访问博客页面**：Alice 使用浏览器向服务器发送 HTTP 请求，获取静态页面内容。此请求是单向的，服务器只在接收到请求后返回页面，之后连接关闭。

#### **HTTP/2 用例**
- **Bob 访问现代 Web 应用**：Bob 使用 HTTP/2 协议访问支持多路复用的电商网站。页面加载过程中，多个请求同时进行，如图片、CSS 文件、JavaScript 脚本等，提高了页面加载速度。

#### **WebSocket 用例**
- **Alice 和 Bob 使用聊天应用**：他们通过 WebSocket 建立持久连接，实现实时消息传递。服务器可以即时推送消息到客户端，客户端也能即时发送消息给服务器。

### 3. **比较表**

| **协议**         | **传输模式**  | **连接方式**  | **性能**          | **典型用例**               | **缺点**                                 |
|------------------|---------------|---------------|-------------------|----------------------------|------------------------------------------|
| **HTTP/1.1**     | 单向请求-响应 | 每次请求单独连接 | 传输速度较慢，无法多路复用 | 浏览静态网页、API 调用         | 每个请求都需要建立和关闭连接，开销大    |
| **HTTP/2**       | 多路复用      | 持久连接        | 性能优化，减少延迟  | 电商网站、图像和资源密集型网站 | 需要服务器和客户端的支持                 |
| **WebSocket**    | 双向通信      | 长连接          | 实时性极高        | 聊天应用、股票行情、在线游戏 | 适用于实时应用，但处理逻辑复杂           |

### 4. **代码示例**

#### **HTTP/1.1 示例**（FastAPI）
以下是一个使用 HTTP/1.1 进行简单 GET 请求的示例：

```python
from fastapi import FastAPI

app = FastAPI()

# 使用 HTTP/1.1 处理 GET 请求
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id, "name": f"Item {item_id}"}

# 启动后使用浏览器访问 http://localhost:8000/items/1
```

#### **HTTP/2 示例**（FastAPI）
FastAPI 支持 HTTP/2，下面的示例演示了如何配置 FastAPI 以支持 HTTP/2：

```python
import uvicorn
from fastapi import FastAPI

app = FastAPI()

# HTTP/2 的多路复用允许多个请求共享同一连接
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id, "name": f"User {user_id}"}

# 使用 HTTP/2 启动服务器
if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000, http="h2")
```

#### **WebSocket 示例**（FastAPI）
WebSocket 是用于实时双向通信的协议，以下是 WebSocket 实现的聊天应用示例：

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

### 5. **总结**
- **HTTP/1.1** 适合传统的静态网页访问和 API 请求，但性能较慢。
- **HTTP/2** 提供了显著的性能改进，适用于资源密集型的现代 Web 应用，特别是在并发请求时表现出色。
- **WebSocket** 是实时应用的最佳选择，如在线游戏、聊天应用，能够提供低延迟和高频率的消息传递。

根据系统需求的不同，选择合适的协议可以大幅提升应用的性能和用户体验。
