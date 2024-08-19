# Docker image-related commands

Here’s a list of commonly used Docker image-related commands along with explanations in both English and Chinese:

| Command                | Description (English)                                         | 描述 (Chinese)                                               | Example Usage                                |
|------------------------|---------------------------------------------------------------|--------------------------------------------------------------|----------------------------------------------|
| `docker build`         | Builds a Docker image from a Dockerfile                       | 从 Dockerfile 构建 Docker 镜像                                | `docker build -t image-name .`               |
| `docker images`        | Lists all Docker images on your local system                  | 列出本地系统上的所有 Docker 镜像                             | `docker images`                              |
| `docker rmi`           | Removes one or more Docker images                             | 删除一个或多个 Docker 镜像                                    | `docker rmi image-name`                      |
| `docker tag`           | Tags an image with a new name                                 | 使用新名称为镜像打标签                                        | `docker tag source-image target-image`       |
| `docker pull`          | Downloads a Docker image from a registry                      | 从注册表下载 Docker 镜像                                      | `docker pull image-name`                     |
| `docker push`          | Uploads a Docker image to a registry                          | 将 Docker 镜像上传到注册表                                    | `docker push image-name`                     |
| `docker save`          | Saves one or more Docker images to a tar archive              | 将一个或多个 Docker 镜像保存为 tar 压缩文件                  | `docker save -o output.tar image-name`       |
| `docker load`          | Loads a Docker image from a tar archive                       | 从 tar 压缩文件加载 Docker 镜像                               | `docker load -i input.tar`                   |
| `docker history`       | Shows the history of an image's layers                        | 显示镜像层的历史记录                                          | `docker history image-name`                  |
| `docker inspect`       | Returns detailed information about a Docker image             | 返回有关 Docker 镜像的详细信息                                | `docker inspect image-name`                  |
| `docker commit`        | Creates a new image from a container's changes                | 从容器的更改创建新镜像                                        | `docker commit container-id new-image-name`  |
| `docker export`        | Exports a container's filesystem as a tar archive             | 将容器的文件系统导出为 tar 压缩文件                           | `docker export container-id > container.tar` |
| `docker import`        | Imports a tarball to create a filesystem image                | 导入 tar 压缩文件以创建文件系统镜像                           | `cat container.tar | docker import - new-image-name` |
| `docker rename`        | Renames an existing image                                     | 重命名现有的镜像                                              | `docker tag old-image-name new-image-name`   |
| `docker prune`         | Removes all unused Docker objects, including images           | 删除所有未使用的 Docker 对象，包括镜像                        | `docker image prune`                         |

This table provides a quick reference to common Docker image commands, including their descriptions in both English and Chinese, along with example usages.

### 1. **docker build**
- **English**: Builds a Docker image from a Dockerfile.
- **Chinese**: 从 Dockerfile 构建 Docker 镜像。
- **Usage**: 
  ```bash
  docker build -t image-name .
  ```

### 2. **docker images**
- **English**: Lists all Docker images on your local system.
- **Chinese**: 列出本地系统上的所有 Docker 镜像。
- **Usage**: 
  ```bash
  docker images
  ```

### 3. **docker rmi**
- **English**: Removes one or more Docker images.
- **Chinese**: 删除一个或多个 Docker 镜像。
- **Usage**: 
  ```bash
  docker rmi image-name
  ```

### 4. **docker tag**
- **English**: Tags an image with a new name.
- **Chinese**: 使用新名称为镜像打标签。
- **Usage**: 
  ```bash
  docker tag source-image target-image
  ```

### 5. **docker pull**
- **English**: Downloads a Docker image from a registry (e.g., Docker Hub).
- **Chinese**: 从注册表（如 Docker Hub）下载 Docker 镜像。
- **Usage**: 
  ```bash
  docker pull image-name
  ```

### 6. **docker push**
- **English**: Uploads a Docker image to a registry.
- **Chinese**: 将 Docker 镜像上传到注册表。
- **Usage**: 
  ```bash
  docker push image-name
  ```

### 7. **docker save**
- **English**: Saves one or more Docker images to a tar archive.
- **Chinese**: 将一个或多个 Docker 镜像保存为 tar 压缩文件。
- **Usage**: 
  ```bash
  docker save -o output.tar image-name
  ```

### 8. **docker load**
- **English**: Loads a Docker image from a tar archive.
- **Chinese**: 从 tar 压缩文件加载 Docker 镜像。
- **Usage**: 
  ```bash
  docker load -i input.tar
  ```

### 9. **docker history**
- **English**: Shows the history of an image's layers.
- **Chinese**: 显示镜像层的历史记录。
- **Usage**: 
  ```bash
  docker history image-name
  ```

### 10. **docker inspect**
- **English**: Returns detailed information about a Docker image.
- **Chinese**: 返回有关 Docker 镜像的详细信息。
- **Usage**: 
  ```bash
  docker inspect image-name
  ```

### 11. **docker commit**
- **English**: Creates a new image from a container's changes.
- **Chinese**: 从容器的更改创建新镜像。
- **Usage**: 
  ```bash
  docker commit container-id new-image-name
  ```

### 12. **docker export**
- **English**: Exports a container's filesystem as a tar archive (Note: different from `docker save`).
- **Chinese**: 将容器的文件系统导出为 tar 压缩文件（注意：不同于 `docker save`）。
- **Usage**: 
  ```bash
  docker export container-id > container.tar
  ```

### 13. **docker import**
- **English**: Imports a tarball to create a filesystem image.
- **Chinese**: 导入 tar 压缩文件以创建文件系统镜像。
- **Usage**: 
  ```bash
  cat container.tar | docker import - new-image-name
  ```

### 14. **docker rename**
- **English**: Renames an existing image.
- **Chinese**: 重命名现有的镜像。
- **Usage**: 
  ```bash
  docker tag old-image-name new-image-name
  ```

### 15. **docker prune**
- **English**: Removes all unused Docker objects, including images.
- **Chinese**: 删除所有未使用的 Docker 对象，包括镜像。
- **Usage**: 
  ```bash
  docker image prune
  ```

These commands cover the most common tasks you'll perform when working with Docker images, from creating and managing images to saving, loading, and cleaning them up.
