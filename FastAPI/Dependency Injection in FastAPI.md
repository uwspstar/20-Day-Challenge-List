### Dependency Injection in FastAPI: Defining and Using Dependencies

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Dependency Injection (DI) is a design pattern that allows you to manage dependencies between different parts of your application. In FastAPI, DI is used to inject dependencies into your routes, making your code more modular, reusable, and testable. FastAPI's dependency injection system is powerful and flexible, allowing you to define dependencies in a straightforward manner and use them across your application.

**Chinese:**
依赖注入（DI）是一种设计模式，它允许你管理应用程序不同部分之间的依赖关系。在 FastAPI 中，DI 用于将依赖项注入到路由中，使你的代码更加模块化、可重用和可测试。FastAPI 的依赖注入系统既强大又灵活，允许你以简单明了的方式定义依赖项，并在整个应用程序中使用它们。

---

#### 2. Defining a Simple Dependency 定义一个简单的依赖项

**English:**
A dependency in FastAPI is typically a function that can return any value or perform any logic you want to reuse. You define a dependency using Python functions and inject it into a route by adding it as a parameter.

**Chinese:**
在 FastAPI 中，依赖项通常是一个函数，可以返回任何值或执行你想要重用的任何逻辑。你可以使用 Python 函数定义依赖项，并通过将其添加为参数的方式注入到路由中。

**Example 例子:**

```python
from fastapi import FastAPI, Depends

app = FastAPI()

def common_parameters(q: str = None, limit: int = 100):
    return {"q": q, "limit": limit}

@app.get("/items/")
def read_items(params: dict = Depends(common_parameters)):
    return params
```

**Explanation 解释:**

- **English:**
  - `common_parameters`: A function that defines common query parameters `q` and `limit`. This function acts as a dependency.
  - `Depends(common_parameters)`: Injects the `common_parameters` function as a dependency into the `read_items` route. The result of `common_parameters` is passed as the `params` argument.

- **Chinese:**
  - `common_parameters`: 一个定义了常见查询参数 `q` 和 `limit` 的函数。此函数作为依赖项。
  - `Depends(common_parameters)`: 将 `common_parameters` 函数作为依赖项注入到 `read_items` 路由中。`common_parameters` 的结果作为 `params` 参数传递。

---

#### 3. Using Dependencies Across Multiple Routes 在多个路由中使用依赖项

**English:**
You can reuse the same dependency across multiple routes, which makes it easy to maintain and update shared logic.

**Chinese:**
你可以在多个路由中重用相同的依赖项，这使得维护和更新共享逻辑变得简单。

**Example 例子:**

```python
@app.get("/users/")
def read_users(params: dict = Depends(common_parameters)):
    return params

@app.get("/products/")
def read_products(params: dict = Depends(common_parameters)):
    return params
```

**Explanation 解释:**

- **English:**
  - The `common_parameters` dependency is reused in both `read_users` and `read_products` routes, ensuring consistent behavior across these endpoints.
  
- **Chinese:**
  - `common_parameters` 依赖项在 `read_users` 和 `read_products` 路由中重用，确保这些端点之间的一致行为。

---

#### 4. Dependencies with More Complex Logic 具有更复杂逻辑的依赖项

**English:**
Dependencies can include more complex logic, such as accessing databases, making API calls, or performing calculations. You can use dependencies to manage these operations in a centralized and reusable way.

**Chinese:**
依赖项可以包含更复杂的逻辑，例如访问数据库、进行 API 调用或执行计算。你可以使用依赖项以集中和可重用的方式管理这些操作。

**Example 例子:**

```python
from fastapi import HTTPException

def verify_token(token: str):
    if token != "secret-token":
        raise HTTPException(status_code=400, detail="Invalid token")
    return {"user": "john_doe"}

@app.get("/secure-data/")
def get_secure_data(user: dict = Depends(verify_token)):
    return {"user": user, "data": "This is secured"}
```

**Explanation 解释:**

- **English:**
  - `verify_token`: A dependency that checks if a token is valid. If the token is invalid, it raises an `HTTPException`. If valid, it returns a user dictionary.
  - `Depends(verify_token)`: Injects the `verify_token` dependency into the `get_secure_data` route, ensuring that only requests with a valid token can access the route.

- **Chinese:**
  - `verify_token`: 一个检查令牌是否有效的依赖项。如果令牌无效，则抛出 `HTTPException`。如果有效，则返回用户字典。
  - `Depends(verify_token)`: 将 `verify_token` 依赖项注入到 `get_secure_data` 路由中，确保只有带有有效令牌的请求才能访问该路由。

---

#### 5. Using Class-Based Dependencies 使用基于类的依赖项

**English:**
You can also define dependencies as classes, which is useful when you need to maintain state or have multiple related methods.

**Chinese:**
你还可以将依赖项定义为类，当你需要维护状态或具有多个相关方法时，这种方法非常有用。

**Example 例子:**

```python
class CommonParameters:
    def __init__(self, q: str = None, limit: int = 100):
        self.q = q
        self.limit = limit

@app.get("/items/")
def read_items(params: CommonParameters = Depends()):
    return {"q": params.q, "limit": params.limit}
```

**Explanation 解释:**

