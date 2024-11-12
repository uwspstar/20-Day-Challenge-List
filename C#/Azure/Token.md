### ID Token vs Access Token vs Refresh Token

以下是关于 **ID Token**、**Access Token** 和 **Refresh Token** 的概述，并包含它们的C#代码示例和Mermaid类图。了解这些令牌的用途有助于在身份验证和授权过程中正确选择和使用它们。

---

### 概念说明

- **ID Token**：用于认证用户身份的令牌，通常包含用户的身份信息（如用户名、电子邮件等），是OAuth2.0和OpenID Connect中常用的令牌类型之一。应用程序通常使用ID Token来确认用户的身份，典型用例为用户登录过程。

- **Access Token**：用于授权访问受保护资源的令牌，包含了用户或客户端的权限信息。Access Token不包含用户的详细身份信息，而是用于让应用程序访问API时，告知资源服务器应用已被授权。

- **Refresh Token**：用于获取新的Access Token的长效令牌。当Access Token过期时，应用程序可以使用Refresh Token向认证服务器请求新的Access Token，而不需要用户再次登录。

---

### C#代码示例：ID Token、Access Token 和 Refresh Token

以下C#代码展示了如何通过Azure AD获取ID Token、Access Token和Refresh Token，并使用Access Token访问受保护的API。

#### 1. 配置 `appsettings.json`

在 `appsettings.json` 中配置Azure AD的相关信息，包括`ClientId`、`TenantId`、`ClientSecret`。

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "yourdomain.com",
    "TenantId": "your-tenant-id",
    "ClientId": "your-client-id",
    "ClientSecret": "your-client-secret"
  },
  "ApiSettings": {
    "BaseAddress": "https://your-protected-api.com",
    "ResourceId": "api://your-api-resource-id"
  }
}
```

#### 2. 代码实现

```csharp
using System;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;
using Microsoft.Extensions.Configuration;
using Microsoft.Identity.Client;

public class TokenService
{
    private readonly string _clientId;
    private readonly string _tenantId;
    private readonly string _clientSecret;
    private readonly string _authority;
    private readonly string _resourceId;
    private readonly HttpClient _httpClient;

    public TokenService(IConfiguration configuration)
    {
        _clientId = configuration["AzureAd:ClientId"];
        _tenantId = configuration["AzureAd:TenantId"];
        _clientSecret = configuration["AzureAd:ClientSecret"];
        _authority = $"{configuration["AzureAd:Instance"]}{_tenantId}";
        _resourceId = configuration["ApiSettings:ResourceId"];
        _httpClient = new HttpClient { BaseAddress = new Uri(configuration["ApiSettings:BaseAddress"]) };
    }

    public async Task<string> AcquireAccessTokenAsync()
    {
        var app = ConfidentialClientApplicationBuilder.Create(_clientId)
                    .WithClientSecret(_clientSecret)
                    .WithAuthority(new Uri(_authority))
                    .Build();

        string[] scopes = new string[] { $"{_resourceId}/.default" };

        try
        {
            var authResult = await app.AcquireTokenForClient(scopes).ExecuteAsync();
            Console.WriteLine("成功获取Access Token！");
            return authResult.AccessToken;
        }
        catch (MsalServiceException ex)
        {
            Console.WriteLine($"获取Access Token失败: {ex.Message}");
            return null;
        }
    }

    public async Task<string> AcquireIdTokenAsync()
    {
        var app = ConfidentialClientApplicationBuilder.Create(_clientId)
                    .WithClientSecret(_clientSecret)
                    .WithAuthority(new Uri(_authority))
                    .Build();

        try
        {
            var authResult = await app.AcquireTokenForClient(new string[] { "openid" }).ExecuteAsync();
            Console.WriteLine("成功获取ID Token！");
            return authResult.IdToken;
        }
        catch (MsalServiceException ex)
        {
            Console.WriteLine($"获取ID Token失败: {ex.Message}");
            return null;
        }
    }

    public async Task<string> AcquireNewAccessTokenWithRefreshTokenAsync(string refreshToken)
    {
        var app = ConfidentialClientApplicationBuilder.Create(_clientId)
                    .WithClientSecret(_clientSecret)
                    .WithAuthority(new Uri(_authority))
                    .Build();

        try
        {
            var authResult = await app.AcquireTokenByRefreshToken(new string[] { $"{_resourceId}/.default" }, refreshToken).ExecuteAsync();
            Console.WriteLine("成功获取新的Access Token！");
            return authResult.AccessToken;
        }
        catch (MsalServiceException ex)
        {
            Console.WriteLine($"使用Refresh Token获取新的Access Token失败: {ex.Message}");
            return null;
        }
    }

