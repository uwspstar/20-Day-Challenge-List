# Middleware in FastAPI: Defining and Applying Custom Middleware

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Middleware is a crucial concept in web development that refers to a layer that sits between the request and response processing in a web application. In FastAPI, middleware can be used to perform operations on incoming requests or outgoing responses, such as logging, authentication, error handling, or modifying the request/response data. Custom middleware allows you to inject custom logic that executes for every request, making it a powerful tool for managing cross-cutting concerns in your application.

**Chinese:**
中间件是 Web 开发中的一个重要概念，指的是位于 Web 应用程序中的请求和响应处理之间的一个层。在 FastAPI 中，中间件可用于对传入请求或传出响应执行操作，例如日志记录、身份验证、错误处理或修改请求/响应数据。自定义中间件允许你注入自定义逻辑，这些逻辑会为每个请求执行，使其成为管理应用程序中横切关注点的强大工具。

---

#### 2. Defining a Custom Middleware 定义自定义中间件

**English:**
To define a custom middleware in FastAPI, you need to create a class that follows a specific structure. This class should implement the `__call__` method, which receives the request and calls the next middleware or route handler.

**Chinese:**
要在 FastAPI 中定义自定义中间件，你需要创建一个遵循特定结构的类。这个类应该实现 `__call__` 方法，该方法接收请求并调用下一个中间件或路由处理器。

**Example 例子:**

```python
from starlette.middleware.base import BaseHTTPMiddleware
from fastapi import FastAPI, Request

app = FastAPI()

class CustomMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        # Pre-processing logic
        print(f"Processing request: {request.url.path}")
        
        # Call the next middleware or the main route handler
        response = await call_next(request)
        
        # Post-processing logic
        print(f"Completed processing request: {request.url.path}")
        return response

app.add_middleware(CustomMiddleware)
```

**Explanation 解释:**

- **English:**
  - `BaseHTTPMiddleware`: A base class provided by Starlette (on which FastAPI is built) for creating HTTP middleware.
  - `dispatch`: The main method of the middleware where you can add pre-processing and post-processing logic. The `request` parameter represents the incoming request, and `call_next` is a function that calls the next middleware or route handler.
  - `app.add_middleware(CustomMiddleware)`: Registers the `CustomMiddleware` with the FastAPI application, so it runs for every incoming request.

- **Chinese:**
  - `BaseHTTPMiddleware`: Starlette（FastAPI 基于的框架）提供的用于创建 HTTP 中间件的基类。
  - `dispatch`: 中间件的主要方法，你可以在其中添加预处理和后处理逻辑。`request` 参数表示传入的请求，`call_next` 是一个调用下一个中间件或路由处理器的函数。
  - `app.add_middleware(CustomMiddleware)`: 将 `CustomMiddleware` 注册到 FastAPI 应用程序中，以便它为每个传入请求运行。

---

#### 3. Common Use Cases for Middleware 中间件的常见用例

**English:**
Middleware can be used for various purposes, depending on your application's needs. Here are some common use cases:

1. **Logging:**
   - Log details about incoming requests and outgoing responses, such as URLs, headers, or response times.

2. **Authentication:**
   - Implement custom authentication mechanisms that check the validity of tokens or credentials before passing requests to route handlers.

3. **Error Handling:**
   - Catch and handle errors or exceptions globally, providing a uniform error response.

4. **Performance Monitoring:**
   - Measure the time taken to process requests and generate responses, helping to identify performance bottlenecks.

**Chinese:**
中间件可以根据应用程序的需求用于各种用途。以下是一些常见的用例：

1. **日志记录:**
   - 记录有关传入请求和传出响应的详细信息，例如 URL、头信息或响应时间。

2. **身份验证:**
   - 实现自定义身份验证机制，在将请求传递给路由处理器之前检查令牌或凭据的有效性。

3. **错误处理:**
   - 全局捕获和处理错误或异常，提供统一的错误响应。

4. **性能监控:**
   - 测量处理请求和生成响应所需的时间，帮助识别性能瓶颈。

**Example of Logging Middleware 日志记录中间件示例:**

```python
class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        print(f"Request received: {request.method} {request.url}")
        response = await call_next(request)
        print(f"Response status: {response.status_code}")
        return response

app.add_middleware(LoggingMiddleware)
```

---

#### 4. Applying Middleware Conditionally 有条件地应用中间件

**English:**
Sometimes, you might want to apply middleware conditionally, for example, only for specific routes or based on certain request attributes. You can achieve this by adding conditional logic within the middleware's `dispatch` method.

**Chinese:**
有时，你可能希望有条件地应用中间件，例如，仅对特定路由或基于某些请求属性进行应用。你可以通过在中间件的 `dispatch` 方法中添加条件逻辑来实现这一点。

