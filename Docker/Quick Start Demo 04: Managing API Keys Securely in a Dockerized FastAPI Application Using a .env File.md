# Quick Start Demo 04: Managing API Keys Securely in a Dockerized FastAPI Application Using a .env File

[Back to Quick Start Demo](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/Docker/Quick%20Start%20Demo.md)

To manage your API key outside the Dockerfile using a `.env` file, you'll need to make a few adjustments to your project. Here's how you can do it:

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
