# Pydantic Models: Defining and Validating Request Body Data

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Pydantic is a powerful data validation and settings management library in Python, widely used with FastAPI to define and validate request body data. Pydantic models allow you to enforce data types, provide default values, and automatically validate incoming data against a predefined schema, making your APIs more robust and error-resistant.

**Chinese:**
Pydantic 是一个功能强大的 Python 数据验证和设置管理库，广泛用于 FastAPI 中以定义和验证请求体数据。Pydantic 模型允许你强制数据类型、提供默认值，并自动根据预定义的模式验证传入数据，使你的 API 更加健壮且抗错误。

---

#### 2. Defining a Basic Pydantic Model 定义基本的 Pydantic 模型

**English:**
A Pydantic model is defined as a Python class that inherits from `BaseModel`. Each attribute in the class represents a field in the request body, and you can specify its data type and default value.

**Chinese:**
Pydantic 模型定义为一个继承自 `BaseModel` 的 Python 类。类中的每个属性代表请求体中的一个字段，你可以指定它的数据类型和默认值。

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
  - `class Item(BaseModel)`: Defines a Pydantic model named `Item`.
  - `name: str`: A required string field.
  - `price: float`: A required float field.
  - `is_offer: bool = None`: An optional boolean field with a default value of `None`.
  - The `create_item` function accepts an instance of `Item` and returns a JSON response with the item's name and price.

- **Chinese:**
  - `class Item(BaseModel)`: 定义了一个名为 `Item` 的 Pydantic 模型。
  - `name: str`: 一个必需的字符串字段。
  - `price: float`: 一个必需的浮点字段。
  - `is_offer: bool = None`: 一个可选的布尔字段，默认值为 `None`。
  - `create_item` 函数接受一个 `Item` 实例，并返回包含项目名称和价格的 JSON 响应。

---

#### 3. Validation and Error Handling 验证和错误处理

**English:**
Pydantic automatically validates the incoming data based on the model definition. If the data does not match the expected types or constraints, FastAPI will return a detailed error response, including the exact field that caused the issue and a description of the problem.

**Chinese:**
Pydantic 会根据模型定义自动验证传入的数据。如果数据不符合预期的类型或约束，FastAPI 将返回详细的错误响应，包括导致问题的确切字段和问题描述。

**Example 例子:**

```python
@app.post("/items/")
def create_item(item: Item):
    return item
```

**Test Case 测试案例:**

```json
{
    "name": "FastAPI Book",
    "price": "not a float",
    "is_offer": true
}
```

**Response 响应:**

```json
{
    "detail": [
        {
            "loc": ["body", "price"],
            "msg": "value is not a valid float",
            "type": "type_error.float"
        }
    ]
}
```

**Explanation 解释:**

- **English:**
  - The input provided a string `"not a float"` for the `price` field, which is expected to be a float.
  - Pydantic catches this mismatch and returns a 422 Unprocessable Entity response, with details about the error.

- **Chinese:**
  - 输入为 `price` 字段提供了一个字符串 `"not a float"`，但期望为浮点数。
  - Pydantic 捕获了这个不匹配，并返回一个 422 Unprocessable Entity 响应，包含错误的详细信息。

---

#### 4. Advanced Validation with Pydantic 通过 Pydantic 进行高级验证

**English:**
Pydantic allows you to implement more complex validations by using custom validators and constraining the fields with built-in types like `constr`, `conint`, `confloat`, etc.

**Chinese:**
Pydantic 允许你通过使用自定义验证器和约束字段的内置类型（如 `constr`、`conint`、`confloat` 等）来实现更复杂的验证。

**Example 例子:**

```python
from pydantic import BaseModel, Field, conint, constr

class Item(BaseModel):
    name: constr(min_length=3, max_length=50)
    price: confloat(gt=0)
    quantity: conint(ge=1)

@app.post("/items/")
def create_item(item: Item):
    return item
```

**Explanation 解释:**

- **English:**
  - `name: constr(min_length=3, max_length=50)`: Restricts the `name` field to a string with a minimum length of 3 and a maximum length of 50.
  - `price: confloat(gt=0)`: Ensures the `price` field is a float greater than 0.
  - `quantity: conint(ge=1)`: Ensures the `quantity` field is an integer greater than or equal to 1.
  - These constraints will be automatically enforced by Pydantic, and any violation will result in a validation error.

