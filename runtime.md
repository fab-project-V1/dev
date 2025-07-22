# ⚙️ Fabric Runtime Architecture

The Fabric runtime is a secure, distributed execution environment that orchestrates model invocation, agent dispatching, and compliance enforcement.

---

## 🧩 Core Components

### 1. Agent VM
- Lightweight containerized environment
- Executes `.fab` modules deterministically
- Supports ONNX, PyTorch, HuggingFace, and Fabric-native models

### 2. Policy Kernel
- Enforces energy, fairness, privacy, and cost policies
- Evaluates SLAs and user entitlements at inference time

### 3. Scheduler
- Determines execution location (local/edge/cloud)
- Balances load across mesh compute nodes
- Integrates with Kubernetes, Nomad, and serverless runtimes

### 4. UDAP Registry
- Tracks model versions and cryptographic signatures
- Enables trusted invocation through signed provenance

### 5. Consensus Ledger
- Maintains verifiable logs of all executions
- Stores hashes of inputs, outputs, and signatures
- Optional zk-rollups for compact audits

---

## 🔒 Secure Execution Flow

```plaintext
[Client] → [fab-cli/SDK] → [Scheduler] → [Agent VM] → [Model Inference] → [Ledger + Return]
All steps are cryptographically signed

Provenance is enforced via embedded policy and ledger validation

Execution tokens ensure integrity of state and resource metering

🚀 Deployment Topologies
Mode	Description
Local	Runs everything on a single developer machine
Edge Mesh	Distributed across edge devices
Cloud	Elastic deployment across cloud providers

Supports hybrid failover and compliance-aware routing.

📊 Observability & Monitoring
Built-in Prometheus and Grafana metrics

Traceable invocations with fab monitor

Log hooks for Splunk, Datadog, and OpenTelemetry

🧠 Intelligent Scheduling (Optional)
Uses real-time telemetry and SLAs

Applies differential privacy during data collection

Optimizes for latency, energy, and cost constraints

🧪 Runtime Testing
Fabric supports full mock and integration test pipelines:

bash

fab test --target runtime
You can emulate full agent execution with fab simulate.

For deeper insights, see deployment/local.md or examples/classical/.
