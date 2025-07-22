compliance-first/multi-jurisdiction.md
Title: Multi-Jurisdiction Compliance with Fabric

🎯 Objective
Configure your Fabric model or agent to meet multiple regulatory frameworks (e.g., GDPR, HIPAA, CCPA) in a single deployment.

📚 1. Why Multi-Jurisdiction Support Matters
🌐 Global users and deployments

🛡️ Regional privacy laws vary: opt-in consent, right to delete, data portability

🧾 Audit requirements differ per region

⚙️ 2. Defining Policies
In your agent’s model.yaml, declare multiple compliance targets:

yaml
Copy
Edit
compliance:
  policies:
    - GDPR
    - HIPAA
    - CCPA
This enables Fabric’s policy kernel to enforce composite checks at runtime.

🏗️ 3. Policy Enforcement Blocks
Add runtime verify_policy blocks in the .fab source:

fabric
Copy
Edit
verify_policy GDPR
verify_policy HIPAA
Or use a conditional:

fabric
Copy
Edit
if region == "EU" then verify_policy GDPR
🔒 4. Consent and Data Controls
Use these Fabric DSL primitives:

request_consent

revoke_access

audit_log "export"

anonymize("personal_data")

These map to GDPR/CCPA rights like access, deletion, and portability.

🧪 5. Test Multi-Region Deployment
Use:

bash
Copy
Edit
FAB_REGION=us-west fab run agent-repacker
FAB_REGION=eu-central fab run agent-repacker
The FAB_REGION context will drive jurisdiction-specific policy validation.

✅ 6. Ledger Compliance Markers
After fab model publish, the provenance ledger will log:

Jurisdictions supported

Signed attestation entries

Provenance audit chain

📌 Best practice: Add README_COMPLIANCE.md to document what laws are implemented and how.
