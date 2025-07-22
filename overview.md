# Fabric System Concepts Overview

This page introduces the foundational concepts underpinning the Fabric 1.0.0 system, including UDAP, agents, workflows, and execution block types. Understanding these concepts is critical for designing, deploying, and maintaining Fabric-powered AI systems.

---

## 📡 UDAP: Universal Decentralized Agent Protocol

UDAP is the backbone communication and identity protocol of the Fabric ecosystem. It defines how agents are registered, discovered, authenticated, and composed into distributed applications.

### Key Features:
- **Decentralized Registry**: No central authority—agents are published and discovered via a distributed ledger.
- **Verifiable Identities**: Agents sign their capabilities, models, and manifest metadata.
- **Composability**: UDAP agents can be chained into multi-agent workflows using typed interface contracts.

---

## 🤖 Agents

Agents are the core autonomous units in Fabric. Each agent encapsulates a model, policy, and execution environment, making it an independently verifiable and composable unit.

### Agent Capabilities:
- **Stateful or Stateless**: Can persist context across invocations or run in isolation.
- **Certified Execution**: Verified and optionally enclave-isolated at runtime.
- **Policy-Bound**: Enforced rules on data provenance, energy use, privacy, and fairness.

---

## 🔁 Workflows

A workflow in Fabric is a directed acyclic graph (DAG) of agents connected through typed interfaces. Workflows are encoded declaratively in `.fab` files using the Fabric DSL.

### Types of Workflows:
- **Sequential Chains**: Agents pass outputs directly to the next.
- **Parallel Branches**: Multiple agents run concurrently and combine results.
- **Conditional Routing**: Decision nodes direct flow based on logic or data attributes.

---

## 🧱 Execution Block Types

Fabric DSL supports various block types for structuring logic within `.fab` modules.

| Block Type      | Description |
|-----------------|-------------|
| `agent`         | Declares a new agent, specifying model path and interface schema. |
| `input` / `output` | Defines the schema for data flow in and out of the module. |
| `compute`       | Wraps execution of logic or invokes another agent. |
| `route`         | Encodes conditional logic for branching workflows. |
| `quantum`       | Defines quantum-aware modules or hybrid computation paths. |
| `policy`        | Binds runtime constraints like privacy, energy, or provenance. |

---

## 🛠 Composability and Reuse

Each agent and block can be reused across applications. Models trained with provenance and compliant packaging can be registered once and imported anywhere in the network using UDAP IDs.

---

## Summary

Fabric’s system concepts—UDAP, agents, workflows, and DSL blocks—create a unified, decentralized, and compliant AI execution framework. These abstractions empower developers to build modular, trustworthy, and portable AI systems across edge, cloud, and mesh environments.
