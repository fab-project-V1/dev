# 🧾 The Provenance Ledger

The **Provenance Ledger** is Fabric’s immutable, cryptographically-verifiable record of all model activities, including training, deployment, inference, and repackaging. It ensures end-to-end traceability and auditability across the lifecycle of AI assets.

---

## 🧱 Ledger Architecture

The ledger operates as a modular append-only log backed by a pluggable consensus engine (default: Merkle-DAG over LevelDB).

### Key Modules:

- **Ledger Daemon** (`daemon/provenance-ledger/ledger.go`)
- **Ledger API** (`daemon/provenance-ledger/api/`)
- **Consensus Hooks** (`policy-kernel` integration)

---

## 🔗 What Gets Logged?

Each ledger entry includes:

| Field                | Description                                 |
|---------------------|---------------------------------------------|
| `id`                | Unique entry hash                           |
| `actor`             | Model, user, or agent performing action     |
| `action`            | `train`, `infer`, `package`, `deploy`       |
| `timestamp`         | UTC ISO 8601                                |
| `input_hash`        | SHA256 of inputs (data, config, query)      |
| `output_hash`       | SHA256 of outputs (model, result)           |
| `signature`         | Auth signature of the action issuer         |
| `metadata`          | Arbitrary fields (hardware, energy, etc.)   |

---

## ⚙️ Logging a Custom Event

To manually log an entry via CLI:


fab ledger log \
  --actor agent-repacker:1.0.0 \
  --action infer \
  --input-hash 123abc... \
  --output-hash 456def... \
  --signature abcdef... \
  --metadata '{"energy":"12J","device":"nanoX"}'
🔍 Verifying Entries
You can audit ledger entries using:


fab ledger query --actor agent-repacker:1.0.0
Output includes all events involving that model or agent.

🔒 Consensus and Tamper-Proofing
Fabric supports multiple backends:

Local Merkle-Chain (default)

Hyperledger Fabric (plugin)

IPFS DAG Chain (experimental)

Each entry is chained and signed, making unauthorized edits cryptographically impossible.

🛡️ Compliance Role
The ledger supports:

Article 30 (GDPR): Record of processing activities

HIPAA: Access tracking and model audit trail

Model risk disclosure logs for regulatory review

📌 When Ledger is Mandatory
The following operations are required to be ledger-logged:

Deployment of any public model

Any inference from a certified model

Training on regulated data

📚 Related Topics
Provenance Enforcement

Policy Kernel

Compliance Profiles