**Example 例子:**

```python
class ConditionalMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        if request.url.path.startswith("/admin"):
            # Apply middleware logic only for /admin routes
            print("Admin route accessed")
        response = await call_next(request)
        return response

app.add_middleware(ConditionalMiddleware)
```

**Explanation 解释:**

- **English:**
  - The middleware checks if the request URL path starts with `/admin` and only applies the middleware logic if this condition is met.

- **Chinese:**
  - 中间件检查请求 URL 路径是否以 `/admin` 开头，只有在满足此条件时才应用中间件逻辑。

---

#### 5. Middleware Ordering and Execution 顺序和执行

**English:**
The order in which middleware is added to the application matters. Middleware is executed in the order it is added, with the first middleware being the first to process the request and the last to process the response. This ordering can impact how middleware interacts, so it's important to add middleware in the correct sequence.

**Chinese:**
中间件添加到应用程序的顺序很重要。中间件按添加顺序执行，第一个中间件首先处理请求，最后一个中间件最后处理响应。这个顺序会影响中间件的交互，因此以正确的顺序添加中间件非常重要。

**Example 例子:**

```python
app.add_middleware(LoggingMiddleware)
app.add_middleware(CustomMiddleware)
```

**Explanation 解释:**

- **English:**
  - In this case, `LoggingMiddleware` will run before `CustomMiddleware` when processing the request, and `CustomMiddleware` will run first when processing the response.

- **Chinese:**
  - 在这种情况下，`LoggingMiddleware` 将在处理请求时先于 `CustomMiddleware` 运行，而在处理响应时 `CustomMiddleware` 将首先运行。

---

#### 6. Combining Middleware with Dependency Injection 将中间件与依赖注入相结合

**English:**
Middleware and dependency injection can be combined effectively in FastAPI. For instance, you can use middleware to set up global state or context that can be accessed through dependencies in your routes.

**Chinese:**
在 FastAPI 中，可以有效地将中间件与依赖注入相结合。例如，你可以使用中间件来设置全局状态或上下文，这些状态或上下文可以通过路由中的依赖项访问。

**Example 例子:**

```python
from fastapi import Request, Depends

class StateMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request: Request, call_next):
        request.state.user = "admin"
        response = await call_next(request)
        return response

def get_current_user(request: Request):
    return request.state.user

@app.get("/current-user")
async def current_user(user: str = Depends(get_current_user)):
    return {"user": user}

app.add_middleware(StateMiddleware)
```

**Explanation 解释:**

- **English:**
  - **StateMiddleware:** This middleware sets a `user` attribute in the `request.state` object, making it available globally during the request lifecycle.
  - **get_current_user:** A dependency that retrieves the `user` from the request state.
  - **current_user:** A route that uses the `get_current_user` dependency to return the current user.

- **Chinese:**
  - **StateMiddleware:** 该中间件在 `request.state` 对象中设置了 `user` 属性，使其在请求生命周期内全局可用。
  - **get_current_user:** 一个从请求状态中检索 `user` 的依赖项。
  - **current_user:** 一个使用 `get_current_user` 依赖项来返回当前用户的路由。

---

#### 7. Tips and Warnings 提示与警告

**Tips 提示:

**

1. **Keep Middleware Lightweight:**
   - Ensure your middleware is efficient and does not add unnecessary latency to your application.
   - 确保中间件高效，并且不会为你的应用程序增加不必要的延迟。

2. **Reuse Middleware:**
   - Write reusable middleware for common tasks such as logging, authentication, and error handling.
   - 为常见任务（如日志记录、身份验证和错误处理）编写可重用的中间件。

**Warnings 警告:**

1. **Avoid Side Effects:**
   - Be cautious of middleware that introduces side effects, as it can make debugging and maintenance difficult.
   - 谨慎使用引入副作用的中间件，因为这会使调试和维护变得困难。

2. **Middleware Ordering:**
   - Pay attention to the order in which you add middleware, as it can significantly affect the behavior of your application.
   - 注意添加中间件的顺序，因为它会显著影响应用程序的行为。

---

#### 8. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on using middleware in FastAPI.
   - 查看关于在 FastAPI 中使用中间件的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/middleware/)

2. **Python Context Managers:**
   - Learn about context managers in Python, which can be useful when working with middleware.
   - 了解 Python 中的上下文管理器，它们在使用中间件时很有用。
   - [Python Context Managers](https://docs.python.org/3/reference/datamodel.html#context-managers)

3. **Middleware Patterns:**
   - Review common middleware patterns and best practices for web applications.
   - 查看 Web 应用程序中常见的中间件模式和最佳实践。
   - [Middleware Patterns](https://www.django-rest-framework.org/topics/middleware/)

This explanation provides a comprehensive guide on defining and applying custom middleware in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
