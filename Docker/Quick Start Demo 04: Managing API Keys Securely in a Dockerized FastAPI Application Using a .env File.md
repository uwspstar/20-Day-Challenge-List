# Quick Start Demo 04: Managing API Keys Securely in a Dockerized FastAPI Application Using a .env File

[Back to Quick Start Demo](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Quick%20Start%20Demo.md)

To manage your API key outside the Dockerfile using a `.env` file, you'll need to make a few adjustments to your project. Here's how you can do it:

### Project Structure
```
fastapi-docker-demo/
│
├── main.py
├── Dockerfile
├── requirements.txt
└── .env
```

### 1. Create a `.env` File

In your project directory, create a `.env` file. This file will store your API key:

```plaintext
# .env
API_KEY=your_secure_api_key_here
```

### 2. Update `main.py` to Use `python-dotenv`

You'll need to update your `main.py` to load environment variables from the `.env` file using the `python-dotenv` package.

First, install `python-dotenv` by adding it to your `requirements.txt`:

```plaintext
fastapi
uvicorn
httpx
python-dotenv
```

Then, modify `main.py` to load the environment variables:

```python
from fastapi import FastAPI, HTTPException
import httpx
import os
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()

app = FastAPI()

# Fetch the API key from environment variables
API_KEY = os.getenv("API_KEY")

if not API_KEY:
    raise ValueError("API_KEY environment variable not set")

@app.get("/weather")
async def get_weather(city: str):
    # Example API endpoint that requires an API key
    weather_api_url = f"https://api.example.com/weather?city={city}&apikey={API_KEY}"

    # Make a request to the external API
    async with httpx.AsyncClient() as client:
        response = await client.get(weather_api_url)

    # Handle the response
    if response.status_code == 200:
        weather_data = response.json()
        return weather_data
    else:
        raise HTTPException(status_code=response.status_code, detail="Failed to fetch weather data")
```

### 3. Update the `Dockerfile`

In the Dockerfile, you can remove the `ENV API_KEY` line because the API key will be loaded from the `.env` file inside the container.

Here’s the updated Dockerfile:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Run uvicorn server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### 4. Build and Run the Docker Container

1. **Build the Docker image**:

   ```bash
   docker build -t fastapi-docker-demo .
   ```

2. **Run the Docker container**:

   ```bash
   docker run --name con-test -p 8000:8000 fastapi-docker-demo
   ```

### 5. Summary

By using the `.env` file:

- **Environment Variables are Managed Outside the Dockerfile**: The API key is stored securely in the `.env` file, which is not included in the Docker image. This helps keep sensitive information out of the source code and Docker image.
  
- **Flexibility in Deployment**: You can easily switch API keys or other configuration settings by modifying the `.env` file without changing the Dockerfile or the source code.

This approach is particularly useful in development and staging environments where secrets are managed externally from the application code.

------

### Explanation of the Command `RUN pip install --no-cache-dir -r requirements.txt`

The line `RUN pip install --no-cache-dir -r requirements.txt` in a Dockerfile is responsible for installing all the Python packages listed in the `requirements.txt` file into the Docker container. Let’s break down this command:

- **`RUN`**: This is a Dockerfile instruction used to execute commands in a new layer on top of the current image and commit the results. It’s commonly used to install software packages within the Docker image.

- **`pip install`**: This is the standard command to install Python packages. `pip` is the package installer for Python, and it’s used to install packages from the Python Package Index (PyPI) or other sources.

- **`--no-cache-dir`**: This option tells `pip` not to cache the packages it downloads. Normally, `pip` caches downloaded packages in the `.cache` directory to speed up future installations. However, in a Docker environment, this cache can take up unnecessary space in the final image. By using `--no-cache-dir`, you ensure that the cache is not saved, resulting in a smaller Docker image.

- **`-r requirements.txt`**: The `-r` option tells `pip` to install all the packages listed in the `requirements.txt` file. Each line in this file typically specifies a package and its version.

### Why This Step is Important

- **Installing Dependencies**: The `requirements.txt` file lists all the dependencies your application needs to run. By including this line in your Dockerfile, you ensure that your Docker container has all the necessary Python packages installed, making your application fully functional when the container starts.