    public async Task CallProtectedApiAsync()
    {
        string accessToken = await AcquireAccessTokenAsync();

        if (!string.IsNullOrEmpty(accessToken))
        {
            _httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);

            try
            {
                var response = await _httpClient.GetAsync("/protected-endpoint");
                if (response.IsSuccessStatusCode)
                {
                    string content = await response.Content.ReadAsStringAsync();
                    Console.WriteLine($"受保护的数据: {content}");
                }
                else
                {
                    Console.WriteLine($"访问受保护的API失败: {response.StatusCode}");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"API调用出错: {ex.Message}");
            }
        }
    }
}

public class Program
{
    public static async Task Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .AddJsonFile("appsettings.json")
            .Build();

        var tokenService = new TokenService(config);

        // 获取ID Token
        await tokenService.AcquireIdTokenAsync();

        // 获取Access Token并调用受保护的API
        await tokenService.CallProtectedApiAsync();

        // 获取新的Access Token使用Refresh Token
        string refreshToken = "your-refresh-token"; // 这里示例假设已有Refresh Token
        await tokenService.AcquireNewAccessTokenWithRefreshTokenAsync(refreshToken);
    }
}
```

### 代码说明

- **`AcquireIdTokenAsync`**：获取ID Token，用于标识用户身份。
- **`AcquireAccessTokenAsync`**：获取Access Token，用于授权访问受保护资源。
- **`AcquireNewAccessTokenWithRefreshTokenAsync`**：使用Refresh Token获取新的Access Token。
- **`CallProtectedApiAsync`**：使用Access Token调用受保护的API。

---

### Mermaid类图

```mermaid
classDiagram
class TokenService {
    -string _clientId
    -string _tenantId
    -string _clientSecret
    -string _authority
    -string _resourceId
    -HttpClient _httpClient
    +TokenService(IConfiguration configuration)
    +AcquireAccessTokenAsync() Task~string~
    +AcquireIdTokenAsync() Task~string~
    +AcquireNewAccessTokenWithRefreshTokenAsync(refreshToken : string) Task~string~
    +CallProtectedApiAsync() Task
}

class Program {
    +Main(args : string[]) Task
}

TokenService --> HttpClient : 使用HTTP客户端
Program --> TokenService : 依赖
```

### 类图说明

- **TokenService**：主要的令牌服务类，包含与Azure AD交互的认证逻辑。
  - **AcquireAccessTokenAsync**：获取Access Token的方法。
  - **AcquireIdTokenAsync**：获取ID Token的方法。
  - **AcquireNewAccessTokenWithRefreshTokenAsync**：使用Refresh Token获取新的Access Token的方法。
  - **CallProtectedApiAsync**：使用Access Token调用受保护API的方法。

- **Program**：应用程序入口，通过`Main`方法实例化 `TokenService` 并调用其方法。

---

通过上面的C#代码示例和类图，展示了如何通过Azure AD获取ID Token、Access Token和Refresh Token，并使用这些令牌在应用中进行身份验证和授权。这种实现方式常用于需要保护的Web应用或API中，有助于确保安全性和用户体验。

---

以下是**ID Token**、**Access Token** 和 **Refresh Token** 的JWT（JSON Web Token）格式示例，每个示例都包含了典型的JWT结构，以帮助理解它们的内容和用途。每种令牌的结构基本相同，通常分为 **Header**、**Payload** 和 **Signature** 三部分。

---

### JWT 示例

JWT的标准格式如下：

```
[Header].[Payload].[Signature]
```

### 1. ID Token 示例

**ID Token** 是用于认证用户身份的令牌，包含用户的身份信息。它通常在登录过程之后发放，以确认用户的身份。

```plaintext
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkphbmUgRG9lIiwidXBuIjoiamFuZWRvZUBleGFtcGxlLmNvbSIsImlzcyI6Imh0dHBzOi8vbG9naW4uZXhhbXBsZS5jb20vIiwiYXVkIjoieW91ci1jbGllbnQtaWQiLCJpYXQiOjE1MTYyMzkwMjIsImV4cCI6MTUxNjI0MjYyMn0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

