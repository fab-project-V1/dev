# 🔬 Provenance Enforcement in Fabric

Provenance enforcement is a core principle in the Universal AI Fabric, ensuring that every model, dataset, and execution trace can be fully verified and attributed. This builds trust, facilitates compliance, and supports auditing at forensic levels.

---

## ✅ What Is Provenance?

**Provenance** refers to the complete traceability of how a model was trained, validated, modified, and executed. This includes:

- Training data lineage (hash, source, and version)
- Code commits and configurations
- Runtime environment details
- Model transformations and repackaging
- Signatures verifying authorship and integrity

---

## 🧩 How Fabric Implements Provenance

Fabric uses a multi-layered system:

1. **Training Provenance**
   - Defined in `model.yaml > provenance` block
   - Hash of training data (`sha256`)
   - Link to training commit (`training_commit`)
   - Reference to training config file

2. **Execution Provenance**
   - Each execution is logged via the **Agent VM**
   - Input/output hashes are logged
   - Execution trace stored in the **Provenance Ledger**

3. **Signature Enforcement**
   - Model artifacts and manifests are signed using `fab sig gen`
   - Stored under the `signatures` block

4. **Policy Kernel Integration**
   - Provenance checks are enforced before scheduling
   - Any tampering or mismatch will block deployment

---

## 🛠 Tools & CLI

Use the following commands to manage provenance:


# Generate data hash
fab data hash path/to/data.jsonl

# Sign model artifacts
fab sig gen path/to/model.onnx --output artifact.sig

# Register model with provenance
fab model publish models/your-model/1.0.0/model.yaml
🔍 Forensic Use Case Example
When an edge device infers using a model:

Its input, model version, and output are hashed

The hashes are stored in the Provenance Ledger

An auditor can later trace:

Exact data used

Signature of model artifact

Person who last signed and deployed

🔒 Compliance Alignment
Fabric’s provenance system aligns with:

GDPR Art. 5: Data accountability

HIPAA: Secure recordkeeping

CCPA: Verifiable data access and deletion

📚 Next Steps
Learn about Ledger Integration

See how Compliance Profiles use provenance in policy checks
