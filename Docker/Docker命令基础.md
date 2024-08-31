# Docker命令基础：`docker run`, `docker ps`, `docker stop`, `docker rm`, `docker images`

#### Introduction / 介绍

When working with Docker, several core commands are essential for managing containers and images. Understanding how to use these commands allows you to run, monitor, and clean up your Docker environment effectively.

在使用 Docker 时，有几个核心命令对于管理容器和镜像至关重要。了解如何使用这些命令可以帮助你有效地运行、监控和清理 Docker 环境。

#### Command 1: `docker run`

1. **Purpose / 目的**  
   `docker run` is used to create and start a new container from a Docker image. It is one of the most frequently used commands in Docker.

   **`docker run` 用于从 Docker 镜像创建并启动一个新容器。它是 Docker 中使用最频繁的命令之一。**

2. **Basic Usage / 基本用法**

   ```bash
   docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
   ```

   - **Example / 示例**: Run a Python script using the official Python image.
   - **示例**: 使用官方的 Python 镜像运行一个 Python 脚本。

   ```bash
   docker run python:3.9 python -c "print('Hello, Docker!')"
   ```

   This command will pull the Python 3.9 image (if not already present), create a new container, run the Python command, and then exit.

   **该命令将拉取 Python 3.9 镜像（如果尚未存在），创建一个新容器，运行 Python 命令，然后退出。**

3. **Common Options / 常用选项**

   - `-d`: Run the container in detached mode (in the background).
     **`-d`**: 在分离模式下运行容器（后台运行）。
   - `-p`: Publish a container’s port(s) to the host.
     **`-p`**: 将容器的端口发布到主机。
   - `--name`: Assign a name to the container.
     **`--name`**: 为容器分配一个名称。
   - `-v`: Bind mount a volume.
     **`-v`**: 绑定挂载一个卷。

   - **Example / 示例**: Run a container in detached mode with a specific name and port mapping.
   - **示例**: 在分离模式下运行一个容器，并指定名称和端口映射。

   ```bash
   docker run -d --name my_container -p 8080:80 nginx
   ```

#### Command 2: `docker ps`

1. **Purpose / 目的**  
   `docker ps` lists the running containers on your system. It's useful for checking which containers are currently active.

   **`docker ps` 列出系统上正在运行的容器。它对于检查当前活跃的容器非常有用。**

2. **Basic Usage / 基本用法**

   ```bash
   docker ps [OPTIONS]
   ```

   - **Example / 示例**: List all running containers.
   - **示例**: 列出所有正在运行的容器。

   ```bash
   docker ps
   ```

3. **Common Options / 常用选项**

   - `-a`: Show all containers (not just running ones).
     **`-a`**: 显示所有容器（不仅仅是正在运行的容器）。
   - `-q`: Only display numeric IDs.
     **`-q`**: 仅显示数字 ID。
   - `--filter`: Filter output based on conditions provided.
     **`--filter`**: 根据提供的条件过滤输出。

   - **Example / 示例**: List all containers, including stopped ones.
   - **示例**: 列出所有容器，包括已停止的容器。

   ```bash
   docker ps -a
   ```

#### Command 3: `docker stop`

1. **Purpose / 目的**  
   `docker stop` stops a running container. It sends a SIGTERM signal to the main process inside the container, allowing it to gracefully shut down.

   **`docker stop` 停止一个正在运行的容器。它向容器内的主进程发送 SIGTERM 信号，允许其正常关闭。**

2. **Basic Usage / 基本用法**

   ```bash
   docker stop [OPTIONS] CONTAINER [CONTAINER...]
   ```

   - **Example / 示例**: Stop a container by name.
   - **示例**: 通过名称停止一个容器。

   ```bash
   docker stop my_container
   ```

3. **Common Options / 常用选项**

   - `-t`: Time to wait before killing the container (defaults to 10 seconds).
     **`-t`**: 在杀死容器之前等待的时间（默认为 10 秒）。

   - **Example / 示例**: Stop a container with a 5-second timeout.
   - **示例**: 在 5 秒超时后停止一个容器。

   ```bash
   docker stop -t 5 my_container
   ```

#### Command 4: `docker rm`

