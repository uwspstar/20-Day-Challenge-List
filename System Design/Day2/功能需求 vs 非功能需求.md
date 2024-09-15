### 功能需求 vs 非功能需求 (Functional vs. Non-Functional Requirements)

#### 1. **5Ws（五个关键问题）**

- **What are Functional Requirements?**  
  **English:** Functional requirements define the specific behavior or functions the system must perform, such as user authentication, data retrieval, or transaction processing.  
  **Chinese:** 功能需求定义了系统必须执行的具体行为或功能，如用户认证、数据检索或事务处理。

- **What are Non-Functional Requirements?**  
  **English:** Non-functional requirements specify the system's operational qualities, like performance, security, scalability, and usability.  
  **Chinese:** 非功能需求规定了系统的操作特性，如性能、安全性、可扩展性和可用性。

- **Why is it Important to Differentiate Between Them?**  
  **English:** Clearly separating functional and non-functional requirements helps ensure that the system meets both the user's needs and operational standards.  
  **Chinese:** 明确区分功能需求和非功能需求有助于确保系统既满足用户需求，又符合操作标准。

- **Who Defines Functional and Non-Functional Requirements?**  
  **English:** Functional requirements are usually defined by business stakeholders, while non-functional requirements are often set by architects or system administrators.  
  **Chinese:** 功能需求通常由业务相关方定义，而非功能需求则由架构师或系统管理员设定。

- **Where Do These Requirements Apply?**  
  **English:** Both functional and non-functional requirements apply across all parts of a system, from the user interface to the backend infrastructure.  
  **Chinese:** 功能需求和非功能需求都适用于系统的各个部分，从用户界面到后端基础设施。

#### 2. **Comparison（比较）**

| **Aspect**               | **Functional Requirements**                           | **Non-Functional Requirements**                          |
|--------------------------|-------------------------------------------------------|----------------------------------------------------------|
| **Definition**            | Defines what the system should do                     | Defines how the system performs                          |
| **Example**               | User can login, view profile, process payment         | System must handle 1,000 requests per second              |
| **Objective**             | Ensures functionality works correctly                 | Ensures system meets performance, security, and scalability |
| **Stakeholders**          | Business analysts, product managers                   | System architects, DevOps, security teams                 |
| **Measurability**         | Often pass/fail based on specific features             | Measured by performance metrics, response time, etc.      |

#### 3. **Tips (技巧)**

- **Clarify Early:**  
  **English:** Define both functional and non-functional requirements early to avoid miscommunication and mismatched expectations.  
  **Chinese:** 及早明确功能需求和非功能需求，避免沟通不畅和期望不一致。

- **Balance Focus:**  
  **English:** Don't over-prioritize functional requirements at the expense of non-functional ones, especially in large-scale systems.  
  **Chinese:** 不要过分优先考虑功能需求而忽视非功能需求，尤其是在大规模系统中。

- **Use Clear Metrics:**  
  **English:** Ensure non-functional requirements are measurable with clear metrics (e.g., latency < 200ms).  
  **Chinese:** 确保非功能需求可以通过明确的指标来衡量（例如，延迟小于200毫秒）。

#### 4. **Warnings (警告)**

- **Neglecting Non-Functional Requirements:**  
  **English:** Ignoring non-functional requirements such as security and performance can lead to system instability or security vulnerabilities.  
  **Chinese:** 忽视非功能需求（如安全性和性能）可能导致系统不稳定或存在安全漏洞。

- **Vague Requirements:**  
  **English:** Vague or ambiguous non-functional requirements (e.g., "the system should be fast") can create confusion during implementation.  
  **Chinese:** 含糊或模棱两可的非功能需求（如“系统应快速”）可能会在实施过程中造成混乱。

#### 5. **Interview Questions（面试问题）**

1. **What is the difference between functional and non-functional requirements?**  
   - **English Answer:** Functional requirements describe what the system should do, such as user registration or data storage, while non-functional requirements describe how the system performs, like response time and security.  
   - **Chinese Answer:** 功能需求描述系统应做什么，如用户注册或数据存储，而非功能需求描述系统的性能，如响应时间和安全性。

2. **Can you provide examples of non-functional requirements?**  
   - **English Answer:** Non-functional requirements include system performance, reliability, scalability, and security, such as ensuring the system handles 10,000 concurrent users.  
   - **Chinese Answer:** 非功能需求包括系统性能、可靠性、可扩展性和安全性，例如确保系统可以处理1万名并发用户。

3. **How do you prioritize functional vs. non-functional requirements?**  
   - **English Answer:** Functional requirements are usually prioritized first to ensure the system works as intended, but non-functional requirements are essential for user experience and long-term stability.  
   - **Chinese Answer:** 功能需求通常优先，以确保系统按预期工作，但非功能需求对于用户体验和系统的长期稳定性至关重要。

4. **What happens if non-functional requirements are not met?**  
   - **English Answer:** If non-functional requirements are not met, the system may become slow, insecure, or unable to scale, leading to user dissatisfaction or system failure.  
   - **Chinese Answer:** 如果未满足非功能需求，系统可能变得缓慢、不安全或无法扩展，导致用户不满或系统故障。

5. **How do you measure non-functional requirements?**  
   - **English Answer:** Non-functional requirements are measured through performance metrics such as latency, throughput, availability, and security testing.  
   - **Chinese Answer:** 非功能需求通过性能指标进行衡量，如延迟、吞吐量、可用性和安全测试。

#### 6. **Summary（总结）**

- **English:** Functional requirements define what a system should do, while non-functional requirements outline how the system performs. Both are critical for a successful system, ensuring not only that it functions correctly but also that it operates efficiently, securely, and reliably. Balancing these requirements is key to creating scalable, maintainable systems.  
- **Chinese:** 功能需求定义了系统应该做什么，而非功能需求则规定了系统的性能。两者对于系统的成功至关重要，不仅确保系统正常工作，还确保其高效、安全和可靠地运行。平衡这些需求是构建可扩展、可维护系统的关键。
