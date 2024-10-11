
# Distributed System Design

---

| #  | Topic (主题)               | Notes (备注)                                     |
|----|----------------------------|-------------------------------------------------|
| 1  | Image/video sharing app (图片/视频分享应用)  | - Instagram (Instagram)                         |
|    |                            | - Pinterest (Pinterest)                         |
| 2  | Chat/messenger app (聊天/消息应用)         | - Whatsapp (Whatsapp)                          |
| 3  | Url shortener (短网址)                    | - Tiny URL (Tiny URL)                          |
| 4  | News Feed (新闻 Feed)                   | - Facebook (Facebook)                          |
|    |                            | - Instagram user and home timelines (Instagram 用户和主页时间线) |
| 5  | Notification system (通知系统)             | - Sending social media updates to users (向用户发送社交媒体更新) |

---

| #  | Topic (主题)                                         | Notes (备注)                                                                                             |
|----|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| 1  | Introduction to Distributed Systems (分布式系统介绍) | - Definition and characteristics of distributed systems (分布式系统的定义和特征)                             |
|    |                                                     | - Common use cases and challenges (常见用例和挑战)                                                        |
|    |                                                     | - Examples of distributed systems (e.g., microservices, databases) (分布式系统的例子，例如：微服务，数据库)     |
| 2  | CAP Theorem (CAP 定理)                             | - Understanding consistency, availability, and partition tolerance (理解一致性、可用性和分区容忍性)            |
|    |                                                     | - Trade-offs in distributed systems (分布式系统中的权衡)                                                  |
|    |                                                     | - Examples of systems prioritizing different aspects of CAP (优先考虑CAP不同方面的系统示例)                 |
| 3  | Distributed System Architectures (分布式系统架构)   | - Client-server vs. peer-to-peer (客户端-服务器与对等网络)                                                |
|    |                                                     | - Service-oriented architecture (SOA) and microservices (面向服务的架构和微服务)                          |
|    |                                                     | - Event-driven architecture (EDA) (事件驱动架构)                                                         |
|    |                                                     | - Data flow and pipeline architectures (数据流和管道架构)                                                |
| 4  | Data Replication (数据复制)                         | - Synchronous vs. asynchronous replication (同步与异步复制)                                               |
|    |                                                     | - Conflict resolution in data replication (数据复制中的冲突解决)                                          |
|    |                                                     | - Data consistency models (eventual consistency, strong consistency) (数据一致性模型：最终一致性、强一致性)  |
| 5  | Distributed Consensus Algorithms (分布式共识算法)   | - Paxos, Raft, and other consensus protocols (Paxos、Raft及其他共识协议)                                 |
|    |                                                     | - Byzantine fault tolerance (BFT) (拜占庭容错)                                                           |
|    |                                                     | - Leader election algorithms (领导者选举算法)                                                            |
| 6  | Fault Tolerance & Reliability (容错与可靠性)         | - Failure models and handling failure in distributed systems (分布式系统中的故障模型和故障处理)             |
|    |                                                     | - Redundancy and replication for fault tolerance (容错的冗余和复制)                                        |
|    |                                                     | - Checkpointing and logging strategies (检查点和日志策略)                                               |
| 7  | Scalability (可扩展性)                             | - Horizontal vs. vertical scaling (横向与纵向扩展)                                                        |
|    |                                                     | - Load balancing strategies (负载均衡策略)                                                               |
|    |                                                     | - Sharding and partitioning (分片与分区)                                                                 |
|    |                                                     | - Elastic scaling (弹性扩展)                                                                             |
| 8  | Distributed Data Stores (分布式数据存储)           | - NoSQL databases (e.g., Cassandra, MongoDB) (NoSQL数据库，例如：Cassandra，MongoDB)                      |
|    |                                                     | - Distributed file systems (e.g., HDFS, Google File System) (分布式文件系统，例如：HDFS，谷歌文件系统)     |
|    |                                                     | - Consistent hashing and its role in distributed databases (一致性哈希及其在分布式数据库中的作用)           |
| 9  | Coordination Services (协调服务)                   | - ZooKeeper, etcd, and other coordination systems (ZooKeeper，etcd及其他协调系统)                        |
|    |                                                     | - Leader election, configuration management, and synchronization (领导者选举、配置管理和同步)              |
|    |                                                     | - Service discovery in distributed environments (分布式环境中的服务发现)                                   |
| 10 | Concurrency and Synchronization (并发与同步)         | - Multithreading and concurrency models in distributed systems (分布式系统中的多线程与并发模型)            |
|    |                                                     | - Locks, semaphores, and other synchronization primitives (锁、信号量及其他同步原语)                       |
|    |                                                     | - Deadlocks and how to avoid them (死锁及其避免方法)                                                      |
| 11 | Networking Basics (网络基础)                       | - TCP/IP, UDP, and sockets (TCP/IP、UDP和套接字)                                                         |
|    |                                                     | - Message passing and RPC (Remote Procedure Call) (消息传递与RPC（远程过程调用）)                          |
|    |                                                     | - Network partitions and their impact on distributed systems (网络分区及其对分布式系统的影响)                 |
| 12 | Messaging Systems (消息系统)                        | - Message queues (e.g., RabbitMQ, Kafka) (消息队列，例如：RabbitMQ，Kafka)                             |
|    |                                                     | - Event streaming and pub/sub systems (事件流和发布/订阅系统)                                           |
|    |                                                     | - Idempotency and delivery guarantees (at-least-once, exactly-once) (幂等性与投递保证（至少一次，准确一次）) |
| 13 | Security in Distributed Systems (分布式系统的安全性) | - Encryption, authentication, and authorization mechanisms (加密、身份验证和授权机制)                     |
|    |                                                     | - Public key infrastructure (PKI) and SSL/TLS (公钥基础设施（PKI）和SSL/TLS)                             |
|    |                                                     | - Handling secure communication between distributed components (处理分布式组件之间的安全通信)                |
| 14 | Consistency Models (一致性模型)                     | - Strong, eventual, and causal consistency (强一致性、最终一致性和因果一致性)                           |
|    |                                                     | - Quorum-based approaches (基于法定人数的方法)                                                         |
|    |                                                     | - Read and write consistency in distributed databases (分布式数据库中的读写一致性)                         |
| 15 | Distributed Transactions (分布式事务)                | - Two-phase commit (2PC) and three-phase commit (3PC) (两阶段提交（2PC）和三阶段提交（3PC）)            |
|    |                                                     | - Distributed transaction coordinators (分布式事务协调者)                                              |
|    |                                                     | - Saga pattern for long-running transactions (长时间运行事务的Saga模式)                                   |
| 16 | Time and Ordering (时间与顺序)                     | - Logical clocks (e.g., Lamport clocks) (逻辑时钟，例如：Lamport时钟)                                    |
|    |                                                     | - Vector clocks and their use in conflict resolution (向量时钟及其在冲突解决中的应用)                      |
|    |                                                     | - Global time synchronization challenges (NTP, GPS) (全球时间同步的挑战（NTP，GPS）)                      |
| 17 | Load Balancing and Reverse Proxy (负载均衡与反向代理) | - Types of load balancers (software vs. hardware) (负载均衡器的类型（软件与硬件）)                      |
|    |                                                     | - Load balancing algorithms (round-robin, least connections) (负载均衡算法（轮询，最少连接）)             |
|    |                                                     | - Reverse proxy and its role in distributed systems (反向代理及其在分布式系统中的作用)                    |
| 18 | Service Discovery (服务发现)                         | - Static vs. dynamic service discovery (静态与动态服务发现)                                            |
|    |                                                     | - Service discovery tools (e.g., Consul, Eureka) (服务发现工具，例如：Consul，Eureka)                    |
|    |                                                     | - Challenges and strategies in service discovery in dynamic environments (动态环境中服务发现的挑战与策略)   |
| 19 | Caching in Distributed Systems (分布式系统中的缓存)  | - Distributed cache solutions (e.g., Redis, Memcached) (分布式缓存解决方案，例如：Redis，Memcached)       |
|    |                                                     | - Cache invalidation strategies (缓存失效策略)                                                          |
|    |                                                     | - Handling cache consistency in distributed systems (处理分布式系统中的缓存一致性)                       |
| 20 | Eventual Consistency & Conflict Resolution (最终一致性与冲突解决) | - Types of conflicts (e.g., read-write, write-write) (冲突类型，例如：读写，写写)                  |
|    |                                                     | - Vector clocks and causal consistency (向量时钟和因果一致性)                                         |
|    |                                                     | - CRDTs (Conflict-free Replicated Data Types) (CRDT（冲突自由复制数据类型）)                            |
| 21 | Monitoring and Observability (监控与可观测性)       | - Logging, metrics, and tracing in distributed systems (分布式系统中的日志、指标和追踪)                   |
|    |                                                     | - Distributed tracing tools (e.g., Jaeger, Zipkin) (分布式追踪工具，例如：Jaeger，Zipkin)              |
|    |                                                     | - Centralized logging systems (集中式日志系统)                                                          |
| 22 | Distributed Scheduling Systems (分布式调度系统)      | - Distributed cron jobs and task scheduling (分布式定时任务和任务调度)                                  |
|    |                                                     | - Tools like Apache Airflow, Kubernetes CronJobs (如Apache Airflow、Kubernetes CronJobs的工具)          |
|    |                                                     | - Distributed job management strategies (分布式作业管理策略)                                          |
| 23 | Geo-Distributed Systems (地理分布式系统)           | - Cross-data center replication (跨数据中心复制)                                                         |
|    |                                                     | - Handling network latency and failures across regions (处理跨区域的网络延迟和故障)                       |
|    |                                                     | - Designing systems for multiple geographic locations (为多个地理位置设计系统)                           |
| 24 | Microservices Design (微服务设计)                    | - Communication patterns (synchronous vs. asynchronous) (通信模式（同步与异步）)                         |
|    |                                                     | - Service decomposition and domain-driven design (服务分解与领域驱动设计)                               |
|    |                                                     | - API Gateway patterns and sidecars (e.g., Istio) (API网关模式和边车（例如：Istio）)                    |
| 25 | Distributed Search and Indexing (分布式搜索与索引)  | - Distributed search engines (e.g., Elasticsearch, Solr) (分布式搜索引擎，例如：Elasticsearch，Solr)    |
|    |                                                     | - Index sharding and replication (索引分片与复制)                                                       |
|    |                                                     | - Search consistency and fault tolerance (搜索一致性与容错)                                             |
| 26 | Cloud-native Distributed Systems (云原生分布式系统)  | - Design principles for cloud-native applications (云原生应用的设计原则)                                 |
|    |                                                     | - Kubernetes and container orchestration (Kubernetes和容器编排)                                        |
|    |                                                     | - Service meshes (e.g., Istio, Linkerd) (服务网格（例如：Istio，Linkerd）)                             |
| 27 | Testing and Debugging Distributed Systems (分布式系统的测试与调试) | - Unit testing, integration testing, and chaos engineering (单元测试、集成测试和混沌工程)          |
|    |                                                     | - Debugging in distributed environments (在分布式环境中的调试)                                          |
|    |                                                     | - Fault injection techniques and tools (e.g., Chaos Monkey) (故障注入技术和工具（例如：Chaos Monkey）)   |
| 28 | Serverless Architectures (无服务器架构)               | - Understanding FaaS (Function as a Service) and BaaS (Backend as a Service) (理解FaaS（功能即服务）和BaaS（后端即服务）) |
|    |                                                     | - Benefits and challenges of serverless (无服务器的好处与挑战)                                          |
|    |                                                     | - Scaling and orchestration of serverless functions (无服务器函数的扩展与编排)                           |
 

