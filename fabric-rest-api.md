Fabric REST API Reference
This document provides an overview of the core Fabric RESTful API endpoints. These endpoints enable external systems and tools to interact with models, workflows, agents, and registry metadata.

🔐 Authentication
All endpoints require API token authentication.

Header:

http

Authorization: Bearer <FABRIC_API_TOKEN>
📦 Model Registry
GET /models
List all published models.

Response:

json

[
  {
    "name": "agent-repacker",
    "version": "1.0.0",
    "framework": "ONNX",
    "tags": ["compliance", "70m"]
  }
]
GET /models/{name}/{version}
Get metadata for a specific model.

POST /models
Publish a model.

Payload:

json

{
  "name": "agent-repacker",
  "version": "1.0.0",
  "manifest": { ... }
}
⚙️ Agent Runtime
POST /execute
Run an agent on input data.

Payload:

json

{
  "agent": "agent-repacker",
  "input": {
    "Text": "What is Fabric?"
  }
}
Response:

json

{
  "output": {
    "Completion": "Fabric is a secure AI runtime..."
  }
}
📖 Workflow Orchestration
GET /workflows
List active workflows.

POST /workflows
Deploy a new workflow.

🔍 Audit & Provenance
GET /provenance/{model_id}
Get signed lineage and training trace.

📊 Metrics & Monitoring
GET /metrics
System performance indicators (latency, throughput, failures).
