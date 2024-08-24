# Bash `curl` Command

## 什么是 `curl`？What is `curl`?

`curl` is a command-line tool used for transferring data from or to a server using various protocols such as HTTP, HTTPS, FTP, and more. The name stands for "Client URL," and it is widely used for making HTTP requests, interacting with APIs, downloading files, and testing server responses. `curl` is an essential tool in the toolkit of any developer or system administrator.

`curl` 是一个命令行工具，用于通过各种协议（如 HTTP、HTTPS、FTP 等）从服务器传输数据或向服务器传输数据。其名称代表 "Client URL"（客户端 URL），并且广泛用于发起 HTTP 请求、与 API 交互、下载文件和测试服务器响应。`curl` 是任何开发人员或系统管理员工具包中的一个重要工具。

## 基本语法
## Basic Syntax

```bash
curl [options] [URL]
```

- **URL**: The address of the resource you want to interact with.
- **options**: Various options to customize the behavior of `curl`.

- **URL**：要与之交互的资源的地址。
- **options**：用于自定义 `curl` 行为的各种选项。

## 示例
## Examples

### 1. 基本 GET 请求
### 1. Basic GET Request

```bash
curl http://example.com
```

**解释**：此命令向 `http://example.com` 发送一个 GET 请求，并将服务器响应的内容打印到终端。GET 请求是最常见的 HTTP 请求方法之一，用于从服务器请求数据。

**Explanation**: This command sends a GET request to `http://example.com` and prints the content of the server's response to the terminal. A GET request is one of the most common HTTP request methods, used to request data from a server.

### 2. 保存响应到文件
### 2. Save Response to a File

```bash
curl -o output.html http://example.com
```

**解释**：此命令将 `http://example.com` 的响应保存到名为 `output.html` 的文件中，而不是打印到终端。

**Explanation**: This command saves the response from `http://example.com` to a file named `output.html` instead of printing it to the terminal.

### 3. 下载文件
### 3. Download a File

```bash
curl -O http://example.com/file.zip
```

**解释**：此命令下载 `http://example.com/file.zip` 并将其保存到当前目录中。`-O` 选项表示使用远程文件名保存文件。

**Explanation**: This command downloads the file `http://example.com/file.zip` and saves it in the current directory. The `-O` option tells `curl` to save the file with its remote name.

### 4. 发送 POST 请求
### 4. Sending a POST Request

```bash
curl -X POST -d "name=John&age=30" http://example.com/form
```

**解释**：此命令向 `http://example.com/form` 发送一个 POST 请求，并将表单数据 `name=John&age=30` 作为请求主体发送。POST 请求通常用于提交数据到服务器。

**Explanation**: This command sends a POST request to `http://example.com/form`, with the form data `name=John&age=30` included in the request body. POST requests are typically used to submit data to a server.

### 5. 发送 JSON 数据
### 5. Sending JSON Data

```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"John", "age":30}' http://example.com/api/users
```

**解释**：此命令向 `http://example.com/api/users` 发送一个 POST 请求，并将 JSON 格式的数据作为请求主体发送。`-H "Content-Type: application/json"` 用于设置请求头，指示发送的数据为 JSON 格式。

**Explanation**: This command sends a POST request to `http://example.com/api/users` with JSON data in the request body. The `-H "Content-Type: application/json"` option sets the request header to indicate that the data being sent is in JSON format.

### 6. 添加自定义请求头
### 6. Adding Custom Request Headers

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" http://example.com/api/data
```

**解释**：此命令向 `http://example.com/api/data` 发送一个 GET 请求，并在请求头中添加 `Authorization: Bearer YOUR_TOKEN`，用于认证或授权。

**Explanation**: This command sends a GET request to `http://example.com/api/data` and includes a custom request header `Authorization: Bearer YOUR_TOKEN`, typically used for authentication or authorization.

### 7. 处理重定向
### 7. Handling Redirects

```bash
curl -L http://example.com
```

**解释**：此命令将跟随服务器返回的任何重定向（如 301 或 302 响应），并最终返回重定向后的资源。`-L` 选项用于告诉 `curl` 跟随重定向。

**Explanation**: This command follows any redirects (e.g., 301 or 302 responses) returned by the server and ultimately retrieves the redirected resource. The `-L` option tells `curl` to follow redirects.

### 8. 显示 HTTP 响应头
### 8. Displaying HTTP Response Headers

```bash
curl -I http://example.com
```

**解释**：此命令将只显示 `http://example.com` 的 HTTP 响应头信息，而不包括响应主体。`-I` 选项用于发送 HEAD 请求。

