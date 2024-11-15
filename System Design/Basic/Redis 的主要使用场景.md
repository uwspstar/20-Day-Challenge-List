### Redis 的主要使用场景 

包括会话管理、缓存、分布式锁、计数器、速率限制、全局 ID 生成、购物车、用户留存、消息队列和排名等

| 数据类型 | 用途                |
| -------- | ------------------- |
| **String** 字符串   | 会话管理           |
|                         | 缓存               |
|                         | 分布式锁          |
|                         | 计数器            |
| **Int** 整数            | 速率限制器       |
|                         | 全局ID            |
| **Hash** 哈希          | 购物车            |
| **Bitmap** 位图      | 用户留存          |
| **List** 列表            | 消息队列          |
| **ZSet** 有序集合    | 排名/排行榜      |

---

下面是 Redis 在不同场景下的应用及相应的代码示例：

### 1. 会话管理 (Session)

我们可以使用 Redis 来在不同服务之间共享用户的会话数据。

```python
import redis

client = redis.StrictRedis(host='localhost', port=6379, db=0)
# 设置用户会话
client.set("user:session:123", "session_data")
# 获取用户会话
session_data = client.get("user:session:123")
print(session_data)
```

### 2. 缓存 (Cache)

我们可以使用 Redis 缓存对象或页面，尤其适合热点数据的缓存。

```python
# 设置缓存，过期时间为 10 分钟
client.setex("page:home", 600, "<html>首页内容</html>")
# 获取缓存的页面
page_content = client.get("page:home")
print(page_content)
```

### 3. 分布式锁 (Distributed Lock)

我们可以使用 Redis 字符串在分布式服务间获取锁。

```python
import time

lock_key = "lock:resource"
# 获取锁，设置 10 秒过期
if client.set(lock_key, "locked", ex=10, nx=True):
    print("获取锁成功")
    # 进行一些操作
    time.sleep(5)
    # 释放锁
    client.delete(lock_key)
else:
    print("锁已被占用")
```

### 4. 计数器 (Counter)

我们可以统计文章的点赞数或阅读次数。

```python
# 增加文章阅读计数
client.incr("article:1001:views")
# 获取当前阅读数
views = client.get("article:1001:views")
print(views)
```

### 5. 速率限制器 (Rate Limiter)

我们可以为特定用户 IP 应用速率限制器。

```python
user_ip = "192.168.0.1"
# 在一分钟内最多允许访问 10 次
if client.incr(f"rate_limit:{user_ip}") <= 10:
    print("允许访问")
else:
    print("访问过多，限制中")
# 设置访问记录的过期时间为 1 分钟
client.expire(f"rate_limit:{user_ip}", 60)
```

### 6. 全局 ID 生成器 (Global ID Generator)

我们可以使用 Redis 的整数类型来生成全局唯一 ID。

```python
# 获取全局唯一 ID
global_id = client.incr("global:id")
print("生成的全局ID:", global_id)
```

### 7. 购物车 (Shopping Cart)

我们可以使用 Redis Hash 来表示购物车中的键值对。

```python
# 添加商品到购物车
client.hset("cart:user:123", "item:apple", 3)
client.hset("cart:user:123", "item:banana", 5)
# 获取购物车内容
cart_items = client.hgetall("cart:user:123")
print(cart_items)
```

### 8. 计算用户留存 (Calculate User Retention)

我们可以使用 Bitmap 表示用户每天的登录情况并计算留存率。

```python
# 标记用户在某一天登录
client.setbit("user:login:2023-11-15", 123, 1)
# 检查用户是否在某一天登录
is_logged_in = client.getbit("user:login:2023-11-15", 123)
print("用户是否登录:", bool(is_logged_in))
```

### 9. 消息队列 (Message Queue)

我们可以使用 Redis List 作为消息队列。

```python
# 推送消息到队列
client.lpush("queue:messages", "Message 1")
client.lpush("queue:messages", "Message 2")
# 消费消息
message = client.rpop("queue:messages")
print("收到消息:", message)
```

### 10. 排名 (Ranking)

我们可以使用 Redis ZSet 对文章进行排序。

```python
# 添加文章及其分数到排行榜
client.zadd("rank:articles", {"article:1001": 300, "article:1002": 150})
# 获取排名前 5 的文章
top_articles = client.zrevrange("rank:articles", 0, 4, withscores=True)
print("排行榜:", top_articles)
```

---

这些代码示例展示了 Redis 在不同应用场景中的使用方法，包括会话管理、缓存、分布式锁、计数器、速率限制、全局 ID 生成、购物车、用户留存、消息队列和排名等。Redis 的多种数据结构使其在这些场景中表现优异。
