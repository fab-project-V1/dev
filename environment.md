# Environment & System Requirements

This document outlines the supported environments and minimum system requirements to develop, run, and deploy Fabric 1.0 applications.

---

## 🖥️ Supported Operating Systems

| Platform      | Minimum Version     | Notes                                     |
|---------------|---------------------|-------------------------------------------|
| Ubuntu Linux  | 20.04 LTS           | Recommended for production deployments    |
| macOS         | 12.0 Monterey       | M1/M2 native support via Rosetta          |
| Windows       | 10 Pro (64-bit)     | WSL2 required for full runtime support    |
| Docker        | 20.10+              | Required for container-based execution    |

---

## 🧠 Minimum Hardware Requirements

| Component       | Minimum           | Recommended          |
|------------------|-------------------|------------------------|
| CPU              | 4 cores            | 8+ cores               |
| RAM              | 8 GB               | 16 GB+                 |
| Disk             | 20 GB free space   | SSD recommended        |
| GPU (Optional)   | CUDA-enabled       | NVIDIA A100/RTX 4090+  |

> **Note:** GPU is required only for model training or ONNX acceleration workflows.

---

## 🔧 Required Dependencies

Ensure the following tools are installed and accessible in your system `PATH`:

| Tool               | Version         | Install Guide |
|--------------------|-----------------|----------------|
| Python             | 3.9 - 3.11       | [python.org](https://www.python.org/downloads/) |
| Node.js + npm      | v18+             | [nodejs.org](https://nodejs.org/) |
| Docker             | 20.10+           | [docker.com](https://www.docker.com/products/docker-desktop) |
| Git                | 2.30+            | [git-scm.com](https://git-scm.com/) |
| `fab-cli`          | latest           | Installed via `npm i -g fab-cli` |
| MLIR + LLVM (opt)  | LLVM 14+         | Required only for compiler backend devs |

---

## 🌐 Network Access

The following domains must be reachable for full runtime and publishing functionality:

- `registry.fabric.run` — model and agent registry
- `mesh.fabric.run` — UDAP coordination layer
- `github.com/fab-project-V1` — plugin and model repositories

---

## ✅ Compatibility Matrix

| Component             | Compatible with Fabric 1.0 |
|------------------------|-----------------------------|
| HuggingFace Transformers | ✅ v4.30+                   |
| ONNX Runtime             | ✅ v1.15+                   |
| Kubernetes               | ✅ v1.25+                   |
| ROS2 Humble              | ✅ (for edge integration)   |
| VSCode Extension         | ✅ latest from Marketplace  |

---

## 🧪 Verification Script

After installing dependencies, run:

```bash
fab doctor
