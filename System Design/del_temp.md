Here’s a **Mermaid diagram representation** for each part based on the provided image:

---

### **1. Adjuster Data Flow**

```mermaid
flowchart LR
    Start1([Start])
    DailyPass[Daily pass refresh<br>Relevant adjuster data marked Ready for Work]
    StatusUpdate[Status updates for adjuster availability]
    RemoveUnavailable[Removes adjusters who are unavailable or on PTO]
    SendData[Send data to CTABS Decision Engine]
    Output1[Output:<br>- CTABS Profile<br>- Location Data<br>- Product Line Assignments<br>- Employee Type, Status, etc.]

    Start1 --> DailyPass --> StatusUpdate --> RemoveUnavailable --> SendData --> Output1
```

---

### **2. Claim Data Flow**

```mermaid
flowchart LR
    Start2([Start])
    QueryClaim[Query Claim Data:<br>- Fetch relevant claim attributes<br>Zip Code, Urgency, Complexity, etc.]
    SendToEngine[Send Data to Decision Engine]
    End2([End])

    Start2 --> QueryClaim --> SendToEngine --> End2
```

---

### **3. Decision Engine Flow**

```mermaid
flowchart LR
    Start3([Start])
    QueryData[Query Claim & Adjuster Data]
    AdjusterAvailable{Adjuster Available?}
    AssignAdjuster[Assign claim to adjuster]
    CriteriaMet{Adjuster Meets Criteria?}
    ConfirmAssign[Confirm Assignment]
    ReEvaluate[Re-evaluate adjuster list]
    GenerateList[Generate matched adjusters and assignments]
    End3([End])

    Start3 --> QueryData --> AdjusterAvailable
    AdjusterAvailable -->|Yes| AssignAdjuster --> CriteriaMet
    CriteriaMet -->|Yes| ConfirmAssign --> GenerateList --> End3
    AdjusterAvailable -->|No| ReEvaluate
    CriteriaMet -->|No| ReEvaluate
    ReEvaluate --> AdjusterAvailable
```

---

These diagrams correspond to the individual sections in the image. Let me know if you'd like adjustments or to combine them!