- **English:**
  - `CommonParameters`: A class that acts as a dependency, allowing you to encapsulate query parameters and logic in a reusable way.
  - `Depends()`: Automatically resolves the `CommonParameters` class as a dependency and injects it into the `read_items` route.

- **Chinese:**
  - `CommonParameters`: 一个作为依赖项的类，允许你以可重用的方式封装查询参数和逻辑。
  - `Depends()`: 自动将 `CommonParameters` 类解析为依赖项，并将其注入到 `read_items` 路由中。

---

#### 6. Sub-dependencies and Dependency Injection Chains 子依赖项和依赖注入链

**English:**
Dependencies can depend on other dependencies, creating a chain of dependencies. This allows you to compose complex logic from simpler, reusable components.

**Chinese:**
依赖项可以依赖于其他依赖项，从而创建依赖链。这使得你可以通过简单、可重用的组件来组合复杂的逻辑。

**Example 例子:**

```python
def get_db():
    db = {"connection": "database connection"}
    return db

def get_user(db: dict = Depends(get_db)):
    return {"username": "john_doe", "db": db}

@app.get("/profile/")
def read_profile(user: dict = Depends(get_user)):
    return {"user": user}
```

**Explanation 解释:**

- **English:**
  - `get_db`: A dependency that returns a database connection.
  - `get_user`: A dependency that depends on `get_db` to fetch a user from the database.
  - `Depends(get_user)`: Injects the `get_user` dependency into the `read_profile` route, which in turn depends on the `get_db` dependency.

- **Chinese:**
  - `get_db`: 一个返回数据库连接的依赖项。
  - `get_user`: 一个依赖 `get_db` 的依赖项，用于从数据库中获取用户。
  - `Depends(get_user)`: 将 `get_user` 依赖项注入到 `read_profile` 路由中，而 `get_user` 又依赖于 `get_db` 依赖项。

---

#### 7. Global Dependencies and Dependency Overrides 全局依赖项和依赖项覆盖

**English:**
FastAPI allows you to apply dependencies globally across all routes or override them in specific cases, giving you flexibility in how you manage dependencies.

**Chinese:**
FastAPI 允许你在所有路由中全局应用依赖项，或在特定情况下覆盖它们，从而为你管理依赖项提供了灵活性。

**Example 例子:**

```python
from fastapi import Depends, FastAPI, HTTPException

app = FastAPI()

def verify_token(token: str):
    if token != "secret-token":
        raise HTTPException(status_code=400, detail="Invalid token")
    return {"user": "john_doe"}

@app.get("/items/")
def read_items(token: dict = Depends(verify_token)):
    return {"token": token}

@app.get("/secure-data/")
def get_secure_data(token: dict = Depends(verify_token)):
    return {"token": token, "data": "This is secured"}
```

**Explanation 解释:**

- **English:**
  - `verify_token`: This dependency is used globally in multiple routes (`read_items` and `get_secure_data`), ensuring that all routes requiring token verification use the

 same logic.
  - `Depends(verify_token)`: Injects the `verify_token` dependency into multiple routes, ensuring consistent security checks across your API.

- **Chinese:**
  - `verify_token`: 此依赖项在多个路由（`read_items` 和 `get_secure_data`）中全局使用，确保所有需要令牌验证的路由使用相同的逻辑。
  - `Depends(verify_token)`: 将 `verify_token` 依赖项注入多个路由，确保 API 中的一致安全检查。

---

#### 8. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Keep Dependencies Reusable:**
   - Design your dependencies to be as reusable as possible to promote consistency and reduce duplication across your application.
   - 尽可能设计可重用的依赖项，以促进一致性并减少应用程序中的重复。

2. **Use Sub-dependencies Wisely:**
   - Leverage sub-dependencies to build complex logic from smaller, more manageable components.
   - 明智地使用子依赖项，从较小、可管理的组件构建复杂逻辑。

**Warnings 警告:**

1. **Dependency Hell:**
   - Be careful with deeply nested dependencies, as they can lead to complex and hard-to-maintain code. Keep your dependency chain as simple as possible.
   - 小心深度嵌套的依赖项，因为它们可能导致复杂且难以维护的代码。保持你的依赖链尽可能简单。

2. **Performance Considerations:**
   - While dependencies are powerful, excessive or unnecessary use of them can impact performance. Use them judiciously to avoid slowing down your application.
   - 虽然依赖项功能强大，但过多或不必要的使用可能会影响性能。谨慎使用它们以避免减慢应用程序速度。

---

#### 9. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on dependency injection in FastAPI.
   - 查看关于 FastAPI 中依赖注入的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/dependencies/)

2. **Python Dependency Injection:**
   - Learn more about the principles of dependency injection in Python and how to implement them.
   - 了解更多关于 Python 中依赖注入原理及其实现方法的信息。
   - [Python Dependency Injection](https://docs.python.org/3/tutorial/classes.html#inheritance)

3. **SOLID Principles:**
   - Understand the SOLID principles in software design, which include guidelines for using dependency injection effectively.
   - 了解软件设计中的 SOLID 原则，其中包括有效使用依赖注入的指南。
   - [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)

This explanation provides a comprehensive guide on defining and using dependencies in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
