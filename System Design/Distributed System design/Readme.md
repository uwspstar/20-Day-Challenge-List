
# Distributed System Design

| #  | Topic (主题)               | Notes (备注)                                     |
|----|----------------------------|-------------------------------------------------|
| 1  | Image/video sharing app (图片/视频分享应用)  | - Instagram (Instagram)                         |
|    |                            | - Pinterest (Pinterest)                         |
| 2  | Chat/messenger app (聊天/消息应用)         | - Whatsapp (Whatsapp)                          |
| 3  | Url shortener (短网址)                    | - Tiny URL (Tiny URL)                          |
| 4  | News Feed (新闻 Feed)                   | - Facebook (Facebook)                          |
|    |                            | - Instagram user and home timelines (Instagram 用户和主页时间线) |
| 5  | Notification system (通知系统)             | - Sending social media updates to users (向用户发送社交媒体更新) |


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
