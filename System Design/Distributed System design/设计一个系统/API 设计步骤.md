# API 设计步骤

以下是针对功能性需求的 API 设计步骤, 可以将其用作模板。

### 第一步：定义API端点

#### 1. **用户注册**
- **端点**：`/api/register`
- **方法**：`POST`
- **描述**：通过提供必要的详细信息如电子邮件、用户名和密码来创建新用户账号。
- **输入参数**： 
  - `username`
  - `email`
  - `password`
- **响应**：
  - 成功：`201 Created`，用户详情包括`user_id`
  - 失败：`400 Bad Request`，错误详情

**FastAPI 代码示例：**

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()

class UserRegistration(BaseModel):
    username: str
    email: str
    password: str

@app.post("/api/register")
async def register_user(user: UserRegistration):
    # 模拟用户注册逻辑
    if user.username == "exists":
        raise HTTPException(status_code=400, detail="User already exists")
    return {"user_id": "12345", "username": user.username}
```

#### 2. **用户登录**
- **端点**：`/api/login`
- **方法**：`POST`
- **描述**：验证用户以访问系统。
- **输入参数**：
  - `email`
  - `password`
- **响应**：
  - 成功：`200 OK`，`access_token`
  - 失败：`401 Unauthorized`

**FastAPI 代码示例：**

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

class UserLogin(BaseModel):
    email: str
    password: str

@app.post("/api/login")
async def login_user(user: UserLogin):
    # 模拟用户登录逻辑
    if user.email != "test@example.com" or user.password != "password":
        raise HTTPException(status_code=401, detail="Invalid credentials")
    return {"access_token": "fake_jwt_token"}
```

#### 3. **发布内容**
- **端点**：`/api/posts`
- **方法**：`POST`
- **描述**：允许用户创建新帖子。
- **输入参数**：
  - `user_id`
  - `content`
  - `media`（可选）
- **响应**：
  - 成功：`201 Created`，`post_id`
  - 失败：`400 Bad Request`

**FastAPI 代码示例：**

```python
class PostContent(BaseModel):
    user_id: str
    content: str
    media: str = None

@app.post("/api/posts")
async def create_post(post: PostContent):
    if len(post.content) == 0:
        raise HTTPException(status_code=400, detail="Content cannot be empty")
    return {"post_id": "post_123", "content": post.content}
```

#### 4. **好友请求**
- **端点**：`/api/friend-requests`
- **方法**：`POST`
- **描述**：向其他用户发送好友请求。
- **输入参数**：
  - `sender_id`
  - `receiver_id`
- **响应**：
  - 成功：`200 OK`
  - 失败：`400 Bad Request`

**FastAPI 代码示例：**

```python
class FriendRequest(BaseModel):
    sender_id: str
    receiver_id: str

@app.post("/api/friend-requests")
async def send_friend_request(request: FriendRequest):
    if request.sender_id == request.receiver_id:
        raise HTTPException(status_code=400, detail="Cannot send request to yourself")
    return {"status": "Friend request sent"}
```

#### 5. **接受/拒绝好友请求**
- **端点**：`/api/friend-requests/{request_id}`
- **方法**：`PATCH`
- **描述**：接受或拒绝好友请求。
- **输入参数**：
  - `request_id`
  - `action`（accept/reject）
- **响应**：
  - 成功：`200 OK`
  - 失败：`400 Bad Request`

**FastAPI 代码示例：**

```python
@app.patch("/api/friend-requests/{request_id}")
async def respond_friend_request(request_id: str, action: str):
    if action not in ["accept", "reject"]:
        raise HTTPException(status_code=400, detail="Invalid action")
    return {"status": f"Friend request {action}ed"}
```

#### 6. **生成新闻推送**
- **端点**：`/api/news-feed`
- **方法**：`GET`
- **描述**：获取用户的个性化新闻推送。
- **输入参数**：
  - `user_id`
  - `page_number`
- **响应**：
  - 成功：`200 OK`，帖子列表
  - 失败：`404 Not Found`

**FastAPI 代码示例：**