---

### 1. **Introduction to Distributed Systems (分布式系统介绍)**
   - Definition and characteristics of distributed systems
   - Common use cases and challenges
   - Examples of distributed systems (e.g., microservices, databases)

### 2. **CAP Theorem (CAP 定理)**
   - Understanding consistency, availability, and partition tolerance
   - Trade-offs in distributed systems
   - Examples of systems prioritizing different aspects of CAP

### 3. **Distributed System Architectures (分布式系统架构)**
   - Client-server vs. peer-to-peer
   - Service-oriented architecture (SOA) and microservices
   - Event-driven architecture (EDA)
   - Data flow and pipeline architectures

### 4. **Data Replication (数据复制)**
   - Synchronous vs. asynchronous replication
   - Conflict resolution in data replication
   - Data consistency models (eventual consistency, strong consistency)

### 5. **Distributed Consensus Algorithms (分布式共识算法)**
   - Paxos, Raft, and other consensus protocols
   - Byzantine fault tolerance (BFT)
   - Leader election algorithms

### 6. **Fault Tolerance & Reliability (容错与可靠性)**
   - Failure models and handling failure in distributed systems
   - Redundancy and replication for fault tolerance
   - Checkpointing and logging strategies

### 7. **Scalability (可扩展性)**
   - Horizontal vs. vertical scaling
   - Load balancing strategies
   - Sharding and partitioning
   - Elastic scaling

