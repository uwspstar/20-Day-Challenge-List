# Quick Start Demo 03: FastAPI Demo Project with Docker

[Back to Quick Start Demo](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Quick%20Start%20Demo.md)

### FastAPI Demo Project with Docker

Let's continue with the previous demo by creating a new FastAPI project and containerizing it with Docker. Then, we'll demonstrate how to call the FastAPI service from another project or using tools like `curl` or Postman.

#### Step 1: Set Up Your FastAPI Project

**English**: Create a new directory for your FastAPI project and add the necessary files:
**Chinese**: 为您的 FastAPI 项目创建一个新目录并添加必要的文件：

```bash
mkdir fastapi-docker-demo
cd fastapi-docker-demo
```

**Create `main.py`:**

**English**: This is the main FastAPI application file.
**Chinese**: 这是主要的 FastAPI 应用程序文件。

```python
# main.py
from fastapi import FastAPI
import httpx

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Welcome to the FastAPI Docker Demo"}

@app.get("/joke")
async def get_joke():
    # Define the URL of the external API that provides jokes
    joke_api_url = "https://official-joke-api.appspot.com/random_joke"

    # Use httpx to fetch the joke from the external API
    async with httpx.AsyncClient() as client:
        response = await client.get(joke_api_url)

    # If the response is successful, return the joke
    if response.status_code == 200:
        joke_data = response.json()
        return {"setup": joke_data['setup'], "punchline": joke_data['punchline']}
    else:
        return {"error": "Failed to fetch joke"}
```
**requirements.txt**
```
fastapi
uvicorn
httpx
```

**Create `Dockerfile`:**

**English**: This Dockerfile defines how to build your FastAPI Docker image.
**Chinese**: 该 Dockerfile 定义了如何构建您的 FastAPI Docker 镜像。

```dockerfile
# Use the official Python image as the base
FROM python:3.8-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the application code into the container
COPY . /app

# Install the required Python packages
RUN pip install -r requirements.txt

# Expose the port that the FastAPI app runs on
EXPOSE 8000

# Define the command to run the FastAPI application
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

#### Step 2: Build the Docker Image

**English**: Build your Docker image for the FastAPI application with the following command:
**Chinese**: 使用以下命令为 FastAPI 应用程序构建 Docker 镜像：

```bash
docker build -t fastapi-docker-demo .
```

#### Step 3: Run the FastAPI Docker Container

**English**: Run the container with the following command:
**Chinese**: 使用以下命令运行容器：

```bash
docker run -d --name fastapi-container -p 8000:8000 fastapi-docker-demo
```

- **English**: This command will:
  - Run the container in detached mode (`-d`) with the name `fastapi-container`.
  - Map port 8000 on the host machine to port 8000 inside the container so you can access the FastAPI application via `http://localhost:8000`.
  
- **Chinese**: 该命令将：
  - 以分离模式（`-d`）运行容器，名称为 `fastapi-container`。
  - 将主机上的 8000 端口映射到容器内的 8000 端口，因此您可以通过 `http://localhost:8000` 访问 FastAPI 应用程序。

#### Step 4: Access the FastAPI Application

**English**: You can now access the FastAPI application by navigating to `http://localhost:8000` in your web browser or by using `curl`.
**Chinese**: 您现在可以通过导航到浏览器中的 `http://localhost:8000` 或使用 `curl` 来访问 FastAPI 应用程序。

**Example 1: Using a Web Browser**

**English**: Open your web browser and go to `http://localhost:8000`.
**Chinese**: 打开浏览器并转到 `http://localhost:8000`。

- **Result**: You should see the message `{"message": "Welcome to the FastAPI Docker Demo"}`.

**Example 2: Using `curl`**

**English**: Use the `curl` command to access the FastAPI endpoints.
**Chinese**: 使用 `curl` 命令访问 FastAPI 端点。

```bash
# Access the root endpoint
curl http://localhost:8000/

# Access the joke endpoint
curl http://localhost:8000/joke
```

- **Result**:
  - For the root endpoint: `{"message": "Welcome to the FastAPI Docker Demo"}`
  - For the joke endpoint: `{"joke": "Why don't programmers like nature? It has too many bugs."}`

**Example 3: Using Postman**

**English**: You can also use Postman to make GET requests to `http://localhost:8000/` and `http://localhost:8000/joke`.
**Chinese**: 您还可以使用 Postman 向 `http://localhost:8000/` 和 `http://localhost:8000/joke` 发送 GET 请求。

#### Step 5: Call the FastAPI Service from Another Dockerized Project

