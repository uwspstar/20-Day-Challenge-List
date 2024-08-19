# Docker volumes-related commands

Here's a list of commonly used Docker volumes-related commands:

| Command                   | Description (English)                                           | 描述 (Chinese)                                                | Example Usage                                      |
|---------------------------|-----------------------------------------------------------------|---------------------------------------------------------------|----------------------------------------------------|
| `docker volume create`     | Creates a new Docker volume                                     | 创建一个新的 Docker 卷                                          | `docker volume create volume-name`                 |
| `docker volume ls`         | Lists all Docker volumes on your local system                   | 列出本地系统上的所有 Docker 卷                                 | `docker volume ls`                                 |
| `docker volume inspect`    | Displays detailed information about a specific Docker volume    | 显示有关特定 Docker 卷的详细信息                               | `docker volume inspect volume-name`                |
| `docker volume rm`         | Removes one or more Docker volumes                              | 删除一个或多个 Docker 卷                                       | `docker volume rm volume-name`                     |
| `docker volume prune`      | Removes all unused Docker volumes                               | 删除所有未使用的 Docker 卷                                     | `docker volume prune`                              |
| `docker run -v`            | Creates and mounts a volume to a container                      | 创建并将卷挂载到容器。如果指定的卷不存在，Docker 会创建它       | `docker run -d -v volume-name:/path/in/container image-name` |
| `docker run --mount`       | Mounts volumes with more options and flexibility than `-v`      | 相比于 `-v` 提供更多选项和灵活性的挂载卷的方法                  | `docker run -d --mount source=volume-name,target=/path/in/container image-name` |
| `docker volume help`       | Displays help information for Docker volume commands            | 显示 Docker 卷命令的帮助信息                                  | `docker volume help`                               |


### 1. **docker volume create**
- **English**: Creates a new Docker volume.
- **Chinese**: 创建一个新的 Docker 卷。
- **Usage**: 
  ```bash
  docker volume create volume-name
  ```

### 2. **docker volume ls**
- **English**: Lists all Docker volumes on your local system.
- **Chinese**: 列出本地系统上的所有 Docker 卷。
- **Usage**: 
  ```bash
  docker volume ls
  ```

### 3. **docker volume inspect**
- **English**: Displays detailed information about a specific Docker volume.
- **Chinese**: 显示有关特定 Docker 卷的详细信息。
- **Usage**: 
  ```bash
  docker volume inspect volume-name
  ```

### 4. **docker volume rm**
- **English**: Removes one or more Docker volumes.
- **Chinese**: 删除一个或多个 Docker 卷。
- **Usage**: 
  ```bash
  docker volume rm volume-name
  ```

### 5. **docker volume prune**
- **English**: Removes all unused Docker volumes.
- **Chinese**: 删除所有未使用的 Docker 卷。
- **Usage**: 
  ```bash
  docker volume prune
  ```

### 6. **docker run -v**
- **English**: Creates and mounts a volume to a container. If the specified volume doesn't exist, Docker will create it.
- **Chinese**: 创建并将卷挂载到容器。如果指定的卷不存在，Docker 会创建它。
- **Usage**: 
  ```bash
  docker run -d -v volume-name:/path/in/container image-name
  ```

### 7. **docker run --mount**
- **English**: Another method to mount volumes with more options and flexibility compared to `-v`.
- **Chinese**: 另一种挂载卷的方法，相比于 `-v` 提供更多的选项和灵活性。
- **Usage**: 
  ```bash
  docker run -d --mount source=volume-name,target=/path/in/container image-name
  ```

### 8. **docker volume help**
- **English**: Displays help information for Docker volume commands.
- **Chinese**: 显示 Docker 卷命令的帮助信息。
- **Usage**: 
  ```bash
  docker volume help
  ```

These commands are essential for managing Docker volumes, from creating and listing volumes to inspecting, removing, and utilizing them in containers.
