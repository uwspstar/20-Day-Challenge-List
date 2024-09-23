# How to Approach

### 1. **Functional Requirements** (功能需求)

Functional requirements describe what the system should do. In a system design interview, you must thoroughly understand the system's core features and how users will interact with it.

**功能需求** 描述了系统应该做什么。在系统设计面试中，你必须彻底了解系统的核心功能以及用户将如何与其交互。

#### Approach (步骤):
- **Identify Core Features (识别核心功能)**: What are the main actions users can perform? For example, in a URL shortening service, the core functionality would be shortening a URL, storing it, and redirecting the user when they use the shortened link.
  - **识别核心功能**：用户可以执行的主要操作是什么？例如，在URL缩短服务中，核心功能是缩短URL、存储它，并在用户使用缩短链接时重定向。
  
- **Define User Interactions (定义用户交互)**: Clearly outline how users will use the service. For example, will they need to log in, upload files, or retrieve data?
  - **定义用户交互**：明确用户如何使用服务。例如，他们是否需要登录、上传文件或检索数据？

- **Examples**:
  - URL shortening: Create and store shortened URLs, retrieve original URLs, manage expired links.
  - 文件上传：提供文件上传、下载功能，并支持文件版本控制。

---

### 2. **Non-Functional Requirements** (非功能需求)

Non-functional requirements define system attributes such as reliability, performance, scalability, and security. These requirements are often just as important as functional ones because they determine how the system performs under different conditions.

**非功能需求** 定义了系统的属性，例如可靠性、性能、可扩展性和安全性。这些需求往往和功能需求一样重要，因为它们决定了系统在不同条件下的表现。

#### Approach (步骤):
- **Scalability (可扩展性)**: Determine how the system will scale as the number of users or the amount of data grows. Will the system handle millions of users or terabytes of data?
  - **可扩展性**：确定系统如何随着用户数量或数据量的增长而扩展。系统能否处理数百万用户或数TB数据？
  
- **Performance (性能)**: How fast should the system respond? What is the acceptable latency for end-users? For example, users might expect near-instantaneous URL redirection or quick file uploads.
  - **性能**：系统的响应速度应该有多快？对终端用户来说，接受的延迟是多少？例如，用户可能期望URL重定向几乎是即时的，或文件上传速度很快。
  
- **Reliability (可靠性)**: Ensure that the system can continue functioning even if certain components fail. For instance, if one server goes down, the system should automatically failover to another without downtime.
  - **可靠性**：确保系统即使在某些组件故障时也能继续运行。例如，如果一台服务器宕机，系统应自动切换到另一台服务器而不影响服务。

- **Security (安全性)**: How will sensitive data be handled? For example, ensuring encrypted storage and communication of sensitive information such as passwords or personal data.
  - **安全性**：如何处理敏感数据？例如，确保加密存储和传输敏感信息（如密码或个人数据）。

---

### 3. **Daily Active Users (DAU)** (每日活跃用户)

Daily Active Users (DAU) is a key metric used to understand the scale and usage of a system. Designing a system that can efficiently handle the expected DAU helps ensure good performance and reliability.

**每日活跃用户 (DAU)** 是用于了解系统规模和使用情况的关键指标。设计一个能够有效处理预期DAU的系统有助于确保性能和可靠性。

#### Approach (步骤):
- **Estimate Traffic (估算流量)**: Based on the DAU, estimate how many requests the system will need to handle. For example, if the system has 1 million DAU, how many API calls per second will the system need to process?
  - **估算流量**：根据DAU，估算系统需要处理的请求数量。例如，如果系统有100万DAU，系统每秒需要处理多少API调用？
  
- **Peak vs. Average Load (峰值 vs. 平均负载)**: Determine both the average and peak traffic. Systems must be designed to handle spikes in usage (e.g., during a sale or event).
  - **峰值 vs. 平均负载**：确定平均流量和峰值流量。系统必须设计成能够应对使用高峰（例如在促销或活动期间）。

- **Horizontal Scalability (水平扩展性)**: Implement strategies such as load balancing and auto-scaling to dynamically allocate resources based on the DAU.
  - **水平扩展性**：实现负载均衡和自动扩展等策略，根据DAU动态分配资源。

- **Examples**:
  - A social media platform with 10 million DAU must handle billions of likes, comments, and posts each day.
  - 一个拥有1000万DAU的社交媒体平台必须每天处理数十亿次点赞、评论和帖子。