- **Reproducibility**: Specifying dependencies in `requirements.txt` and installing them via `pip` ensures that your application’s environment is consistent across different deployments. This is crucial for avoiding the "it works on my machine" problem.

- **Image Size Optimization**: Using the `--no-cache-dir` option helps in keeping the Docker image size smaller by not storing unnecessary package caches, which is particularly important for efficient storage and faster deployment times.

### Practical Example

Assume your `requirements.txt` looks like this:

```plaintext
fastapi==0.70.0
uvicorn==0.15.0
httpx==0.21.1
python-dotenv==0.19.1
```

When the Dockerfile’s `RUN pip install --no-cache-dir -r requirements.txt` command is executed, it will:

1. Download the specified versions of `fastapi`, `uvicorn`, `httpx`, and `python-dotenv` from PyPI.
2. Install them in the Docker container’s Python environment.
3. Discard the download cache, ensuring that the container remains as lightweight as possible.

### Conclusion

This command is a critical part of the Docker build process, ensuring that your Python application has all the required dependencies installed while keeping the Docker image size optimized. By following this approach, you make sure that the environment within the Docker container is consistent with your development and production environments.

------

### Explanation of the Command `CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]`

The line `CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]` in a Dockerfile is used to specify the default command that should be executed when a Docker container starts. Let's break down what each part of this line does:

- **`CMD`**: 
  - This Dockerfile instruction specifies the command that will be run when a container is started. Unlike `RUN`, which is used to build the image, `CMD` is executed at runtime, when you launch a container from the image.
  - There can only be one `CMD` instruction in a Dockerfile. If multiple `CMD` instructions are specified, only the last one will take effect.
  
- **`["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]`**: 
  - This is the command that the container will execute. The command is given as a JSON array, which is the preferred way to define the command and its arguments in Docker because it avoids issues with shell parsing.
  
### Breaking Down the Uvicorn Command

- **`uvicorn`**: 
  - Uvicorn is an ASGI (Asynchronous Server Gateway Interface) server for Python web applications. It's commonly used to serve FastAPI and other ASGI-compatible frameworks. This server is fast and lightweight, making it ideal for running production-grade FastAPI applications.

- **`main:app`**: 
  - This tells Uvicorn where to find the FastAPI application instance that it needs to serve. 
  - `main` refers to the Python file `main.py`. 
  - `app` is the FastAPI instance inside the `main.py` file (e.g., `app = FastAPI()`).
  - Together, `main:app` means "import the `app` object from the `main.py` file."

- **`--host "0.0.0.0"`**: 
  - The `--host` option specifies the network interface on which Uvicorn should listen. 
  - `"0.0.0.0"` means "listen on all available network interfaces." This makes the application accessible both from inside the Docker container and from outside, such as from your local machine's browser.

- **`--port "8000"`**: 
  - The `--port` option specifies the port on which Uvicorn will listen for incoming HTTP requests.
  - `"8000"` is the common default port used for FastAPI and many other web applications during development. This means your application will be accessible at `http://localhost:8000/` on your local machine.

### Why This Step is Important

- **Entry Point**: The `CMD` instruction defines the entry point for your Docker container. It ensures that when the container starts, it runs the Uvicorn server with the specified configuration, thereby serving your FastAPI application.

- **Exposing the Application**: By setting the host to `0.0.0.0`, the application becomes accessible from outside the Docker container, which is crucial for testing and production environments where the container might be running on a remote server.

- **Default Behavior**: The `CMD` instruction provides the default behavior for the container. While it can be overridden at runtime by passing a different command, it ensures that your application runs with the expected configuration out of the box.

### Practical Example

When you build and run your Docker container, the `CMD` instruction will automatically start the Uvicorn server and serve your FastAPI application. For instance:

```bash
docker build -t fastapi-docker-demo .
docker run --name con-test -p 8000:8000 fastapi-docker-demo
```

After running these commands, your FastAPI application will be accessible at `http://localhost:8000/`.

### Conclusion

The `CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]` line is the final step in setting up your Dockerized FastAPI application. It defines how the container should start and serve your application, making sure that when the container runs, your API is ready to handle requests. This setup is essential for deploying and running FastAPI applications in a consistent and reliable manner.