- **Chinese:**
  - `name: constr(min_length=3, max_length=50)`: 将 `name` 字段限制为最小长度为 3、最大长度为 50 的字符串。
  - `price: confloat(gt=0)`: 确保 `price` 字段为大于 0 的浮点数。
  - `quantity: conint(ge=1)`: 确保 `quantity` 字段为大于或等于 1 的整数。
  - 这些约束将由 Pydantic 自动执行，任何违反都会导致验证错误。

---

#### 5. Nested Models 嵌套模型

**English:**
Pydantic models can be nested inside one another, allowing you to represent more complex data structures. This is particularly useful when dealing with JSON objects that contain other objects.

**Chinese:**
Pydantic 模型可以相互嵌套，允许你表示更复杂的数据结构。这在处理包含其他对象的 JSON 对象时特别有用。

**Example 例子:**

```python
from pydantic import BaseModel

class SubItem(BaseModel):
    name: str
    price: float

class Item(BaseModel):
    name: str
    description: str = None
    sub_items: list[SubItem] = []

@app.post("/items/")
def create_item(item: Item):
    return item
```

**Explanation 解释:**

- **English:**
  - `SubItem(BaseModel)`: Defines a nested model `SubItem` representing a sub-item with `name` and `price` fields.
  - `sub_items: list[SubItem] = []`: Defines a list of `SubItem` instances as part of the `Item` model.
  - The endpoint now accepts and validates a more complex JSON structure with nested objects.

- **Chinese:**
  - `SubItem(BaseModel)`: 定义了一个嵌套模型 `SubItem`，表示具有 `name` 和 `price` 字段的子项。
  - `sub_items: list[SubItem] = []`: 定义了一个由 `SubItem` 实例组成的列表，作为 `Item` 模型的一部分。
  - 端点现在接受并验证具有嵌套对象的更复杂的 JSON 结构。

---

#### 6. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Use Pydantic for Data Integrity:**
   - Leverage Pydantic models to ensure the integrity and validity of the data entering your API. This prevents common bugs and security vulnerabilities.
   - 利用 Pydantic 模型确保进入 API 的数据的完整性和有效性。这可以防止常见的错误和安全漏洞。

2. **Custom Validation:**
   - Implement custom validators when you need to enforce complex business rules or data constraints that go beyond basic type validation.
   - 当你需要强制执行超出基本类型验证的复杂业务规则或数据约束时，实现自定义验证器。

**Warnings 警告:**

1. **Avoid Over-Validation:**
   - Be mindful of over-complicating your models with too many constraints, as this can make maintenance more difficult and introduce unnecessary rigidity.
   - 注意不要因过多的约束而使模型过于复杂，因为这可能会使维护变得更加困难，并引入不必要的僵化性。

2. **Error Handling:**
   - Ensure that you properly handle validation errors to provide meaningful feedback to API users. FastAPI's automatic error responses are a good start, but consider customizing error messages if needed.
   - 确保你正确处理验证

错误，以便为 API 用户提供有意义的反馈。FastAPI 的自动错误响应是一个好的开始，但如果需要，考虑自定义错误消息。

---

#### 7. Recommended Resources 推荐资源

1. **Pydantic Documentation:**
   - The official Pydantic documentation offers a detailed guide to all features, including model definitions, validation, and custom validators.
   - 官方 Pydantic 文档提供了所有功能的详细指南，包括模型定义、验证和自定义验证器。
   - [Pydantic Documentation](https://pydantic-docs.helpmanual.io/)

2. **FastAPI Documentation:**
   - Explore how FastAPI integrates with Pydantic for request body validation.
   - 了解 FastAPI 如何与 Pydantic 集成以进行请求体验证。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/body/)

3. **YouTube - FastAPI and Pydantic:**
   - A video tutorial that covers the basics of using Pydantic with FastAPI.
   - 一个涵盖使用 Pydantic 和 FastAPI 基础知识的视频教程。
   - [FastAPI and Pydantic](https://www.youtube.com/watch?v=cRSZa8WZkvI)

4. **RealPython - Data Validation with Pydantic:**
   - An article that delves into data validation using Pydantic in Python.
   - 一篇深入探讨使用 Pydantic 进行数据验证的文章。
   - [RealPython - Data Validation with Pydantic](https://realpython.com/python-data-validation-pydantic/)

This explanation provides a comprehensive guide to defining and validating request body data using Pydantic models in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
