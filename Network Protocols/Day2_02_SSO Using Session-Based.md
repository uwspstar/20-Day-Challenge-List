### SSO Using Session-Based

The image illustrates how Single Sign-On (SSO) works, focusing on a centralized authentication system that allows users to log in once and gain access to multiple related systems.

#### 1. User Login (用户登录)
- The user logs into the authentication center with their credentials.
- **用户使用其凭据登录认证中心。**

#### 2. Session Creation (会话创建)
- Upon successful login, the authentication center creates a session and generates a session ID (`sid`), storing it along with the user's identity information.
- **登录成功后，认证中心创建会话并生成会话ID (`sid`)，并将其与用户身份信息一起存储。**

#### 3. Cookie Storage (Cookie存储)
- The session ID (`sid`) is sent back to the user's browser in the form of a cookie.
- **会话ID (`sid`) 以Cookie的形式发送回用户的浏览器。**

#### 4. Accessing Subsystem A (访问子系统A)
- The user attempts to access protected resources on Subsystem A, and the cookie (`sid`) is automatically sent with the request.
- **用户尝试访问子系统A上的受保护资源，Cookie (`sid`) 会自动随请求发送。**

#### 5. Session Validation (会话验证)
- Subsystem A sends the `sid` to the authentication center to validate whether the session is still active.
- **子系统A将 `sid` 发送到认证中心，验证会话是否仍然有效。**

#### 6. Access Granted (访问授权)
- If the session is valid, Subsystem A grants the user access to the requested resources.
- **如果会话有效，子系统A授予用户对请求资源的访问权限。**

#### 7. Accessing Subsystem B (访问子系统B)
- When the user accesses Subsystem B, the same `sid` in the cookie is used for authentication, and the process repeats.
- **当用户访问子系统B时，相同的 `sid` 会在Cookie中用于认证，过程重复。**

### Tips and Warnings (提示与警告)

- **Tip**: Ensure that your session IDs (`sid`) are securely generated and transmitted over HTTPS to prevent session hijacking.
- **提示**: 确保您的会话ID (`sid`) 安全生成并通过HTTPS传输，以防止会话劫持。

- **Warning**: If the session is not managed correctly, it can lead to security vulnerabilities, such as unauthorized access.
- **警告**: 如果会话管理不当，可能导致安全漏洞，例如未经授权的访问。

### The 5Ws of SSO (SSO的5W)

- **Who (谁)**: Organizations that want to provide seamless access to multiple systems for their users.
- **谁**: 希望为用户提供无缝访问多个系统的组织。

- **What (什么)**: SSO allows users to log in once and access multiple related systems without needing to log in again.
- **什么**: SSO允许用户登录一次，访问多个相关系统，而无需再次登录。

- **When (何时)**: Typically used in environments with multiple interrelated systems, such as enterprise software suites.
- **何时**: 通常在具有多个相关系统的环境中使用，如企业软件套件。

- **Where (哪里)**: Across web-based applications, intranets, and cloud services that are part of the same authentication domain.
- **哪里**: 在同一认证域中的基于网络的应用程序、内部网和云服务中。

- **Why (为什么)**: To improve user experience by reducing the number of logins required and to centralize authentication management.
- **为什么**: 通过减少所需的登录次数并集中认证管理来改善用户体验。

### Conclusion (结论)
SSO streamlines the authentication process, allowing users to access multiple systems with a single login. By centralizing session management, organizations can enhance security while simplifying the user experience.

SSO简化了认证过程，使用户能够通过一次登录访问多个系统。通过集中会话管理，组织可以在简化用户体验的同时增强安全性。

- [Understanding and Comparing Two SSO Methods: Session-Based vs. Token-Based Authentication](https://codebitwave.com/security-101-understanding-and-comparing-two-sso-methods-session-based-vs-token-based-authentication/)