**English**: You can call this FastAPI service from another Dockerized Python project. Assuming you have a project similar to the `python-joke-app-quickstart` project from earlier, you can modify it to make an HTTP request to the FastAPI service.
**Chinese**: 您可以从另一个 Docker 化的 Python 项目调用此 FastAPI 服务。假设您有一个类似于之前的 `python-joke-app-quickstart` 项目，您可以修改它以向 FastAPI 服务发出 HTTP 请求。

**Example `app.py`**:

```python
# app.py
import os
import logging
import requests

# Ensure the logs directory exists
os.makedirs("/logs", exist_ok=True)

# Set up logging
logging.basicConfig(filename='/logs/app.log', level=logging.INFO,
                    format='%(asctime)s - %(levelname)s - %(message)s')

def get_joke():
    response = requests.get("http://localhost:8000/joke") # localhost is this docker container
    if response.status_code != 200:
        raise Exception("Failed to fetch joke from FastAPI service")
    joke = response.json()
    return joke['joke']

def main():
    logging.info("Starting the application")
    print("Fetching a random joke from FastAPI service...")
    
    try:
        joke = get_joke()
        logging.info(f"Fetched joke: {joke}")
        print(f"Here’s a joke for you: {joke}")
    except Exception as e:
        logging.error(f"An error occurred: {e}")
        print("Failed to fetch a joke.")

    logging.info("Application finished")

if __name__ == "__main__":
    main()
```

**Note**:
- **English**: This script will attempt to fetch a joke from the FastAPI service running on `http://localhost:8000/joke`.
- **Chinese**: 该脚本将尝试从运行在 `http://localhost:8000/joke` 的 FastAPI 服务获取笑话。

#### Step 6: Run the Updated Project

**English**: Rebuild the Docker image for the `python-joke-app-quickstart` project and run it.
**Chinese**: 重新构建 `python-joke-app-quickstart` 项目的 Docker 镜像并运行它。

```bash
docker build -t python-joke-app-quickstart .
docker run -d --restart on-failure:5 -v $(pwd)/logs:/logs python-joke-app-quickstart
```

- **English**: The container will now call the FastAPI service to fetch a joke and log the result.
- **Chinese**: 容器现在将调用 FastAPI 服务以获取笑话并记录结果。

#### Step 7: Verify the Integration

**English**: Check the logs to verify that the `python-joke-app-quickstart` container successfully called the FastAPI service and retrieved a joke.
**Chinese**: 检查日志以验证 `python-joke-app-quickstart` 容器是否成功调用了 FastAPI 服务并检索到笑话。

```bash
cat logs/app.log
```

**Expected Log Output**: (NO logs See Understanding the `localhost` Issue in Docker Containers)
```
2024-08-28 10:00:00,000 - INFO - Starting the application
2024-08-28 10:00:00,500 - INFO - Fetched joke: Why don't programmers like nature? It has too many bugs.
2024-08-28 10:00:00,600 - INFO - Application finished
```

**Conclusion**

**English**: You now have a complete setup where a FastAPI service is running in a Docker container, and another Dockerized Python project is calling this service to fetch data. This demonstrates how to integrate different Dockerized services effectively.
**Chinese**: 您现在有一个完整的设置，其中 FastAPI 服务在 Docker 容器中运行，另一个 Docker 化的 Python 项目正在调用该服务以获取数据。这演示了如何有效地集成不同的 Docker 化服务。

------

### Understanding the `localhost` Issue in Docker Containers

#### Context

**English**:
- When running multiple services in Docker containers, it’s common to have them communicate with each other over a network. However, a common pitfall occurs when using `localhost` to reference services, which can lead to connectivity issues between containers.

**Chinese**:
- 在 Docker 容器中运行多个服务时，通常会让它们通过网络相互通信。然而，当使用 `localhost` 引用服务时，常见的陷阱是可能导致容器之间的连接问题。

#### The `localhost` Problem

**English**:
- **Localhost Inside Containers**: When you refer to `localhost` within a Docker container, it points to the container's own loopback interface, not the host machine or any other container.
- **Misconception**: Developers often assume that `localhost` inside one container would somehow point to services running on the host machine or another container, but this is not the case.
- **Result**: In the scenario described, the `python-joke-app-quickstart` container tries to fetch data from `http://localhost:8000`, thinking it will reach the FastAPI service. However, this request never leaves the container and ends up trying to reach a service on the container itself, which doesn't exist. This leads to a failed request, and the log remains empty because the intended service (FastAPI) is never reached.

