# Using Query Parameters for Filtering, Pagination, and Sorting in FastAPI

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Query parameters are an essential part of building flexible and dynamic APIs. They allow you to filter results, paginate large datasets, and sort data according to specific criteria. FastAPI provides an easy way to handle query parameters, making it simple to implement these functionalities in your endpoints.

**Chinese:**
查询参数是构建灵活动态 API 的关键部分。它们允许你过滤结果、分页大数据集，并根据特定标准对数据进行排序。FastAPI 提供了一种简单的方式来处理查询参数，使你可以轻松地在端点中实现这些功能。

---

#### 2. Filtering Results with Query Parameters 使用查询参数过滤结果

**English:**
Filtering results using query parameters allows users to narrow down the data returned by an API endpoint based on specific criteria. This is useful when working with large datasets where users might only be interested in a subset of the data.

**Chinese:**
使用查询参数过滤结果允许用户根据特定标准缩小 API 端点返回的数据范围。这在处理大数据集时特别有用，因为用户可能只对数据的一个子集感兴趣。

**Example 例子:**

```python
from fastapi import FastAPI, Query
from typing import List

app = FastAPI()

items = [
    {"item_id": 1, "name": "Item One", "category": "Books"},
    {"item_id": 2, "name": "Item Two", "category": "Electronics"},
    {"item_id": 3, "name": "Item Three", "category": "Books"},
    {"item_id": 4, "name": "Item Four", "category": "Clothing"},
]

@app.get("/items/")
def read_items(category: str = Query(None, description="Category to filter items by")):
    if category:
        filtered_items = [item for item in items if item["category"] == category]
    else:
        filtered_items = items
    return filtered_items
```

**Explanation 解释:**

- **English:**
  - `category: str = Query(None, description="Category to filter items by")`: Defines an optional query parameter `category`. If provided, it filters items based on the category.
  - The function `read_items` checks if the `category` parameter is provided and filters the items accordingly. If not, it returns all items.

- **Chinese:**
  - `category: str = Query(None, description="Category to filter items by")`: 定义了一个可选的查询参数 `category`。如果提供了该参数，它会根据类别过滤项目。
  - `read_items` 函数检查是否提供了 `category` 参数，并相应地过滤项目。如果没有提供，它会返回所有项目。

---

#### 3. Pagination with Query Parameters 使用查询参数进行分页

**English:**
Pagination is a common technique used to divide large datasets into smaller, manageable chunks. This is particularly useful for APIs that return large lists of items. By using `skip` and `limit` query parameters, you can easily implement pagination.

**Chinese:**
分页是一种常用技术，用于将大数据集分成较小的、可管理的块。这对于返回大量项目列表的 API 特别有用。通过使用 `skip` 和 `limit` 查询参数，你可以轻松实现分页。

**Example 例子:**

```python
@app.get("/items/")
def read_items(skip: int = 0, limit: int = 10):
    return items[skip: skip + limit]
```

**Explanation 解释:**

- **English:**
  - `skip: int = 0, limit: int = 10`: Defines two optional query parameters, `skip` and `limit`, with default values. `skip` is used to determine the offset from where to start, and `limit` determines the number of items to return.
  - The function `read_items` slices the `items` list according to the `skip` and `limit` values, effectively paginating the results.

- **Chinese:**
  - `skip: int = 0, limit: int = 10`: 定义了两个可选的查询参数 `skip` 和 `limit`，并带有默认值。`skip` 用于确定从哪里开始的偏移量，`limit` 确定返回的项目数量。
  - `read_items` 函数根据 `skip` 和 `limit` 值对 `items` 列表进行切片，从而有效地对结果进行分页。

---

#### 4. Sorting Results with Query Parameters 使用查询参数排序结果

**English:**
Sorting allows users to specify the order in which the data should be returned. You can implement sorting by defining a query parameter that specifies the field to sort by and the order (ascending or descending).

**Chinese:**
排序允许用户指定数据返回的顺序。你可以通过定义一个查询参数来指定要排序的字段和排序顺序（升序或降序），以实现排序功能。

**Example 例子:**

