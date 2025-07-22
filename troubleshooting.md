# 🛠️ Troubleshooting Guide

This guide covers common issues developers may encounter when working with Fabric 1.0 and how to resolve them.

---

## ❌ Model Publish Fails

**Symptoms:**
- Error: `Missing name/version/serial_id`
- Error: `Schema validation failed`

**Solution:**
- Ensure `model.yaml` includes:
  ```yaml
  name: model-name
  version: x.y.z
  serial_id: model-name@x.y.z#<hash>
Validate YAML against /reference/dsl.md schema.

🔄 Git Push Claims Success but Not Visible on GitHub
Symptoms:

Terminal output says “pushed successfully”

Model doesn't appear in remote repo

Solution:

Check .fabric-models-tmp directory contents

Confirm git remote -v matches https://github.com/fab-project-V1/fabric-models.git

Ensure push uses a non-detached HEAD

🐞 CLI Crashes or Behaves Unexpectedly
Symptoms:

Fabric CLI crashes

Unrecognized command errors

Solution:

Run fab --version to confirm compatibility

Reinstall dependencies:

bash

cd tooling/fab-cli
npm install
🧠 Model Inference Fails
Symptoms:

model not found

invalid input format

Solution:

Validate input schema in model.yaml

Ensure weights.onnx or model.safetensors exists in path

Run test suite:

bash

python tests/test_inference.py
⚙️ Docker/K8s Deployment Fails
Symptoms:

Container errors

Failed to bind ports

Solution:

Verify ports in docker-compose.yml or helm-chart/values.yaml

Use docker logs <container> for details

Run:

bash

docker-compose config
helm lint
📦 Fabric Build Errors
Symptoms:

Errors during fab init or fab build

Solution:

Confirm all .fab files are in correct syntax

Use VS Code extension to lint grammar

Check compiler/frontend/parser.ts for grammar rules

For anything not covered, reach out via GitHub Discussions or open an issue.