```python
@app.get("/api/news-feed")
async def get_news_feed(user_id: str, page_number: int):
    # 模拟新闻推送逻辑
    if user_id != "valid_user":
        raise HTTPException(status_code=404, detail="User not found")
    return {"posts": ["post1", "post2"], "page": page_number}
```

#### 7. **点赞和评论**
- **点赞帖子**：
  - **端点**：`/api/posts/{post_id}/like`
  - **方法**：`POST`
  - **描述**：点赞指定帖子。
  - **输入参数**：
    - `user_id`
  - **响应**：
    - 成功：`200 OK`
    - 失败：`400 Bad Request`

**FastAPI 代码示例：**

```python
@app.post("/api/posts/{post_id}/like")
async def like_post(post_id: str, user_id: str):
    if user_id == "":
        raise HTTPException(status_code=400, detail="User ID required")
    return {"status": "Post liked"}
```

- **评论帖子**：
  - **端点**：`/api/posts/{post_id}/comment`
  - **方法**：`POST`
  - **描述**：对帖子进行评论。
  - **输入参数**：
    - `user_id`
    - `comment`
  - **响应**：
    - 成功：`201 Created`，`comment_id`
    - 失败：`400 Bad Request`

**FastAPI 代码示例：**

```python
class CommentPost(BaseModel):
    user_id: str
    comment: str

@app.post("/api/posts/{post_id}/comment")
async def comment_on_post(post_id: str, comment: CommentPost):
    if len(comment.comment) == 0:
        raise HTTPException(status_code=400, detail="Comment cannot be empty")
    return {"comment_id": "comment_123"}
```

#### 8. **通知**
- **端点**：`/api/notifications`
- **方法**：`GET`
- **描述**：获取用户通知。
- **输入参数**：
  - `user_id`
- **响应**：
  - 成功：`200 OK`，通知列表
  - 失败：`404 Not Found`

**FastAPI 代码示例：**

```python
@app.get("/api/notifications")
async def get_notifications(user_id: str):
    if user_id != "valid_user":
        raise HTTPException(status_code=404, detail="User not found")
    return {"notifications": ["You have a new friend request", "Your post was liked"]}
```

### 第二步：定义数据模型

#### 1. **用户模型**
- `user_id`：字符串（主键）
- `username`：字符串
- `email`：字符串
- `password`：字符串（加密）

#### 2. **帖子模型**
- `post_id`：字符串（主键）
- `user_id`：字符串（外键）
- `content`：文本
- `created_at`：时间戳

#### 3. **好友请求模型**
- `request_id`：字符串（主键）
- `sender_id`：字符串
- `receiver_id`：字符串
- `status`：字符串（待处理，已接受，已拒绝）

#### 4. **通知模型**
- `notification_id`：字符串（主键）
- `user_id`：字符串（外键）
- `message`：字符串
- `created_at`：时间戳

### 第三步：定义认证与授权

1. **认证**：
   - 使用**JWT（JSON Web Tokens）**来管理用户会话并保护API。
   - 为受保护的路由（如`/api/posts`，`/api/friend-requests`）添加认证中间件以验证令牌。

2. **授权**：
   - 根据需要添加基于角色或权限的访问控制。例如，只有好友才能查看私人帖子。

### 第四步：错误处理与验证

1. **输入验证**：
   - 验证用户输入，如电子邮件格式、内容长度等，在处理请求之前。
   - 对无效输入返回`400 Bad Request`。

2. **错误响应**：
   - 使用标准化的错误响应来处理意外情况。
   - 返回有意义的错误代码和消息（例如`404 Not Found`，

`401 Unauthorized`）。

### 第五步：限流与节流

1. **限流**：
   - 限制用户在给定时间内可以发出的请求数量。
   - 使用**Redis**或**API Gateway**等工具实现限流。

### 第六步：API文档

1. **使用Swagger或Postman**来创建和发布API文档。
2. **为每个端点编写文档**：包括URL、方法、输入参数和响应示例。

### 总结
这个API设计指南包含了逐步实现的每个功能，包括定义端点、数据模型、认证与授权、错误处理、限流以及API文档。
