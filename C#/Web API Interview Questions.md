# Web API
Sure! I will answer each of the questions with code examples where applicable to help you understand. I'll provide line-by-line explanations in both **English** and **Chinese** to make it easier for you.

### 1. What is Web API? What is the purpose of Web API?

**Answer:**
A **Web API** is an application programming interface (API) for the web that allows different systems to communicate over HTTP. It enables applications to exchange data or functionality with one another.

- **Purpose**: The main purpose of Web API is to allow multiple client applications (e.g., web, mobile) to communicate with the server for accessing or manipulating data.

```csharp
public class ValuesController : ApiController
{
    // GET api/values
    public IEnumerable<string> Get()
    {
        return new string[] { "value1", "value2" };
    }
}
```

**Translation:**
Web API 是一种通过 HTTP 进行通信的接口，允许不同的系统交换数据或功能。

- **目的**：Web API 的主要目的是让多个客户端应用（如 Web、移动应用）与服务器通信，访问或操作数据。

### 2. What are Web API advantages over WCF and web services?

**Answer:**
- **Simpler**: Web API is much easier to use compared to WCF.
- **Supports full HTTP features**: It supports HTTP verbs (GET, POST, PUT, DELETE), unlike WCF which is more complex.
- **Open source**: Web API is part of ASP.NET, which is open source.

**Translation:**
- **更简单**：与 WCF 相比，Web API 更容易使用。
- **支持完整的 HTTP 功能**：它支持 HTTP 动词 (GET, POST, PUT, DELETE)，而 WCF 更为复杂。
- **开源**：Web API 是 ASP.NET 的一部分，并且是开源的。

### 3. What is REST and Restful?

**Answer:**
- **REST (Representational State Transfer)**: It is an architectural style that uses HTTP requests to access and manipulate data.
- **Restful**: A service that conforms to the REST principles is called a Restful service.

**Translation:**
- **REST（表述性状态转移）**：是一种使用 HTTP 请求来访问和操作数据的架构风格。
- **Restful**：符合 REST 原则的服务称为 Restful 服务。

### 4. Is it possible to use WCF as Restful services?

**Answer:**
Yes, it is possible to use WCF as Restful services by configuring the WCF service to handle HTTP requests and using webHttpBinding in WCF.

**Example**:

```xml
<bindings>
  <webHttpBinding>
    <binding name="webHttp" />
  </webHttpBinding>
</bindings>
```

**Translation:**
是的，可以通过配置 WCF 服务处理 HTTP 请求，并使用 webHttpBinding 来将 WCF 作为 Restful 服务。

### 5. What are HTTP verbs or HTTP methods?

**Answer:**
- **GET**: Retrieve data.
- **POST**: Submit data.
- **PUT**: Update existing data.
- **DELETE**: Remove data.

```csharp
[HttpGet]
public string GetValue()
{
    return "value";
}
```

**Translation:**
- **GET**：检索数据。
- **POST**：提交数据。
- **PUT**：更新现有数据。
- **DELETE**：删除数据。

### 6. How to consume Web API from a .NET MVC application?

**Answer:**
You can use `HttpClient` in .NET to consume a Web API.

```csharp
HttpClient client = new HttpClient();
HttpResponseMessage response = await client.GetAsync("api/values");
if (response.IsSuccessStatusCode)
{
    var data = await response.Content.ReadAsStringAsync();
}
```

**Translation:**
可以使用 `.NET` 中的 `HttpClient` 来消费 Web API。

### 7. What is the difference between Web API and MVC Controller?

**Answer:**
- **Web API**: Designed for building RESTful services that return data in JSON/XML.
- **MVC Controller**: Designed for rendering views (HTML) as the response.

**Translation:**
- **Web API**：用于构建返回 JSON/XML 数据的 RESTful 服务。
- **MVC 控制器**：用于呈现 HTML 作为响应。

### 8. What is Basic Authentication in Web API?

**Answer:**
Basic Authentication uses a username and password to authenticate the user.

```csharp
public class BasicAuthenticationAttribute : AuthorizationFilterAttribute
{
    // Implement Basic Authentication logic
}
```

**Translation:**
基本身份验证使用用户名和密码来验证用户。

### 9. What is API Key Authentication in Web API?

**Answer:**
API Key Authentication uses a token (API Key) passed in the request header to authenticate the client.

```csharp
[HttpGet]
public HttpResponseMessage Get([FromHeader(Name = "ApiKey")] string apiKey)
{
    if (apiKey == "validApiKey")
    {
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
    return new HttpResponseMessage(HttpStatusCode.Unauthorized);
}
```

