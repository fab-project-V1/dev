# Audit Policies in Fabric

Audit policies in Fabric ensure transparent, accountable, and verifiable execution of AI agents and data flows. These are enforced at compile time and runtime across the model lifecycle and execution environment.

---

## 🛡️ What is an Audit Policy?

An audit policy defines which aspects of a model or agent must be:

- Tracked for provenance
- Evaluated for compliance
- Logged for post-hoc inspection

These policies can be declared directly in `.fab` modules and are enforced by the Fabric compiler and ledger systems.

---

## 📝 Declaring Audit Policies

Fabric DSL allows you to embed audit rules in your agents:

```fab
agent SecureNLP {
  input: { prompt: Text }
  output: { response: Text }
  audit: {
    log_inputs: true,
    log_outputs: true,
    hash_model: "SHA256"
  }
}
🔍 Runtime Enforcement
The Agent VM respects these policies at runtime:

Input/output logging: Stored in encrypted logs

Hashing models: Model weights are fingerprinted

Control flow checks: Execution paths are monitored

🔗 Ledger Integration
Audit results are written to the Fabric Provenance Ledger:

json

{
  "agent_id": "SecureNLP",
  "inputs": "...",
  "outputs": "...",
  "model_hash": "abc123...",
  "timestamp": "2025-07-22T10:15:00Z"
}
This allows forensic-grade traceability.

🧩 Custom Audit Backends
You can register custom backends via the policy kernel:

ts

registerAuditHook('my-compliance-db', async (record) => {
  await db.save(record);
});
This enables compatibility with HIPAA, GDPR, CCPA data stores.

✅ Summary
Feature	Enforced By	Location
Input logging	Agent VM	Encrypted logs
Output logging	Agent VM	Encrypted logs
Hashing	Compiler & runtime	Audit ledger
Custom hooks	Policy kernel	User-defined