---

### 4. **Storage Design** (存储设计)

Storage design in system architecture refers to how data is stored, retrieved, and managed. Depending on the size of the data and the frequency of access, different storage strategies can be employed.

系统架构中的存储设计涉及如何存储、检索和管理数据。根据数据的大小和访问频率，可以采用不同的存储策略。

#### Approach (步骤):
- **Database Selection (数据库选择)**: Decide whether to use a relational database (e.g., MySQL, PostgreSQL) for structured data or a NoSQL solution (e.g., MongoDB, Cassandra) for unstructured or semi-structured data.
  - **数据库选择**：决定是使用关系型数据库（如MySQL，PostgreSQL）处理结构化数据，还是使用NoSQL解决方案（如MongoDB，Cassandra）处理非结构化或半结构化数据。
  
- **Data Partitioning (数据分区)**: Implement sharding or partitioning strategies for horizontal scaling. Sharding splits the data into smaller, manageable chunks that can be distributed across multiple servers.
  - **数据分区**：实现分片或分区策略进行水平扩展。分片将数据分成较小的可管理块，可以分布在多个服务器上。
  
- **Caching (缓存)**: Use caching mechanisms such as Redis or Memcached to store frequently accessed data in-memory, reducing database load.
  - **缓存**：使用如Redis或Memcached等缓存机制，将频繁访问的数据存储在内存中，减少数据库负载。

- **Backup and Recovery (备份和恢复)**: Ensure that there are backup strategies in place to recover data in case of data loss or corruption.
  - **备份和恢复**：确保有备份策略，以便在数据丢失或损坏的情况下恢复数据。

---

### 5. **Handling Traffic and Load Balancing** (处理流量与负载均衡)

Handling traffic effectively is crucial for ensuring a system's reliability and availability. Load balancing distributes incoming traffic across multiple servers to prevent any one server from becoming a bottleneck.

有效处理流量对于确保系统的可靠性和可用性至关重要。负载均衡将传入流量分配到多个服务器，以防止任何一台服务器成为瓶颈。

#### Approach (步骤):
- **Load Balancers (负载均衡器)**: Use load balancers to distribute traffic evenly across servers. Common solutions include NGINX, HAProxy, or cloud-based services like AWS Elastic Load Balancing.
  - **负载均衡器**：使用负载均衡器将流量均匀分配到服务器上。常见的解决方案包括NGINX、HAProxy或基于云的服务如AWS Elastic Load Balancing。
  
- **Auto-Scaling (自动扩展)**: Use auto-scaling to dynamically add or remove servers based on real-time traffic demands. For example, during high traffic periods, additional servers can be spun up automatically.
  - **自动扩展**：使用自动扩展根据实时流量需求动态添加或删除服务器。例如，在高流量时段，系统可以自动启动额外的服务器。
  
- **Failover Mechanisms (故障切换机制)**: Implement failover mechanisms to ensure that if one server goes down, another server can take over without downtime.
  - **故障切换机制**：实现故障切换机制，以确保当一台服务器宕机时，另一台服务器可以接管而不影响运行。

---

### 6. **Security Considerations** (安全考虑)

Security is essential in system design, especially when handling sensitive data like user credentials, financial transactions, or personal information.

安全在系统设计中至关重要，特别是在处理用户凭证、金融交易或个人信息等敏感数据时。

#### Approach (步骤):
- **Data Encryption (数据加密)**: Encrypt sensitive data both at rest (in storage) and in transit (during communication). Use encryption algorithms such as AES for data storage and TLS/SSL for communication.
  - **数据加

密**：对静态数据（存储中的数据）和传输中的数据进行加密。使用AES等加密算法存储数据，并使用TLS/SSL加密通信。
  
- **Authentication and Authorization (认证与授权)**: Implement strong authentication (e.g., OAuth, JWT) to verify users' identities, and use role-based access control (RBAC) to enforce proper authorization.
  - **认证与授权**：实施强认证（如OAuth，JWT）以验证用户身份，并使用基于角色的访问控制（RBAC）来强制执行适当的授权。
  
- **Rate Limiting (速率限制)**: Implement rate limiting to prevent Denial of Service (DoS) attacks, where a malicious actor overwhelms the system with excessive requests.
  - **速率限制**：实施速率限制，防止拒绝服务（DoS）攻击，恶意用户通过过多的请求压垮系统。
