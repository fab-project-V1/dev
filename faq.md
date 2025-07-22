# ❓ Frequently Asked Questions (FAQ)

This section addresses the most common questions developers have when using Fabric 1.0.

---

### 📦 What is Fabric?

Fabric is a full-stack system for deploying provenance-enforced, multi-modal AI agents using a custom DSL, runtime, and compliance framework. It supports deployment on cloud, edge, and local environments.

---

### 🧠 What is a `.fab` file?

A `.fab` file defines an agent or execution block using Fabric DSL. These files are the core unit of logic in a Fabric system and are compiled into executable runtimes.

---

### 🔒 What is a serial ID?

A `serial_id` uniquely identifies a model version with cryptographic provenance. The format is:

<model-name>@<version>#<hash>

yaml


---

### 🚀 How do I deploy a model to Fabric?

1. Define `model.yaml` in `models/<name>/<version>/`
2. Run:
   ```bash
   fab model publish models/<name>/<version>/model.yaml
Ensure Git push to the shared model registry succeeds.

🧪 How do I test my model?
Use the built-in testing suite:

bash

python models/<name>/<version>/tests/test_inference.py
You can customize test scripts under tests/.

🔁 Why does fab model publish say it succeeded but the model is not on GitHub?
Ensure your FABRIC_MODELS_REPO is correctly set in the CLI tooling and that .fabric-models-tmp contains a valid Git clone with origin set to the public repository.

💻 What OS is supported?
Fabric supports:

Ubuntu 20.04+

macOS 12+

Windows 10+ (with WSL 2 or PowerShell + Docker Desktop)

🧩 Can I integrate third-party models?
Yes. Fabric supports ONNX and HuggingFace exports. See:

/ecosystem/onnx-integration.md

/ecosystem/huggingface-export.md

🧱 What are the core components?
Compiler: Translates .fab to LLVM, QASM, or WASM

Daemon: Manages agents, scheduling, and provenance

Tooling: CLI and VSCode for developer workflows

Ledger: Provenance and policy validation

📄 How do I contribute?
See /CONTRIBUTING.md for contribution flow and PR guidelines.

Still stuck? Join the GitHub Discussions or open an Issue.
