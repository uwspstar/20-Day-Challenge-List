# Security in FastAPI: Basics of OAuth2 and JWT Authentication

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Security is a critical component of any web application. FastAPI provides built-in support for implementing secure authentication mechanisms, including OAuth2 and JWT (JSON Web Tokens). OAuth2 is a widely used authorization framework that allows third-party services to access a user's resources without exposing their credentials. JWT, on the other hand, is a compact, URL-safe token format used to represent claims between two parties. Combining OAuth2 with JWT is a common practice for building secure APIs.

**Chinese:**
安全性是任何 Web 应用程序的重要组成部分。FastAPI 提供了内置支持，用于实现安全的身份验证机制，包括 OAuth2 和 JWT（JSON Web Tokens）。OAuth2 是一种广泛使用的授权框架，允许第三方服务访问用户资源，而无需暴露用户的凭据。另一方面，JWT 是一种紧凑的、URL 安全的令牌格式，用于在两方之间表示声明。将 OAuth2 与 JWT 结合使用是构建安全 API 的常见做法。

---

#### 2. Basics of OAuth2 OAuth2 的基础知识

**English:**
OAuth2 is a protocol that enables secure authorization in a simple and standard method for web, mobile, and desktop applications. It allows applications to access resources on behalf of a user by providing a token, rather than directly using the user's credentials.

**Chinese:**
OAuth2 是一种协议，它为 Web、移动和桌面应用程序提供了简单标准的安全授权方法。它允许应用程序通过提供令牌而非直接使用用户凭据来代表用户访问资源。

**Example 例子:**

```python
from fastapi import FastAPI, Depends, HTTPException
from fastapi.security import OAuth2PasswordBearer

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    if form_data.username == "user" and form_data.password == "pass":
        return {"access_token": "fake-jwt-token", "token_type": "bearer"}
    raise HTTPException(status_code=400, detail="Invalid username or password")

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

**Explanation 解释:**

- **English:**
  - `OAuth2PasswordBearer`: A class that sets up the OAuth2 password flow. The `tokenUrl` parameter specifies the URL where the client can request a token.
  - `login`: A route that simulates a token endpoint. It checks the user's credentials and returns a fake JWT token if they match.
  - `read_users_me`: A protected route that requires a valid token to access. It uses the `oauth2_scheme` dependency to extract the token from the request.

- **Chinese:**
  - `OAuth2PasswordBearer`: 一个设置 OAuth2 密码流的类。`tokenUrl` 参数指定客户端可以请求令牌的 URL。
  - `login`: 模拟令牌端点的路由。它检查用户的凭据，如果匹配则返回一个假的 JWT 令牌。
  - `read_users_me`: 一个受保护的路由，需要有效的令牌才能访问。它使用 `oauth2_scheme` 依赖项从请求中提取令牌。

---

#### 3. Understanding JWT (JSON Web Tokens) 理解 JWT（JSON Web Tokens）

**English:**
JWT is a compact and self-contained token format that is commonly used for securely transmitting information between parties as a JSON object. JWTs can be signed using a secret (with HMAC algorithm) or a public/private key pair (using RSA or ECDSA). The token typically consists of three parts: Header, Payload, and Signature.

**Chinese:**
JWT 是一种紧凑的、自包含的令牌格式，通常用于在各方之间以 JSON 对象的形式安全传输信息。JWT 可以使用密钥（通过 HMAC 算法）或公钥/私钥对（使用 RSA 或 ECDSA）签名。令牌通常由三个部分组成：头部（Header）、载荷（Payload）和签名（Signature）。

**Example of JWT Structure JWT 结构示例:**

```text
header.payload.signature
```

- **Header:** Contains metadata about the type of token and the signing algorithm being used.
- **Payload:** Contains the claims, which are statements about an entity (typically, the user) and additional data.
- **Signature:** Ensures that the token hasn't been altered. It is created by encoding the header and payload using the secret key.

- **头部:** 包含有关令牌类型和使用的签名算法的元数据。
- **载荷:** 包含声明，这些声明是关于实体（通常是用户）的陈述以及附加数据。
- **签名:** 确保令牌没有被篡改。它是通过使用密钥对头部和载荷进行编码创建的。

---

#### 4. Implementing JWT Authentication in FastAPI 在 FastAPI 中实现 JWT 身份验证

**English:**
To implement JWT authentication in FastAPI, you'll need to create a function to generate tokens and another to decode and verify them. You can use the `jwt` library for this purpose.

**Chinese:**
要在 FastAPI 中实现 JWT 身份验证，你需要创建一个生成令牌的函数和另一个用于解码和验证令牌的函数。你可以使用 `jwt` 库来实现这一目的。

**Example 例子:**

```python
import jwt
from datetime import datetime, timedelta
from fastapi import Depends, FastAPI, HTTPException
from fastapi.security import OAuth2PasswordBearer

SECRET_KEY = "mysecretkey"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

