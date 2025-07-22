# Tutorial: Integrating Fabric Agents on Edge Devices

This tutorial guides you through deploying a Fabric model agent on an edge device (e.g., Jetson Nano, Raspberry Pi) using the universal Fabric runtime and UDAP compatibility.

---

## 🎯 Goal

- Run a Fabric-compliant model on a low-power edge device.
- Maintain provenance, energy policy, and compliance.

---

## ⚙️ Prerequisites

- Docker or container runtime on device
- Model published via `/tutorials/end-to-end-workflow.md`
- `fab-cli` installed on development host

---

## 🧰 Step 1: Pull Published Model

On your host system:

```bash
fab model pull agent-repacker --version 1.0.0
This pulls the signed container and dependencies.

📦 Step 2: Export Lightweight Runtime
Use:

bash

fab deploy edge --model agent-repacker --version 1.0.0 --target jetson
This will:

Cross-compile the agent container

Strip debug layers

Optimize for low-power inference

Supported targets:

jetson

pi4

tpu

coral

📤 Step 3: Transfer to Device
Copy bundle to edge device:

bash

scp dist/agent-repacker-1.0.0.tar.gz user@edge:/opt/fabric/
SSH into device:

bash

ssh user@edge
Load container:

bash

docker load < /opt/fabric/agent-repacker-1.0.0.tar.gz
🚀 Step 4: Run Agent on Device
bash

docker run -p 9000:9000 fabric/agent-repacker:1.0.0
Test with:

bash

curl -X POST localhost:9000/invoke -d '{"text": "What is Fabric?"}'
🔍 Step 5: Validate Runtime Compliance
Run on-device checks:

bash

fab verify --local
This confirms:

Policy enforcement (e.g., energy budget)

Provenance replay

Signature validation

✅ Summary
You've successfully deployed and invoked a signed, compliant Fabric model on an edge device. You preserved:

Energy and privacy policies

Auditability and lineage

Container integrity

Next: Review /deployment/edge.md and /deployment/cloud.md for scaling to hybrid environments.
