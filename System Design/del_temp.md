Here is the **full JSON request example** based on the provided payload structure:

```json
{
  "dateTimeUTC": "2024-04-12T23:20:50.52Z",
  "webhookSLA": 3000,
  "data": {
    "textItems": [
      {
        "id": "claim_summary",
        "text": "Date of Note: 2023-06-30, User: SYSTEM, Note Type: C4, \"Claim Note: \\\" The claim was evaluated as ...",
        "prompt": {
          "tag": "claim_summary_analysis_01"
        }
      }
    ],
    "fileItems": [
      {
        "id": "some_supporting_file",
        "base64source": "JVBERi0xLjYJNJeJlz9MNCjkgMCBvYmoNPDwvTG...",
        "filename": "some_supporting_file.pdf",
        "prompt": {
          "tag": "claim_summary_analysis_02"
        }
      }
    ]
  }
}
```

### **Explanation of Fields:**
- **`dateTimeUTC`**: Timestamp when the request is generated.
- **`webhookSLA`**: Service Level Agreement (SLA) in milliseconds.
- **`data`**:
  - **`textItems`**: Array containing text-based data.
    - `id`: Identifier for the text entry.
    - `text`: The content of the note or claim summary.
    - `prompt.tag`: A tag for categorization or processing.
  - **`fileItems`**: Array containing file-based data.
    - `id`: Identifier for the file entry.
    - `base64source`: The Base64-encoded file content.
    - `filename`: Name of the file.
    - `prompt.tag`: A tag for processing the file.

This JSON format is used for **sending structured text and file-based data** through a webhook or API request. 

### **Full JSON Example of the Error Response**

```json
{
  "error": {
    "code": "PermissionDeniedError",
    "message": "The user lacks sufficient permissions to perform the operation",
    "details": [
      {
        "code": "RequiredPermission",
        "message": "This operation requires permission: Integration.SIR.Use"
      }
    ]
  }
}
```

---

### **Explanation of Fields:**
- **`error`**: Root object containing error details.
  - **`code`**: `"PermissionDeniedError"` → Indicates that the operation failed due to insufficient permissions.
  - **`message`**: `"The user lacks sufficient permissions to perform the operation"`  
    - Provides a clear explanation of the issue.
  - **`details`**: An array containing more specific details about the permission issue.
    - **`code`**: `"RequiredPermission"` → A specific code indicating the missing permission.
    - **`message`**: `"This operation requires permission: Integration.SIR.Use"`  
      - Specifies the exact permission required for the operation.

---

### **Use Case:**
- This **error response** is typically returned by an API when a user **does not have the necessary permissions** to execute a request.
- To **resolve the issue**, the user must be granted the `"Integration.SIR.Use"` permission in the system.