```python
@app.get("/items/")
def read_items(sort_by: str = "name", order: str = "asc"):
    sorted_items = sorted(items, key=lambda x: x[sort_by], reverse=(order == "desc"))
    return sorted_items
```

**Explanation 解释:**

- **English:**
  - `sort_by: str = "name", order: str = "asc"`: Defines two query parameters `sort_by` and `order`. `sort_by` determines which field to sort by (e.g., `name`), and `order` determines the sort direction (`asc` for ascending, `desc` for descending).
  - The function `read_items` sorts the `items` list based on the provided parameters and returns the sorted list.

- **Chinese:**
  - `sort_by: str = "name", order: str = "asc"`: 定义了两个查询参数 `sort_by` 和 `order`。`sort_by` 决定按哪个字段排序（例如 `name`），`order` 决定排序方向（`asc` 表示升序，`desc` 表示降序）。
  - `read_items` 函数根据提供的参数对 `items` 列表进行排序，并返回排序后的列表。

---

#### 5. Combining Filtering, Pagination, and Sorting 组合过滤、分页和排序

**English:**
You can combine filtering, pagination, and sorting in a single endpoint to create a powerful and flexible API. This approach allows users to retrieve data in a way that best fits their needs.

**Chinese:**
你可以在一个端点中组合过滤、分页和排序，以创建一个强大且灵活的 API。这种方法允许用户以最适合他们需求的方式检索数据。

**Example 例子:**

```python
@app.get("/items/")
def read_items(category: str = None, skip: int = 0, limit: int = 10, sort_by: str = "name", order: str = "asc"):
    filtered_items = [item for item in items if item["category"] == category] if category else items
    sorted_items = sorted(filtered_items, key=lambda x: x[sort_by], reverse=(order == "desc"))
    return sorted_items[skip: skip + limit]
```

**Explanation 解释:**

- **English:**
  - The function `read_items` combines filtering by `category`, sorting by `sort_by` and `order`, and pagination with `skip` and `limit`.
  - This setup allows users to retrieve items filtered by category, sorted in a specified order, and paginated.

- **Chinese:**
  - `read_items` 函数结合了按 `category` 过滤、按 `sort_by` 和 `order` 排序，以及使用 `skip` 和 `limit` 进行分页。
  - 这种设置允许用户检索按类别过滤、按指定顺序排序和分页的项目。

---

#### 6. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Combine Features for Flexibility:**
   - Combining filtering, pagination, and sorting in your endpoints provides users with a powerful way to interact with your API, making it more user-friendly and efficient.
   - 在端点中组合过滤、分页和排序功能，为用户提供了与 API 交互的强大方式，使其更加用户友好和高效。

2. **Use Default Values:**
   - Providing sensible default values for query parameters can make your API easier to use, especially for new users who may not be familiar with all the available options.
   - 为查询参数提供合理的默认值，可以使你的 API 更易于使用，特别是对于可能不熟悉所有可用选项的新用户。

**Warnings 警告:**

1. **Validate Query Parameters:**
   - Always validate and sanitize query parameters to prevent potential security risks such as SQL injection or excessive memory usage.
   - 始终验证和清理查询参数，以防止潜在的安全风险，例如 SQL 注入或过度内存使用。

2. **Handle Empty Results Gracefully:**
   - Ensure that your API handles cases where no items match the filtering criteria gracefully, by returning an empty list or a meaningful message.
   - 确保你的 API 能够优雅地处理没有项目匹配过滤条件的情况，可以返回一个空列表或有意义的消息。

---

#### 7. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on

 using query parameters for filtering, pagination, and sorting.
   - 查看关于使用查询参数进行过滤、分页和排序的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/query-params/)

2. **RealPython - FastAPI Guide:**
   - A guide on building APIs with FastAPI, including advanced usage of query parameters.
   - 一份关于使用 FastAPI 构建 API 的指南，包括查询参数的高级用法。
   - [RealPython FastAPI Guide](https://realpython.com/fastapi-python-web-apis/)

This explanation provides a comprehensive guide on using query parameters for filtering, pagination, and sorting in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
