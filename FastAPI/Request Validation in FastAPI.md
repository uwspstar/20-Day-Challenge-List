### Request Validation in FastAPI: Using Dependency Injection for Validation

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Request validation is a critical aspect of API development, ensuring that incoming data meets the expected criteria before processing it further. FastAPI allows you to perform request validation using dependency injection, which keeps your code modular, reusable, and clean. This approach is particularly powerful when you need to apply complex validation logic across multiple endpoints.

**Chinese:**
请求验证是 API 开发中的关键环节，它确保传入的数据在进一步处理之前符合预期标准。FastAPI 允许你使用依赖注入进行请求验证，这样可以保持代码模块化、可重用和清晰。对于需要在多个端点上应用复杂验证逻辑的情况，这种方法尤其强大。

---

#### 2. Basic Validation Using Dependency Injection 使用依赖注入进行基本验证

**English:**
You can use dependency injection to validate request parameters or body data. A common use case is to validate query parameters or path parameters before processing the request.

**Chinese:**
你可以使用依赖注入来验证请求参数或请求体数据。一个常见的用例是在处理请求之前验证查询参数或路径参数。

**Example 例子:**

```python
from fastapi import FastAPI, Depends, HTTPException

app = FastAPI()

def validate_query(limit: int = 10, offset: int = 0):
    if limit > 100:
        raise HTTPException(status_code=400, detail="Limit must be 100 or less")
    if offset < 0:
        raise HTTPException(status_code=400, detail="Offset must be 0 or greater")
    return {"limit": limit, "offset": offset}

@app.get("/items/")
def read_items(params: dict = Depends(validate_query)):
    return {"params": params}
```

**Explanation 解释:**

- **English:**
  - `validate_query`: This function validates the `limit` and `offset` query parameters. If the `limit` exceeds 100 or the `offset` is negative, it raises an `HTTPException` with a 400 status code.
  - `Depends(validate_query)`: Injects the `validate_query` function as a dependency in the `read_items` route, ensuring that the parameters are validated before processing the request.

- **Chinese:**
  - `validate_query`: 此函数验证 `limit` 和 `offset` 查询参数。如果 `limit` 超过 100 或 `offset` 为负数，它会抛出带有 400 状态码的 `HTTPException`。
  - `Depends(validate_query)`: 将 `validate_query` 函数作为依赖项注入到 `read_items` 路由中，确保在处理请求之前对参数进行验证。

---

#### 3. Validating Request Body Data 验证请求体数据

**English:**
You can also use dependency injection to validate data in the request body. This is particularly useful for complex validations that go beyond basic Pydantic model validation.

**Chinese:**
你还可以使用依赖注入来验证请求体中的数据。这对于超出基本 Pydantic 模型验证的复杂验证特别有用。

**Example 例子:**

```python
from pydantic import BaseModel, Field

class Item(BaseModel):
    name: str = Field(..., min_length=3)
    price: float
    quantity: int

def validate_item(item: Item):
    if item.price <= 0:
        raise HTTPException(status_code=400, detail="Price must be greater than 0")
    if item.quantity <= 0:
        raise HTTPException(status_code=400, detail="Quantity must be greater than 0")
    return item

@app.post("/items/")
def create_item(item: Item = Depends(validate_item)):
    return {"item": item}
```

**Explanation 解释:**

- **English:**
  - `Item(BaseModel)`: A Pydantic model that defines the structure of the request body. It includes basic validation like `min_length=3` for the `name` field.
  - `validate_item`: A function that performs additional validation on the `Item` model. It checks that the `price` and `quantity` are greater than 0, raising an `HTTPException` if they are not.
  - `Depends(validate_item)`: Injects the `validate_item` function as a dependency, ensuring that the item data is validated before the `create_item` route processes it.

- **Chinese:**
  - `Item(BaseModel)`: 一个 Pydantic 模型，定义了请求体的结构。它包括基本验证，例如 `name` 字段的 `min_length=3`。
  - `validate_item`: 一个对 `Item` 模型执行额外验证的函数。它检查 `price` 和 `quantity` 是否大于 0，如果不是，则抛出 `HTTPException`。
  - `Depends(validate_item)`: 将 `validate_item` 函数作为依赖项注入，确保在 `create_item` 路由处理数据之前对项目数据进行验证。

---

#### 4. Complex Validation Scenarios 复杂的验证场景

**English:**
In more complex scenarios, you may need to perform validation that involves multiple fields or external dependencies, such as checking data against a database.

**Chinese:**
在更复杂的场景中，你可能需要执行涉及多个字段或外部依赖项的验证，例如将数据与数据库进行比对。

**Example 例子:**

```python
def validate_item_with_db(item: Item, db = Depends(get_db)):
    if db.check_item_exists(item.name):
        raise HTTPException(status_code=400, detail="Item already exists")
    if item.price <= 0 or item.quantity <= 0:
        raise HTTPException(status_code=400, detail="Price and quantity must be greater than 0")
    return item

@app.post("/items/")
def create_item(item: Item = Depends(validate_item_with_db)):
    return {"item": item}
```

**Explanation 解释:**

