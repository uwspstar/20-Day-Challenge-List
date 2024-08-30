# FastAPI Response Models and Status Codes: Customizing Response Formats and Status Codes

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
In FastAPI, you can define custom response models to ensure that your API returns data in a consistent format. Additionally, you can set custom status codes for your responses to better convey the result of an operation. These features help in building clear, predictable, and well-documented APIs.

**Chinese:**
在 FastAPI 中，你可以定义自定义响应模型，以确保你的 API 以一致的格式返回数据。此外，你还可以为响应设置自定义状态码，以更好地传达操作结果。这些功能有助于构建清晰、可预测和文档齐全的 API。

---

#### 2. Defining a Response Model 定义响应模型

**English:**
A response model in FastAPI is a Pydantic model that defines the structure and data types of the response data. This ensures that the API always returns data that adheres to a specific schema, which is useful for documentation and validation.

**Chinese:**
FastAPI 中的响应模型是一个 Pydantic 模型，它定义了响应数据的结构和数据类型。这确保了 API 始终返回符合特定模式的数据，这对于文档编制和验证非常有用。

**Example 例子:**

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

class ItemResponse(BaseModel):
    name: str
    price: float

@app.post("/items/", response_model=ItemResponse)
def create_item(item: Item):
    return item
```

**Explanation 解释:**

- **English:**
  - `response_model=ItemResponse`: Specifies that the response will follow the structure of the `ItemResponse` model.
  - Even though the `Item` model includes fields like `description` and `tax`, only `name` and `price` will be returned in the response, as defined by `ItemResponse`.

- **Chinese:**
  - `response_model=ItemResponse`: 指定响应将遵循 `ItemResponse` 模型的结构。
  - 尽管 `Item` 模型包括 `description` 和 `tax` 等字段，但响应中只会返回 `name` 和 `price`，这是由 `ItemResponse` 定义的。

---

#### 3. Setting Custom Status Codes 设置自定义状态码

**English:**
FastAPI allows you to set custom status codes for your endpoints. This is useful when you want to indicate specific outcomes, such as resource creation (201), successful processing (200), or even client errors (400 series) and server errors (500 series).

**Chinese:**
FastAPI 允许你为端点设置自定义状态码。这在你想要指示特定结果时非常有用，例如资源创建 (201)、成功处理 (200)，甚至客户端错误 (400 系列) 和服务器错误 (500 系列)。

**Example 例子:**

```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: str = None
    price: float
    tax: float = None

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def create_item(item: Item):
    return item

@app.get("/items/{item_id}", status_code=status.HTTP_200_OK)
def read_item(item_id: int):
    if item_id != 1:
        raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="Item not found")
    return {"item_id": item_id, "name": "Sample Item"}
```

**Explanation 解释:**

- **English:**
  - `status_code=status.HTTP_201_CREATED`: Sets the status code to 201, indicating that a new resource was created.
  - The `read_item` function sets a 200 status code for successful retrieval. If the item is not found, it raises a 404 error with a custom message.

- **Chinese:**
  - `status_code=status.HTTP_201_CREATED`: 将状态码设置为 201，表示已创建一个新资源。
  - `read_item` 函数为成功检索设置了 200 状态码。如果未找到项目，它会抛出 404 错误并带有自定义消息。

---

#### 4. Customizing the Entire Response 自定义整个响应

**English:**
Sometimes, you might want to customize the entire response, including the headers, status code, and body. FastAPI allows you to return a `Response` or `JSONResponse` object directly, giving you full control over the response.

**Chinese:**
有时，你可能想要自定义整个响应，包括头信息、状态码和正文。FastAPI 允许你直接返回 `Response` 或 `JSONResponse` 对象，从而完全控制响应。

**Example 例子:**

```python
from fastapi import FastAPI, Response, status
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def create_item(item: Item):
    return Response(
        content=f"Item {item.name} created with price {item.price}",
        media_type="text/plain",
        status_code=status.HTTP_201_CREATED
    )
