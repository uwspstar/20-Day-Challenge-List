### 20-Day System Design Learning Plan

![Version](https://img.shields.io/badge/version-1.0.0-blue)

#### Recommend Resources:
- [不同层次的架构：从企业架构到应用架构](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/%E4%B8%8D%E5%90%8C%E5%B1%82%E6%AC%A1%E7%9A%84%E6%9E%B6%E6%9E%84:%20%E4%BB%8E%E4%BC%81%E4%B8%9A%E6%9E%B6%E6%9E%84%E5%88%B0%E5%BA%94%E7%94%A8%E6%9E%B6%E6%9E%84.md)
- [软件架构中常见的质量属性检查清单](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/%E8%BD%AF%E4%BB%B6%E6%9E%B6%E6%9E%84%E4%B8%AD%E5%B8%B8%E8%A7%81%E7%9A%84%E8%B4%A8%E9%87%8F%E5%B1%9E%E6%80%A7%E6%A3%80%E6%9F%A5%E6%B8%85%E5%8D%95.md)
- [System Design Interview Questions](https://codebitwave.com/system-design-interview-questions/)
- [8 Must-Know Strategies to Scale Your System](https://codebitwave.com/system-design-101-8-must-know-strategies-to-scale-your-system/)
- [From Zero to Hero](https://github.com/uwspstar/From-Zero-to-Hero/tree/main)

------

### 系统设计面试学习计划（四周）

#### 第一周：系统设计基础与关键技术概念

**Day 1: 系统设计介绍**  
- **[系统设计的重要性](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/Day1_basic/%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1%E7%9A%84%E9%87%8D%E8%A6%81%E6%80%A7.md)**  
   - 了解系统设计在构建可扩展、效率高的系统中的关键作用。
- **[系统设计的关键原则](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/Day1_basic/%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1%E7%9A%84%E5%85%B3%E9%94%AE%E5%8E%9F%E5%88%99.md)**  
   - 学习模块化、抽象、关注点分离等基本设计原则。
- **[常见的系统设计面试问题](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/Day1_basic/%E5%B8%B8%E8%A7%81%E7%9A%84%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1%E9%9D%A2%E8%AF%95%E9%97%AE%E9%A2%98.md)**  
   - 回顾常见的系统设计面试问题，了解面试官的期望。

**Day 2: 理解需求与计算机架构**  
- **[功能需求 vs 非功能需求](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/Day2/%E5%8A%9F%E8%83%BD%E9%9C%80%E6%B1%82%20vs%20%E9%9D%9E%E5%8A%9F%E8%83%BD%E9%9C%80%E6%B1%82.md)**  
   - 区分功能需求（系统应做什么）和非功能需求（系统的特性）。
- **[计算机架构](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/Day2/%E8%AE%A1%E7%AE%97%E6%9C%BA%E6%9E%B6%E6%9E%84.md)**  
   - 了解CPU、内存、硬盘的工作原理及其对系统设计的影响。

**Day 3: 网络基础与TCP/UDP**  
- **网络基础**  
   - 学习IP地址、路由、子网掩码等基本网络概念。
- **TCP和UDP协议**  
   - 了解TCP和UDP的区别及在不同场景下的应用。

**Day 4: DNS、HTTP与WebSockets**  
- **DNS的工作原理**  
   - 探讨DNS如何解析域名为IP地址。
- **HTTP协议**  
   - 学习HTTP请求和响应的详细过程。
- **WebSockets在实时通信中的应用**  
   - 理解WebSockets与HTTP的区别，以及其在实时消息系统中的应用。

**Day 5: 应用架构与API设计**  
- **应用架构（单体架构 vs 微服务架构）**  
   - 探讨单体和微服务架构的优缺点及适用场景。
- **API设计范式**  
   - 学习RESTful API、GraphQL的区别与API设计的最佳实践。

**Day 6: 缓存策略、CDN与负载均衡**  
- **缓存的作用**  
   - 学习缓存机制与不同类型的缓存（如客户端缓存、服务器缓存、CDN）的应用场景。
- **负载均衡**  
   - 了解负载均衡器在分配流量中的作用，学习硬件与软件负载均衡的区别。
- **一致性哈希**  
   - 了解一致性哈希在分布式系统中的应用。

**Day 7: 数据库设计与CAP定理**  
- **SQL vs NoSQL**  
   - 了解关系型数据库和NoSQL数据库的区别及应用场景。
- **数据库分片与复制**  
   - 探讨数据库的分片设计和复制策略。
- **CAP定理**  
   - 学习CAP定理及其在分布式系统设计中的重要性。

**Day 8: 消息队列、对象存储与MapReduce**  
- **消息队列**  
   - 学习Kafka、RabbitMQ等常见消息队列系统及其应用场景。
- **对象存储**  
   - 了解对象存储的基本概念及应用，如Amazon S3。
- **MapReduce**  
   - 探讨MapReduce如何处理海量数据及其在大数据系统中的应用。

---

#### 第二周：核心架构模式与实践

**Day 9-10: 实践设计问题**  
- **设计Rate Limiter（限流器）**  
   - 探讨如何设计一个能够处理高并发的限流器。
- **设计TinyUrl（短链接服务）**  
   - 学习如何设计一个类似bit.ly的短链接服务。

**Day 11-12: 实践设计问题**  
- **设计Twitter（社交平台）**  
   - 探讨如何设计一个能够支持用户动态流的社交平台。
- **设计Discord（实时聊天应用）**  
   - 学习如何设计一个支持实时通信和群组聊天的应用。

**Day 13-14: 实践设计问题**  
- **设计YouTube（视频分享平台）**  
   - 探讨如何设计一个支持大规模视频上传和分发的平台。
- **设计Google Drive（文件存储服务）**  
   - 学习如何设计一个支持大规模文件存储和版本控制的服务。

**Day 15-16: 实践设计问题**  
- **设计Google Maps（地图服务）**  
   - 探讨如何设计一个具备实时路况和路线规划功能的地图服务。
- **设计Key-Value存储系统**  
   - 学习如何设计一个分布式键值对存储系统。

**Day 17-18: 实践设计问题**  
- **设计分布式消息队列**  
   - 学习如何设计一个高可用、高吞吐量的分布式消息队列系统。

通过本计划的逐步学习，你将全面掌握系统设计面试中涉及的核心概念和实践技巧。