def create_access_token(data: dict):
    to_encode = data.copy()
    expire = datetime.utcnow() + timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

def decode_token(token: str):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        return payload
    except jwt.ExpiredSignatureError:
        raise HTTPException(status_code=401, detail="Token has expired")
    except jwt.JWTError:
        raise HTTPException(status_code=401, detail="Invalid token")

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    if form_data.username == "user" and form_data.password == "pass":
        access_token = create_access_token(data={"sub": form_data.username})
        return {"access_token": access_token, "token_type": "bearer"}
    raise HTTPException(status_code=400, detail="Invalid username or password")

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    payload = decode_token(token)
    return {"username": payload.get("sub")}
```

**Explanation 解释:**

- **English:**
  - **create_access_token:** This function generates a JWT token with a specified expiration time. The `data` dictionary typically contains user information (like username) that you want to include in the token.
  - **decode_token:** This function decodes and verifies the JWT token. It checks for token expiration and validates the token using the secret key.
  - **login:** The `login` route generates an access token for valid users. The token is returned to the client as a bearer token.
  - **read_users_me:** This protected route uses the JWT token to identify and authenticate the user.

- **Chinese:**
  - **create_access_token:** 此函数生成具有指定过期时间的 JWT 令牌。`data` 字典通常包含你希望包含在令牌中的用户信息（如用户名）。
  - **decode_token:** 此函数解码并验证 JWT 令牌。它检查令牌是否过期，并使用密钥验证令牌。
  - **login:** `login` 路由为有效用户生成访问令牌。令牌作为持有者令牌返回给客户端。
  - **read_users_me:** 这个受保护的路由使用 JWT 令牌来识别和验证用户。

---

#### 5. Refreshing JWT Tokens 刷新 JWT 令牌

**English:**
JWT tokens are typically short-lived, which reduces the impact of a compromised token. However, you can implement a refresh token mechanism that allows users to obtain a new token without re-authenticating. This is usually done by issuing a long-lived refresh token alongside the short-lived access token.

**Chinese:**
JWT 令牌通常是短期有效的，这减少了被泄露令牌的影响。然而，你可以实现一个刷新令牌机制，允许用户在不重新验证的情况下获取新令牌。这通常通过在发放短期访问令牌的同时发放长期刷新令牌来实现。

**Example 例子:**

```python
from fastapi import status

@app.post("/refresh")
async def refresh_token(refresh_token: str):
    payload = decode_token(refresh_token)
    new_access_token = create_access_token(data={"sub": payload.get("sub")})
    return {"access_token": new_access_token, "token_type": "bearer"}
```

**Explanation 解释:**

- **English:**
  - **refresh_token:** This endpoint accepts a refresh token, dec

odes it, and issues a new access token based on the original token's payload. This allows the user to stay logged in without re-authenticating.
  
- **Chinese:**
  - **refresh_token:** 此端点接受一个刷新令牌，解码后基于原令牌的载荷发放一个新的访问令牌。这允许用户在不重新验证的情况下保持登录状态。

---

#### 6. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Use Secure Secrets:**
   - Always use a strong, secure secret key for signing JWTs to prevent unauthorized access.
   - 始终使用强大且安全的密钥来签署 JWT，以防止未经授权的访问。

2. **Implement Token Expiration:**
   - Set an appropriate expiration time for access tokens to minimize the risk if a token is compromised.
   - 为访问令牌设置适当的过期时间，以在令牌泄露时将风险降至最低。

3. **Use HTTPS:**
   - Always serve tokens over HTTPS to prevent them from being intercepted by attackers.
   - 始终通过 HTTPS 传输令牌，以防止它们被攻击者截获。

**Warnings 警告:**

1. **Token Revocation:**
   - JWTs are stateless and cannot be easily revoked. Implement a mechanism to handle token revocation if needed, such as maintaining a blacklist of revoked tokens.
   - JWT 是无状态的，无法轻易撤销。如果需要，实施一个机制来处理令牌撤销，例如维护已撤销令牌的黑名单。

2. **Refresh Token Security:**
   - Treat refresh tokens as highly sensitive, as they allow users to obtain new access tokens without re-authentication.
   - 将刷新令牌视为高度敏感的，因为它们允许用户在不重新验证的情况下获取新的访问令牌。

---

#### 7. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on security, OAuth2, and JWT in FastAPI.
   - 查看关于 FastAPI 中的安全性、OAuth2 和 JWT 的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/security/)

2. **OAuth2 Specification:**
   - Understand the OAuth2 protocol and its various flows.
   - 了解 OAuth2 协议及其各种流。
   - [OAuth2 Specification](https://tools.ietf.org/html/rfc6749)

3. **JWT Specification:**
   - Learn more about JWTs and how they are structured and used.
   - 了解更多关于 JWT 的信息，以及它们的结构和使用方法。
   - [JWT Specification](https://tools.ietf.org/html/rfc7519)

This explanation provides a comprehensive guide on the basics of OAuth2 and JWT authentication in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
