### Comparison Table for HTTP Status Codes

| **Status Code** | **Category**        | **Description**                                                    | **Common Use Cases**                                             | **Example**               |
|-----------------|---------------------|--------------------------------------------------------------------|------------------------------------------------------------------|---------------------------|
| **100 Continue**| Informational (1xx)  | The request has been received, and the client can continue to send | Initial acknowledgment for large uploads                         | Initiating file upload    |
| **200 OK**      | Success (2xx)        | The request was successful, and the response contains the data     | Standard response for successful HTTP requests                   | Fetching user profile     |
| **201 Created** | Success (2xx)        | The request has been fulfilled, and a new resource is created      | POST request to create a new resource                            | Creating a new account    |
| **204 No Content**| Success (2xx)      | The request was successful but no content is returned              | Deleting a resource, no data to return                           | Deleting a record         |
| **301 Moved Permanently**| Redirection (3xx) | The requested resource has been permanently moved to a new URL    | Permanent redirection of a URL                                   | Old URL redirects to new  |
| **302 Found**   | Redirection (3xx)    | The requested resource is temporarily available at a different URL | Temporary redirect for maintenance                               | Temporary website move    |
| **400 Bad Request** | Client Error (4xx)  | The server could not understand the request due to invalid syntax  | Malformed request (e.g., missing required parameters)             | Missing form field        |
| **401 Unauthorized** | Client Error (4xx) | The request requires user authentication                          | Accessing protected resources without valid credentials           | Accessing user dashboard  |
| **403 Forbidden** | Client Error (4xx)  | The client does not have permission to access the resource         | Trying to access restricted content                              | Accessing admin page      |
| **404 Not Found** | Client Error (4xx)  | The requested resource could not be found on the server            | Requesting a non-existent page                                   | Broken link               |
| **500 Internal Server Error** | Server Error (5xx) | The server encountered an unexpected condition                    | Server misconfiguration or crash                                 | Server down               |
| **502 Bad Gateway** | Server Error (5xx) | The server received an invalid response from an upstream server    | A proxy or gateway error                                         | Reverse proxy error       |

### Code Example for HTTP Status Codes using FastAPI (Python)

Below is a code example that demonstrates how to return various **HTTP status codes** in a FastAPI application.

```python
from fastapi import FastAPI, HTTPException, status

app = FastAPI()

# In-memory user data simulation
users_db = {
    1: {"name": "Alice", "email": "alice@example.com"},
    2: {"name": "Bob", "email": "bob@example.com"},
}

# 200 OK: Success response
@app.get("/users/{user_id}")
def get_user(user_id: int):
    if user_id in users_db:
        return users_db[user_id]
    raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="User not found")

# 201 Created: Resource created
@app.post("/users", status_code=status.HTTP_201_CREATED)
def create_user(user: dict):
    user_id = len(users_db) + 1
    users_db[user_id] = user
    return {"id": user_id, "user": users_db[user_id]}

# 204 No Content: Successfully processed but no content to return
@app.delete("/users/{user_id}", status_code=status.HTTP_204_NO_CONTENT)
def delete_user(user_id: int):
    if user_id in users_db:
        del users_db[user_id]
        return  # Returning no content
    raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="User not found")

# 400 Bad Request: Invalid request
@app.get("/search")
def search_user(email: str = None):
    if not email:
        raise HTTPException(status_code=status.HTTP_400_BAD_REQUEST, detail="Email query parameter is required")
    for user in users_db.values():
        if user["email"] == email:
            return user
    raise HTTPException(status_code=status.HTTP_404_NOT_FOUND, detail="User not found")

# 401 Unauthorized: Access denied
@app.get("/protected")
def protected_resource(auth_token: str = None):
    if not auth_token or auth_token != "secret-token":
        raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="Unauthorized access")
    return {"message": "Access granted"}

# 500 Internal Server Error: Server error simulation
@app.get("/trigger-error")
def trigger_error():
    raise HTTPException(status_code=status.HTTP_500_INTERNAL_SERVER_ERROR, detail="Something went wrong on the server")
```

### Explanation of the Code:

1. **200 OK**: A successful request returning user data.
   - **GET `/users/{user_id}`**
   - Example request: `GET http://localhost:8000/users/1`
   - **Response**:
   ```json
   {
     "name": "Alice",
     "email": "alice@example.com"
   }
   ```

2. **201 Created**: A successful resource creation (e.g., creating a new user).
   - **POST `/users`**
   - Example request:
   ```bash
   curl -X POST "http://localhost:8000/users" -H "Content-Type: application/json" -d '{"name": "Charlie", "email": "charlie@example.com"}'
   ```
   - **Response**:
   ```json
   {
     "id": 3,
     "user": {
       "name": "Charlie",
       "email": "charlie@example.com"
     }
   }
   ```

3. **204 No Content**: Successfully deleted a resource, returning no content.
   - **DELETE `/users/{user_id}`**
   - Example request: `DELETE http://localhost:8000/users/1`
   - **Response**: No content (HTTP status 204).

4. **400 Bad Request**: If a required query parameter is missing or malformed.
   - **GET `/search?email=invalid`**
   - Example request:
   ```bash
   curl -X GET "http://localhost:8000/search"
   ```
   - **Response**:
   ```json
   {
     "detail": "Email query parameter is required"
   }
   ```

5. **401 Unauthorized**: Unauthorized access, e.g., missing or invalid token.
   - **GET `/protected`**
   - Example request:
   ```bash
   curl -X GET "http://localhost:8000/protected"
   ```
   - **Response**:
   ```json
   {
     "detail": "Unauthorized access"
   }
   ```

6. **500 Internal Server Error**: Simulating a server-side error.
   - **GET `/trigger-error`**
   - Example request:
   ```bash
   curl -X GET "http://localhost:8000/trigger-error"
   ```
   - **Response**:
   ```json
   {
     "detail": "Something went wrong on the server"
   }
   ```

### Summary:

This example demonstrates how to handle different **HTTP status codes** using FastAPI. Each status code corresponds to specific scenarios in API development, whether it’s for successful responses (2xx), client errors (4xx), or server errors (5xx). The comparison table provides a high-level overview of common HTTP status codes, their use cases, and practical examples.
