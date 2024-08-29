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

### Explanation of the Command

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