```

**Explanation 解释:**

- **English:**
  - This example returns a plain text response instead of JSON.
  - `media_type="text/plain"`: Specifies that the content type is plain text.
  - `status_code=status.HTTP_201_CREATED`: Sets the status code to 201 for resource creation.

- **Chinese:**
  - 这个例子返回纯文本响应而不是 JSON。
  - `media_type="text/plain"`: 指定内容类型为纯文本。
  - `status_code=status.HTTP_201_CREATED`: 将状态码设置为 201，表示资源创建成功。

---

#### 5. Returning JSON Responses with Custom Status Codes 返回带有自定义状态码的 JSON 响应

**English:**
If you need to return a JSON response with custom status codes, you can use the `JSONResponse` class. This is especially useful for error handling or when you want to return a more structured response.

**Chinese:**
如果你需要返回带有自定义状态码的 JSON 响应，可以使用 `JSONResponse` 类。这在错误处理或希望返回更结构化的响应时特别有用。

**Example 例子:**

```python
from fastapi import FastAPI, status
from fastapi.responses import JSONResponse
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def create_item(item: Item):
    return JSONResponse(
        content={"message": f"Item {item.name} created successfully."},
        status_code=status.HTTP_201_CREATED
    )

@app.get("/items/{item_id}")
def read_item(item_id: int):
    if item_id != 1:
        return JSONResponse(
            content={"error": "Item not found"},
            status_code=status.HTTP_404_NOT_FOUND
        )
    return JSONResponse(
        content={"item_id": item_id, "name": "Sample Item"},
        status_code=status.HTTP_200_OK
    )
```

**Explanation 解释:**

- **English:**
  - `JSONResponse`: Allows you to return a JSON response with a custom structure and status code.
  - The example demonstrates how to handle both successful and error responses using `JSONResponse`.

- **Chinese:**
  - `JSONResponse`: 允许你返回带有自定义结构和状态码的 JSON 响应。
  - 示例演示了如何使用 `JSONResponse` 处理成功和错误响应。

---

#### 6. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Use Response Models for Consistency:**
   - Define and use response models to ensure your API returns data in a consistent format across different endpoints.
   - 定义并使用响应模型，确保你的 API 在不同端点返回一致格式的数据。

2. **Custom Status Codes for Clarity:**
   - Use custom status codes to clearly communicate the result of an API operation, whether it's a success, client error, or server error.
   - 使用自定义状态码清楚地传达 API 操作的结果，无论是成功、客户端错误还是服务器错误。

**Warnings 警告:**

1. **Avoid Over-Complicating Responses:**
   - While customizing responses is powerful, avoid making them overly complex, as this can make the API harder to use and understand.
   - 虽然自定义响应很强大，但避免使它们过于复杂，因为这可能会使 API 更难使用和理解。

2. **Security Considerations:**
   - Be cautious when customizing error responses, as exposing too much information can lead to security vulnerabilities.
   - 自定义错误响应时要谨慎，因为暴露过多信息可能会导致安全漏洞。

---

#### 7. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on response models and custom status codes.
   - 查看关于响应模型和自定义状态码的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/response-model/)

2. **HTTP Status Code Documentation:**
   -

 Understand the meaning and usage of different HTTP status codes.
   - 了解不同 HTTP 状态码的含义和使用方法。
   - [HTTP Status Codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

3. **YouTube - FastAPI Response Models:**
   - A video tutorial on how to use response models and status codes in FastAPI.
   - 一个关于如何在 FastAPI 中使用响应模型和状态码的视频教程。
   - [FastAPI Response Models](https://www.youtube.com/watch?v=a5N-_fLymD4)

4. **RealPython - FastAPI Guide:**
   - A guide on building APIs with FastAPI, including response handling.
   - 一份关于使用 FastAPI 构建 API 的指南，包括响应处理。
   - [RealPython FastAPI Guide](https://realpython.com/fastapi-python-web-apis/)

This explanation provides a comprehensive guide to customizing response formats and status codes in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