- **Header**：
  ```json
  {
    "alg": "RS256",
    "typ": "JWT"
  }
  ```

- **Payload**：
  ```json
  {
    "sub": "1234567890",                 // 用户ID
    "name": "Jane Doe",                  // 用户名称
    "upn": "janedoe@example.com",        // 用户主名称（例如邮箱）
    "iss": "https://login.example.com/", // 颁发者
    "aud": "your-client-id",             // 客户端ID
    "iat": 1516239022,                   // 令牌颁发时间
    "exp": 1516242622                    // 令牌过期时间
  }
  ```

- **Signature**：
  基于Header和Payload的签名部分，使用私钥和指定的算法生成。

### 2. Access Token 示例

**Access Token** 用于授权访问受保护的资源，通常包含用户的权限信息，并且不包含详细的身份信息。Access Token在OAuth2.0流程中用于资源服务器验证访问权限。

```plaintext
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwiYXVkIjoiYXBpOi8veW91ci1hcGktcmVzb3VyY2UtaWQiLCJpc3MiOiJodHRwczovL2xvZ2luLmV4YW1wbGUuY29tLyIsInJvbGVzIjpbInVzZXIiLCJhZG1pbiJdLCJzY29wZXMiOlsicmVhZCIsIndyaXRlIl0sImlhdCI6MTUxNjIzOTAyMiwiZXhwIjoxNTE2MjQyNjIyfQ.ZWQjPHTp0y0qK...ZkWtOxLXHYOlM
```

- **Header**：
  ```json
  {
    "alg": "RS256",
    "typ": "JWT"
  }
  ```

- **Payload**：
  ```json
  {
    "sub": "1234567890",                    // 用户ID
    "aud": "api://your-api-resource-id",    // API资源ID
    "iss": "https://login.example.com/",    // 颁发者
    "roles": ["user", "admin"],             // 用户角色
    "scopes": ["read", "write"],            // 访问权限范围
    "iat": 1516239022,                      // 令牌颁发时间
    "exp": 1516242622                       // 令牌过期时间
  }
  ```

- **Signature**：
  由Header和Payload生成的签名部分。

### 3. Refresh Token 示例

**Refresh Token** 是一个长效令牌，用于获取新的Access Token。当Access Token过期时，客户端可以使用Refresh Token来重新获取新的Access Token，而不需要重新登录。

**注意**：Refresh Token通常不采用JWT格式，以下是一个假设的示例，用于展示Refresh Token的基本结构。如果使用JWT格式，它可能会类似于以下内容。

```plaintext
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNzUwMjJ9.MEYCIQDC2azgY2qsk2ai5cEb_wuL9lQsEwhLomSkYmz6PnaEEwIhAPvGb1IYXZkfsduQZ7TtV4J5gXGFlqfEbQUHg-K4TnKn
```

- **Header**：
  ```json
  {
    "alg": "HS256",
    "typ": "JWT"
  }
  ```

- **Payload**：
  ```json
  {
    "sub": "1234567890",                    // 用户ID
    "iat": 1516239022,                      // 令牌颁发时间
    "exp": 1516275022                       // 令牌过期时间，通常比Access Token长
  }
  ```

- **Signature**：
  由Header和Payload生成的签名部分。

---

### JWT 总结

| 令牌类型       | 用途                                       | 包含的信息                                                |
| -------------- | ------------------------------------------ | --------------------------------------------------------- |
| **ID Token**   | 确认用户身份，通常在登录后发放               | 用户身份信息（`sub`、`name`、`upn`等）                     |
| **Access Token** | 授权访问受保护的API资源                    | 用户权限信息（`aud`、`roles`、`scopes`等）                 |
| **Refresh Token** | 用于获取新的Access Token，无需重新登录     | 用户ID和过期时间（一般没有具体的身份和权限信息）            |

### 注意事项

- **ID Token** 主要用于身份验证，一般不用于访问资源。
- **Access Token** 用于授权访问资源，并在请求API时提供授权。
- **Refresh Token** 应妥善保存，因为它可以在Access Token失效后获取新的Access Token。

这些示例展示了ID Token、Access Token 和 Refresh Token的典型结构以及它们包含的信息，帮助理解它们的用途和内容差异。

