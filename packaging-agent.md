model-authoring/packaging-agent.md
Title: Packaging an Agent for Fabric Deployment

🎯 Objective
Package a trained model with its metadata, Docker container, and compliance manifest to prepare it for publishing in the Fabric ecosystem.

🧱 Required Directory Layout
bash
Copy
Edit
models/agent-name/1.0.0/
├── model.yaml
├── scripts/
│   └── model.onnx
├── docker/
│   └── Dockerfile
├── tests/
│   └── test_inference.py
├── data/
│   └── sample_inputs.jsonl
└── training/
    └── output/...
🛠 Step 1: Define model.yaml
yaml
Copy
Edit
name: agent-repacker
version: 1.0.0
type: vision
entrypoint: scripts/model.onnx
framework: onnx
format: onnx
dockerfile: docker/Dockerfile
license: Apache-2.0
tags:
  - edge
  - image-classification
🧪 Step 2: Add Test Script
python
Copy
Edit
import onnxruntime as ort
import json

sess = ort.InferenceSession("scripts/model.onnx")
with open("data/sample_inputs.jsonl") as f:
    inputs = json.loads(next(f))
outputs = sess.run(None, {"input": inputs["input"]})
print(outputs)
Save as tests/test_inference.py.

🐳 Step 3: Write Dockerfile
Dockerfile
Copy
Edit
FROM onnx/onnxruntime
COPY scripts/model.onnx /app/model.onnx
CMD ["onnxruntime_test", "/app/model.onnx"]
🔏 Step 4: Add Manifest (Optional)
json
Copy
Edit
{
  "schema_version": "1.0",
  "author": "Your Name",
  "description": "Classifies aerial images for edge AI tasks",
  "contact": "team@fabric.ai"
}
Save as scripts/manifest.json.

🔐 Step 5: Generate Checksum
bash
Copy
Edit
sha256sum scripts/model.onnx > scripts/model.onnx.sha256
🚀 Step 6: Validate and Publish
bash
Copy
Edit
fab model validate models/agent-repacker/1.0.0/model.yaml
fab model publish models/agent-repacker/1.0.0/model.yaml
✅ Done!
Your agent is now fully packaged and ready for registry deployment.