### 8. **Distributed Data Stores (分布式数据存储)**
   - NoSQL databases (e.g., Cassandra, MongoDB)
   - Distributed file systems (e.g., HDFS, Google File System)
   - Consistent hashing and its role in distributed databases

### 9. **Coordination Services (协调服务)**
   - ZooKeeper, etcd, and other coordination systems
   - Leader election, configuration management, and synchronization
   - Service discovery in distributed environments

### 10. **Concurrency and Synchronization (并发与同步)**
   - Multithreading and concurrency models in distributed systems
   - Locks, semaphores, and other synchronization primitives
   - Deadlocks and how to avoid them

### 11. **Networking Basics (网络基础)**
   - TCP/IP, UDP, and sockets
   - Message passing and RPC (Remote Procedure Call)
   - Network partitions and their impact on distributed systems

### 12. **Messaging Systems (消息系统)**
   - Message queues (e.g., RabbitMQ, Kafka)
   - Event streaming and pub/sub systems
   - Idempotency and delivery guarantees (at-least-once, exactly-once)

### 13. **Security in Distributed Systems (分布式系统的安全性)**
   - Encryption, authentication, and authorization mechanisms
   - Public key infrastructure (PKI) and SSL/TLS
   - Handling secure communication between distributed components

### 14. **Consistency Models (一致性模型)**
   - Strong, eventual, and causal consistency
   - Quorum-based approaches
   - Read and write consistency in distributed databases

