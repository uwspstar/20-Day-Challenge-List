# Docker container-related commands

Here's a list of commonly used Docker container-related commands:

| Command              | Description (English)                                               | 描述 (Chinese)                                           | Example Usage                                   |
|----------------------|---------------------------------------------------------------------|----------------------------------------------------------|-------------------------------------------------|
| `docker run`         | Runs a command in a new container                                   | 在一个新的容器中运行一个命令                              | `docker run -d -p 8080:80 --name my-container nginx` |
| `docker ps`          | Lists all running containers                                        | 列出所有正在运行的容器                                    | `docker ps`                                      |
| `docker ps -a`       | Lists all containers, including stopped ones                        | 列出所有容器，包括已停止的容器                            | `docker ps -a`                                   |
| `docker stop`        | Stops one or more running containers                                | 停止一个或多个正在运行的容器                              | `docker stop container-id`                       |
| `docker start`       | Starts one or more stopped containers                               | 启动一个或多个已停止的容器                                | `docker start container-id`                      |
| `docker restart`     | Restarts one or more running containers                             | 重启一个或多个正在运行的容器                              | `docker restart container-id`                    |
| `docker rm`          | Removes one or more containers                                      | 删除一个或多个容器                                        | `docker rm container-id`                         |
| `docker logs`        | Fetches the logs of a container                                     | 获取容器的日志                                            | `docker logs container-id`                       |
| `docker exec`        | Runs a command in a running container                               | 在一个正在运行的容器中运行一个命令                        | `docker exec -it container-id bash`              |
| `docker attach`      | Attaches your terminal to a running container                       | 将您的终端连接到正在运行的容器                            | `docker attach container-id`                     |
| `docker inspect`     | Returns detailed information about a container                      | 返回有关容器的详细信息                                    | `docker inspect container-id`                    |
| `docker port`        | Lists port mappings or a specific mapping for a container           | 列出容器的端口映射或特定映射                              | `docker port container-id`                       |
| `docker cp`          | Copies files/folders between a container and the local filesystem   | 在容器与本地文件系统之间复制文件/文件夹                  | `docker cp container-id:/path/to/file /local/path` |
| `docker rename`      | Renames an existing container                                       | 重命名现有容器                                            | `docker rename old-name new-name`               |
| `docker stats`       | Displays a live stream of resource usage statistics for containers  | 实时显示容器的资源使用统计信息                            | `docker stats`                                   |
| `docker top`         | Displays the running processes of a container                       | 显示容器中运行的进程                                      | `docker top container-id`                        |
| `docker kill`        | Kills one or more running containers                                | 强制终止一个或多个正在运行的容器                          | `docker kill container-id`                       |
| `docker pause`       | Pauses all processes within a container                             | 暂停容器中的所有进程                                      | `docker pause container-id`                      |
| `docker unpause`     | Unpauses all processes within a container                           | 恢复容器中的所有进程                                      | `docker unpause container-id`                    |
| `docker update`      | Updates configuration of one or more containers                     | 更新一个或多个容器的配置                                  | `docker update --cpu-shares 512 container-id`    |


### 1. **docker run**
- **English**: Runs a command in a new container.
- **Chinese**: 在一个新的容器中运行一个命令。
- **Usage**: 
  ```bash
  docker run -d -p 8080:80 --name my-container nginx
  ```

### 2. **docker ps**
- **English**: Lists all running containers.
- **Chinese**: 列出所有正在运行的容器。
- **Usage**: 
  ```bash
  docker ps
  ```

### 3. **docker ps -a**
- **English**: Lists all containers, including stopped ones.
- **Chinese**: 列出所有容器，包括已停止的容器。
- **Usage**: 
  ```bash
  docker ps -a
  ```

### 4. **docker stop**
- **English**: Stops one or more running containers.
- **Chinese**: 停止一个或多个正在运行的容器。
- **Usage**: 
  ```bash
  docker stop container-id
  ```

### 5. **docker start**
- **English**: Starts one or more stopped containers.
- **Chinese**: 启动一个或多个已停止的容器。
- **Usage**: 
  ```bash
  docker start container-id
  ```

### 6. **docker restart**
- **English**: Restarts one or more running containers.
- **Chinese**: 重启一个或多个正在运行的容器。
- **Usage**: 
  ```bash
  docker restart container-id
  ```

### 7. **docker rm**
- **English**: Removes one or more containers.
- **Chinese**: 删除一个或多个容器。
- **Usage**: 
  ```bash
  docker rm container-id
  ```

### 8. **docker logs**
- **English**: Fetches the logs of a container.
- **Chinese**: 获取容器的日志。
- **Usage**: 
  ```bash
  docker logs container-id
  ```

### 9. **docker exec**
- **English**: Runs a command in a running container.
- **Chinese**: 在一个正在运行的容器中运行一个命令。
- **Usage**: 
  ```bash
  docker exec -it container-id bash
  ```

### 10. **docker attach**
- **English**: Attaches your terminal to a running container.
- **Chinese**: 将您的终端连接到正在运行的容器。
- **Usage**: 
  ```bash
  docker attach container-id
  ```

### 11. **docker inspect**
- **English**: Returns detailed information about a container.
- **Chinese**: 返回有关容器的详细信息。
- **Usage**: 
  ```bash
  docker inspect container-id
  ```

### 12. **docker port**
- **English**: Lists port mappings or a specific mapping for a container.
- **Chinese**: 列出容器的端口映射或特定映射。
- **Usage**: 
  ```bash
  docker port container-id
  ```

### 13. **docker cp**
- **English**: Copies files/folders between a container and the local filesystem.
- **Chinese**: 在容器与本地文件系统之间复制文件/文件夹。
- **Usage**: 
  ```bash
  docker cp container-id:/path/to/file /local/path
  ```

### 14. **docker rename**
- **English**: Renames an existing container.
- **Chinese**: 重命名现有容器。
- **Usage**: 
  ```bash
  docker rename old-name new-name
  ```

### 15. **docker stats**
- **English**: Displays a live stream of resource usage statistics for containers.
- **Chinese**: 实时显示容器的资源使用统计信息。
- **Usage**: 
  ```bash
  docker stats
  ```

### 16. **docker top**
- **English**: Displays the running processes of a container.
- **Chinese**: 显示容器中运行的进程。
- **Usage**: 
  ```bash
  docker top container-id
  ```

### 17. **docker kill**
- **English**: Kills one or more running containers.
- **Chinese**: 强制终止一个或多个正在运行的容器。
- **Usage**: 
  ```bash
  docker kill container-id
  ```

### 18. **docker pause**
- **English**: Pauses all processes within a container.
- **Chinese**: 暂停容器中的所有进程。
- **Usage**: 
  ```bash
  docker pause container-id
  ```

### 19. **docker unpause**
- **English**: Unpauses all processes within a container.
- **Chinese**: 恢复容器中的所有进程。
- **Usage**: 
  ```bash
  docker unpause container-id
  ```

### 20. **docker update**
- **English**: Updates configuration of one or more containers.
- **Chinese**: 更新一个或多个容器的配置。
- **Usage**: 
  ```bash
  docker update --cpu-shares 512 container-id
  ```

These commands are essential for managing Docker containers, from creating and running containers to inspecting, logging, and managing their lifecycle.
