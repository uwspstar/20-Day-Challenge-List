### SSO Using Token-Based Authentication

The image illustrates the second method of implementing Single Sign-On (SSO) using token-based authentication. Here’s how it works:

#### Step-by-Step Process:

1. **User Login (用户登录)**:
   - The user logs in to the authentication center using their credentials.
   - **用户使用其凭据登录认证中心。**

2. **Token Issuance (令牌签发)**:
   - Upon successful authentication, the authentication center issues a token, which contains encoded user identity information.
   - **认证成功后，认证中心签发一个包含用户身份信息的加密令牌。**

3. **Token Storage (令牌存储)**:
   - The token is sent back to the user's browser and stored, usually in local storage or as a cookie.
   - **令牌被发送回用户的浏览器并存储，通常在本地存储或作为Cookie存储。**

4. **Accessing Subsystems (访问子系统)**:
   - When accessing protected resources on any subsystem (e.g., Subsystem A or B), the stored token is automatically sent with the request.
   - **在访问任何子系统（如子系统A或B）上的受保护资源时，存储的令牌会自动随请求发送。**

5. **Token Validation (令牌验证)**:
   - The subsystem verifies the token by decoding it and checking the validity. If valid, access to the requested resource is granted.
   - **子系统通过解码并检查令牌的有效性来验证令牌。如果有效，则授予对请求资源的访问权限。**

### Tips and Warnings (提示与警告):

- **Tip**: Tokens are usually short-lived and should be securely stored and transmitted over HTTPS.
- **提示**: 令牌通常是短期有效的，应该安全存储并通过HTTPS传输。

- **Warning**: Token misuse or interception can lead to unauthorized access, so always implement secure storage practices.
- **警告**: 令牌滥用或拦截可能导致未经授权的访问，因此始终实施安全存储实践。

### The 5Ws of Token-Based SSO (基于令牌的SSO的5W):

- **Who (谁)**: Organizations looking to implement a scalable and secure SSO mechanism.
- **谁**: 希望实施可扩展且安全的SSO机制的组织。

- **What (什么)**: Token-based authentication allows users to access multiple systems using a single token issued after login.
- **什么**: 基于令牌的认证允许用户在登录后使用一个令牌访问多个系统。

- **When (何时)**: Typically used in modern web applications and APIs to manage authentication across multiple services.
- **何时**: 通常在现代Web应用程序和API中使用，以管理多个服务之间的认证。

- **Where (哪里)**: Across systems that require seamless access control with minimal user input after the initial login.
- **哪里**: 在需要最小用户输入即可实现无缝访问控制的系统中。

- **Why (为什么)**: To enhance user experience by reducing the need for multiple logins and to centralize authentication management.
- **为什么**: 通过减少多次登录的需求并集中管理认证，以提升用户体验。 

### Conclusion (结论)
Token-based SSO provides a secure and scalable solution for managing user authentication across multiple systems, offering both convenience and security for modern applications.

基于令牌的SSO为管理多个系统间的用户认证提供了一种安全且可扩展的解决方案，为现代应用程序提供了便利和安全。

- [Understanding and Comparing Two SSO Methods: Session-Based vs. Token-Based Authentication](https://codebitwave.com/security-101-understanding-and-comparing-two-sso-methods-session-based-vs-token-based-authentication/)