### 15. **Distributed Transactions (分布式事务)**
   - Two-phase commit (2PC) and three-phase commit (3PC)
   - Distributed transaction coordinators
   - Saga pattern for long-running transactions

### 16. **Time and Ordering (时间与顺序)**
   - Logical clocks (e.g., Lamport clocks)
   - Vector clocks and their use in conflict resolution
   - Global time synchronization challenges (NTP, GPS)

### 17. **Load Balancing and Reverse Proxy (负载均衡与反向代理)**
   - Types of load balancers (software vs. hardware)
   - Load balancing algorithms (round-robin, least connections)
   - Reverse proxy and its role in distributed systems

### 18. **Service Discovery (服务发现)**
   - Static vs. dynamic service discovery
   - Service discovery tools (e.g., Consul, Eureka)
   - Challenges and strategies in service discovery in dynamic environments

### 19. **Caching in Distributed Systems (分布式系统中的缓存)**
   - Distributed cache solutions (e.g., Redis, Memcached)
   - Cache invalidation strategies
   - Handling cache consistency in distributed systems

### 20. **Eventual Consistency & Conflict Resolution (最终一致性与冲突解决)**
   - Types of conflicts (e.g., read-write, write-write)
   - Vector clocks and causal consistency
   - CRDTs (Conflict-free Replicated Data Types)

### 21. **Monitoring and Observability (监控与可观测性)**
   - Logging, metrics, and tracing in distributed systems
   - Distributed tracing tools (e.g., Jaeger, Zipkin)
   - Centralized logging systems

### 22. **Distributed Scheduling Systems (分布式调度系统)**
   - Distributed cron jobs and task scheduling
   - Tools like Apache Airflow, Kubernetes CronJobs
   - Distributed job management strategies

### 23. **Geo-Distributed Systems (地理分布式系统)**
   - Cross-data center replication
   - Handling network latency and failures across regions
   - Designing systems for multiple geographic locations

### 24. **Microservices Design (微服务设计)**
   - Communication patterns (synchronous vs. asynchronous)
   - Service decomposition and domain-driven design
   - API Gateway patterns and sidecars (e.g., Istio)

### 25. **Distributed Search and Indexing (分布式搜索与索引)**
   - Distributed search engines (e.g., Elasticsearch, Solr)
   - Index sharding and replication
   - Search consistency and fault tolerance

### 26. **Cloud-native Distributed Systems (云原生分布式系统)**
   - Design principles for cloud-native applications
   - Kubernetes and container orchestration
   - Service meshes (e.g., Istio, Linkerd)

### 27. **Testing and Debugging Distributed Systems (分布式系统的测试与调试)**
   - Unit testing, integration testing, and chaos engineering
   - Debugging in distributed environments
   - Fault injection techniques and tools (e.g., Chaos Monkey)

### 28. **Serverless Architectures (无服务器架构)**
   - Understanding FaaS (Function as a Service) and BaaS (Backend as a Service)
   - Benefits and challenges of serverless
   - Scaling and orchestration of serverless functions

---

These topics will help you build a strong foundation in **Distributed System Design** and understand the key concepts and techniques used to design reliable, scalable, and efficient systems.

Would you like to explore one of these topics in detail?
