
Rules Evaluation Process - Sequence Diagram Overview
This diagram represents the interaction between three components in the Rules Evaluation System:

Controller
RulesEngineService
RuleEvaluate
Process Flow:
Controller sends a request to the RulesEngineService to evaluate rules.
RulesEngineService loads the ruleset.
RulesEngineService invokes Evaluate(), which processes each rule.
For each rule, it checks:
Claim
Adjuster
RuleEvaluate processes EvaluateRule(), performing:
Get Object Property
Rule Condition Check
Once conditions are checked, a result is returned to RulesEngineService.
RulesEngineService compiles all evaluation results.
Final response is returned to Controller in the form of a List<EvaluationResult>.
Key Insights:
The Rules Engine systematically processes claims and adjusters based on predefined conditions.
The evaluation process involves fetching object properties and applying rule conditions before returning results.
The final response is a list of evaluation results, which the Controller can use for decision-making.

--
Claim Auto Assignment - System Architecture Overview
This diagram provides a detailed view of the Claim Auto Assignment process within the Sedgwick Core Network, highlighting data flow, automation logic, and external integrations.

Key Components:
Users

Initiate the process via Email Intake (e.g., sending claim-related emails).
Queue Service

Adds incoming emails and related documents to the Work Queue.
Saves attachments for processing.
Work Order

Created from the queued data.
Processed via CTABS API for status updates.
Claim Automation Service (Core Processing Unit)

Monitors the Work Order Queue.
Reads configuration from the Queue Automation Service Configuration.
Uploads PDFs to Infrrd for OCR-based document extraction.
Receives webhook callbacks from Infrrd with extracted data.
Subscribes to Message Bus (MB) Topic for further processing.
Saves responses to the Message Bus.
Infrrd (OCR Processing)

Extracts structured data from claim documents.
Sends the processed data back via webhook.
Message Bus

Acts as an event-driven architecture component.
Stores responses from Infrrd for downstream processing.
Assignment Service

Determines claim handler assignments.
Interacts with CTABS VQ and Queue Files for processing.
Stores Infrrd raw responses.
Finalizes claim setup.
Process Flow:
Monitor Work Order Queue.
Upload PDFs to Infrrd for OCR processing.
Receive webhook callback from Infrrd.
Save response to Message Bus.
Subscribe to MB Topic for processing.
Store Infrrd raw response.
Assign the claim to the correct adjuster.
This system automates claim processing, leveraging OCR for document extraction and event-driven architecture for efficiency. Let me know if you need a breakdown of any specific part

--

Claim Auto Assignment - System Architecture Overview
This diagram illustrates the Claim Auto Assignment process within the Sedgwick Core Network, highlighting data flow, automation logic, and integrations.

Key Components:
WorkOrder Dispatch Queue

Stores incoming work orders before automation processing.
CTABB API

Facilitates data communication between different components.
Updates Work Order (WO) status and adds notes.
Claim Automation Service (Core Processing Component)

Monitors the dispatch queue.
Retrieves claim data.
Gets adjusters based on predefined rules.
Handles scheduled jobs.
Queue Automation Service Configuration

Reads configuration settings for automation processing.
Rules Engine

Loads and caches policy/routing rules.
Processes claim assignments based on predefined logic.
CTABS Database

Stores claim and adjuster data.
Provides claim details to the automation service.
Salesforce Integration

Claims and adjuster assignments are sent to Salesforce via API App.
Uses SFTP (Secure File Transfer Protocol) for data transmission.
Process Flow:
Claim Automation Service monitors the dispatch queue.
Retrieves claim data from CTABS.
Invokes the Rules Engine to determine the best adjuster.
Updates the Work Order (WO) status.
Assigns claims and sends the details to Salesforce via SFTP & API.
This system ensures automated and efficient claim assignments, reducing manual effort and improving processing speed. Let me know if you need further clarification or a breakdown of specific sections
