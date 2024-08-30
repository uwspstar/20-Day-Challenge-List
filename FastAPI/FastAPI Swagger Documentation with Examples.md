### FastAPI Swagger Documentation with Examples

#### 1. Introduction 简介

**English:**
FastAPI automatically generates interactive API documentation using Swagger UI. This documentation allows developers to interact with the API directly from the browser, making it easy to understand and test different endpoints. Swagger UI is accessible by default at `/docs` when running a FastAPI application. 

**Chinese:**
FastAPI 自动生成交互式 API 文档，使用 Swagger UI。这些文档允许开发人员直接从浏览器与 API 交互，便于理解和测试不同的端点。Swagger UI 在运行 FastAPI 应用程序时，默认可以通过 `/docs` 访问。

---

#### 2. Basic Example of Swagger Documentation Swagger 文档的基本示例

**English:**
When you define your FastAPI routes, Swagger documentation is automatically created. For example, a simple FastAPI application with a single endpoint will automatically generate a Swagger UI interface.

**Chinese:**
当你定义 FastAPI 路由时，会自动创建 Swagger 文档。例如，一个带有单一端点的简单 FastAPI 应用程序会自动生成一个 Swagger UI 界面。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

**Explanation 解释:**

- **English:**
  - This simple API has one endpoint `/items/{item_id}` that accepts a path parameter `item_id` and an optional query parameter `q`.
  - When you run this FastAPI app, Swagger documentation will be available at `http://127.0.0.1:8000/docs`.

- **Chinese:**
  - 这个简单的 API 有一个端点 `/items/{item_id}`，接受一个路径参数 `item_id` 和一个可选的查询参数 `q`。
  - 当你运行这个 FastAPI 应用程序时，Swagger 文档可以通过 `http://127.0.0.1:8000/docs` 访问。

---

#### 3. Adding Descriptions and Metadata 添加描述和元数据

**English:**
You can enhance your Swagger documentation by adding descriptions, summaries, and other metadata to your endpoints. This makes the API documentation more informative and user-friendly.

**Chinese:**
你可以通过添加描述、摘要和其他元数据来增强 Swagger 文档的内容。这样可以使 API 文档更加丰富且易于使用。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}", summary="Get an item", description="Retrieve an item by its ID and optionally filter with a query string.")
def read_item(item_id: int, q: str = None):
    """
    - **item_id**: The ID of the item to retrieve.
    - **q**: An optional query string to filter the item.
    """
    return {"item_id": item_id, "q": q}
```

**Explanation 解释:**

- **English:**
  - `summary="Get an item"`: Provides a brief summary of what the endpoint does.
  - `description="Retrieve an item by its ID..."`: Offers a more detailed explanation of the endpoint's functionality.
  - The documentation for this endpoint will now include these descriptions, making it easier for users to understand what the endpoint does.

- **Chinese:**
  - `summary="Get an item"`: 提供端点功能的简短摘要。
  - `description="Retrieve an item by its ID..."`: 提供关于端点功能的更详细的解释。
  - 这个端点的文档现在将包括这些描述，使用户更容易理解端点的作用。

---

#### 4. Adding Example Responses and Request Bodies 添加示例响应和请求体

**English:**
You can further enhance your Swagger documentation by including example request bodies and responses. This helps users understand the expected input and output for each endpoint.

**Chinese:**
你可以通过包含示例请求体和响应进一步增强 Swagger 文档的内容。这有助于用户理解每个端点的预期输入和输出。

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

@app.post("/items/", response_model=Item, summary="Create an item", description="Create an item with the given details.")
def create_item(item: Item):
    """
    Create an item with the following properties:

    - **name**: The name of the item.
    - **description**: A short description of the item.
    - **price**: The price of the item.
    - **tax**: Optional tax for the item.
    """
    return item
```

**Explanation 解释:**

- **English:**
  - `response_model=Item`: Specifies that the response will follow the structure of the `Item` model.
  - The `summary` and `description` fields provide metadata about the endpoint.
  - The Pydantic model `Item` is used to define the expected structure of both the request body and the response.
  - Swagger will now display this model in the documentation, helping users understand what data is expected and what will be returned.

- **Chinese:**
  - `response_model=Item`: 指定响应将遵循 `Item` 模型的结构。
  - `summary` 和 `description` 字段提供了有关端点的元数据。
  - Pydantic 模型 `Item` 用于定义请求体和响应的预期结构。
  - Swagger 现在会在文档中显示这个模型，帮助用户理解预期的数据结构和返回内容。

---

#### 5. Adding Example Values to Swagger Documentation 向 Swagger 文档添加示例值