- **English:**
  - `get_db`: A hypothetical dependency that provides access to the database.
  - `validate_item_with_db`: This function validates the item by checking if it already exists in the database. It also checks the price and quantity, similar to the previous example.
  - `Depends(validate_item_with_db)`: Injects the validation function into the `create_item` route, ensuring that the item passes both database checks and value constraints before being created.

- **Chinese:**
  - `get_db`: 一个假设的依赖项，提供对数据库的访问。
  - `validate_item_with_db`: 这个函数通过检查项目是否已存在于数据库中来验证项目。它还检查价格和数量，类似于前面的例子。
  - `Depends(validate_item_with_db)`: 将验证函数注入到 `create_item` 路由中，确保项目在创建之前通过数据库检查和数值约束。

---

#### 5. Combining Multiple Dependencies 组合多个依赖项

**English:**
You can combine multiple dependencies in a single route to perform a series of validations. This is useful when you need to validate different aspects of a request independently.

**Chinese:**
你可以在一个路由中组合多个依赖项来执行一系列验证。当你需要独立验证请求的不同方面时，这非常有用。

**Example 例子:**

```python
def validate_quantity(quantity: int):
    if quantity <= 0:
        raise HTTPException(status_code=400, detail="Quantity must be greater than 0")
    return quantity

def validate_price(price: float):
    if price <= 0:
        raise HTTPException(status_code=400, detail="Price must be greater than 0")
    return price

@app.post("/items/")
def create_item(name: str, quantity: int = Depends(validate_quantity), price: float = Depends(validate_price)):
    return {"name": name, "quantity": quantity, "price": price}
```

**Explanation 解释:**

- **English:**
  - `validate_quantity`: A dependency that validates the `quantity` parameter.
  - `validate_price`: A dependency that validates the `price` parameter.
  - The `create_item` route combines these dependencies to ensure that both the quantity and price are valid before creating the item.

- **Chinese:**
  - `validate_quantity`: 一个验证 `quantity` 参数的依赖项。
  - `validate_price`: 一个验证 `price` 参数的依赖项。
  - `create_item` 路由组合了这些依赖项，以确保在创建项目之前数量和价格都是有效的。

---

#### 6. Handling Optional Dependencies 处理可选的依赖项

**English:**
In some cases, you may have optional dependencies where the validation logic should only be applied if certain conditions are met, such as if a particular query parameter is provided.

**Chinese:**
在某些情况下，你可能有可选的依赖项，其中只有在满足某些条件（例如提供特定查询参数）时才应应用验证逻辑。

**Example 例子:**

```python
def optional_validation(token: str = None):
    if token and token != "secret-token":
        raise HTTPException(status_code=400, detail="Invalid token")
    return token

@app.get("/items/")
def read_items(token: str = Depends(optional_validation)):
    return {"token": token}
```

**Explanation 解释:**

- **English:**
  - `optional_validation`: A dependency that checks if a token is provided. If the token is present but invalid, it raises an error. If no token is provided, the validation is

 skipped.
  - `Depends(optional_validation)`: Injects the optional validation dependency into the `read_items` route.

- **Chinese:**
  - `optional_validation`: 一个检查是否提供了令牌的依赖项。如果提供了令牌但无效，则会抛出错误。如果未提供令牌，则跳过验证。
  - `Depends(optional_validation)`: 将可选的验证依赖项注入到 `read_items` 路由中。

---

#### 7. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Reuse Validation Logic:**
   - Create reusable validation functions to keep your code DRY (Don't Repeat Yourself) and maintainable.
   - 创建可重用的验证函数，以保持代码的 DRY（Don't Repeat Yourself）原则和可维护性。

2. **Modularize Complex Validation:**
   - Break down complex validation logic into smaller, manageable dependencies to simplify testing and maintenance.
   - 将复杂的验证逻辑拆分为更小、易于管理的依赖项，以简化测试和维护。

**Warnings 警告:**

1. **Error Handling:**
   - Ensure that your validation functions raise appropriate exceptions, such as `HTTPException`, to provide meaningful feedback to API users.
   - 确保你的验证函数抛出适当的异常，如 `HTTPException`，以向 API 用户提供有意义的反馈。

2. **Performance Considerations:**
   - Be mindful of the performance impact when chaining multiple dependencies, especially if they involve database access or external API calls.
   - 在链接多个依赖项时注意性能影响，特别是当它们涉及数据库访问或外部 API 调用时。

---

#### 8. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on request validation and dependency injection in FastAPI.
   - 查看关于 FastAPI 中请求验证和依赖注入的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/dependencies/)

2. **Python Exception Handling:**
   - Learn more about exception handling in Python, including custom exceptions.
   - 了解更多关于 Python 中异常处理的信息，包括自定义异常。
   - [Python Exception Handling](https://docs.python.org/3/tutorial/errors.html)

3. **Data Validation Best Practices:**
   - Review best practices for data validation in API development.
   - 查看 API 开发中数据验证的最佳实践。
   - [Data Validation Best Practices](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)

This explanation provides a comprehensive guide on using dependency injection for request validation in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
