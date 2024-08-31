# Quick Start Demo 05: Connecting a Python App with a FastAPI App in Separate Docker Containers (Without Docker Compose)

[Back to Quick Start Demo](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Quick%20Start%20Demo.md)

#### Introduction / 介绍

In this guide, we will demonstrate how to set up a Python app in one Docker container to call a FastAPI app in another Docker container without using Docker Compose. Each application will have its own `Dockerfile` and can be deployed independently in different environments. We will ensure proper communication between the containers using Docker's networking capabilities, allowing the containers to use their respective names as DNS-resolvable hostnames.

在本指南中，我们将演示如何在一个 Docker 容器中设置 Python 应用程序，以调用另一个 Docker 容器中的 FastAPI 应用程序，而不使用 Docker Compose。每个应用程序将有自己的 `Dockerfile`，并且可以在不同的环境中独立部署。我们将通过使用 Docker 的网络功能确保容器之间的正确通信，使容器能够使用各自的名称作为 DNS 可解析的主机名。

#### Step 1: Create and Dockerize the FastAPI Application / 步骤1: 创建并 Docker 化 FastAPI 应用程序

1. **Create a directory for the FastAPI app** and navigate into it.
   **创建一个用于 FastAPI 应用程序的目录**，并进入该目录。

   ```bash
   mkdir fastapi_app
   cd fastapi_app
   ```

2. **Create a FastAPI app** in `main.py` with a simple endpoint.

   **在 `main.py` 中创建一个 FastAPI 应用程序**，包含一个简单的端点。

   ```python
   # main.py
   from fastapi import FastAPI

   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"message": "Hello from FastAPI"}
   ```

3. **Create a `Dockerfile`** for the FastAPI app.

   **为 FastAPI 应用程序创建一个 `Dockerfile`。**

   ```dockerfile
   # Dockerfile
   FROM python:3.9-slim

   WORKDIR /app

   COPY . .

   RUN pip install fastapi uvicorn

   CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
   ```

4. **Build the Docker image for the FastAPI app**.

   **为 FastAPI 应用程序构建 Docker 镜像。**

   ```bash
   docker build -t fastapi_app .
   ```

5. **Run the FastAPI app container** on a specified network.

   **在指定网络上运行 FastAPI 应用程序容器。**

   ```bash
   docker network create my_network
   docker run -d --name fastapi_app --network my_network -p 8000:8000 fastapi_app
   ```

   This command creates a Docker network named `my_network` and runs the FastAPI app within this network.

   此命令创建一个名为 `my_network` 的 Docker 网络，并在该网络内运行 FastAPI 应用程序。

#### Step 2: Create and Dockerize the Python Application / 步骤2: 创建并 Docker 化 Python 应用程序

1. **Create a directory for the Python app** and navigate into it.
   **创建一个用于 Python 应用程序的目录**，并进入该目录。

   ```bash
   mkdir python_app
   cd python_app
   ```

2. **Create a Python script** in `app.py` that calls the FastAPI app.

   **在 `app.py` 中创建一个调用 FastAPI 应用程序的 Python 脚本。**

   ```python
   # app.py
   import requests

   response = requests.get("http://fastapi_app:8000/")
   print(response.json())
   ```

3. **Create a `Dockerfile`** for the Python app.

   **为 Python 应用程序创建一个 `Dockerfile`。**

   ```dockerfile
   # Dockerfile
   FROM python:3.9-slim

   WORKDIR /app

   COPY . .

   RUN pip install requests

   CMD ["python", "app.py"]
   ```

4. **Build the Docker image for the Python app**.

   **为 Python 应用程序构建 Docker 镜像。**

   ```bash
   docker build -t python_app .
   ```

5. **Run the Python app container** on the same network as the FastAPI app.

   **在与 FastAPI 应用程序相同的网络上运行 Python 应用程序容器。**

   ```bash
   docker run -it --name python_app --network my_network python_app
   ```

   You should see the Python app output the response from the FastAPI app:

   你应该看到 Python 应用程序输出 FastAPI 应用程序的响应：

   ```bash
   {'message': 'Hello from FastAPI'}
   ```

#### Step 3: Explanation of Communication / 步骤3: 通信解释

Docker allows containers to connect to a shared network so that they can use their respective container names as DNS-resolvable hostnames to communicate with each other. In this setup, `fastapi_app` is the hostname that the Python app uses to reach the FastAPI service.

Docker 允许容器连接到共享网络，以便它们可以使用各自的容器名称作为 DNS 可解析的主机名来相互通信。在此设置中，`fastapi_app` 是 Python 应用程序用于访问 FastAPI 服务的主机名。

#### Tips / 提示

- Ensure both containers are running on the same Docker network to allow communication.
- Container names should be used as hostnames for inter-service communication.

- 确保两个容器都在同一个 Docker 网络上运行，以允许通信。
- 容器名称应作为主机名用于服务间通信。

#### Warnings / 警告

- If containers are not on the same network, they will not be able to communicate.
- Avoid using `localhost` in multi-container setups as it refers to the container itself.

- 如果容器不在同一网络上，它们将无法通信。
- 避免在多容器设置中使用 `localhost`，因为它指的是容器本身。

#### 5Ws / 5个W

1. **What:** Demonstrating how a Python app calls a FastAPI app in different Docker containers.
   **什么:** 演示 Python 应用程序如何调用不同 Docker 容器中的 FastAPI 应用程序。
2. **Why:** To understand inter-container communication using Docker's networking features.
   **为什么:** 了解如何使用 Docker 的网络功能进行容器间通信。
3. **When:** When deploying microservices or distributed applications using Docker.
   **什么时候:** 当使用 Docker 部署微服务或分布式应用程序时。
4. **Where:** In Dockerized environments where multiple services need to interact.
   **在哪里:** 在需要多个服务交互的 Docker 化环境中。
5. **Who:** Developers building microservices or multi-container applications.
   **谁:** 构建微服务或多容器应用程序的开发人员。

#### Recommended Resources / 推荐资源

1. **Docker Networking Documentation:** [Docker Networking](https://docs.docker.com/network/)
2. **Docker Run Command Documentation:** [Docker Run](https://docs.docker.com/engine/reference/run/)
3. **FastAPI Documentation:** [FastAPI](https://fastapi.tiangolo.com/)

1. **Docker 网络文档:** [Docker 网络](https://docs.docker.com/network/)
2. **Docker Run 命令文档:** [Docker Run](https://docs.docker.com/engine/reference/run/)
3. **FastAPI 文档:** [FastAPI](https://fastapi.tiangolo.com/)

---

By following these steps, you can deploy a Python app and a FastAPI app in separate Docker containers while ensuring they communicate properly using Docker's networking features.

通过遵循这些步骤，你可以将 Python 应用程序和 FastAPI 应用程序部署在单独的 Docker 容器中，同时确保它们通过 Docker 的网络功能进行正确的通信。
