# Quick Start Demo 06: Best Practices in Production Deploying and Connecting Two Dockerized Apps on Different Servers

[Back to Quick Start Demo](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Quick%20Start%20Demo.md)

#### Introduction / 介绍

In a production environment, it is common to deploy different services across multiple servers. This scenario often involves deploying containerized applications (e.g., a Python app and a FastAPI app) on different servers. To ensure these containers can communicate, you need to follow best practices, such as configuring Docker networks, using appropriate DNS or IP address management, and ensuring secure communication between services.

在生产环境中，不同的服务通常部署在多个服务器上。这种情况下，通常需要将容器化的应用程序（如 Python 应用程序和 FastAPI 应用程序）部署在不同的服务器上。为了确保这些容器可以通信，你需要遵循最佳实践，例如配置 Docker 网络、使用适当的 DNS 或 IP 地址管理，以及确保服务之间的安全通信。

#### Step 1: Set Up Dockerized FastAPI App on Server 1 / 步骤1: 在服务器 1 上设置 Docker 化的 FastAPI 应用程序

1. **Create and Dockerize the FastAPI App** / 创建并 Docker 化 FastAPI 应用程序

   ```bash
   mkdir fastapi_app
   cd fastapi_app
   ```

   Create the `main.py` for the FastAPI app:

   **创建 FastAPI 应用程序的 `main.py`：**

   ```python
   # main.py
   from fastapi import FastAPI

   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"message": "Hello from FastAPI on Server 1"}
   ```

   Create the `Dockerfile`:

   **创建 `Dockerfile`：**

   ```dockerfile
   # Dockerfile
   FROM python:3.9-slim

   WORKDIR /app

   COPY . .

   RUN pip install fastapi uvicorn

   CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
   ```

2. **Build and Run the FastAPI App on Server 1** / 在服务器 1 上构建并运行 FastAPI 应用程序

   ```bash
   docker build -t fastapi_app .
   docker run -d --name fastapi_app -p 8000:8000 fastapi_app
   ```

   The FastAPI app is now running on Server 1 and accessible via the server's IP address on port 8000.

   **FastAPI 应用程序现在在服务器 1 上运行，并可以通过服务器的 IP 地址和端口 8000 进行访问。**

#### Step 2: Set Up Dockerized Python App on Server 2 / 步骤2: 在服务器 2 上设置 Docker 化的 Python 应用程序

1. **Create and Dockerize the Python App** / 创建并 Docker 化 Python 应用程序

   ```bash
   mkdir python_app
   cd python_app
   ```

   Create the `app.py` for the Python app:

   **创建 Python 应用程序的 `app.py`：**

   ```python
   # app.py
   import requests

   # Replace 'server1_ip_address' with the actual IP address of Server 1
   response = requests.get("http://server1_ip_address:8000/")
   print(response.json())
   ```

   Create the `Dockerfile`:

   **创建 `Dockerfile`：**

   ```dockerfile
   # Dockerfile
   FROM python:3.9-slim

   WORKDIR /app

   COPY . .

   RUN pip install requests

   CMD ["python", "app.py"]
   ```

2. **Build and Run the Python App on Server 2** / 在服务器 2 上构建并运行 Python 应用程序

   ```bash
   docker build -t python_app .
   docker run -it --name python_app python_app
   ```

   The Python app on Server 2 will call the FastAPI app on Server 1 using the IP address of Server 1.

   **服务器 2 上的 Python 应用程序将使用服务器 1 的 IP 地址调用服务器 1 上的 FastAPI 应用程序。**

   You should see the output:

   **你应该看到输出：**

   ```bash
   {'message': 'Hello from FastAPI on Server 1'}
   ```

#### Step 3: Best Practices for Cross-Server Communication / 步骤3: 跨服务器通信的最佳实践

