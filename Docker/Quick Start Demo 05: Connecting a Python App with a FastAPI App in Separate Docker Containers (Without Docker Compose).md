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

------

### Setting Network and Container Name Inside Dockerfile: A Best Practice Analysis

#### Introduction / 介绍

In Docker, while it is possible to configure some aspects of container behavior within the `Dockerfile`, such as defining the container's working directory, environment variables, and the command to run when the container starts, other configurations, such as networking and container names, are typically not set inside the `Dockerfile`. This is because these configurations are considered environment-specific and are better managed outside the `Dockerfile`, either through the Docker CLI commands or orchestration tools like Docker Compose, Kubernetes, etc.

在 Docker 中，虽然可以在 `Dockerfile` 中配置容器行为的某些方面，例如定义容器的工作目录、环境变量以及容器启动时运行的命令，但其他配置，例如网络和容器名称，通常不会在 `Dockerfile` 中设置。这是因为这些配置被认为是特定于环境的，通常通过 Docker CLI 命令或编排工具（如 Docker Compose、Kubernetes 等）来管理会更好。

#### Why Network and Container Name Shouldn't Be Set in Dockerfile / 为什么不应在 Dockerfile 中设置网络和容器名称

1. **Separation of Concerns / 职责分离**:  
   The `Dockerfile` is meant to define how to build the container image (e.g., base image, dependencies, application code). Network configuration and container names, however, are deployment concerns that can vary depending on where and how the container is deployed (e.g., in a local development environment, on a staging server, or in a production cluster).

   **Dockerfile** 用于定义如何构建容器镜像（例如，基础镜像、依赖项、应用程序代码）。然而，网络配置和容器名称是部署相关的事项，可能会根据容器的部署位置和方式而有所不同（例如，在本地开发环境中、在测试服务器上或在生产集群中）。

2. **Flexibility / 灵活性**:  
   By keeping network and container names out of the `Dockerfile`, you maintain flexibility. You can easily deploy the same container image in different environments with different network configurations and container names without having to rebuild the image.

   通过将网络和容器名称保持在 `Dockerfile` 之外，你可以保持灵活性。你可以在不同的环境中使用不同的网络配置和容器名称轻松部署相同的容器镜像，而无需重新构建镜像。

3. **Best Practices in Production / 生产环境中的最佳实践**:  
   In production environments, network configurations and container orchestration are typically managed by external tools like Kubernetes or Docker Compose. These tools provide better control and scaling capabilities. Embedding network configurations in the `Dockerfile` would make it harder to adapt the container to different environments.

   在生产环境中，网络配置和容器编排通常由外部工具（如 Kubernetes 或 Docker Compose）管理。这些工具提供了更好的控制和扩展能力。将网络配置嵌入到 `Dockerfile` 中会使容器难以适应不同的环境。

#### Example: Why Not to Set Network and Container Name in Dockerfile / 示例：为什么不在 Dockerfile 中设置网络和容器名称

1. **Dockerfile for FastAPI App** / FastAPI 应用程序的 Dockerfile

   ```dockerfile
   # Dockerfile
   FROM python:3.9-slim

   WORKDIR /app

   COPY . .

   RUN pip install fastapi uvicorn

   CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
   ```

   - **Note**: This `Dockerfile` does not include any network or container name configurations. It is focused solely on building the FastAPI application.

   - **注意**：此 `Dockerfile` 不包含任何网络或容器名称配置。它仅专注于构建 FastAPI 应用程序。

2. **Running the Container** / 运行容器

   The network and container name are specified at runtime using the Docker CLI:

   网络和容器名称在运行时使用 Docker CLI 指定：

   ```bash
   docker network create my_network
   docker run -d --name fastapi_app --network my_network -p 8000:8000 fastapi_app
   ```

   - **Note**: This command allows flexibility in setting up the network and container name depending on the deployment environment.

   - **注意**：此命令允许根据部署环境灵活设置网络和容器名称。

3. **Why Avoid Setting These in Dockerfile** / 为什么避免在 Dockerfile 中设置这些

   If you were to set the network and container name in the `Dockerfile`, you would lose flexibility. For example, deploying the same image in a different environment with different network requirements would require modifying the `Dockerfile` and rebuilding the image, which is not efficient.

   如果你在 `Dockerfile` 中设置网络和容器名称，你将失去灵活性。例如，在具有不同网络要求的不同环境中部署相同的镜像将需要修改 `Dockerfile` 并重新构建镜像，这并不高效。

#### Best Practice Recommendations / 最佳实践建议

- **Use Docker CLI or Orchestration Tools**: Manage network settings and container names using the Docker CLI, Docker Compose, Kubernetes, or other orchestration tools. This keeps your `Dockerfile` focused on building the image and allows for greater flexibility during deployment.

  **使用 Docker CLI 或编排工具**：使用 Docker CLI、Docker Compose、Kubernetes 或其他编排工具管理网络设置和容器名称。这样可以让你的 `Dockerfile` 专注于构建镜像，并在部署过程中提供更大的灵活性。

- **Environment-Specific Configurations**: Handle network configurations and container names as environment-specific settings that can be adjusted based on the deployment target (development, testing, production).

  **特定于环境的配置**：将网络配置和容器名称视为特定于环境的设置，可以根据部署目标（开发、测试、生产）进行调整。

#### 5Ws / 5个W

1. **What:** Understanding why network and container name should not be set in `Dockerfile`.
   **什么:** 了解为什么不应在 `Dockerfile` 中设置网络和容器名称。
2. **Why:** To maintain flexibility and adhere to best practices in container deployment.
   **为什么:** 为了保持灵活性并遵循容器部署中的最佳实践。
3. **When:** During container image creation and deployment.
   **什么时候:** 在容器镜像创建和部署期间。
4. **Where:** In any environment where Docker containers are used (development, staging, production).
   **在哪里:** 在使用 Docker 容器的任何环境中（开发、测试、生产）。
5. **Who:** Developers and DevOps engineers managing containerized applications.
   **谁:** 管理容器化应用程序的开发人员和 DevOps 工程师。

#### Recommended Resources / 推荐资源

1. **Docker Networking Documentation:** [Docker Networking](https://docs.docker.com/network/)
2. **Best Practices for Writing Dockerfiles:** [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
3. **Kubernetes Networking:** [Kubernetes Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

1. **Docker 网络文档:** [Docker 网络](https://docs.docker.com/network/)
2. **编写 Dockerfile 的最佳实践:** [Dockerfile 最佳实践](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
3. **Kubernetes 网络:** [Kubernetes 网络](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

---

By following these practices, you ensure that your Docker containers are both flexible and maintainable, and can be easily adapted to different deployment environments.

通过遵循这些实践，你可以确保 Docker 容器既灵活又可维护，并且可以轻松适应不同的部署环境。
