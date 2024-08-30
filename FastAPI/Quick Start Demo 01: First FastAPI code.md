# Quick Start Demo 01: First FastAPI code

- [Uvicorn](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Uvicorn%20in%20Python.md)
- [](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/How%20to%20Handle%20Asynchronous%20HTTP%20Requests%20in%20Python%20FastAPI.md)

#### 1. Introduction 简介

```python
# main.py
from fastapi import FastAPI
import httpx

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Welcome to the FastAPI Docker Demo"}

@app.get("/joke")
async def get_joke():
    # Define the URL of the external API that provides jokes
    joke_api_url = "https://official-joke-api.appspot.com/random_joke"

    # Use httpx to fetch the joke from the external API
    async with httpx.AsyncClient() as client:
        response = await client.get(joke_api_url)

    # If the response is successful, return the joke
    if response.status_code == 200:
        joke_data = response.json()
        return {"setup": joke_data['setup'], "punchline": joke_data['punchline']}
    else:
        return {"error": "Failed to fetch joke"}
```
This code is a simple FastAPI application that has two routes: one for a welcome message and another to fetch a random joke from an external API. The second route uses `httpx`, an asynchronous HTTP client, to fetch data from an external API.

这段代码是一个简单的 FastAPI 应用程序，包含两个路由：一个用于欢迎消息，另一个用于从外部 API 获取随机笑话。第二个路由使用 `httpx`，一个异步 HTTP 客户端，从外部 API 获取数据。

---

#### 2. Code Explanation 代码解释

**English:**
- `FastAPI` is imported to create a new web application.
- `httpx` is imported to handle asynchronous HTTP requests.
- `app` is an instance of the FastAPI class, which serves as the main entry point for the web application.
- The `/` route returns a simple welcome message.
- The `/joke` route fetches a random joke from an external API asynchronously.

**Chinese:**
- 导入 `FastAPI` 用于创建一个新的 Web 应用程序。
- 导入 `httpx` 以处理异步 HTTP 请求。
- `app` 是 FastAPI 类的一个实例，作为 Web 应用程序的主要入口。
- `/` 路由返回一个简单的欢迎消息。
- `/joke` 路由异步地从外部 API 获取随机笑话。

---

#### 3. Detailed Explanation 详细解释

**English:**

- **FastAPI Instance Creation (`app = FastAPI()`)**: 
  - This line creates an instance of the FastAPI class. This instance (`app`) will be used to define all the routes and configurations of your web application.
  - **Tip:** You can think of `app` as the central component of your FastAPI application, which manages incoming HTTP requests and routes them to the appropriate function.
  
- **Welcome Route (`@app.get("/")`)**:
  - This is a simple route that listens for GET requests to the root URL (`/`). When accessed, it returns a JSON response with a welcome message.
  
- **Joke Route (`@app.get("/joke")`)**:
  - This route is defined as asynchronous with `async def`. It listens for GET requests to the `/joke` endpoint.
  - **Warning:** If your function is asynchronous (`async def`), you must use `await` for asynchronous operations, like the HTTP request made with `httpx.AsyncClient()`.
  
- **HTTP Client (`async with httpx.AsyncClient() as client`)**:
  - Here, an instance of `httpx.AsyncClient()` is created to make the HTTP request asynchronously. The `async with` statement ensures that the client is properly closed after the request is completed.
  - **Tip:** `httpx.AsyncClient()` is preferable for asynchronous operations because it doesn't block the event loop, allowing other tasks to run concurrently.
  
- **Making the Request (`response = await client.get(joke_api_url)`)**:
  - This line sends an asynchronous GET request to the joke API URL. The `await` keyword is used to pause the function's execution until the response is received.
  
- **Handling the Response (`if response.status_code == 200`)**:
  - If the response is successful (`status_code == 200`), the JSON data is parsed and returned. If the request fails, an error message is returned.
  
**Chinese:**

- **FastAPI 实例创建 (`app = FastAPI()`)**：
  - 这一行创建了 FastAPI 类的一个实例。这个实例 (`app`) 将用于定义你的 Web 应用程序的所有路由和配置。
  - **提示：** 你可以将 `app` 视为 FastAPI 应用程序的中央组件，负责管理传入的 HTTP 请求并将它们路由到适当的函数。
  
- **欢迎路由 (`@app.get("/")`)**：
  - 这是一个简单的路由，监听对根 URL (`/`) 的 GET 请求。当被访问时，它返回一个包含欢迎消息的 JSON 响应。
  
