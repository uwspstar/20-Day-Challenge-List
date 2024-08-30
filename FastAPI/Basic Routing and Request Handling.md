# FastAPI: Basic Routing and Request Handling

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
FastAPI is designed to make building APIs simple and efficient. One of the core components of FastAPI is its routing system, which allows you to define how different URLs in your application should respond to client requests. Understanding how to define basic routes and handle requests is fundamental to working with FastAPI.

**Chinese:**
FastAPI 旨在使构建 API 变得简单而高效。FastAPI 的核心组件之一是其路由系统，它允许你定义应用程序中的不同 URL 如何响应客户端请求。理解如何定义基本路由和处理请求是使用 FastAPI 的基础。

---

#### 2. Defining Basic Routes 定义基本路由

**English:**
In FastAPI, a route is defined using Python decorators. A route specifies a URL path and associates it with a Python function that handles requests to that path. The most common HTTP methods you will work with are `GET`, `POST`, `PUT`, and `DELETE`.

**Chinese:**
在 FastAPI 中，路由是使用 Python 装饰器定义的。路由指定一个 URL 路径，并将其与一个处理该路径请求的 Python 函数关联起来。你将使用的最常见的 HTTP 方法是 `GET`、`POST`、`PUT` 和 `DELETE`。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Welcome to FastAPI!"}

@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}

@app.post("/items/")
def create_item(name: str, price: float):
    return {"name": name, "price": price}
```

**Explanation 解释:**

- **English:**
  - `@app.get("/")`: Defines a `GET` route at the root URL (`/`). When a client sends a `GET` request to the root URL, the `read_root` function is executed, returning a welcome message.
  - `@app.get("/items/{item_id}")`: Defines a `GET` route with a path parameter `item_id`. The `read_item` function handles requests to URLs like `/items/1`, returning the `item_id`.
  - `@app.post("/items/")`: Defines a `POST` route to create a new item. The `create_item` function accepts `name` and `price` as parameters and returns a JSON object with these values.

- **Chinese:**
  - `@app.get("/")`: 定义根 URL (`/`) 的 `GET` 路由。当客户端发送 `GET` 请求到根 URL 时，`read_root` 函数被执行，返回一条欢迎消息。
  - `@app.get("/items/{item_id}")`: 定义一个带有路径参数 `item_id` 的 `GET` 路由。`read_item` 函数处理类似于 `/items/1` 这样的 URL 请求，返回 `item_id`。
  - `@app.post("/items/")`: 定义一个 `POST` 路由以创建新项目。`create_item` 函数接受 `name` 和 `price` 作为参数，并返回一个包含这些值的 JSON 对象。

---

#### 3. Handling Query Parameters 处理查询参数

**English:**
Query parameters are optional parameters that are added to the URL to filter or modify the request. In FastAPI, you can define query parameters by adding them as function arguments with default values.

**Chinese:**
查询参数是可选参数，它们添加到 URL 以过滤或修改请求。在 FastAPI 中，你可以通过将查询参数作为具有默认值的函数参数来定义它们。

**Example 例子:**

```python
@app.get("/items/")
def read_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

**Explanation 解释:**

- **English:**
  - `skip: int = 0, limit: int = 10`: Defines two optional query parameters, `skip` and `limit`, with default values. If the client sends a request to `/items/?skip=5&limit=20`, these values will be passed to the `read_items` function.
  - The function returns a JSON object containing the `skip` and `limit` values.

- **Chinese:**
  - `skip: int = 0, limit: int = 10`: 定义两个可选查询参数 `skip` 和 `limit`，并带有默认值。如果客户端发送请求到 `/items/?skip=5&limit=20`，这些值将传递给 `read_items` 函数。
  - 该函数返回一个包含 `skip` 和 `limit` 值的 JSON 对象。

---

#### 4. Handling Request Body 处理请求体

**English:**
Request bodies are typically used in `POST`, `PUT`, or `PATCH` requests where you need to send data to the server. In FastAPI, you define the structure of the request body using Pydantic models.

**Chinese:**
请求体通常用于 `POST`、`PUT` 或 `PATCH` 请求中，你需要将数据发送到服务器。在 FastAPI 中，你可以使用 Pydantic 模型定义请求体的结构。

**Example 例子:**

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.post("/items/")
def create_item(item: Item):
    return item