**Chinese**:
- **容器内的 Localhost**: 当您在 Docker 容器内引用 `localhost` 时，它指向的是容器自己的回环接口，而不是主机或任何其他容器。
- **误解**: 开发人员常常误以为在一个容器内使用 `localhost` 可以指向运行在主机或另一个容器上的服务，但事实并非如此。
- **结果**: 在上述场景中，`python-joke-app-quickstart` 容器尝试从 `http://localhost:8000` 获取数据，以为它会到达 FastAPI 服务。然而，这个请求从未离开容器，最终尝试在容器本身上访问一个不存在的服务。这导致请求失败，并且日志保持为空，因为预期的服务（FastAPI）从未被访问到。

#### Why `localhost` Doesn’t Work Across Containers

**English**:
- **Isolation**: Each Docker container is an isolated environment with its own networking stack, including its own `localhost` (loopback) interface. This isolation is what allows multiple containers to run on the same machine without interfering with each other.
- **Network Namespaces**: Docker containers are placed in separate network namespaces, meaning the `localhost` in one container is isolated from the `localhost` in another container or the host machine.
- **Communication**: To allow containers to communicate, Docker provides networking capabilities that allow containers to be connected on a shared network, enabling them to talk to each other using their container names as DNS resolvable hostnames.

**Chinese**:
- **隔离性**: 每个 Docker 容器都是一个独立的环境，拥有自己的网络栈，包括它自己的 `localhost`（回环）接口。这种隔离性使多个容器可以在同一台机器上运行而不互相干扰。
- **网络命名空间**: Docker 容器被放置在不同的网络命名空间中，这意味着一个容器中的 `localhost` 与另一个容器或主机的 `localhost` 是隔离的。
- **通信**: 为了使容器能够通信，Docker 提供了网络功能，允许容器连接到共享网络，使它们能够使用各自的容器名称作为 DNS 可解析的主机名来互相通信。

#### Solution: Using Docker Networks

**English**:
- **Create a Docker Network**: By creating a custom Docker network, containers can communicate with each other using their container names as hostnames.
- **Networked Communication**: When both the `python-joke-app-quickstart` and FastAPI containers are on the same Docker network, the `python-joke-app-quickstart` container can reach the FastAPI service by using the container name `fastapi-container` as the hostname, e.g., `http://fastapi-container:8000`.

**Chinese**:
- **创建 Docker 网络**: 通过创建自定义 Docker 网络，容器可以使用它们的容器名称作为主机名进行通信。
- **网络通信**: 当 `python-joke-app-quickstart` 和 FastAPI 容器都在同一个 Docker 网络上时，`python-joke-app-quickstart` 容器可以使用容器名称 `fastapi-container` 作为主机名来访问 FastAPI 服务，例如 `http://fastapi-container:8000`。

**Steps to Fix**:
1. **Create a Docker Network**: `docker network create demo-network`
2. **Run the FastAPI Container on the Network**: `docker run -d --name fastapi-container --network demo-network -p 8000:8000 fastapi-docker-demo`
3. **Update the `app.py` in `python-joke-app-quickstart`**: Change the request URL to `http://fastapi-container:8000/joke`.
4. **Run the `python-joke-app-quickstart` Container on the Same Network**: `docker run --name quickstart-container --network demo-network -v $(pwd)/logs:/logs python-joke-app-quickstart`

**Explanation**:
- **English**: These steps ensure that both containers are on the same network, allowing them to resolve each other’s hostnames and communicate effectively. The FastAPI service can now be accessed from the `python-joke-app-quickstart` container using `http://fastapi-container:8000`.
- **Chinese**: 这些步骤确保两个容器都在同一个网络上，使它们能够解析对方的主机名并有效通信。现在可以从 `python-joke-app-quickstart` 容器使用 `http://fastapi-container:8000` 访问 FastAPI 服务。

This approach resolves the issue caused by the incorrect use of `localhost` in a Docker container context, enabling proper inter-container communication.

------

### Running Multiple Services in Docker Containers: Understanding the Pitfalls of `localhost`

#### Introduction
When running multiple services within Docker containers, they often need to communicate with each other over the network. However, a common pitfall when referencing services using `localhost` is that it can lead to connectivity issues between containers.

当在 Docker 容器中运行多个服务时，它们通常需要通过网络相互通信。然而，当使用 `localhost` 引用服务时，一个常见的陷阱是这可能导致容器之间的连接问题。

#### 5Ws (Who, What, When, Where, Why)

- **Who:** Anyone running multiple services within Docker containers.
  **谁:** 在 Docker 容器中运行多个服务的任何人。

- **What:** The issue of containers failing to communicate when using `localhost`.
  **什么:** 使用 `localhost` 时，容器之间通信失败的问题。

- **When:** This problem arises when you attempt to have containers talk to each other using `localhost`.
  **何时:** 当你尝试让容器使用 `localhost` 互相通信时会出现这个问题。

