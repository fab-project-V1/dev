# 📘 Fabric Glossary

This glossary defines the key terms and concepts used throughout the Fabric system and its documentation.

---

### Agent

A composable AI service unit that encapsulates a model, its policies, runtime, and input/output schemas. Agents operate autonomously or collaboratively in Fabric workflows.

---

### Agent Block

A code-defined execution block (`agent {}`) in the Fabric DSL specifying behavior, constraints, and interaction interfaces for an agent.

---

### Block

A discrete unit of computation in Fabric. Blocks include `agent`, `run`, `fork`, `chain`, and `quantum` among others, defined within `.fab` scripts.

---

### Chain Block

A control structure for sequential execution of multiple blocks, ensuring ordered dependency resolution.

---

### CLI

The `fab` command-line interface used to initialize, build, test, deploy, and publish Fabric agents and modules.

---

### Compliance Profile

A set of enforced privacy, fairness, and regulatory parameters bound to an agent to ensure legal and ethical constraints during execution.

---

### CRD

Custom Resource Definitions used to deploy Fabric workloads into Kubernetes environments.

---

### DSL

The domain-specific language of Fabric (`.fab` files) used to define agent logic, workflows, and module structure.

---

### Execution Kernel

The Fabric runtime component that manages block execution, scheduling, memory safety, and enclave security across edge/cloud.

---

### Fork Block

A block type that enables parallel execution of multiple downstream agents or modules.

---

### Governance

Fabric’s framework for managing updates, auditability, and policy enforcement across the model and agent registry.

---

### Mesh

The distributed fabric of nodes that execute agent-based workflows, managed through provenance-aware orchestration.

---

### Model

An ML model wrapped in metadata, runtime, and compliance policy as part of an agent. Models are versioned and published to the Fabric registry.

---

### Ontology

JSON-LD schemas used to structure semantic interoperability of agent interfaces and modular contracts.

---

### Provenance

Cryptographic lineage tracking of training data, config, and code to enforce accountability and reproducibility.

---

### Quantum Module

A `.fab` module utilizing quantum blocks, which compile to QIR or QASM for hybrid quantum-classical workflows.

---

### Scheduler

Part of the daemon layer, it manages agent and job execution across the Fabric mesh based on policy constraints.

---

### Serial ID

A unique identifier of a model version combining its name, semantic version, and commit hash.

Example: `agent-repacker@1.0.0#abc123...`

---

### UDAP

Unified Decentralized Agent Protocol – defines secure interactions between agents, services, and ledgers.

---

### Workspace

A `fab-project/` structured directory that contains apps, models, training config, and deployment tooling.

---

### Zero-Knowledge Proof (ZKP)

A privacy-preserving proof mechanism optionally used in Fabric to validate computation without revealing data.

---

This glossary evolves with each version of Fabric. Contributions welcome via [CONTRIBUTING.md](./CONTRIBUTING.md).