**Translation:**
API 密钥身份验证使用请求头中传递的令牌（API 密钥）来验证客户端。

### 10. What is Token-based authentication?

**Answer:**
Token-based authentication uses a token (such as JWT) to identify the user, which is passed in the HTTP header.

```csharp
[Authorize]
public IHttpActionResult GetData()
{
    return Ok("Authorized Data");
}
```

**Translation:**
基于令牌的身份验证使用令牌（例如 JWT）来标识用户，并在 HTTP 头中传递。

### 11. What is OAuth?

**Answer:**
OAuth is an open-standard authorization protocol that allows third-party services to exchange tokens for user data.

**Translation:**
OAuth 是一种开放标准授权协议，允许第三方服务交换令牌以获取用户数据。

### 12. What is JWT Authentication?

**Answer:**
JWT (JSON Web Token) is a compact token format used for authentication and information exchange between parties.

```csharp
public string GenerateToken(string username)
{
    var tokenHandler = new JwtSecurityTokenHandler();
    var key = Encoding.ASCII.GetBytes("secretkey");
    var tokenDescriptor = new SecurityTokenDescriptor
    {
        Subject = new ClaimsIdentity(new[] { new Claim("username", username) }),
        Expires = DateTime.UtcNow.AddHours(1),
        SigningCredentials = new SigningCredentials(new SymmetricSecurityKey(key), SecurityAlgorithms.HmacSha256Signature)
    };
    var token = tokenHandler.CreateToken(tokenDescriptor);
    return tokenHandler.WriteToken(token);
}
```

**Translation:**
JWT（JSON Web Token）是一种用于身份验证和信息交换的紧凑令牌格式。

### 13. What are the parts of a JWT token?

**Answer:**
A JWT token has three parts:
1. **Header**: Metadata about the token.
2. **Payload**: Contains claims (data).
3. **Signature**: Used to verify the authenticity.

**Translation:**
JWT 令牌有三部分：
1. **头部**：关于令牌的元数据。
2. **载荷**：包含声明（数据）。
3. **签名**：用于验证真实性。

### 14. Where does the JWT token reside in the request?

**Answer:**
The JWT token resides in the HTTP request's **Authorization** header.

```http
Authorization: Bearer <token>
```

**Translation:**
JWT 令牌位于 HTTP 请求的 **Authorization** 头部。

### 15. How to test Web API? What are the tools?

**Answer:**
You can test Web API using tools like **Postman**, **Swagger**, or **curl**.

```bash
curl -X GET "https://example.com/api/values"
```

**Translation:**
可以使用 **Postman**、**Swagger** 或 **curl** 等工具来测试 Web API。

### 16. What are the main Return Types supported in Web API?

**Answer:**
- **IHttpActionResult**
- **HttpResponseMessage**
- **JSON/XML**

**Translation:**
Web API 支持的主要返回类型：
- **IHttpActionResult**
- **HttpResponseMessage**
- **JSON/XML**

### 17. What is the difference between HTTPResponseMessage and IHttpActionResult?

**Answer:**
- **HttpResponseMessage**: Represents a complete HTTP response.
- **IHttpActionResult**: Simplifies returning HTTP responses in Web API by abstracting the response creation process.

**Translation:**
- **HttpResponseMessage**：表示完整的 HTTP 响应。
- **IHttpActionResult**：简化了 Web API 中 HTTP 响应的返回，通过抽象响应创建过程。

### 18. What is Content Negotiation in Web API?

**Answer:**
Content Negotiation allows the client and server to agree on the best format for the response, such as JSON or XML.

**Translation:**
内容协商允许客户端和服务器协商最佳的响应格式，如 JSON 或 XML。

### 19. What is MediaTypeFormatter class in Web API?

**Answer:**
MediaTypeFormatter is responsible for serializing and deserializing data between the server and client in Web API.

**Translation:**
MediaTypeFormatter 类负责在 Web API 中序列化和反序列化服务器和客户端之间的数据。

### 20. What are Response Codes in Web API?

**Answer:**
- **200 OK

**: Success.
- **404 Not Found**: Resource not found.
- **500 Internal Server Error**: Server error.

**Translation:**
- **200 OK**：成功。
- **404 Not Found**：未找到资源。
- **500 Internal Server Error**：服务器错误。

This format includes explanations and code examples for each question to help you understand the concepts clearly. Let me know if you need further details on any of these.
