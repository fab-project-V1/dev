compliance-first/adding-signatures.md
Title: Adding Cryptographic Signatures to Fabric Agent Metadata

🎯 Objective
Digitally sign a Fabric model’s compliance policy and metadata to establish authenticity, integrity, and trust.

📄 1. Why Sign Fabric Modules?
✅ Integrity: Prevent tampering after creation

🔐 Provenance: Ensure the author matches what’s declared

🧾 Auditability: Verifiable cryptographic trace for regulators

🔧 2. Generate a Signing Key (PGP/GPG)
If you don’t already have one:

bash
Copy
Edit
gpg --full-generate-key
Export your key:

bash
Copy
Edit
gpg --export --armor "you@example.com" > public.asc
gpg --export-secret-keys --armor "you@example.com" > private.asc
🖋️ 3. Sign the Model
Navigate to the model directory:

bash
Copy
Edit
cd models/agent-repacker/1.0.0/
Sign the compliance policy and manifest:

bash
Copy
Edit
gpg --armor --output compliance_policy.yaml.asc --sign compliance_policy.yaml
gpg --armor --output model.yaml.asc --sign model.yaml
📁 4. Directory Structure After Signing
pgsql
Copy
Edit
1.0.0/
├── model.yaml
├── model.yaml.asc
├── data/
│   └── compliance_policy.yaml
│   └── compliance_policy.yaml.asc
🔗 5. Reference Signatures in Metadata
Update model.yaml:

yaml
Copy
Edit
signatures:
  model: model.yaml.asc
  policy: data/compliance_policy.yaml.asc
🛡️ 6. Validate Signature
bash
Copy
Edit
gpg --verify model.yaml.asc model.yaml
Fabric will also validate this automatically during fab model publish.

🧠 Tip
Distribute your public.asc to verification tools and audit partners for downstream trust validation.
