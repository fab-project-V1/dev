# Fabric Universal AI Stack

Welcome to the Fabric 1.0 Universal AI Development Stack. This repository powers the full lifecycle of agentic, multimodal, and quantum-augmented AI systems with complete compliance, provenance, and deployment support.

---

## Overview
Fabric 1.0 provides a complete AI OS for building, training, validating, and deploying models and agents with:

- **DSL Compiler** with quantum-classical IR support
- **Agent VM and Execution Daemon** stack
- **Model Packaging and Publishing** via `fab model` tools
- **Compliance Enforcement** (GDPR, HIPAA, CCPA)
- **Kubernetes, ROS, TensorRT, ONNX, WASM support**
- **CLI and VSCode extension** for development

This repository includes source code, models, configuration, ontology definitions, and benchmark tooling.

---

## Directory Structure

- `apps/` - Full AI applications (e.g., urban-dreamweaving)
- `compiler/` - DSL frontend, IRs, and codegen targets (LLVM, WASM, QASM, Quil)
- `daemon/` - Runtime stack (UDAP registry, Agent VM, scheduler, ledger)
- `language-spec/` - DSL specification and governance RFCs
- `tooling/` - CLI tools, VSCode plugin, CI pipelines
- `ontologies/` - JSON-LD ontologies for multimodal inputs
- `benchmarks/` - Performance, energy, and consensus benchmarks
- `compliance/` - Privacy and regulatory policy definitions
- `models/` - Public Fabric-compatible model packages
- `examples/` - Minimal examples in classical and quantum domains
- `data/` - Test and benchmark datasets
- `training/` - Fine-tuning, distillation, orchestrated training modules

---

## Getting Started

### Install CLI

npm install -g fab-cli
Scaffold a project

fab init my-app
cd my-app
fab build
fab deploy
Run the Agent VM locally


fab vm start
Publish a model
bash

fab model publish models/my-model/1.0.0/model.yaml
Contributing
Follow the RFC and semantic versioning process in language-spec/rfcs/

All models must pass compliance tests in fab model test before publishing

Lint and format all code with Prettier and Clang-Format where applicable

License
Apache 2.0

Authors
Fabric is developed by the Universal AI Foundation with contributors from the Fab Dev Network. Reach out via fabprojectV1@gmail.com.

Related Projects
fabric-models: Registry of public model definitions

fabric-spec: DSL and runtime specification
