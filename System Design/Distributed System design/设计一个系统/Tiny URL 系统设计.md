# Tiny URL 系统设计步骤

## **URESCAS 步骤**

- **U (Understand)**: 理解系统需求，包括生成短链接、重定向、访问统计。
- **R (Requirements)**: 定义功能性需求和非功能性需求，确保系统满足性能和可靠性。
- **E (Estimate)**: 估算流量和存储需求，确保系统容量足够。
- **S (Select)**: 选择合适的数据库、缓存、架构等技术栈。
- **C (Combine)**: 结合数据库和缓存层，实现最佳性能。
- **A (Architect)**: 设计数据库架构、缓存层和应用层的架构。
- **S (Secure)**: 考虑安全性、备份、速率限制等措施。

## 1. 理解系统需求 / Understand System Requirements

- **功能性需求 / Functional Requirements**:
  - 生成短链接以映射长链接。
  - 短链接重定向到原始长链接。
  - 统计短链接的访问次数。

- **非功能性需求 / Non-Functional Requirements**:
  - 高可用性：确保短链接服务始终可用。
  - 高并发：能够处理大量用户请求。
  - 低延迟：生成短链接和访问重定向应快速响应。

## 2. 估算流量和存储需求 / Estimate Traffic and Storage Needs

- **写入请求估算**：
  - 假设每日生成 100 万个短链接，每个短链接长度为 7 个字符。
  - 每个短链接的存储空间大约为 10 字节（包括一些元数据）。
  - 每年生成大约 3.65 亿个短链接，总存储需求约为 25GB（假设每个短链接平均需要 70 字节存储空间，包括元数据）。

- **读取请求估算**：
  - 假设每个短链接每天被访问 10 次，则每日访问请求为 1000 万次。
  - 对于高频访问的短链接，需要使用缓存层来减少对数据库的直接读取压力。

- **存储需求估算**：
  - 短链接映射存储：每个短链接平均需要 70 字节存储空间。
  - 访问统计数据：如果记录每个短链接的访问次数，每次访问需要大约 16 字节（包括短链接和计数器），则每天的访问统计存储需求为约 160MB。
  - 总存储需求：考虑到短链接数据和访问统计数据，每年的存储需求约为 50GB。

## 3. 数据库选择 / Choose Database

- **关系型数据库（SQL）**：
  - **优点**：适合存储短链接和长链接的映射关系，确保数据一致性，适合需要事务性的操作。
  - **缺点**：扩展性较差，尤其在高并发写入时可能成为瓶颈。
  - **推荐使用场景**：用于核心数据的持久化存储，例如短链接和长链接的映射关系。

- **NoSQL 数据库（如 Cassandra 或 Redis）**：
  - **优点**：高扩展性，适合高并发读取和写入请求，能够方便地水平扩展。
  - **缺点**：数据一致性较弱，尤其是最终一致性模型，适合对一致性要求不高的场景。
  - **推荐使用场景**：Cassandra 用于存储访问统计数据，Redis 用于缓存短链接和长链接的映射，减少数据库读取压力。

- **决策**：
  - **SQL 数据库** 用于存储短链接和长链接的映射关系，确保核心数据的持久性和一致性。
  - **Redis** 用于缓存层，存储热点数据以加速读取操作。
  - **Cassandra** 用于存储访问统计数据，支持高扩展性和高并发写入需求。

## 4. 数据库架构设计 / Design Database Architecture

- **SQL 数据库用于映射存储**：
  - **短链接表 / Short URL Table**：用于存储短链接和长链接之间的映射关系。

  ```sql
  CREATE TABLE short_urls (
      id SERIAL PRIMARY KEY,
      short_url VARCHAR(10) UNIQUE NOT NULL,
      original_url TEXT NOT NULL,
      created_at TIMESTAMP DEFAULT NOW()
  );
  ```

- **NoSQL 数据库用于缓存和统计**：
  - **Redis 缓存层**：用于存储常用短链接的映射，加速重定向过程。
  - **访问统计表 / Visit Stats Table**：用于记录每个短链接的访问次数。

  ```sql
  CREATE TABLE visit_stats (
      short_url VARCHAR(10) PRIMARY KEY,
      visit_count INT DEFAULT 0
  );
  ```

## 5. 短链接生成算法 / URL Shortening Algorithm

- 使用 Base62 编码生成唯一的短链接。
- **步骤**：
  1. 对每个新链接生成一个唯一的 ID。
  2. 将 ID 编码为 Base62 字符串（使用大小写字母和数字）。
  3. 将编码后的字符串作为短链接。

### Python 代码示例 / Python Code Example
```python
import string
import random

class URLShortener:
    def __init__(self):
        self.url_map = {}
        self.charset = string.ascii_letters + string.digits

    def encode(self, original_url):
        short_url = ''.join(random.choices(self.charset, k=7))
        while short_url in self.url_map:
            short_url = ''.join(random.choices(self.charset, k=7))
        self.url_map[short_url] = original_url
        return short_url

    def decode(self, short_url):
        return self.url_map.get(short_url)

# 使用示例
url_shortener = URLShortener()
short_url = url_shortener.encode("http://example.com")
print(f"Short URL: {short_url}")
original_url = url_shortener.decode(short_url)
print(f"Original URL: {original_url}")
```

## 6. API 设计 / API Design

- **生成短链接 API / Create Short URL API**
  - **方法**: POST
  - **URL**: `/api/shorten`
  - **请求参数**:
    - `original_url` (string): 原始长链接
  - **响应**:
    - `short_url` (string): 生成的短链接

  ```json
  {
    "original_url": "http://example.com"
  }
  ```

  **响应示例**:
  ```json
  {
    "short_url": "http://tinyurl.com/abc1234"
  }
  ```

- **重定向短链接 API / Redirect Short URL API**
  - **方法**: GET
  - **URL**: `/{short_url}`
  - **响应**: 重定向到原始 URL

- **访问统计 API / Visit Stats API**
  - **方法**: GET
  - **URL**: `/api/stats/{short_url}`
  - **响应**:
    - `visit_count` (int): 短链接的访问次数

  **响应示例**:
  ```json
  {
    "short_url": "abc1234",
    "visit_count": 1500
  }
  ```

## 7. 缓存层和重定向服务 / Caching and Redirect Service

- **缓存**：
  - 使用 Redis 缓存短链接和长链接的映射，减少对数据库的读取压力。
- **重定向服务**：
  - 用户访问短链接时，通过缓存查找对应的长链接，若未命中则从数据库中获取。

## 8. 系统扩展性 / System Scalability

- **水平扩展**：
  - 将短链接和长链接的映射分片存储在多个数据库节点中，以应对大量数据增长。
- **负载均衡**：
  - 使用负载均衡器将请求分发到多个应用服务器，以应对高并发访问。

## 9. 安全和其他注意事项 / Security and Additional Considerations

- **安全性**：
  - 防止恶意生成大量短链接，可设置速率限制。
- **备份与恢复**：
  - 对数据库进行定期备份，确保数据安全。
- **数据过期管理**：
  - 对长期未使用的短链接进行清理，以释放存储空间。

## 总结 / Summary
通过设计 Tiny URL 系统，我们实现了短链接的生成、重定向和访问统计功能。结合使用 SQL 和 NoSQL 数据库、缓存层和负载均衡，确保系统的高可用性和高性能。在实现过程中需考虑安全性、数据备份和扩展性，以满足大规模用户的需求。