1. **Purpose / 目的**  
   `docker rm` removes one or more containers. A container must be stopped before it can be removed.

   **`docker rm` 删除一个或多个容器。容器必须先停止，然后才能删除。**

2. **Basic Usage / 基本用法**

   ```bash
   docker rm [OPTIONS] CONTAINER [CONTAINER...]
   ```

   - **Example / 示例**: Remove a stopped container by name.
   - **示例**: 通过名称删除一个已停止的容器。

   ```bash
   docker rm my_container
   ```

3. **Common Options / 常用选项**

   - `-f`: Force remove a running container (using `docker stop` internally).
     **`-f`**: 强制删除正在运行的容器（内部使用 `docker stop`）。
   - `-v`: Remove the volumes associated with the container.
     **`-v`**: 删除与容器关联的卷。

   - **Example / 示例**: Force remove a container along with its volumes.
   - **示例**: 强制删除容器及其卷。

   ```bash
   docker rm -f -v my_container
   ```

#### Command 5: `docker images`

1. **Purpose / 目的**  
   `docker images` lists all the Docker images on your system. It helps you manage the images that you have downloaded or built.

   **`docker images` 列出系统上的所有 Docker 镜像。它可以帮助你管理已下载或构建的镜像。**

2. **Basic Usage / 基本用法**

   ```bash
   docker images [OPTIONS] [REPOSITORY[:TAG]]
   ```

   - **Example / 示例**: List all Docker images on your system.
   - **示例**: 列出系统上的所有 Docker 镜像。

   ```bash
   docker images
   ```

3. **Common Options / 常用选项**

   - `-q`: Show only the image IDs.
     **`-q`**: 仅显示镜像 ID。
   - `--filter`: Filter output based on conditions provided.
     **`--filter`**: 根据提供的条件过滤输出。
   - `--no-trunc`: Don’t truncate output.
     **`--no-trunc`**: 不截断输出。

   - **Example / 示例**: List all image IDs only.
   - **示例**: 仅列出所有镜像的 ID。

   ```bash
   docker images -q
   ```

#### Summary / 总结

These basic Docker commands (`docker run`, `docker ps`, `docker stop`, `docker rm`, `docker images`) are essential for managing Docker containers and images. They provide the functionality needed to run containers, monitor their status, stop and remove them, and manage images.

这些基本的 Docker 命令（`docker run`，`docker ps`，`docker stop`，`docker rm`，`docker images`）对于管理 Docker 容器和镜像至关重要。它们提供了运行容器、监控其状态、停止和删除它们以及管理镜像所需的功能。

#### 5Ws / 5个W

1. **What:** Introduction to essential Docker commands for container and image management.
   **什么:** 介绍用于容器和镜像管理的基本 Docker 命令。
2. **Why:** To effectively manage Docker containers and images, ensuring smooth operation in a Dockerized environment.
   **为什么:** 为了有效管理 Docker 容器和镜像，确保 Docker 化环境中的顺利操作。
3. **When:** Whenever you need to create, run, monitor, stop, remove containers, or manage images.
   **什么时候:** 无论何时需要创建、运行、监控、停止、删除容器或管理镜像时。
4. **Where:** In any environment that uses Docker for containerized applications.
   **在哪里:** 在任何使用 Docker 进行容器化应用程序的环境中。
5. **Who:** Developers, DevOps engineers, system administrators working with Docker.
   **谁:** 使用 Docker 的开发人员、DevOps 工程师、系统管理员。

#### Recommended

 Resources / 推荐资源

1. **Docker CLI Documentation:** [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)
2. **Docker Run Command:** [Docker Run](https://docs.docker.com/engine/reference/run/)
3. **Docker PS Command:** [Docker PS](https://docs.docker.com/engine/reference/commandline/ps/)

1. **Docker CLI 文档:** [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)
2. **Docker Run 命令:** [Docker Run](https://docs.docker.com/engine/reference/run/)
3. **Docker PS 命令:** [Docker PS](https://docs.docker.com/engine/reference/commandline/ps/)

---

By mastering these Docker commands, you can efficiently manage your containers and images, ensuring that your Docker environment remains organized and under control.

通过掌握这些 Docker 命令，你可以高效地管理你的容器和镜像，确保你的 Docker 环境保持有序和可控。
