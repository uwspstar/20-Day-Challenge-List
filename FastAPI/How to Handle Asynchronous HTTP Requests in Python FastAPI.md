### How to Handle Asynchronous HTTP Requests in Python FastAPI

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

Handling asynchronous HTTP requests in Python FastAPI is crucial for improving performance, especially when dealing with I/O-bound tasks such as calling external APIs. FastAPI, built on top of Starlette, fully supports asynchronous programming, allowing you to write high-performance code that handles multiple requests concurrently.

在 Python FastAPI 中处理异步 HTTP 请求对于提高性能至关重要，特别是在处理像调用外部 API 这样的 I/O 绑定任务时。FastAPI 构建于 Starlette 之上，完全支持异步编程，使你能够编写高性能代码来并发处理多个请求。

---

#### 2. Key Concepts 关键概念

**English:**
- **Asynchronous Programming 异步编程:** Involves writing code that allows other tasks to run while waiting for an operation to complete. This is achieved using `async` and `await` keywords.
- **`httpx` Library:** A powerful HTTP client for Python that supports asynchronous requests out of the box. It's commonly used with FastAPI for making external API calls.

**Chinese:**
- **异步编程:** 涉及编写代码，在等待操作完成时允许其他任务运行。使用 `async` 和 `await` 关键字实现。
- **`httpx` 库:** 一个强大的 Python HTTP 客户端，开箱即用地支持异步请求。它通常与 FastAPI 一起使用以进行外部 API 调用。

---

#### 3. Detailed Explanation 详细解释

**1. Importing the Required Libraries 导入所需库**

```python
from fastapi import FastAPI
import httpx
```

**Explanation 解释:**
- `FastAPI` is imported to create the web application.
- `httpx` is used for making asynchronous HTTP requests.

- `FastAPI` 被导入以创建 Web 应用程序。
- `httpx` 用于进行异步 HTTP 请求。

**2. Creating a FastAPI Instance 创建 FastAPI 实例**

```python
app = FastAPI()
```

**Explanation 解释:**
- The `app` variable is an instance of the FastAPI class, which will handle incoming HTTP requests.

- `app` 变量是 FastAPI 类的一个实例，它将处理传入的 HTTP 请求。

**3. Defining an Asynchronous Route 定义异步路由**

```python
@app.get("/joke")
async def get_joke():
    joke_api_url = "https://official-joke-api.appspot.com/random_joke"

    async with httpx.AsyncClient() as client:
        response = await client.get(joke_api_url)

    if response.status_code == 200:
        joke_data = response.json()
        return {"setup": joke_data['setup'], "punchline": joke_data['punchline']}
    else:
        return {"error": "Failed to fetch joke"}
```

**Explanation 解释:**
- **`@app.get("/joke")`:** Defines a GET route at `/joke`.
- **`async def get_joke()`:** Declares the function as asynchronous.
- **`async with httpx.AsyncClient() as client`:** Uses `httpx` to create an asynchronous HTTP client.
- **`await client.get(joke_api_url)`:** Sends a GET request to the external API asynchronously.
- **`response.status_code == 200`:** Checks if the response is successful and returns the joke if true.

- **`@app.get("/joke")`:** 定义 `/joke` 的 GET 路由。
- **`async def get_joke()`:** 将函数声明为异步。
- **`async with httpx.AsyncClient() as client`:** 使用 `httpx` 创建一个异步 HTTP 客户端。
- **`await client.get(joke_api_url)`:** 异步发送一个 GET 请求到外部 API。
- **`response.status_code == 200`:** 检查响应是否成功，如果是，则返回笑话。

---

#### 4. Tips and Warnings 提示与警告

**Tips 提示:**
1. **Use `async def` and `await`:** Ensure that your function is asynchronous by using `async def`, and always `await` asynchronous calls to avoid blocking the event loop.
   - 使用 `async def` 和 `await`: 确保你的函数是异步的，并且始终 `await` 异步调用，以避免阻塞事件循环。
   
