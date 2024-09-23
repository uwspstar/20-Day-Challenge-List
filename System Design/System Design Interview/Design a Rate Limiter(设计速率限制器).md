### **Design a Rate Limiter** (设计速率限制器)

[Back to System Design List](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/System%20Design/System%20Design%20Interview/readme.md)


A **rate limiter** is used to control the number of requests a user can make to a system within a given period. This is especially important for preventing abuse, managing traffic, and ensuring that system resources are fairly allocated among users.

**速率限制器** 用于控制用户在特定时间内向系统发出的请求数量。这对于防止滥用、管理流量和确保系统资源在用户之间公平分配非常重要。

---

### 1. **Functional Requirements** (功能需求)

Before designing the rate limiter, it's important to define what the rate limiter should accomplish.

在设计速率限制器之前，首先需要定义速率限制器应实现的目标。

#### Approach (步骤):

- **Limit Requests (限制请求)**: The rate limiter should restrict the number of requests a user or IP address can make within a given time period, such as allowing 100 requests per minute.
  - **限制请求**：速率限制器应限制用户或IP地址在给定时间段内的请求数量，例如每分钟允许100个请求。
  
- **Reject Excess Requests (拒绝超额请求)**: If the limit is exceeded, further requests should be rejected or delayed.
  - **拒绝超额请求**：如果请求超过限制，后续请求应被拒绝或延迟处理。
  
- **Track User Requests (跟踪用户请求)**: The system needs to track each user’s request count within the defined time window.
  - **跟踪用户请求**：系统需要在定义的时间窗口内跟踪每个用户的请求计数。
  
- **Reset Mechanism (重置机制)**: After the time window expires, the request count should reset.
  - **重置机制**：在时间窗口到期后，请求计数应重置。

---

### 2. **Rate Limiting Algorithms** (速率限制算法)

Several algorithms are commonly used to implement rate limiting. Let's explore the most popular ones.

几种常见的速率限制算法可用于实现速率限制。让我们探索几种最常用的算法。

#### **1. Token Bucket Algorithm (令牌桶算法)**

In the **Token Bucket** algorithm, tokens are added to a bucket at a fixed rate. Each incoming request consumes a token. If the bucket is empty, the request is rejected or delayed.

在**令牌桶算法**中，令牌以固定速率添加到桶中。每个传入的请求消耗一个令牌。如果桶是空的，请求将被拒绝或延迟。

**Advantages (优势)**:
- Smooth request processing.
- Can handle short bursts of traffic.

**Disadvantages (劣势)**:
- Requires tracking the token count and replenishment rate.

**Implementation (实现)**:

```python
class TokenBucketRateLimiter:
    def __init__(self, rate, capacity):
        self.rate = rate  # Token replenishment rate
        self.capacity = capacity  # Max bucket capacity
        self.tokens = capacity
        self.last_refill_timestamp = time.time()

    def allow_request(self):
        current_time = time.time()
        elapsed_time = current_time - self.last_refill_timestamp
        self.tokens = min(self.capacity, self.tokens + elapsed_time * self.rate)
        self.last_refill_timestamp = current_time

        if self.tokens >= 1:
            self.tokens -= 1
            return True
        return False
```

```python
class TokenBucketRateLimiter:
    def __init__(self, rate, capacity):
        self.rate = rate  # 令牌补充速率
        self.capacity = capacity  # 桶的最大容量
        self.tokens = capacity
        self.last_refill_timestamp = time.time()

    def allow_request(self):
        current_time = time.time()
        elapsed_time = current_time - self.last_refill_timestamp
        self.tokens = min(self.capacity, self.tokens + elapsed_time * self.rate)
        self.last_refill_timestamp = current_time

        if self.tokens >= 1:
            self.tokens -= 1
            return True
        return False
```

---

#### **2. Leaky Bucket Algorithm (漏桶算法)**

In the **Leaky Bucket** algorithm, requests are processed at a constant rate. Excessive requests are queued or dropped if the queue is full.

在**漏桶算法**中，请求以恒定速率处理。如果请求过多，将被排队或丢弃（当队列满时）。

**Advantages (优势)**:
- Ensures smooth, consistent request processing.

**Disadvantages (劣势)**:
- May reject valid requests if the queue is full.

---

#### **3. Fixed Window Algorithm (固定窗口算法)**

In the **Fixed Window** algorithm, requests are limited based on a fixed time window. For example, a user can make 100 requests per minute. After each minute, the counter resets.

在**固定窗口算法**中，请求基于固定的时间窗口限制。例如，用户每分钟可以发出100个请求。每分钟后，计数器重置。

**Advantages (优势)**:
- Simple to implement.

**Disadvantages (劣势)**:
- Susceptible to traffic spikes at the edge of the window.

---

#### **4. Sliding Window Log Algorithm (滑动窗口日志算法)**

