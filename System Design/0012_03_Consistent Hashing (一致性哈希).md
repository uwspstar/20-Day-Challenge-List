### Consistent Hashing (一致性哈希)

**English**: Consistent hashing is a load balancing technique that allows uniform distribution of requests across servers.  
**Chinese**: 一致性哈希是一种负载均衡技术，能够在服务器之间均匀分配请求。

#### How It Works (工作原理)

**English**: In consistent hashing, requests are assigned to servers using a hash function and a ring-based structure.  
**Chinese**: 在一致性哈希中，使用哈希函数和环形结构将请求分配给服务器。

**English**: Each request has a unique identifier, such as an IP address or user ID, which is hashed and then mapped to the ring.  
**Chinese**: 每个请求都有一个唯一标识符，例如 IP 地址或用户 ID，该标识符被哈希并映射到环上。

**English**: If a server goes down, the requests it handled are reassigned to the next available server on the ring.  
**Chinese**: 如果某个服务器宕机，它处理的请求将重新分配给环上下一个可用的服务器。

---

#### **Consistent Hashing Example (一致性哈希示例)**

1. **Normal Hashing (普通哈希)**  
   **English**: With three servers (0, 1, 2), requests with IP addresses 6, 7, 8 are mapped as follows:  
   **Chinese**: 对于三台服务器（0、1、2），IP 地址为 6、7、8 的请求映射如下：  
   - 6 % 3 = 0 (Server 0)  
   - 7 % 3 = 1 (Server 1)  
   - 8 % 3 = 2 (Server 2)  

2. **Consistent Hashing (一致性哈希)**  
   **English**: In consistent hashing, servers are arranged on a ring, and requests are mapped to the nearest server.  
   **Chinese**: 在一致性哈希中，服务器按环状排列，请求被映射到最近的服务器。  

---

#### **Benefits of Consistent Hashing (一致性哈希的好处)**

1. **Consistent Mapping (一致映射)**  
   **English**: A specific IP address is always directed to the same server.  
   **Chinese**: 一个特定的 IP 地址总是指向同一个服务器。  
   **Example (示例)**: Users with the same IP are directed to the same cache server for efficiency.  
   **示例**：具有相同 IP 的用户总是指向同一个缓存服务器，以提高效率。  

2. **Minimal Disruption (最小干扰)**  
   **English**: If a server goes down, only the requests it handled are redistributed, minimizing the impact.  
   **Chinese**: 如果服务器宕机，只有它处理的请求会被重新分配，从而减少影响。  

3. **Load Distribution (负载分配)**  
   **English**: Requests are evenly distributed across servers, preventing overload.  
   **Chinese**: 请求在服务器之间均匀分配，防止过载。  

---

#### **Comparison Table: Normal Hashing vs. Consistent Hashing (对比表：普通哈希与一致性哈希)**

| **Method (方法)**       | **Normal Hashing (普通哈希)**                                           | **Consistent Hashing (一致性哈希)**                                    |
|------------------------|------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Server Failure (服务器宕机)** | Redistributes all requests when a server fails.                           | Only redistributes the requests of the failed server.                |
| **Mapping (映射)**      | Modulus operation maps requests to servers.                            | Hash function maps requests to servers based on ring structure.      |
| **Use Case (使用场景)** | Works well in smaller systems with fewer dynamic changes.               | Ideal for systems where servers can fail or be added dynamically.    |

---

#### **Code Example (代码示例)**

```python
# Python example of consistent hashing
class ConsistentHashing:
    def __init__(self, servers):
        self.servers = sorted(servers)
    
    def get_server(self, request_hash):
        for server in self.servers:
            if request_hash <= server:
                return server
        return self.servers[0]

# Example usage
servers = [0, 120, 240]
hashing = ConsistentHashing(servers)

# Request hash
request_hash = 180
assigned_server = hashing.get_server(request_hash)
print(f"Request is assigned to server: {assigned_server}")
```

**English**: In this Python code, a list of servers is created and sorted. The request hash is used to determine the next available server on the ring.  
**Chinese**: 在此 Python 代码中，创建并排序服务器列表。请求哈希用于确定环上下一个可用的服务器。

---

#### **5 Interview Questions with Answers (5 个面试问题与答案)**

1. **What is consistent hashing? (什么是一致性哈希？)**  
   **Answer (答案)**: Consistent hashing is a technique for distributing requests across servers in a way that minimizes disruption when servers are added or removed.  
   一致性哈希是一种负载均衡技术，可以在添加或移除服务器时尽量减少对请求分配的干扰。

2. **How does consistent hashing work? (一致性哈希如何工作？)**  
   **Answer (答案)**: It maps requests to servers using a ring-based structure. If a server fails, requests are reassigned to the next available server in a clockwise direction.  
   它使用环形结构将请求映射到服务器。如果服务器故障，请求将重新分配给顺时针方向上的下一个可用服务器。

3. **What is the problem with regular hashing in load balancing? (普通哈希在负载均衡中的问题是什么？)**  
   **Answer (答案)**: When a server goes down, regular hashing requires all requests to be redistributed, leading to cache misses.  
   当服务器宕机时，普通哈希需要重新分配所有请求，导致缓存未命中。

4. **Why is consistent hashing useful for CDNs? (一致性哈希为什么对 CDN 有用？)**  
   **Answer (答案)**: It ensures users are consistently routed to the same cache server, improving performance and reducing latency.  
   它确保用户始终路由到同一个缓存服务器，从而提高性能并减少延迟。

5. **What are the advantages of consistent hashing over round-robin? (一致性哈希相比轮询的优势是什么？)**  
   **Answer (答案)**: Consistent hashing is better for maintaining cache consistency, especially when servers frequently go down or are added.  
   一致性哈希在维护缓存一致性方面更好，尤其是在服务器频繁宕机或添加时。

---

### Summary (总结)

**English**: Consistent hashing ensures that requests are evenly distributed across servers and minimizes disruption when servers go down.  
**Chinese**: 一致性哈希确保请求均匀分布在服务器之间，并在服务器宕机时将干扰降到最低。

**English**: It is ideal for distributed systems like CDNs and databases that require consistent routing of user requests.  
**Chinese**: 它非常适合需要一致请求路由的分布式系统，如 CDN 和数据库。