- **Where:** This issue occurs within the Docker network, particularly when using bridge networking.
  **哪里:** 这个问题发生在 Docker 网络中，特别是在使用桥接网络时。

- **Why:** Each Docker container has its own network namespace, meaning `localhost` refers to the container itself, not other containers.
  **为什么:** 每个 Docker 容器都有自己的网络命名空间，这意味着 `localhost` 指的是容器自身，而不是其他容器。

#### Detailed Explanation

When you run services in separate Docker containers, each container operates in its own isolated environment. This includes its own network namespace. As a result, `localhost` inside a container refers to the loopback interface of that container. If you try to use `localhost` to communicate with another container, the connection will fail because the `localhost` in one container does not point to the other container.

当你在不同的 Docker 容器中运行服务时，每个容器都在其自己的隔离环境中运行。这包括它自己的网络命名空间。因此，容器内部的 `localhost` 指的是该容器的回环接口。如果你尝试使用 `localhost` 与另一个容器通信，连接将会失败，因为一个容器中的 `localhost` 不会指向另一个容器。

Instead, Docker provides an internal DNS that allows you to reference other containers by their names or network aliases. This method ensures that containers can properly communicate with each other over the Docker network.

相反，Docker 提供了一个内部 DNS，允许你通过容器的名称或网络别名来引用其他容器。这种方法确保容器可以通过 Docker 网络正确地相互通信。

#### Python Code Example

Here’s a simple example of two services, one running a Python Flask app and another running a Redis server. Instead of using `localhost`, the Flask app will reference the Redis container by its service name.

以下是两个服务的简单示例，一个运行 Python Flask 应用程序，另一个运行 Redis 服务器。Flask 应用程序将通过服务名称引用 Redis 容器，而不是使用 `localhost`。

```python
from flask import Flask
import redis

app = Flask(__name__)

# Connect to Redis service by name
r = redis.Redis(host='redis_service', port=6379, db=0)

@app.route('/')
def index():
    r.incr('hits')
    return f'This page has been viewed {r.get("hits").decode()} times.'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

In this example, `redis_service` should be the name of the Redis container or the network alias you've assigned to it.

在此示例中，`redis_service` 应该是 Redis 容器的名称或你分配给它的网络别名。

#### Tips
- **Tip:** Use Docker Compose to easily manage and network multiple services. Each service can be referenced by its name defined in the `docker-compose.yml` file.
  
  **提示:** 使用 Docker Compose 来轻松管理和网络多个服务。每个服务都可以通过 `docker-compose.yml` 文件中定义的名称进行引用。

#### Warnings
- **Warning:** Avoid hardcoding `localhost` when trying to connect services within Docker containers. Always use container names or network aliases.
  
  **警告:** 在尝试连接 Docker 容器中的服务时，避免硬编码 `localhost`。始终使用容器名称或网络别名。

#### Comparison Table

| Method          | Description                                                     | Pros                                                | Cons                                |
|-----------------|-----------------------------------------------------------------|-----------------------------------------------------|-------------------------------------|
| `localhost`     | Refers to the container's own loopback interface                | Simple for single-container applications            | Does not work for inter-container communication |
| Container Name  | Use the container's name to reference it                        | Easy to set up, works across multiple containers     | Requires consistent naming          |
| Network Alias   | Assign an alias to the container and use it for communication   | Flexible, allows for renaming without changing code  | Additional configuration needed     |

#### Conclusion
In Docker, when running multiple services, it's crucial to avoid using `localhost` for inter-container communication. Instead, rely on Docker's internal DNS system to reference containers by name or alias. This ensures smooth and reliable communication between services.

在 Docker 中运行多个服务时，避免使用 `localhost` 进行容器间通信至关重要。相反，依赖 Docker 的内部 DNS 系统通过名称或别名引用容器。这可以确保服务之间的通信顺畅且可靠。

#### Recommended Resources

1. **Docker Documentation:** Official Docker docs on networking [Docker Documentation](https://docs.docker.com/network/).
2. **Docker Networking Best Practices:** Detailed guide on best practices for Docker networking.
3. **Flask and Redis with Docker Compose:** Example tutorial on setting up Flask and Redis with Docker Compose.

**推荐资源**

1. **Docker 文档:** 官方 Docker 网络文档 [Docker 文档](https://docs.docker.com/network/).
2. **Docker 网络最佳实践:** Docker 网络最佳实践的详细指南。
3. **使用 Docker Compose 的 Flask 和 Redis:** 设置 Flask 和 Redis 的 Docker Compose 示例教程。
