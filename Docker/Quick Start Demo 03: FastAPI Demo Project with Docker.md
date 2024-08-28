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
    response = requests.get("http://localhost:8000/joke")
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

**Expected Log Output**:
```
2024-08-28 10:00:00,000 - INFO - Starting the application
2024-08-28 10:00:00,500 - INFO - Fetched joke: Why don't programmers like nature? It has too many bugs.
2024-08-28 10:00:00,600 - INFO - Application finished
```

**Conclusion**

**English**: You now have a complete setup where a FastAPI service is running in a Docker container, and another Dockerized Python project is calling this service to fetch data. This demonstrates how to integrate different Dockerized services effectively.
**Chinese**: 您现在有一个完整的设置，其中 FastAPI 服务在 Docker 容器中运行，另一个 Docker 化的 Python 项目正在调用该服务以获取数据。这演示了如何有效地集成不同的 Docker 化服务。
