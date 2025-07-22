# 📦 Model Packaging in Fabric

Packaging is the step where trained and evaluated models are bundled into portable, executable artifacts compatible with Fabric's runtime and registry.

---

## 🎯 Goals of Packaging

- Create an ONNX or containerized version of the model
- Generate a validated manifest
- Ensure compliance and runtime compatibility
- Prepare for publishing to Fabric registry

---

## 🧱 Directory Structure

models/
└── my-model/
└── 1.0.0/
├── training/
├── evaluation/
└── scripts/
├── export_to_onnx.py
├── package.py
└── manifest.json



---

## 🧪 ONNX Export

Use provided script:

```python
# export_to_onnx.py
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch

model = AutoModelForCausalLM.from_pretrained("training/output")
tokenizer = AutoTokenizer.from_pretrained("training/output")

input_ids = tokenizer("Test input", return_tensors="pt").input_ids

torch.onnx.export(
    model, (input_ids,),
    f="scripts/model.onnx",
    input_names=["input_ids"],
    output_names=["logits"],
    dynamic_axes={"input_ids": {0: "batch_size", 1: "seq_len"},
                  "logits": {0: "batch_size", 1: "seq_len"}},
    opset_version=14
)
🛠️ Manifest Generation

bash


fab model manifest --output scripts/manifest.json
Includes:

Model metadata (name, version, framework)

Provenance references

Compliance tags

Output schema

🐳 Containerization (Optional)

Dockerfile

# Dockerfile
FROM python:3.10-slim
COPY training/output /app/model
COPY scripts/model.onnx /app/model.onnx
CMD ["python", "-m", "inference"]
Build:

bash

docker build -t my-model:1.0.0 .
✅ Verification
Use Fabric CLI to validate the package:

bash

fab model verify --path scripts/manifest.json

📁 Output
pgsql

scripts/
├── model.onnx
├── manifest.json
└── Dockerfile
🎯 Next Steps
Publishing


