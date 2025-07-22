compliance-first/verifying-provenance.md
Title: Verifying Provenance of Fabric Modules

🎯 Objective
Use Fabric’s ledger tools to verify the cryptographic and procedural lineage of a published model or agent.

📦 1. What is Provenance in Fabric?
🧬 Lineage: Every action (training, signing, publishing) creates an audit trail

🪪 Identity: Linked to signing keys and developer UUIDs

🔐 Tamper-proof: Ledger entries are append-only and cryptographically secure

🔍 2. Use fab model verify
To verify a model’s lineage:

bash
Copy
Edit
fab model verify agent-repacker --version 1.0.0
Output includes:

✅ Signature chain (creator, publisher, auditor)

📅 Timestamps and commit hashes

🔗 Compliance policy and jurisdiction mapping

🔐 3. Signature Validation
Fabric checks:

GPG key validity

Signature-to-file integrity

Developer public identity binding

Output (example):

bash
Copy
Edit
✔ Signature valid (model.yaml.asc)
✔ Created by @shawn.dev (UUID: fab1234)
✔ Compliance: GDPR, HIPAA
✔ Ledger Hash: 0xabcde...
🧬 4. Provenance Ledger Query
Query the public provenance ledger:

bash
Copy
Edit
fab ledger inspect agent-repacker --version 1.0.0
This checks:

🔎 Who trained and modified it

🧠 What data sources were used

🔐 What environment it was executed in

🛠️ 5. Local Ledger Debugging
Inspect .fabric/provenance.db (SQLite) if running offline:

bash
Copy
Edit
sqlite3 ~/.fabric/provenance.db
📚 6. Use in Audits
Export verified records:

bash
Copy
Edit
fab model verify agent-repacker --version 1.0.0 --export audit.json
Include this in compliance submissions or share with regulators.
