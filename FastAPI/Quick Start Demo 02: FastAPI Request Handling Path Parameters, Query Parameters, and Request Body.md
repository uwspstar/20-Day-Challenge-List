# Quick Start Demo 02: FastAPI Request Handling Path Parameters, Query Parameters, and Request Body

#### 1. Introduction 简介

**English:**
FastAPI is a modern web framework that allows you to define web APIs with Python using an easy and intuitive approach. Understanding how to handle different types of request data—such as path parameters, query parameters, and request body—is crucial for building robust APIs.

**Chinese:**
FastAPI 是一个现代的 Web 框架，它允许你使用 Python 以简单直观的方式定义 Web API。理解如何处理不同类型的请求数据（如路径参数、查询参数和请求体）对于构建健壮的 API 至关重要。

---

#### 2. Path Parameters 路径参数

**English:**
Path parameters are used to capture values from the URL path and pass them to your API endpoint. These parameters are part of the URL and are typically used to identify specific resources.

**Chinese:**
路径参数用于从 URL 路径中捕获值，并将它们传递给你的 API 端点。这些参数是 URL 的一部分，通常用于标识特定资源。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```

**Explanation 解释:**

- **English:**
  - `@app.get("/items/{item_id}")`: Defines a route that includes a path parameter `item_id`.
  - `item_id: int`: The parameter is declared as an integer, meaning it will be automatically validated and converted.
  - The function returns a JSON response containing the `item_id`.

- **Chinese:**
  - `@app.get("/items/{item_id}")`: 定义一个包含路径参数 `item_id` 的路由。
  - `item_id: int`: 该参数声明为整数，这意味着它将自动验证和转换。
  - 该函数返回包含 `item_id` 的 JSON 响应。

---

#### 3. Query Parameters 查询参数

**English:**
Query parameters are passed in the URL after the `?` symbol and are typically used to filter, sort, or paginate results. They are optional and can have default values.

**Chinese:**
查询参数在 `?` 符号之后传递，并且通常用于过滤、排序或分页结果。它们是可选的，并且可以有默认值。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/")
def read_item(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

**Explanation 解释:**

- **English:**
  - `@app.get("/items/")`: Defines a route that handles GET requests.
  - `skip: int = 0, limit: int = 10`: Query parameters with default values are declared. `skip` is used for pagination offset, and `limit` defines the number of items to return.
  - The function returns a JSON response with the values of `skip` and `limit`.

- **Chinese:**
  - `@app.get("/items/")`: 定义一个处理 GET 请求的路由。
  - `skip: int = 0, limit: int = 10`: 声明了具有默认值的查询参数。`skip` 用于分页偏移，`limit` 定义返回的项目数量。
  - 该函数返回包含 `skip` 和 `limit` 值的 JSON 响应。

---

#### 4. Request Body 请求体

**English:**
Request bodies are used when you need to send data to the API in a structured format, typically as JSON. This is common in POST, PUT, or DELETE requests where you need to create or update resources.

**Chinese:**
请求体用于在需要以结构化格式（通常为 JSON）向 API 发送数据时。这在需要创建或更新资源的 POST、PUT 或 DELETE 请求中很常见。

**Example 例子:**

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.post("/items/")
def create_item(item: Item):
    return {"item_name": item.name, "item_price": item.price}
```

**Explanation 解释:**

- **English:**
  - `Item(BaseModel)`: Defines a Pydantic model that describes the structure of the request body. It includes fields `name`, `price`, and an optional `is_offer`.
  - `@app.post("/items/")`: Defines a POST route to handle requests with a JSON body.
  - `item: Item`: The function parameter `item` will automatically be populated with the data from the request body, and it will be validated against the `Item` model.
  - The function returns a JSON response with the item's `name` and `price`.

- **Chinese:**
  - `Item(BaseModel)`: 定义一个 Pydantic 模型，用于描述请求体的结构。它包括字段 `name`、`price` 和一个可选的 `is_offer`。
  - `@app.post("/items/")`: 定义一个处理带有 JSON 请求体的 POST 路由。
  - `item: Item`: 函数参数 `item` 将自动填充请求体中的数据，并根据 `Item` 模型进行验证。
  - 该函数返回包含项目 `name` 和 `price` 的 JSON 响应。

---

#### 5. Combining Path Parameters, Query Parameters, and Request Body 组合路径参数、查询参数和请求体

**English:**
You can combine path parameters, query parameters, and request bodies in a single API endpoint. FastAPI handles the validation and parsing of these components automatically.

**Chinese:**
你可以在单个 API 端点中组合路径参数、查询参数和请求体。FastAPI 会自动处理这些组件的验证和解析。

**Example 例子:**

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item, q: str = None):
    return {"item_id": item_id, "item_name": item.name, "q": q}
```

**Explanation 解释:**

- **English:**
  - `@app.put("/items/{item_id}")`: Defines a PUT route that takes a path parameter (`item_id`), a request body (`item`), and an optional query parameter (`q`).
  - The function returns a JSON response with the `item_id`, `item_name`, and the optional query parameter `q`.

- **Chinese:**
  - `@app.put("/items/{item_id}")`: 定义一个包含路径参数 (`item_id`)、请求体 (`item`) 和可选查询参数 (`q`) 的 PUT 路由。
  - 该函数返回包含 `item_id`、`item_name` 和可选查询参数 `q` 的 JSON 响应。

---

#### 6. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Leverage Pydantic Models:**
   - Use Pydantic models to define and validate request bodies, ensuring the data structure is correct and avoiding potential errors.
   - 使用 Pydantic 模型定义和验证请求体，确保数据结构正确，避免潜在错误。

2. **Default Values for Query Parameters:**
   - Provide default values for query parameters to make your API more robust and user-friendly.
   - 为查询参数提供默认值，使你的 API 更加健壮和用户友好。

**Warnings 警告:**

1. **Data Validation:**
   - Always validate the data passed through path parameters, query parameters, and request bodies to prevent security vulnerabilities and ensure data integrity.
   - 始终验证通过路径参数、查询参数和请求体传递的数据，以防止安全漏洞并确保数据完整性。

2. **Complexity Management:**
   - Avoid over-complicating your API endpoints by mixing too many different types of parameters, as this can make your code harder to maintain and understand.
   - 避免通过混合太多不同类型的参数使你的 API 端点过于复杂，因为这会使你的代码更难维护和理解。

---

#### 7. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - The official FastAPI documentation provides a comprehensive guide on request handling.
   - 官方 FastAPI 文档提供了关于请求处理的全面指南。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/)

2. **Pydantic Documentation:**
   - Learn more about Pydantic, which is used for data validation in FastAPI.
   - 了解更多关于 Pydantic 的信息，它用于 FastAPI 中的数据验证。
   - [Pydantic Documentation](https://pydantic-docs.helpmanual.io/)

3. **YouTube - FastAPI Crash Course:**
   - A video tutorial that covers the basics of FastAPI, including request handling.
   - 一个涵盖 FastAPI 基础知识的视频教程，包括请求处理。
   - [FastAPI Crash Course](https://www.youtube.com/watch?v=7t2alSnE2-I)

4. **RealPython - FastAPI

 Guide:**
   - A detailed guide on building APIs with FastAPI, including handling different types of requests.
   - 一份关于使用 FastAPI 构建 API 的详细指南，包括处理不同类型的请求。
   - [RealPython FastAPI Guide](https://realpython.com/fastapi-python-web-apis/)

This explanation covers how to handle path parameters, query parameters, and request bodies in FastAPI, with detailed examples, tips, warnings, and recommended resources in both English and Chinese.
