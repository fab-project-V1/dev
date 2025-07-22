# Tutorial: End-to-End Fabric Workflow

This tutorial walks you through building, deploying, and publishing a fully functional AI agent using the Fabric 1.0.0 system. It covers every step from model creation to public registry push.

---

## 🎯 Goal

Build a compliant, signed NLP model that:
- Accepts text input
- Returns text completion
- Runs inside a verifiable agent
- Is published to the Fabric global registry

---

## 🧱 Step 1: Scaffold Your Model Agent

```bash
fab init agent-repacker
This creates:

markdown

models/
└── agent-repacker/
    ├── model/
    ├── training/
    └── tests/
🧪 Step 2: Train or Import Your Model
You can:

Train with training/train.py using transformers

Export an existing model to ONNX or TorchScript

Document config in training/config_1_0_0.yaml

Add sample input/output tests in tests/test_inference.py.

🔏 Step 3: Write a Manifest
Create model.yaml:

yaml

name: agent-repacker
version: 1.0.0
framework: ONNX
input_schema:
  type: object
  properties:
    text: { type: string }
output_schema:
  type: object
  properties:
    completion: { type: string }
parameter_count: 70000000
tags: [nlp, completion]
...
Include:

training_data_hash

training_commit

license

performance, policy, and finance sections

🧪 Step 4: Validate
bash

fab model validate models/agent-repacker/1.0.0/model.yaml
Fix any compliance, schema, or provenance errors.

📦 Step 5: Package
bash

fab model package agent-repacker --version 1.0.0
This creates a signed and reproducible container.

🚀 Step 6: Deploy Locally
bash

fab run agent-repacker
Test via CLI or REST using:

bash

curl -X POST localhost:9000/invoke -d '{"text": "Hello"}'
🌐 Step 7: Publish
bash

fab model publish models/agent-repacker/1.0.0/model.yaml
This:

Clones fabric-models.git

Commits model directory

Pushes to public Git registry

✅ Summary
You now have a signed, compliant Fabric agent:

Trained or imported

Validated and benchmarked

Running locally or in mesh

Published to UDAP registry

Next: Try /tutorials/device-integration.md to integrate with edge devices.