**Explanation**: This command displays only the HTTP response headers from `http://example.com`, without the response body. The `-I` option sends a HEAD request.

### 9. 进行基本认证
### 9. Performing Basic Authentication

```bash
curl -u username:password http://example.com/protected
```

**解释**：此命令使用提供的用户名和密码对 `http://example.com/protected` 进行基本 HTTP 认证。`-u` 选项用于指定认证凭据。

**Explanation**: This command performs basic HTTP authentication to access `http://example.com/protected` using the provided username and password. The `-u` option specifies the authentication credentials.

### 10. 限制下载速度
### 10. Limiting Download Speed

```bash
curl --limit-rate 100k http://example.com/file.zip -O
```

**解释**：此命令将下载 `http://example.com/file.zip`，并将下载速度限制为每秒 100 KB。`--limit-rate` 选项用于控制下载速度。

**Explanation**: This command downloads `http://example.com/file.zip` and limits the download speed to 100 KB per second. The `--limit-rate` option controls the download speed.

## 复杂用法
## Advanced Usage

### 1. 发送文件作为表单数据
### 1. Sending Files as Form Data

```bash
curl -F "file=@/path/to/file.txt" http://example.com/upload
```

**解释**：此命令将本地文件 `/path/to/file.txt` 作为表单数据上传到 `http://example.com/upload`。`-F` 选项用于指定表单数据，其中 `@` 表示文件路径。

**Explanation**: This command uploads a local file located at `/path/to/file.txt` as form data to `http://example.com/upload`. The `-F` option specifies form data, where `@` indicates the file path.

### 2. 静默模式（不输出进度）
### 2. Silent Mode (No Progress Output)

```bash
curl -s http://example.com
```

**解释**：此命令将在静默模式下运行 `curl`，不显示任何下载进度或错误消息。`-s` 选项用于静默模式。

**Explanation**: This command runs `curl` in silent mode, suppressing all download progress and error messages. The `-s` option enables silent mode.

### 3. 测试服务器响应时间
### 3. Testing Server Response Time

```bash
curl -w "Time: %{time_total}s\n" -o /dev/null -s http://example.com
```

**解释**：此命令将测试 `http://example.com` 的服务器响应时间，并以秒为单位打印总时间。`-w` 选项用于格式化输出，`-o /dev/null` 忽略响应主体，`-s` 使命令静默运行。

**Explanation**: This command tests the server response time for `http://example.com` and prints the total time in seconds. The `-w` option formats the output, `-o /dev/null` discards the response body, and `-s` runs the command silently.

## 常用选项
## Common Options

- **`-X`**: 指定请求方法（如 GET、POST、PUT、DELETE）。
- **`-d`**: 发送请求数据。
- **`-H`**: 添加自定义请求头。
- **`-o`**:

 保存响应到指定文件。
- **`-O`**: 使用远程文件名保存下载的文件。
- **`-u`**: 指定用户名和密码进行认证。
- **`-I`**: 发送 HEAD 请求，只获取响应头。
- **`-L`**: 跟随重定向。
- **`-F`**: 指定表单数据进行文件上传。
- **`-s`**: 静默模式，抑制进度条和错误消息。
- **`--limit-rate`**: 限制下载速度。

- **`-X`**: Specify the request method (e.g., GET, POST, PUT, DELETE).
- **`-d`**: Send data in the request.
- **`-H`**: Add custom request headers.
- **`-o`**: Save the response to a specified file.
- **`-O`**: Save the downloaded file with its remote name.
- **`-u`**: Specify the username and password for authentication.
- **`-I`**: Send a HEAD request to retrieve headers only.
- **`-L`**: Follow redirects.
- **`-F`**: Specify form data for file uploads.
- **`-s`**: Silent mode, suppress progress and error messages.
- **`--limit-rate`**: Limit the download speed.

## 结论
## Conclusion

The `curl` command is an extremely versatile and powerful tool for interacting with web servers and APIs. It is commonly used for tasks such as downloading files, testing API endpoints, automating web requests, and even performing complex data transfers. Mastering `curl` is essential for developers, sysadmins, and anyone who regularly works with HTTP or other network protocols.

`curl` 命令是一个极其多功能且强大的工具，用于与 Web 服务器和 API 进行交互。它通常用于下载文件、测试 API 端点、自动化 Web 请求，甚至执行复杂的数据传输。掌握 `curl` 对于开发人员、系统管理员以及任何经常处理 HTTP 或其他网络协议的人来说都是必不可少的技能。
