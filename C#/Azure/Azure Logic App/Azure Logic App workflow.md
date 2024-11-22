### Azure Logic App workflow

```mermaid
graph LR
    A[Start: When an HTTP request is received] --> B{Condition}
    B -->|True| C[Send Manual Review Request Email]
    C --> D{Review}
    D -->|Approve| E[Process Order]
    D -->|Escalate| F[Send Escalation Email]
    F --> G{Check Response}
    G -->|True| H[Process Order After Escalation]
    G -->|False| I[Send an Email]
    D -->|Default| J[No Action]
    B -->|False| K[Process Order Without Review]
    K --> L[End]
    H --> L
    I --> L
    E --> L
```

### Workflow Flowchart Steps:

1. **Start**:
   - Trigger: "When an HTTP request is received".

2. **Condition**:
   - Check if a condition is true or false.

3. **If True**:
   - **Send Manual Review Request Email**:
     - Notify someone to manually review the request.

   - **Review**:
     - Sub-options:
       - **Approve**:
         - Action: "Process order".
       - **Escalate**:
         - **Send Escalation Email**:
           - Notify about escalation.
         - **Check Response**:
           - If True:
             - Action: "Process order after escalation".
           - If False:
             - Action: "Send an email".
       - **Default**:
         - No specific action mentioned.

4. **If False**:
   - **Process Order Without Review**:
     - Skip the review process and directly process the order.

5. **End**:
   - Workflow completes.

---

```mermaid
sequenceDiagram
    autonumber
    participant Client as Client
    participant Server as Workflow Server

    %% Step 1: HTTP Request Received
    Client->>+Server: 1. Send HTTP Request (Trigger Workflow)

    %% Step 2: Condition Check
    Server->>Server: 2. Evaluate Condition
    alt Condition is True
        Server->>+Server: 3. Send Manual Review Request Email
        Server->>+Server: 4. Enter Review Process
        alt Review: Approve
            Server->>+Server: 5. Process Order
        else Review: Escalate
            Server->>+Server: 6. Send Escalation Email
            Server->>+Server: 7. Check Response
            alt Response is True
                Server->>+Server: 8. Process Order After Escalation
            else Response is False
                Server->>+Server: 9. Send Escalation Failure Email
            end
        else Review: Default
            Server->>+Server: 10. No Specific Action
        end
    else Condition is False
        Server->>+Server: 11. Process Order Without Review
    end

    %% Step 3: End Workflow
    Server-->>-Client: 12. Respond with Workflow Completion
```

### Explanation:
- **Step 1**: The client initiates the workflow by sending an HTTP request.
- **Step 2**: The server evaluates a condition, branching into:
  - If **true**, it follows the review process:
    - Approve: Processes the order.
    - Escalate: Sends an escalation email, checks the response, and processes accordingly.
    - Default: No specific action.
  - If **false**, the order is processed without review.
- **Step 3**: The server responds to the client, signaling workflow completion.
