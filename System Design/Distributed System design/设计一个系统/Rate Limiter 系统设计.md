# Rate Limiter 系统设计步骤

## **URESCAS 步骤**

- **U (Understand)**: 理解系统需求，限制用户请求速率以保护系统免受恶意流量的影响。
- **R (Requirements)**: 定义功能性需求和非功能性需求，确保系统稳定且可扩展。
- **E (Estimate)**: 估算请求流量和系统负载需求。
- **S (Select)**: 选择合适的算法、数据结构、数据库等技术栈。
- **C (Combine)**: 结合算法、数据库和缓存层，实现最佳性能。
- **A (Architect)**: 设计整体架构，定义 API 接口和请求流程。
- **S (Secure)**: 考虑防止绕过速率限制的安全措施，以及数据的持久化和备份方案。

## 1. 理解系统需求 / Understand System Requirements

- **功能性需求 / Functional Requirements**:

  - 限制每个用户在指定时间段内的请求次数。
  - 提供灵活的配置，可以针对不同的 API、用户或 IP 设置不同的限制。
  - 支持不同限速策略，如固定窗口计数器、滑动窗口日志、令牌桶等。

- **非功能性需求 / Non-Functional Requirements**:

  - 高可用性：即使在高并发情况下，系统也应能够正常工作。
  - 低延迟：限速逻辑应尽量减少对请求处理速度的影响。
  - 可扩展性：应支持水平扩展，以应对增加的请求量。

## 2. 估算请求流量和系统负载 / Estimate Traffic and System Load

- 假设每秒有 10 万个请求进入系统，且每个请求需要执行速率限制检查。
- 如果系统中有 1000 万活跃用户，每个用户每天平均发出 100 个请求，则每日的请求量为 10 亿次。
- 系统需要能够处理如此大量的请求并迅速做出响应。

## 3. 选择合适的算法和数据结构 / Choose Suitable Algorithm and Data Structure

- **固定窗口计数器（Fixed Window Counter）**：

  - **优点**：实现简单，适合基本的限速需求。
  - **缺点**：在窗口边界时可能出现“突发”请求。
  - **适用场景**：对于简单的限速需求，可以使用此方法。

  **Python 示例代码**：

  ```python
  import time

  class FixedWindowCounter:
      def __init__(self, limit, window_size):
          self.limit = limit
          self.window_size = window_size
          self.counter = 0
          self.window_start = time.time()

      def allow_request(self):
          current_time = time.time()
          if current_time - self.window_start >= self.window_size:
              self.window_start = current_time
              self.counter = 0
          if self.counter < self.limit:
              self.counter += 1
              return True
          return False
  ```

- **滑动窗口日志（Sliding Window Log）**：

  - **优点**：能够精确控制请求速率，避免窗口边界问题。
  - **缺点**：需要存储每个请求的时间戳，存储开销大。
  - **适用场景**：需要精确限速的情况，如防止突发性滥用。

  **Python 示例代码**：

  ```python
  from collections import deque
  import time

  class SlidingWindowLog:
      def __init__(self, limit, window_size):
          self.limit = limit
          self.window_size = window_size
          self.requests = deque()

      def allow_request(self):
          current_time = time.time()
          while self.requests and self.requests[0] <= current_time - self.window_size:
              self.requests.popleft()
          if len(self.requests) < self.limit:
              self.requests.append(current_time)
              return True
          return False
  ```

- **令牌桶（Token Bucket）**：

  - **优点**：允许一定程度的突发请求，灵活性高。
  - **缺点**：实现复杂，需要定期补充令牌。
  - **适用场景**：对于需要支持突发流量的服务，可以使用此方法。

  **Python 示例代码**：

  ```python
  import time

  class TokenBucket:
      def __init__(self, capacity, refill_rate):
          self.capacity = capacity
          self.refill_rate = refill_rate
          self.tokens = capacity
          self.last_refill_timestamp = time.time()

      def allow_request(self):
          current_time = time.time()
          elapsed = current_time - self.last_refill_timestamp
          self.tokens = min(self.capacity, self.tokens + elapsed * self.refill_rate)
          self.last_refill_timestamp = current_time

          if self.tokens >= 1:
              self.tokens -= 1
              return True
          return False
  ```

- **决策**：选择令牌桶算法用于限速，因为它能够平衡流量的控制和突发请求的需求。

## 4. 数据库和缓存选择 / Choose Database and Cache

- **Redis**：

  - **优点**：支持高并发读写操作，低延迟，适合存储用户的速率限制状态。
  - **适用场景**：使用 Redis 作为速率限制数据的存储，以快速读取和更新请求状态。

- **数据库（如 PostgreSQL）**：

  - **优点**：适合长期存储用户的限速配置和策略。
  - **适用场景**：存储限速策略和用户的基本信息。

## 5. 系统架构设计 / System Architecture Design

- **缓存层**：

  - 使用 Redis 作为缓存层，存储用户的请求计数和时间戳。
  - 每次请求都会检查 Redis 中是否存在该用户的限速信息，并根据算法判断是否允许请求通过。

- **数据库层**：

  - 使用关系型数据库（如 PostgreSQL）存储用户的限速配置、策略和全局设置。

- **请求处理流程**：

  - 用户请求 -> API Gateway -> Rate Limiter (Redis 限速检查) -> 请求通过或被拒绝。

  **系统架构图**：


  *此架构图展示了用户请求经过 API Gateway 和 Rate Limiter 的流程，其中包括 Redis 和 PostgreSQL 的交互。*

## 6. API 设计 / API Design

- **限速配置 API / Rate Limiter Configuration API**

  - **方法**: POST
  - **URL**: `/api/set_rate_limit`
  - **请求参数**:
    - `user_id` (string): 用户 ID
    - `limit` (int): 每分钟的请求次数限制
    - `window` (int): 时间窗口大小（秒）
  - **响应**:
    - `status` (string): 操作状态

  ```json
  {
    "user_id": "user123",
    "limit": 100,
    "window": 60
  }
  ```

  **响应示例**:

  ```json
  {
    "status": "success"
  }
  ```

- **请求限速检查 API / Rate Limit Check API**

  - **方法**: GET
  - **URL**: `/api/check_rate_limit`
  - **请求参数**:
    - `user_id` (string): 用户 ID
  - **响应**:
    - `allowed` (boolean): 是否允许请求
    - `remaining` (int): 剩余的请求次数

  ```json
  {
    "user_id": "user123"
  }
  ```

  **响应示例**:

  ```json
  {
    "allowed": true,
    "remaining": 95
  }
  ```

## 7. 缓存和数据持久化 / Caching and Data Persistence

- **缓存策略**：

  - 使用 Redis 缓存每个用户的请求计数，以确保限速检查的快速响应。
  - 定期将 Redis 中的数据同步到 PostgreSQL，以便进行数据持久化和分析。

- **数据持久化**：

  - 将限速策略和用户配置信息存储在 PostgreSQL 中，以便支持系统重启或扩展。

## 8. 系统扩展性 / System Scalability

- **水平扩展**：
  - 使用 Redis 集群来扩展速率限制的存储容量和处理能力。
- **负载均衡**：
  - 使用负载均衡
