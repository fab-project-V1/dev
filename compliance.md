# ✅ Compliance Architecture in Fabric

Fabric embeds compliance as a first-class concern across the full AI lifecycle. From data lineage to model execution, every step is audit-ready and governed by enforceable policies.

---

## 📜 Regulatory Frameworks

Fabric supports native mapping to:

- **GDPR**: General Data Protection Regulation (EU)
- **CCPA**: California Consumer Privacy Act
- **HIPAA**: Health Insurance Portability and Accountability Act

Each `.fab` module can declare applicable profiles and enforce runtime checks.

---

## 🧬 Compliance Modules

### 1. **Profiles**
- Defined under `compliance/` as `.profile` files
- Include scoped policies for data handling, access, and retention

### 2. **Inference Constraints**
- Runtime policies specify:
  - Anonymization
  - Redaction
  - Energy caps
  - Fairness bounds

### 3. **Audit Hooks**
- All execution artifacts are hashed and logged
- Hooks available for compliance officers to retrieve signed traces

---

## 🔍 Example: GDPR Policy

```yaml
policy:
  privacy: anonymized
  data_retention: 30d
  subject_rights:
    - access
    - erasure
  consent_required: true
This can be referenced in model.yaml or enforced by fab test --compliance.

🏛️ Certification Pipeline
Annotate model with provenance fields

Run fab certify to validate:

Dataset hashes

Training commits

Config lineage

Upload to ledger

All certified models are traceable and reproducible.

🔐 Provenance Ledger
Verifiable Merkle-chain log of every inference and training run

Supports public and private proofs

Exportable via fab ledger export

🧪 Continuous Compliance Testing
bash

fab test --compliance
Tests against:

Declared privacy and fairness settings

GDPR/CCPA/HIPAA mappings

Log retention and signing coverage

Fabric ensures compliance is not an afterthought, but an embedded property of your AI system.