- **笑话路由 (`@app.get("/joke")`)**：
  - 这个路由被定义为异步的 (`async def`)。它监听对 `/joke` 端点的 GET 请求。
  - **警告：** 如果你的函数是异步的 (`async def`)，你必须使用 `await` 进行异步操作，如使用 `httpx.AsyncClient()` 进行的 HTTP 请求。
  
- **HTTP 客户端 (`async with httpx.AsyncClient() as client`)**：
  - 这里创建了一个 `httpx.AsyncClient()` 实例，以异步方式进行 HTTP 请求。`async with` 语句确保请求完成后，客户端被正确关闭。
  - **提示：** `httpx.AsyncClient()` 适用于异步操作，因为它不会阻塞事件循环，从而允许其他任务并发运行。
  
- **发送请求 (`response = await client.get(joke_api_url)`)**：
  - 这一行向笑话 API URL 发送异步 GET 请求。`await` 关键字用于暂停函数执行，直到收到响应。
  
- **处理响应 (`if response.status_code == 200`)**：
  - 如果响应成功 (`status_code == 200`)，则解析 JSON 数据并返回。如果请求失败，则返回错误消息。

---

#### 4. 5Ws (Who, What, When, Where, Why) 五个W (谁、什么、什么时候、在哪里、为什么)

**Who 谁:**
- Developers who need to create a FastAPI web application that interacts with external APIs.
- 需要创建与外部 API 交互的 FastAPI Web 应用程序的开发人员。

**What 什么:**
- The code demonstrates how to use FastAPI and `httpx` to create routes and make asynchronous HTTP requests.
- 该代码演示了如何使用 FastAPI 和 `httpx` 创建路由并进行异步 HTTP 请求。

**When 什么时候:**
- Use this approach when you need to fetch data from an external service in your FastAPI application.
- 当你需要在 FastAPI 应用程序中从外部服务获取数据时使用这种方法。

**Where 哪里:**
- This code is typically used in backend applications that need to interface with third-party APIs.
- 该代码通常用于需要与第三方 API 接口的后端应用程序中。

**Why 为什么:**
- Using asynchronous operations with FastAPI allows handling multiple requests concurrently, improving performance.
- 在 FastAPI 中使用异步操作可以并发处理多个请求，从而提高性能。

---

#### 5. Comparison Table 比较表

| Feature | Synchronous Request 同步请求 | Asynchronous Request 异步请求 |
|---------|-----------------------------|-----------------------------|
| **Performance 性能** | Blocks the event loop, limiting concurrency 阻塞事件循环，限制并发 | Does not block the event loop, allows concurrency 不阻塞事件循环，允许并发 |
| **Use Case 使用场景** | Suitable for single tasks 适合单一任务 | Suitable for I/O-bound tasks 适合 I/O 绑定任务 |
| **Complexity 复杂性** | Easier to implement 实现较容易 | Slightly more complex 稍微复杂一些 |

---

#### 6. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Official FastAPI documentation provides in-depth knowledge of how to use FastAPI effectively.
   - 官方 FastAPI 文档提供了如何有效使用 FastAPI 的深入知识。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/)

2. **httpx Documentation:**
   - Learn more about how to perform HTTP requests asynchronously with `httpx`.
   - 了解更多关于如何使用 `httpx` 进行异步 HTTP 请求的信息。
   - [httpx Documentation](https://www.python-httpx.org/)

3. **Asynchronous Programming in Python:**
   - A guide to understanding asynchronous programming concepts in Python.
   - 理解 Python 中异步编程概念的指南。
   - [Asyncio Documentation](https://docs.python.org/3/library/asyncio.html)

4. **FastAPI Crash Course:**
   - A YouTube tutorial that covers the basics of FastAPI, ideal for beginners.
   - 一份涵盖 FastAPI 基础知识的 YouTube 教程，非常适合初学者。
   - [FastAPI Crash Course](https://www.youtube.com/watch?v=7t2alSnE2-I)

5. **RealPython - Asynchronous HTTP Requests in Python with `httpx`:**
   - An article that explains how to use `httpx` for asynchronous HTTP requests.
   - 一篇解释如何使用 `httpx` 进行异步 HTTP 请求的文章。
   - [RealPython Article](https://realpython.com/python-httpx/)

This explanation provides a comprehensive understanding of the code, enriched with tips, warnings, 5Ws, and a comparison table in both English and Chinese.
