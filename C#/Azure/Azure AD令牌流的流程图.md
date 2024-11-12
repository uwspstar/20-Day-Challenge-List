### Azure AD令牌流的流程图

此流程展示了客户端应用如何向Azure AD请求并获取访问令牌的过程。

```mermaid
flowchart TD
    Start[开始 - 客户端应用程序] -->|请求访问受保护的资源| ClientApp[客户端应用]
    ClientApp -->|向Azure AD发送身份验证请求| AzureAD[Azure AD]
    AzureAD -->|验证客户端凭据（ClientId, TenantId, ClientSecret）| AzureADValidation[验证]
    AzureADValidation -->|验证通过| Token[生成访问令牌 (Access Token)]
    AzureADValidation -->|验证失败| Error[返回错误信息]
    
    Token -->|返回访问令牌| ClientApp
    ClientApp -->|携带令牌访问API| ProtectedResource[受保护的API资源]
    ProtectedResource -->|验证令牌| TokenValidation[令牌验证]
    TokenValidation -->|令牌有效| Success[返回受保护数据]
    TokenValidation -->|令牌无效或过期| Unauthorized[拒绝访问]

    style Start fill:#d3e3fc,stroke:#333,stroke-width:1px;
    style ClientApp fill:#b3d4fc,stroke:#333,stroke-width:1px;
    style AzureAD fill:#a2c4f9,stroke:#333,stroke-width:1px;
    style AzureADValidation fill:#e3f2fd,stroke:#333,stroke-width:1px;
    style Token fill:#fdd835,stroke:#333,stroke-width:1px;
    style Error fill:#f8bbd0,stroke:#333,stroke-width:1px;
    style ProtectedResource fill:#c8e6c9,stroke:#333,stroke-width:1px;
    style TokenValidation fill:#dcedc8,stroke:#333,stroke-width:1px;
    style Success fill:#a5d6a7,stroke:#333,stroke-width:1px;
    style Unauthorized fill:#ffcdd2,stroke:#333,stroke-width:1px;
```

### 流程说明

1. **客户端应用程序发起请求**：客户端应用程序请求访问受保护的API资源。
2. **向Azure AD发送身份验证请求**：客户端应用向Azure AD请求访问令牌，传递`ClientId`、`TenantId`和`ClientSecret`等凭据。
3. **Azure AD验证凭据**：Azure AD验证客户端凭据，确保身份验证请求的合法性。
   - 如果验证成功，Azure AD生成并返回访问令牌。
   - 如果验证失败，返回错误信息。
4. **客户端获取令牌并访问受保护资源**：客户端应用携带令牌请求受保护的API资源。
5. **受保护资源验证令牌**：受保护的API验证访问令牌的有效性。
   - 如果令牌有效，返回受保护的数据。
   - 如果令牌无效或已过期，拒绝访问。

此流程图直观地展示了Azure AD身份验证和授权的令牌流，帮助理解Azure AD如何确保访问控制的安全性。
