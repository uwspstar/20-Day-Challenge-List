### Handling Multiple File Uploads and Validation in FastAPI

[Back to 7天的FastAPI学习计划](https://github.com/uwspstar/20-Day-Challenge-List/blob/main/FastAPI/Readme.MD)

#### 1. Introduction 简介

**English:**
Handling multiple file uploads is a common scenario in web applications, where users may need to upload several files at once, such as images or documents. FastAPI allows you to handle multiple file uploads easily and efficiently. In addition, you can implement validation to ensure that the uploaded files meet specific criteria, such as file type, size, and content.

**Chinese:**
在 Web 应用程序中处理多个文件上传是一个常见的场景，用户可能需要一次上传多个文件，例如图片或文档。FastAPI 使你能够轻松高效地处理多个文件上传。此外，你还可以实现验证，以确保上传的文件符合特定的标准，例如文件类型、大小和内容。

---

#### 2. Handling Multiple File Uploads 处理多个文件上传

**English:**
To handle multiple file uploads in FastAPI, you can define an endpoint that accepts a list of `UploadFile` objects. This allows clients to upload several files in a single request.

**Chinese:**
要在 FastAPI 中处理多个文件上传，你可以定义一个接受 `UploadFile` 对象列表的端点。这允许客户端在单个请求中上传多个文件。

**Example 例子:**

```python
from typing import List
from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/uploadfiles/")
async def upload_files(files: List[UploadFile] = File(...)):
    file_details = []
    for file in files:
        content = await file.read()
        file_details.append({
            "filename": file.filename,
            "content_type": file.content_type,
            "size": len(content)
        })
    return {"files": file_details}
```

**Explanation 解释:**

- **English:**
  - `files: List[UploadFile] = File(...)`: This parameter accepts a list of files uploaded by the client. Each item in the list is an `UploadFile` object.
  - The function iterates over each file, reads its content, and collects details like filename, content type, and size. These details are returned as part of the response.

- **Chinese:**
  - `files: List[UploadFile] = File(...)`: 这个参数接受客户端上传的文件列表。列表中的每个项目都是一个 `UploadFile` 对象。
  - 函数遍历每个文件，读取其内容，并收集文件名、内容类型和大小等详细信息。这些详细信息作为响应的一部分返回。

---

#### 3. Validating Multiple Uploaded Files 验证多个上传的文件

**English:**
When handling multiple file uploads, it's essential to validate each file to ensure it meets your application's requirements. Common validations include checking the file type, size, and content.

**Chinese:**
在处理多个文件上传时，验证每个文件以确保其符合应用程序的要求至关重要。常见的验证包括检查文件类型、大小和内容。

**Example 例子:**

```python
@app.post("/uploadfiles/")
async def upload_files(files: List[UploadFile] = File(...)):
    accepted_file_types = ["image/jpeg", "image/png"]
    max_size = 1024 * 1024 * 5  # 5 MB

    file_details = []
    for file in files:
        if file.content_type not in accepted_file_types:
            return {"error": f"File type {file.content_type} not supported"}
        
        content = await file.read()
        if len(content) > max_size:
            return {"error": f"File {file.filename} is too large"}
        
        file_details.append({
            "filename": file.filename,
            "content_type": file.content_type,
            "size": len(content)
        })
    
    return {"files": file_details, "message": "All files uploaded successfully"}
```

**Explanation 解释:**

- **English:**
  - **File Type Validation:** The function checks if each file's content type is in the list of accepted file types (`image/jpeg` and `image/png`). If a file has an unsupported content type, the function returns an error message.
  - **File Size Validation:** The function checks if the file size exceeds 5 MB. If a file is too large, the function returns an error message.
  - **File Processing:** If all validations pass, the function processes the files and returns details such as filename, content type, and size, along with a success message.

- **Chinese:**
  - **文件类型验证:** 函数检查每个文件的内容类型是否在接受的文件类型列表（`image/jpeg` 和 `image/png`）中。如果文件具有不支持的内容类型，函数将返回错误消息。
  - **文件大小验证:** 函数检查文件大小是否超过 5 MB。如果文件太大，函数将返回错误消息。
  - **文件处理:** 如果所有验证通过，函数处理文件并返回文件名、内容类型和大小等详细信息，以及一条成功消息。

---

#### 4. Saving Multiple Files to the Server 将多个文件保存到服务器

**English:**
After validating the files, you might want to save them to the server. You can use Python's file handling methods to write each file to the desired location on the server.

**Chinese:**
在验证文件之后，你可能希望将它们保存到服务器。你可以使用 Python 的文件处理方法将每个文件写入服务器上的指定位置。

**Example 例子:**

```python
import os

@app.post("/uploadfiles/")
async def upload_files(files: List[UploadFile] = File(...)):
    accepted_file_types = ["image/jpeg", "image/png"]
    max_size = 1024 * 1024 * 5  # 5 MB

    file_details = []
    for file in files:
        if file.content_type not in accepted_file_types:
            return {"error": f"File type {file.content_type} not supported"}
        
        content = await file.read()
        if len(content) > max_size:
            return {"error": f"File {file.filename} is too large"}
        
        file_path = f"uploads/{file.filename}"
        with open(file_path, "wb") as f:
            f.write(content)
        
        file_details.append({
            "filename": file.filename,
            "content_type": file.content_type,
            "size": len(content),
            "saved_to": file_path
        })
    
    return {"files": file_details, "message": "All files uploaded and saved successfully"}
```

**Explanation 解释:**

- **English:**
  - **File Path Definition:** `file_path = f"uploads/{file.filename}"` defines the path where each file will be saved on the server.
  - **Saving Files:** The function uses a `with open(file_path, "wb") as f` block to write the file content to the specified path.
  - **Response:** After saving the files, the function returns details about each file, including the filename, content type, size, and the location where the file was saved.

- **Chinese:**
  - **文件路径定义:** `file_path = f"uploads/{file.filename}"` 定义了每个文件将被保存到服务器上的路径。
  - **保存文件:** 函数使用 `with open(file_path, "wb") as f` 语句块将文件内容写入指定路径。
  - **响应:** 在保存文件后，函数返回每个文件的详细信息，包括文件名、内容类型、大小和文件保存的位置。

---

#### 5. Tips and Warnings 提示与警告

**Tips 提示:**

1. **Proper File Validation:**
   - Always validate file types and sizes to ensure that only acceptable files are uploaded. This prevents potential security risks and ensures the integrity of your application.
   - 始终验证文件类型和大小，以确保仅上传可接受的文件。这可以防止潜在的安全风险，并确保应用程序的完整性。

2. **Organizing Uploaded Files:**
   - Consider organizing uploaded files in a structured directory system, such as categorizing by file type or user, to make file management easier.
   - 考虑将上传的文件按结构化目录系统进行组织，例如按文件类型或用户分类，以便更容易地管理文件。

**Warnings 警告:**

1. **Security Risks:**
   - Be cautious about storing files directly on the server. Ensure that file names are sanitized to prevent path traversal attacks, and consider storing files in a secure location.
   - 注意直接在服务器上存储文件的安全风险。确保对文件名进行清理以防止路径遍历攻击，并考虑将文件存储在安全的位置。

2. **Handling Large Files:**
   - When dealing with large file uploads, consider implementing file size limits and streaming uploads to handle large files efficiently without consuming too much memory.
   - 在处理大文件上传时，考虑实施文件大小限制，并通过流式上传高效处理大文件，避免消耗过多内存。

---

#### 6. Recommended Resources 推荐资源

1. **FastAPI Documentation:**
   - Explore detailed information on handling file uploads and validations in FastAPI.
   - 查看关于在 FastAPI 中处理文件上传和验证的详细信息。
   - [FastAPI Documentation](https://fastapi.tiangolo.com/tutorial/request-files/)

2. **Python File Handling:**
   - Learn more about file handling in Python, including reading, writing, and working with files.
   - 了解更多关于 Python 文件处理的信息，包括读取、写入和处理文件。
   - [Python File Handling](

https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)

3. **Security Guidelines for File Uploads:**
   - Review best practices for securely handling file uploads in web applications.
   - 查看安全处理 Web 应用程序中文件上传的最佳实践。
   - [OWASP File Upload Guidelines](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)

This explanation provides a comprehensive guide on handling multiple file uploads and validation in FastAPI, including detailed examples, tips, warnings, and recommended resources in both English and Chinese.