1. **Use a Stable DNS Name Instead of IP** / 使用稳定的 DNS 名称而不是 IP

   - In a production environment, IP addresses might change due to server restarts or network reconfigurations. Using a DNS name (e.g., `fastapi-app.example.com`) instead of a hardcoded IP address ensures that your services can always communicate even if the underlying IP address changes.

   - **在生产环境中，IP 地址可能会因服务器重启或网络重新配置而更改。使用 DNS 名称（例如 `fastapi-app.example.com`）而不是硬编码的 IP 地址可以确保你的服务即使在底层 IP 地址更改的情况下仍能通信。**

2. **Secure Communication with HTTPS** / 使用 HTTPS 进行安全通信

   - Use HTTPS for secure communication between services, especially when they are deployed across different servers. You can set up an Nginx or Apache server as a reverse proxy to handle SSL/TLS termination.

   - **使用 HTTPS 进行服务之间的安全通信，尤其是在它们部署在不同服务器上的情况下。你可以设置 Nginx 或 Apache 服务器作为反向代理来处理 SSL/TLS 终止。**

3. **Network Configuration** / 网络配置

   - Ensure proper firewall rules are in place to allow communication between the two servers. Only the necessary ports (e.g., 8000 for FastAPI) should be open.

   - **确保有适当的防火墙规则以允许两台服务器之间的通信。只有必要的端口（例如，FastAPI 的 8000 端口）应该开放。**

4. **Load Balancing and Scaling** / 负载均衡和扩展

   - For high availability, consider setting up a load balancer in front of your FastAPI service. The load balancer can distribute incoming requests across multiple instances of your FastAPI app running on different servers.

   - **为了高可用性，考虑在 FastAPI 服务前设置一个负载均衡器。负载均衡器可以将传入请求分配到运行在不同服务器上的多个 FastAPI 应用程序实例。**

5. **Monitoring and Logging** / 监控和日志记录

   - Implement monitoring and logging for both applications to track performance and errors, especially for cross-server communication. Tools like Prometheus, Grafana, and ELK stack (Elasticsearch, Logstash, Kibana) can be useful.

   - **为这两个应用程序实施监控和日志记录，以跟踪性能和错误，特别是跨服务器通信。像 Prometheus、Grafana 和 ELK 堆栈（Elasticsearch、Logstash、Kibana）这样的工具会很有用。**

#### 5Ws / 5个W

1. **What:** Demonstrating how two Dockerized applications communicate across different servers.
   **什么:** 演示两个 Docker 化应用程序如何在不同服务器之间通信。
2. **Why:** To understand best practices in production environments for cross-server communication.
   **为什么:** 了解生产环境中跨服务器通信的最佳实践。
3. **When:** When deploying containerized microservices or distributed applications in a production environment.
   **什么时候:** 在生产环境中部署容器化的微服务或分布式应用程序时。
4. **Where:** In any production setup where services are distributed across different servers.
   **在哪里:** 在服务分布在不同服务器上的任何生产设置中。
5. **Who:** DevOps engineers, system administrators, and developers deploying multi-server applications.
   **谁:** 部署多服务器应用程序的 DevOps 工程师、系统管理员和开发人员。

#### Recommended Resources / 推荐资源

1. **Docker Networking Documentation:** [Docker Networking](https://docs.docker.com/network/)
2. **Nginx Reverse Proxy Documentation:** [Nginx Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
3. **Prometheus Monitoring:** [Prometheus](https://prometheus.io/)

1. **Docker 网络文档:** [Docker 网络](https://docs.docker.com/network/)
2. **Nginx 反向代理文档:** [Nginx 反向代理](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
3. **Prometheus 监控:** [Prometheus](https://prometheus.io/)

---

By following these best practices, you can ensure secure, reliable, and scalable communication between Dockerized applications deployed on different servers in a production environment.

通过遵循这些最佳实践，你可以确保在生产环境中部署在不同服务器上的 Docker 化应用程序之间进行安全、可靠和可扩展的通信。
