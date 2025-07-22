# Role-Based Access Control (RBAC) in Fabric

Fabric implements a robust Role-Based Access Control (RBAC) system to manage user permissions and secure AI workflows across decentralized deployments.

---

## 🔐 Why RBAC?

RBAC ensures that only authorized actors can:

- Register or publish models
- Execute sensitive agents
- Access compliance logs
- Deploy changes in multi-tenant environments

It’s critical for enterprise governance, regulatory adherence, and platform security.

---

## 🧑‍💼 RBAC Roles

Fabric defines these default roles:

| Role         | Description                                  |
|--------------|----------------------------------------------|
| `admin`      | Full control over models, agents, and users  |
| `developer`  | Can push models and deploy agents            |
| `auditor`    | Read-only access to logs and policies        |
| `tenant`     | Scoped access within a specific domain       |

---

## 🛠️ Declaring Permissions

Permissions are declared in your `fabric.policy` file:

```yaml
roles:
  admin:
    - model:push
    - agent:deploy
    - ledger:read
    - user:grant
  developer:
    - model:push
    - agent:deploy
  auditor:
    - ledger:read
You can extend this per-tenant or per-agent.

🔗 Policy Kernel Integration
The Fabric runtime invokes the RBAC policy kernel during:

fab model push

fab agent deploy

API requests to compliance or ledger subsystems

Access is granted only if the calling user has the appropriate token and role permissions.

🔍 Token-Based Authentication
RBAC uses signed JWTs:

json

{
  "sub": "shawn@example.com",
  "role": "developer",
  "exp": 1720000000,
  "sig": "0xdeadbeef..."
}
These are verified by the runtime enclave or scheduler daemon.

📜 Logging Denials
All denied actions are logged with timestamps and context:

pgsql

[WARN] Access denied for user 'foo@bar.com' attempting 'agent:deploy'
These logs are auditable and immutable.

✅ Summary
Feature	Enforcement Point	Stored In
Role checks	Scheduler, Daemon	In-memory / cache
Policy source	fabric.policy	Source repo
Token verification	Runtime enclaves	JWT cert chain
Denial logging	Ledger, compliance VM	Audit log