```

**Explanation 解释:**

- **English:**
  - `Item(BaseModel)`: Defines a Pydantic model named `Item` with three fields: `name`, `price`, and an optional `is_offer`.
  - `create_item(item: Item)`: The `item` parameter automatically receives the data from the request body, validates it against the `Item` model, and returns the validated data.

- **Chinese:**
  - `Item(BaseModel)`: 定义一个名为 `Item` 的 Pydantic 模型，包含三个字段：`name`、`price` 和一个可选的 `is_offer`。
  - `create_item(item: Item)`: `item` 参数会自动接收来自请求体的数据，并根据 `Item` 模型进行验证，返回验证后的数据。

---

#### 5. Handling Path Parameters 处理路径参数

**English:**
Path parameters are used to capture specific parts of the URL path, allowing your endpoints to handle dynamic content based on the URL structure.

**Chinese:**
路径参数用于捕获 URL 路径的特定部分，使你的端点能够根据 URL 结构处理动态内容。

**Example 例子:**

```python
@app.get("/users/{user_id}/items/{item_id}")
def read_user_item(user_id: int, item_id: int):
    return {"user_id": user_id, "item_id": item_id}
```

**Explanation 解释:**

- **English:**
  - The `read_user_item` function handles requests to URLs like `/users/1/items/5`, where `user_id` and `item_id` are extracted from the path and passed as function arguments.
  - FastAPI automatically converts the path parameters to the specified types (`int` in this case) and includes them in the response.

- **Chinese:**
  - `read_user_item` 函数处理类似于 `/users/1/items/5` 这样的 URL 请求，其中 `user_id` 和 `item_id` 从路径中提取并作为函数参数传递。
  - FastAPI 会自动将路径参数转换为指定类型（在此示例中为 `int`），并将它们包含在响应中。

---

#### 6. Handling Form Data 处理表单数据

**English:**
FastAPI also supports form data, which is typically used in web forms. You can handle form data using the `Form` class.

**Chinese:**
FastAPI 还支持表单数据，表单数据通常用于网页表单中。你可以使用 `Form` 类来处理表单数据。

**Example 例子:**

```python
from fastapi import Form

@app.post("/login/")
def login(username: str = Form(...), password: str = Form(...)):
    return {"username": username}
```

**Explanation 解释:**

- **English:**
  - `username: str = Form(...)` and `password: str = Form(...)`: Defines two required form fields, `username` and `password`.
  - The `login` function handles the form submission and returns the `username`.

- **Chinese:**
  - `username: str = Form(...)` 和 `password: str = Form(...)`: 定义两个必需的表单字段 `username` 和 `password`。
  - `login` 函数处理表单提交并返回 `username`。

---

#### 7. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Use Path Parameters for Resource Identification:**
   - Use path parameters to identify resources in your application, such as `user_id`, `item_id`, etc.
   - 使用路径参数来标识应用程序中的资源，例如 `user_id`、`item_id` 等。

2. **Leverage Query Parameters for Filtering and Pagination:**
   - Use query parameters for filtering results, pagination, or sorting, which allows for more flexible and dynamic endpoints.
   - 使用查询参数进行结果过滤、分页

或排序，这使得端点更加灵活和动态。

**Warnings 警告:**

1. **Ensure Data Validation:**
   - Always validate incoming data, especially when dealing with form data, query parameters, and request bodies, to prevent security issues and data corruption.
   - 始终验证传入数据，尤其是在处理表单数据、查询参数和请求体时，以防止安全问题和数据损坏。

2. **Avoid Overloading Endpoints:**
   - Keep endpoints focused and avoid overloading them with too many responsibilities. This improves maintainability and readability.
   - 让端点专注于一个职责，避免给它们增加太多责任。这可以提高可维护性和可读性。

---

#### 8. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on routing and request handling.
   - 查看关于路由和请求处理的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/)

2. **HTTP Methods and Status Codes:**
   - Learn more about HTTP methods like GET, POST, PUT, DELETE, and their associated status codes.
   - 了解更多关于 GET、POST、PUT、DELETE 等 HTTP 方法及其相关状态码的信息。
   - [HTTP Methods Documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

3. **YouTube - FastAPI Basics:**
   - A video tutorial that covers the basics of routing and request handling in FastAPI.
   - 一个涵盖 FastAPI 中路由和请求处理基础的视频教程。
   - [FastAPI Basics](https://www.youtube.com/watch?v=DNJSI__oNO4)

4. **RealPython - FastAPI Guide:**
   - A guide on building APIs with FastAPI, including routing and request handling.
   - 一份关于使用 FastAPI 构建 API 的指南，包括路由和请求处理。
   - [RealPython FastAPI Guide](https://realpython.com/fastapi-python-web-apis/)

This explanation provides a comprehensive guide to basic routing and request handling in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
