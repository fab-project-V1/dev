# Smart Contracts in Fabric

Smart contracts in Fabric define programmable enforcement for policies, incentives, and governance mechanisms across the distributed system.

---

## 📜 What Are Fabric Smart Contracts?

Unlike traditional blockchain smart contracts, Fabric's contracts are:

- **Deterministic scripts** triggered on system events
- **Bound to governance or compliance contexts**
- **Executed by verified runtime enclaves**

They can manage incentives, enforce regulatory guardrails, or enable autonomous agent behaviors.

---

## 🔁 Trigger Types

| Trigger              | Description                                 |
|----------------------|---------------------------------------------|
| `on_model_publish`   | Runs when a model is published              |
| `on_agent_execution` | Wraps or restricts agent inference          |
| `on_fork`            | Activated when a model or agent is forked   |
| `on_payment`         | Custom fee-sharing or royalty logic         |

---

## 🧠 Contract Example: Fork Royalty Enforcement

```python
# contracts/fork_royalty.py
def on_fork(model, new_owner):
    if model.fork_royalty_pct > 0:
        enforce_payment(
            from_=new_owner,
            to=model.owner,
            amount=model.fee_per_call * model.fork_royalty_pct
        )
This ensures forks automatically transfer royalties to the original author.

🔒 Determinism and Safety
Fabric contracts are executed inside sandboxed VMs

No I/O, side effects, or non-determinism allowed

Gas metering ensures bounded resource usage

🚦 Deployment
Contracts are registered in the model.yaml or agent.yaml:

yaml

policy:
  contract: contracts/fork_royalty.py
They’re cryptographically signed and verified on chain.

🔄 Updating Contracts
To update a smart contract:

Bump the model or agent version

Sign the updated contract hash

Re-publish with provenance

Immutable contract history is stored in the ledger.

✅ Summary
Feature	Fabric Support
Fork enforcement	✅ Built-in via smart contracts
Fairness logic	✅ Configurable via weights
Reward structures	✅ Enforced via contract triggers
Runtime sandboxing	✅ Enclave-executed and audited