**English:**
You can specify example values for request bodies and responses, which will be shown in the Swagger UI. This is useful for providing clear examples of how to use your API.

**Chinese:**
你可以为请求体和响应指定示例值，这些值将显示在 Swagger UI 中。这对于提供清晰的 API 使用示例非常有用。

**Example 例子:**

```python
from fastapi import FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Item(BaseModel):
    name: str = Field(..., example="FastAPI Book")
    description: str = Field(None, example="A comprehensive guide to FastAPI.")
    price: float = Field(..., example=49.99)
    tax: float = Field(None, example=5.0)

@app.post("/items/", response_model=Item, summary="Create an item with example values", description="Create an item using example values provided in the documentation.")
def create_item(item: Item):
    return item
```

**Explanation 解释:**

- **English:**
  - `example="FastAPI Book"`: Specifies an example value for each field in the `Item` model.
  - When users view this endpoint in Swagger UI, they will see the example values pre-populated, making it easier to understand how to structure the request.

- **Chinese:**
  - `example="FastAPI Book"`: 为 `Item` 模型中的每个字段指定一个示例值。
  - 当用户在 Swagger UI 中查看这个端点时，他们将看到预填充的示例值，使他们更容易理解请求的结构。

---

#### 6. Customizing Swagger UI 自定义 Swagger UI

**English:**
FastAPI allows you to customize the appearance and behavior of Swagger UI. You can change the title, description, and version of your API documentation, as well as enable or disable specific features.

**Chinese:**
FastAPI 允许你自定义 Swagger UI 的外观和行为。你可以更改 API 文档的标题、描述和版本，以及启用或禁用特定功能。

**Example 例子:**

```python
from fastapi import FastAPI

app = FastAPI(
    title="My FastAPI Application",
    description="This is a sample FastAPI application with customized Swagger UI.",
    version="1.0.0",
    docs_url="/my-docs",
    redoc_url="/my-redoc"
)

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

**Explanation 解释:**

- **English:**
  - `title`, `description`, and `version`: Customize the metadata displayed in the Swagger UI.
  - `docs_url="/my-docs"`: Changes the URL where Swagger UI is available.
  - `redoc_url="/my-redoc"`: Changes the URL where ReDoc (an alternative documentation UI) is available.

- **Chinese:**
  - `title`, `description`, 和 `version`: 自定义显示在 Swagger UI 中的元数据。
  - `docs_url="/my-docs"`: 更改 Swagger UI 可访问的 URL。
  - `redoc_url="/my-redoc"`: 更改 ReDoc（一个替代的文档 UI）可访问的 URL。

---

#### 7. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Use Examples Wisely:**
   - Providing clear and relevant examples in Swagger UI helps users understand how to interact with your API effectively.
   - 在 Swagger UI 中提供清晰且相关的示

例，有助于用户有效地与 API 交互。

2. **Customize for Clarity:**
   - Customize Swagger UI metadata to make your API documentation more user-friendly and tailored to your audience.
   - 自定义 Swagger UI 元数据，使你的 API 文档更加用户友好，并适应你的受众。

**Warnings 警告:**

1. **Security Considerations:**
   - Be cautious about exposing too much information in your API documentation, especially in production environments. Ensure sensitive data and endpoints are protected.
   - 注意不要在 API 文档中暴露过多信息，特别是在生产环境中。确保敏感数据和端点受到保护。

2. **Versioning:**
   - Keep your API documentation versioned, especially if you plan to make changes over time. This helps users know which version of the API they are interacting with.
   - 使你的 API 文档具备版本控制，特别是如果你计划随时间进行更改时。这有助于用户了解他们正在使用的 API 版本。

---

#### 8. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on customizing Swagger UI and using examples.
   - 查看有关自定义 Swagger UI 和使用示例的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/)

2. **Swagger UI Documentation:**
   - Learn more about Swagger UI and how to leverage its features.
   - 了解更多关于 Swagger UI 的信息，以及如何利用其功能。
   - [Swagger UI Documentation](https://swagger.io/tools/swagger-ui/)

3. **Pydantic Documentation:**
   - Dive deeper into Pydantic for defining models and using example values.
   - 深入了解 Pydantic 以定义模型和使用示例值。
   - [Pydantic Documentation](https://pydantic-docs.helpmanual.io/)

4. **YouTube - FastAPI with Swagger UI:**
   - A video guide on using Swagger UI with FastAPI.
   - 一个关于使用 Swagger UI 和 FastAPI 的视频指南。
   - [FastAPI with Swagger UI](https://www.youtube.com/watch?v=4DTV1dLzgtw)

This explanation provides a comprehensive understanding of how to use and customize Swagger documentation in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
