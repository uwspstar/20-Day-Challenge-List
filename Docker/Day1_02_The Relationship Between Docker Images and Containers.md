# 镜像（Image）和容器（Container）的关系 The Relationship Between Docker Images and Containers

在 Docker 中，镜像（Image）和容器（Container）之间的关系类似于面向对象程序设计中的类（Class）和实例（Instance）的关系。镜像就像是一个类，它定义了应用程序的所有组成部分和依赖项，而容器就像是类的实例，是镜像在运行时的具体化体现。理解这一点对于掌握 Docker 的使用至关重要。

In Docker, the relationship between an image and a container is akin to the relationship between a class and an instance in object-oriented programming. The image is like a class, defining all the components and dependencies of an application, while the container is like an instance, representing the actual running entity of the image. Understanding this analogy is crucial for effectively using Docker.

## 镜像是静态的定义 Docker Images as Static Definitions

### What is a Docker Image? 什么是 Docker 镜像？

Docker 镜像是一个静态的、不可变的文件，包含了应用程序运行所需的所有指令。它包括应用程序的代码、运行时、库和其他依赖项，以及运行时环境的配置。镜像是由一系列分层文件系统构成的，每一层都可以添加新的功能或改变现有的功能。当你从镜像创建容器时，这些层会被合并成一个统一的文件系统供容器使用。

A Docker image is a static, immutable file that contains all the instructions needed to run an application. It includes the application's code, runtime, libraries, and other dependencies, as well as the configuration for the runtime environment. Images are composed of a series of layered filesystems, each layer adding new functionality or modifying existing ones. When you create a container from an image, these layers are combined into a single unified filesystem for the container to use.

### Example of a Docker Image Docker 镜像示例

Consider a simple `Dockerfile` that creates a Docker image for a Python application:

考虑一个简单的 `Dockerfile`，它为一个 Python 应用程序创建 Docker 镜像：

```dockerfile
# Use the official Python image as the base
FROM python:3.8-slim

# Set the working directory
WORKDIR /app

# Copy the application code into the container
COPY . /app

# Install the required Python packages
RUN pip install -r requirements.txt

# Define the command to run the application
CMD ["python", "app.py"]
```

When you build this Dockerfile using the `docker build` command, it creates a Docker image. This image is a static definition of everything needed to run the Python application. It does not execute anything on its own but serves as a template for creating containers.

当你使用 `docker build` 命令构建这个 `Dockerfile` 时，它会创建一个 Docker 镜像。这个镜像是运行 Python 应用程序所需的所有内容的静态定义。它本身不会执行任何操作，而是作为创建容器的模板。

## 容器是镜像的运行时实体 Containers as Runtime Instances of Images

### What is a Docker Container? 什么是 Docker 容器？

Docker 容器是 Docker 镜像的运行时实例。当你从镜像启动一个容器时，Docker 会创建一个可写的层，并将其放在镜像的只读层之上，这样容器中的所有更改都会记录在这个可写层中。容器是独立的，意味着它们可以在不影响其他容器的情况下运行、修改和删除。容器的生命周期包括创建、启动、停止、删除和暂停等操作。

A Docker container is a runtime instance of a Docker image. When you start a container from an image, Docker creates a writable layer on top of the image's read-only layers, where all changes made to the container are recorded. Containers are isolated, meaning they can be run, modified, and deleted without affecting other containers. The lifecycle of a container includes operations such as creation, starting, stopping, deletion, and pausing.

### Example of Creating and Managing a Docker Container Docker 容器的创建与管理示例

1. **Creating a Container 创建容器**  
   You can create a container from an image without starting it immediately using the `docker create` command.

   你可以使用 `docker create` 命令从镜像创建一个容器，而无需立即启动它。

   ```bash
   docker create --name my-container my-python-app
   ```

2. **Starting a Container 启动容器**  
   You can start a created container using the `docker start` command.

   你可以使用 `docker start` 命令启动已创建的容器。

   ```bash
   docker start my-container
   ```

3. **Stopping a Container 停止容器**  
   You can stop a running container using the `docker stop` command.

   你可以使用 `docker stop` 命令停止正在运行的容器。

   ```bash
   docker stop my-container
   ```

4. **Deleting a Container 删除容器**  
   You can remove a stopped container using the `docker rm` command.

   你可以使用 `docker rm` 命令删除已停止的容器。

   ```bash
   docker rm my-container
   ```

5. **Pausing a Container 暂停容器**  
   You can temporarily pause all processes within a container using the `docker pause` command.

   你可以使用 `docker pause` 命令暂时暂停容器中的所有进程。

   ```bash
   docker pause my-container
   ```

### Lifecycle of a Docker Container Docker 容器的生命周期

The lifecycle of a Docker container typically involves the following stages:

Docker 容器的生命周期通常涉及以下阶段：

1. **Creation**: The container is created from an image but not yet running.
2. **Starting**: The container is started and begins executing its defined process.
3. **Running**: The container is actively running and performing its tasks.
4. **Stopping**: The container is stopped, halting all processes.
5. **Deletion**: The container is removed from the system.
6. **Pausing**: The container is paused, temporarily halting its processes without stopping it completely.

1. **创建**：容器从镜像创建，但尚未运行。
2. **启动**：容器启动并开始执行其定义的进程。
3. **运行**：容器正在积极运行并执行其任务。
4. **停止**：容器停止，终止所有进程。
5. **删除**：容器从系统中删除。
6. **暂停**：容器被暂停，暂时停止其进程，而不完全停止。

### The Analogy to Classes and Instances 类与实例的类比

Just like a class in object-oriented programming defines the properties and behaviors of objects, a Docker image defines the environment and configuration needed to run an application. However, a class is not an actual object; it’s a blueprint. Similarly, a Docker image is not a running application; it’s a blueprint for creating containers.

When you instantiate a class, you create an object that has its own state and can be manipulated independently of other objects. In Docker, when you run a container from an image, you create an independent instance of that image with its own state, which can be started, stopped, modified, or deleted without affecting the original image or other containers.

就像面向对象编程中的类定义了对象的属性和行为一样，Docker 镜像定义了运行应用程序所需的环境和配置。然而，类不是实际的对象，它是一个蓝图。同样，Docker 镜像也不是一个正在运行的应用程序，它是创建容器的蓝图。

当你实例化一个类时，你创建了一个具有自身状态的对象，并且可以独立于其他对象进行操作。在 Docker 中，当你从镜像运行一个容器时，你创建了一个独立的镜像实例，具有自己的状态，可以启动、停止、修改或删除，而不会影响原始镜像或其他容器。

## Conclusion 结论

理解 Docker 中镜像（Image）和容器（Container）之间的关系，对于掌握 Docker 的核心概念至关重要。镜像是静态的定义，就像是类的蓝图，而容器则是这些定义在运行时的具体化，就像类的实例一样。容器可以被创建、启动、停止、删除和暂停，灵活地支持应用程序的开发和部署。通过理解这种类比，您可以更好地理解 Docker 的工作方式，并更有效地使用 Docker 来管理和部署应用程序。

Understanding the relationship between Docker images and containers is crucial for mastering Docker's core concepts. An image is a static definition, like the blueprint of a class, while a container is the runtime realization of that definition, like an instance of a class. Containers can be created, started, stopped, deleted, and paused, providing flexibility in developing and deploying applications. By understanding this analogy, you can better grasp how Docker works and more effectively use Docker to manage and deploy applications.