In the **Sliding Window Log** algorithm, each request is timestamped, and the system tracks requests within a sliding window. Only requests within the window are counted.

在**滑动窗口日志算法**中，每个请求都有时间戳，系统跟踪在滑动窗口内的请求。只有窗口内的请求才会被计数。

**Advantages (优势)**:
- Provides more accurate rate limiting compared to fixed window.
  
**Disadvantages (劣势)**:
- Requires more memory to track timestamps.

---

#### **5. Sliding Window Counter Algorithm (滑动窗口计数器算法)**

In the **Sliding Window Counter** algorithm, we divide the time window into smaller intervals and count requests per interval. The rate limiter sums up the counts from all intervals that fall within the window.

在**滑动窗口计数器算法**中，我们将时间窗口划分为较小的区间，并计算每个区间的请求数量。速率限制器会将所有落在窗口内的区间计数相加。

**Advantages (优势)**:
- Provides a balance between accuracy and memory efficiency.
  
**Disadvantages (劣势)**:
- Slightly more complex to implement than fixed window.

---

### 3. **Distributed Rate Limiting** (分布式速率限制)

When designing a rate limiter for distributed systems, we need a centralized way to track user requests. This is especially important for systems where requests are handled by multiple servers.

在为分布式系统设计速率限制器时，我们需要一种集中方式来跟踪用户请求。这对于多个服务器处理请求的系统尤为重要。

#### Approach (步骤):

- **Using Redis (使用Redis)**: Redis, an in-memory key-value store, can be used to track the request count for each user in a distributed environment. Redis offers fast read/write operations, making it ideal for implementing distributed rate limiting.
  - **使用Redis**：Redis是一种内存键值存储，可以用于在分布式环境中跟踪每个用户的请求计数。Redis提供了快速的读写操作，非常适合实现分布式速率限制。

**Example (示例)**:

```python
import redis
import time

class RedisRateLimiter:
    def __init__(self, client_id, limit, window_size):
        self.redis_client = redis.StrictRedis(host='localhost', port=6379, db=0)
        self.client_id = client_id
        self.limit = limit
        self.window_size = window_size

    def allow_request(self):
        current_time = int(time.time())
        pipeline = self.redis_client.pipeline()
        pipeline.zadd(self.client_id, {current_time: current_time})
        pipeline.zremrangebyscore(self.client_id, 0, current_time - self.window_size)
        pipeline.zcard(self.client_id)
        result = pipeline.execute()

        if result[2] < self.limit:
            return True
        return False
```

```python
import redis
import time

class RedisRateLimiter:
    def __init__(self, client_id, limit, window_size):
        self.redis_client = redis.StrictRedis(host='localhost', port=6379, db=0)
        self.client_id = client_id
        self.limit = limit
        self.window_size = window_size

    def allow_request(self):
        current_time = int(time.time())
        pipeline = self.redis_client.pipeline()
        pipeline.zadd(self.client_id, {current_time: current_time})
        pipeline.zremrangebyscore(self.client_id, 0, current_time - self.window_size)
        pipeline.zcard(self.client_id)
        result = pipeline.execute()

        if result[2] < self.limit:
            return True
        return False
```

This implementation uses Redis's sorted set (zset) to track requests with timestamps. The window size represents the time frame, and the limit represents the maximum number of requests allowed.

这个实现使用Redis的有序集合（zset）来跟踪带有时间戳的请求。窗口大小表示时间范围，限制表示允许的最大请求数。

---

### 4. **Handling Rate Limiting in Distributed Systems** (在分布式系统中处理速率限制)

#### Approach (步骤):

- **

Consistency Across Servers (跨服务器的一致性)**: Ensure that all servers are synchronized when counting requests. Distributed rate limiters often use centralized data stores like Redis to keep track of request counts.
  - **跨服务器的一致性**：确保所有服务器在计数请求时保持同步。分布式速率限制器通常使用像Redis这样的集中式数据存储来跟踪请求计数。

- **Handling Failures (处理故障)**: Design the rate limiter to handle failures gracefully. For instance, if the Redis server is temporarily unavailable, the rate limiter should have a fallback mechanism, such as using local counters.
  - **处理故障**：设计速率限制器时要能优雅地处理故障。例如，如果Redis服务器暂时不可用，速率限制器应有后备机制，例如使用本地计数器。

---

### Conclusion (结论)

Designing a rate limiter is crucial for protecting system resources, ensuring fairness, and preventing abuse. By using algorithms like **Token Bucket**, **Leaky Bucket**, or **Sliding Window**, and implementing distributed rate limiting with tools like Redis, you can build an efficient and scalable solution.

设计速率限制器对于保护系统资源、确保公平性和防止滥用至关重要。通过使用**令牌桶**、**漏桶**或**滑动窗口**等算法，并结合Redis等工具实现分布式速率限制，你可以构建一个高效且可扩展的解决方案。

---

Let me know if you'd like further details or another topic!
