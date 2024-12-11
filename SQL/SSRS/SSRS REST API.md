### SSRS REST API

The SSRS REST API, introduced with SQL Server 2017 Reporting Services and later, is a modern, JSON-based interface that allows you to interact with the report server programmatically. Instead of relying solely on SOAP endpoints, you can now use these RESTful endpoints to manage and render reports, view folders, manage subscriptions, and much more. The API returns responses in JSON and uses HTTP methods like GET, POST, PATCH, and DELETE, making it more natural for integration with modern web applications and services.

### General Structure  
By default, the REST API endpoints are accessible at:  
```
http://<reportserver>/reports/api/v2.0
```
- `<reportserver>` is the base URL of your Reporting Services web portal. 
- `/api/v2.0` is the base path for the REST API.

### Authentication  
The REST API uses the same authentication methods as the SSRS web portal. In a typical on-prem scenario, this might be Windows Integrated Authentication.

### Common Endpoints and Examples

#### 1. Listing Items (Folders, Reports, Data Sources)  
You can explore the items stored on the report server. For example, to list all top-level folders:
```
GET http://<reportserver>/reports/api/v2.0/Folders
```
**Response (JSON):**
```json
[
  {
    "Id": "e4fa8e70-52fc-4c5c-9bf6-b9abf2d3a931",
    "Name": "MyReports",
    "Path": "/MyReports",
    "Type": "Folder",
    "Size": 0,
    "ModifiedBy": "DOMAIN\\User",
    "ModifiedDate": "2024-09-01T12:34:56.789Z",
    "CreatedBy": "DOMAIN\\User",
    "CreatedDate": "2024-09-01T12:34:56.789Z"
  }
]
```

Similarly, to get a list of all reports in the root folder:
```
GET http://<reportserver>/reports/api/v2.0/Reports
```
**Response (JSON):**
```json
[
  {
    "Id": "2f3c8571-9df0-4d76-a751-85c13f5333d2",
    "Name": "SalesReport",
    "Path": "/SalesReport",
    "Type": "Report",
    "Size": 10240,
    "ModifiedBy": "DOMAIN\\User",
    "ModifiedDate": "2024-09-02T10:20:30.000Z",
    "CreatedBy": "DOMAIN\\User",
    "CreatedDate": "2024-09-02T10:20:30.000Z"
  }
]
```

#### 2. Retrieving a Single Item  
If you know the item’s ID, you can fetch its details:
```
GET http://<reportserver>/reports/api/v2.0/Reports('<ItemId>')
```
Replace `'<ItemId>'` with the GUID you retrieved from the listing endpoints. For example:
```
GET http://<reportserver>/reports/api/v2.0/Reports('2f3c8571-9df0-4d76-a751-85c13f5333d2')
```

**Response (JSON):**
```json
{
  "Id": "2f3c8571-9df0-4d76-a751-85c13f5333d2",
  "Name": "SalesReport",
  "Path": "/SalesReport",
  "Type": "Report",
  "Description": "Monthly sales by region",
  "Hidden": false,
  "ModifiedBy": "DOMAIN\\User",
  "ModifiedDate": "2024-09-02T10:20:30.000Z",
  "CreatedBy": "DOMAIN\\User",
  "CreatedDate": "2024-09-02T10:20:30.000Z"
}
```

#### 3. Rendering a Report  
You can also render a report directly via the REST API. To do so, you call the `Export` action on the report. For example, to get a PDF version of a report:
```
GET http://<reportserver>/reports/api/v2.0/Reports('<ItemId>')/Export/PDF
```
If your report has parameters, you can provide them as query parameters. For instance, if the report expects a `Year` parameter:
```
GET http://<reportserver>/reports/api/v2.0/Reports('<ItemId>')/Export/PDF?Year=2024
```
This will return a binary PDF stream which you can save as a file. Using a tool like `curl`, you might do:
```bash
curl -o SalesReport_2024.pdf "http://<reportserver>/reports/api/v2.0/Reports('2f3c8571-9df0-4d76-a751-85c13f5333d2')/Export/PDF?Year=2024"
```

#### 4. Creating and Managing Items  
You can also use POST requests to create folders or upload reports. For example, to create a new folder:
```
POST http://<reportserver>/reports/api/v2.0/Folders

Body (JSON):
{
  "Name": "NewFolder",
  "ParentFolderId": "e4fa8e70-52fc-4c5c-9bf6-b9abf2d3a931"
}
```
This request would create a folder named “NewFolder” under the folder with the given `ParentFolderId`. The response will contain details about the newly created folder.

#### 5. Discovering Available Actions  
You can query related actions from certain endpoints. For instance, fetching a report often includes links that guide you to what you can do next. The SSRS REST API leverages OData-like conventions. Check the `@odata.nextLink` properties for pagination and use `$filter`, `$top`, `$skip` query parameters where supported.

### Tooling and Exploration  
You can browse the API endpoints using tools such as:  
- **Web Browser:** For GET requests, you might view results in a browser (though you may need an extension to format JSON).  
- **Postman or Fiddler:** For authenticated requests and calls that require parameters, these tools make exploring and testing endpoints easier.

### Summary  
- The SSRS REST API provides a modern JSON-based interface to interact with reports, folders, and resources.  
- It uses intuitive resource-based endpoints (`/Folders`, `/Reports`, `/DataSources`, etc.).  
- You can list items, get item details, render reports in various formats, and even create or modify resources.  
- Responses are typically JSON, making it easy to integrate into modern web or mobile applications.

This REST API is a significant improvement over the older SOAP-based interfaces, making it much simpler to integrate SSRS functionality into modern applications and services.
