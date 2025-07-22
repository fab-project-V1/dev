deployment-patterns/private-enclave-network.md
Title: Deploying a Secure Multi-Agent Enclave Topology

🧭 Objective
This tutorial walks through deploying Fabric agents within a private enclave mesh, enabling secure execution, data isolation, and compliance-bound inference.

🧰 Prerequisites
Fabric CLI and runtime installed

Docker or Kubernetes with enclave plugins (e.g., Kata Containers, gVisor)

TLS certs or identity keys for enclave nodes

Agent manifests with provenance: strict and security: enclave

🔧 Step 1: Define Agent Topology
You want to run multiple agents like this:

less
Copy
Edit
  [ IngestAgent ] ---> [ ProcessingAgent ] ---> [ StorageAgent ]
         |                     |                     |
      enclave-A            enclave-B            enclave-C
Each agent is deployed in a separate isolated node, with signed input/output, policy binding, and attested execution.

🛡️ Step 2: Annotate .fab Modules
Each agent must declare secure context in model.yaml:

yaml
Copy
Edit
security:
  execution: enclave
  isolation: true
  attestation: enabled
  compliance_profiles: [GDPR, HIPAA]
🧱 Step 3: Provision Enclave Runtimes
Install the following on each node:

Intel SGX or AMD SEV plugin

gVisor or Kata Containers

TLS or mTLS certificates for inter-agent trust

Then label your K8s nodes:

bash
Copy
Edit
kubectl label node node-a fabric/enclave=true
📦 Step 4: Deploy via Helm/K8s
Create a custom values.yaml with:

yaml
Copy
Edit
agent:
  image: ingest-agent:1.0.0
  securityContext:
    runAsUser: 0
    privileged: false
    runtimeClassName: kata-containers
Then deploy:

bash
Copy
Edit
helm install ingest-agent ./charts/fabric-agent -f values.yaml
Repeat for each enclave.

🔗 Step 5: Connect Enclave Agents
In your workflow file:

yaml
Copy
Edit
workflow SecureFlow:
  blocks:
    - IngestAgent
    - ProcessingAgent
    - StorageAgent
  provenance: enforce
  network:
    secure_channel: mTLS
The secure_channel enforces TLS or PGP signatures between enclaves.

🧪 Step 6: Validate
Use fab monitor to ensure enclave status

Check attestation logs (/var/log/fabric/attestation.log)

View inter-agent signatures in the Fabric ledger

✅ Summary
You've deployed a secure enclave mesh of Fabric agents using:

Confidential containers

Enforced provenance

TLS/mTLS-based agent isolation

Runtime attestation for regulatory confidence
