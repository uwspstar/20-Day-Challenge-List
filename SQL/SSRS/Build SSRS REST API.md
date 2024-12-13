### Build SSRS REST API

To build and interact with the **SSRS REST API**, follow these steps:

---

### Step 1: Enable SSRS REST API on the Report Server
1. **Open Reporting Services Configuration Manager**:
   - Connect to your Report Server instance.
   
2. **Configure the Web Service URL**:
   - Ensure the Web Service URL (e.g., `http://localhost/ReportServer`) is configured.
   - Verify the URL is accessible from a browser.

3. **Enable HTTPS (Optional)**:
   - While not mandatory, it's highly recommended to enable HTTPS for secure communication.

4. **Verify REST API Support**:
   - The SSRS REST API is available in SSRS 2017 and later. If you’re using a compatible version, the API is automatically enabled.

---

### Step 2: Understand the SSRS REST API Endpoints
- The SSRS REST API provides endpoints for common tasks, such as:
  - **Catalog Items**: Manage folders, reports, and data sources.
  - **Executions**: Render and export reports.
  - **Subscriptions**: Manage subscriptions for reports.

- Base URL for the API:
  ```
  http://<report_server>/api/v2.0/
  ```
  Replace `<report_server>` with your server's hostname or IP.

---

### Step 3: Install and Use Postman (Optional)
1. Download and install [Postman](https://www.postman.com/) to test REST API calls.
2. Set up a new collection for SSRS API endpoints.

---

### Step 4: Example API Calls
#### **1. Get Reports**
To list reports and folders:
- **Endpoint**: `GET http://<report_server>/api/v2.0/Folders`
- **Headers**:
  - `Accept: application/json`
  - `Authorization: Basic <Base64EncodedUsername:Password>` (if authentication is required).

#### **2. Render a Report**
To render a report:
- **Endpoint**: `POST http://<report_server>/api/v2.0/Reports(<report_id>)/Render`
- **Body** (JSON):
  ```json
  {
    "format": "PDF",
    "parameters": [
      {
        "name": "Parameter1",
        "value": "Value1"
      }
    ]
  }
  ```

#### **3. Create a Folder**
To create a new folder:
- **Endpoint**: `POST http://<report_server>/api/v2.0/Folders`
- **Body** (JSON):
  ```json
  {
    "Name": "NewFolder",
    "ParentFolderId": "<parent_folder_id>"
  }
  ```

---

### Step 5: Develop a Client Application
You can automate or interact with the SSRS REST API using programming languages like **C#**, **Python**, or **JavaScript**.

#### **C# Example**
Use `HttpClient` to call the REST API:
```csharp
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        var client = new HttpClient();
        client.BaseAddress = new Uri("http://<report_server>/api/v2.0/");
        client.DefaultRequestHeaders.Add("Accept", "application/json");

        // Example: Get Folders
        var response = await client.GetAsync("Folders");
        var content = await response.Content.ReadAsStringAsync();
        Console.WriteLine(content);
    }
}
```

#### **Python Example**
Use the `requests` library:
```python
import requests
import json

url = "http://<report_server>/api/v2.0/Folders"
headers = {
    "Accept": "application/json"
}

response = requests.get(url, headers=headers)
print(response.json())
```

---

### Step 6: Security and Authentication
- **Authentication**:
  - Basic authentication (Username/Password).
  - Windows Authentication (use NTLM or Kerberos).
- **Tokens**:
  - If you’re deploying in an enterprise, use OAuth or API tokens to enhance security.

---

### Step 7: Deploy Your Solution
1. Develop a front-end or back-end client to interact with the SSRS REST API.
2. Use the REST API to automate tasks like generating reports, creating subscriptions, or managing report catalogs.

---

Let me know if you need help with any specific part of this process!