2. **Context Manager for HTTP Client:** Always use `async with` when creating an `httpx.AsyncClient` to ensure the client is closed properly after the request.
   - HTTP 客户端的上下文管理器: 创建 `httpx.AsyncClient` 时始终使用 `async with`，以确保请求后正确关闭客户端。
   
**Warnings 警告:**
1. **Blocking Code:** Avoid using blocking code inside asynchronous functions as it can negate the benefits of async programming.
   - 阻塞代码: 避免在异步函数中使用阻塞代码，因为它可能会抵消异步编程的优势。

2. **Error Handling:** Always handle possible errors when making external API calls, such as network issues or unexpected response formats.
   - 错误处理: 在进行外部 API 调用时始终处理可能的错误，例如网络问题或意外的响应格式。

---

#### 5. 5Ws (Who, What, When, Where, Why) 五个W (谁、什么、什么时候、在哪里、为什么)

**Who 谁:**
- Developers working on FastAPI projects that require interaction with external services.
- 从事需要与外部服务交互的 FastAPI 项目的开发人员。

**What 什么:**
- The code shows how to handle asynchronous HTTP requests in a FastAPI application.
- 代码展示了如何在 FastAPI 应用程序中处理异步 HTTP 请求。

**When 什么时候:**
- When you need to fetch or post data to an external API in a non-blocking manner.
- 当你需要以非阻塞方式向外部 API 获取或发送数据时。

**Where 哪里:**
- This technique is used in backend services or APIs where performance and concurrency are critical.
- 该技术用于性能和并发性至关重要的后端服务或 API 中。

**Why 为什么:**
- Asynchronous requests improve application performance by allowing other tasks to run while waiting for I/O operations to complete.
- 异步请求通过允许其他任务在等待 I/O 操作完成时运行，从而提高应用程序性能。

---

#### 6. Comparison Table 比较表

| Feature | Synchronous Requests 同步请求 | Asynchronous Requests 异步请求 |
|---------|------------------------------|------------------------------|
| **Performance 性能** | Slower due to blocking 阻塞导致较慢 | Faster, non-blocking 快速，非阻塞 |
| **Concurrency 并发** | Limited 并发性有限 | High concurrency 并发性高 |
| **Complexity 复杂性** | Easier to understand 容易理解 | More complex 复杂度更高 |

---

#### 7. Recommended Resources 推荐资源

1. **FastAPI Official Documentation:**
   - Learn more about FastAPI and asynchronous programming.
   - 了解更多关于 FastAPI 和异步编程的信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/)

2. **Python `httpx` Documentation:**
   - Understand how to use `httpx` for making HTTP requests asynchronously.
   - 了解如何使用 `httpx` 进行异步 HTTP 请求。
   - [httpx Documentation](https://www.python-httpx.org/)

3. **Asyncio Library Documentation:**
   - Official Python documentation on asynchronous programming with `asyncio`.
   - 官方 Python 文档关于使用 `asyncio` 进行异步编程的指南。
   - [Asyncio Documentation](https://docs.python.org/3/library/asyncio.html)

4. **RealPython - Asyncio in Python:**
   - A comprehensive guide on asynchronous programming in Python.
   - 一份关于 Python 中异步编程的全面指南。
   - [RealPython Asyncio Guide](https://realpython.com/async-io-python/)

5. **YouTube - FastAPI Asynchronous Programming:**
   - A video tutorial on how to handle asynchronous programming in FastAPI.
   - 一个关于如何在 FastAPI 中处理异步编程的视频教程。
   - [FastAPI Async Programming](https://www.youtube.com/watch?v=tLKKmouUams)

This explanation provides a thorough understanding of how to handle asynchronous HTTP requests in FastAPI, with detailed explanations, tips, warnings, 5Ws, a comparison table, and recommended resources in both English and Chinese.
