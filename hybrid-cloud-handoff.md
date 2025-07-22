deployment-patterns/hybrid-cloud-handoff.md
Title: Hybrid Cloud Handoff — On-Prem Inference, Cloud Post-Processing

🧭 Objective
Demonstrate how to split an AI pipeline across on-premises infrastructure (for real-time inference) and cloud services (for aggregation, analytics, or compliance archiving).

📦 Use Case
Example: A retail chain runs inference on edge devices (detecting customer movement) and offloads weekly summaries to a cloud compliance agent.

Pipeline:

scss
Copy
Edit
[ VisionAgent ] ---(on-prem)--> [ SummaryAgent ] ---(cloud)--> [ ComplianceLedger ]
🧰 Prerequisites
Fabric runtime installed on both on-prem and cloud nodes

VPN, tunnel, or mTLS-secured channel between sites

Agent registry accessible to both locations

Docker or Kubernetes support

🏗️ Step 1: Package Your On-Prem Agent
Define the agent used at edge (e.g., VisionAgent):

yaml
Copy
Edit
name: vision-agent
version: 1.0.0
execution:
  runtime: local
  isolation: edge
outputs:
  - summary.json
Deploy on-prem with:

bash
Copy
Edit
fab model deploy models/vision-agent/1.0.0/model.yaml --target=edge01.local
☁️ Step 2: Cloud-Side Agent
The cloud agent ingests summary.json and stores it securely:

yaml
Copy
Edit
name: summary-agent
version: 1.0.0
inputs:
  - summary.json
execution:
  runtime: kubernetes
  security:
    compliance_profiles: [CCPA]
Deploy to your cloud Fabric mesh:

bash
Copy
Edit
kubectl apply -f k8s/summary-agent.yaml
🔗 Step 3: Define Fabric Workflow with Handoff
Your .fab DSL script:

fabric
Copy
Edit
agent VisionAgent at edge01:
  output: summary.json

agent SummaryAgent at cloud01:
  input: VisionAgent.output

workflow HybridAudit:
  sequence:
    - VisionAgent
    - SummaryAgent
  handoff: encrypted
🔒 Step 4: Secure Transfer Layer
Options:

Use mTLS between locations

Leverage UDAP registry for endpoint discovery

Enable object-level signing of JSON payloads

Example config:

yaml
Copy
Edit
handoff:
  protocol: https
  signing: pgp
  compression: gzip
✅ Step 5: Monitoring and Recovery
Use fab monitor HybridAudit to track runs

On failure, retry handoff via fab resume

Validate lineage with:

bash
Copy
Edit
fab verify models/summary-agent/1.0.0/
🧾 Summary
This hybrid deployment pattern enables:

Real-time inference near the data source

Asynchronous post-processing in the cloud

Full audit trail and compliance readiness

