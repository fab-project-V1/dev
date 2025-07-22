# 🛡️ Enclave Isolation in Fabric

Fabric enforces agent and model execution within **isolated enclaves** to guarantee deterministic execution, memory protection, and tamper resistance—core to its zero-trust compute model.

---

## 🧱 What Is an Enclave?

An enclave in Fabric is:

- 🔐 A secure VM with memory isolation
- 🔁 Stateless by design, loaded from verified artifacts
- 📦 Attested and audited at runtime

Fabric supports enclave backends via:
- Intel SGX
- AMD SEV
- Arm CCA
- WASI sandboxing (default)

---

## 🧪 Runtime Isolation Guarantees

Each `.fab` agent runs in its own:

- 📦 Filesystem jail
- 🔒 Seccomp-secured syscall context
- 🧮 Deterministic compute capsule

Enclaves are **ephemeral**: no persistent state unless explicitly modeled.

---

## 🧾 Auditability and Forensics

Fabric logs:

- ⌚ Execution window
- 🧾 Input/output digests
- ✍️ Signature proofs
- 📉 Energy envelope compliance

This is enforced by the **provenance ledger**.

---

## 🔄 Reproducibility

Every enclave execution is:

- ⏱ Time-bounded
- 🔁 Deterministically replayable
- 📚 Linked to its model+policy commit

This is essential for compliance with GDPR and HIPAA data handling.

---

## 🛠 How to Enable

Agents are enclave-isolated by default.

To opt-out (for sandboxed dev only):

```yaml
policy:
  enclave: false
Warning: Disabling enclaves disables provenance guarantees.

🔐 Attestation Pipeline
Agent build is hashed

Signed by dev or CI key

Policy + provenance included

Enclave image verified at launch

Attestation hash submitted to ledger

Enclave isolation is the security backbone of Fabric’s distributed intelligence mesh, ensuring models never run outside their cryptographic cage.
