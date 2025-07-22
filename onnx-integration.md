# ONNX Integration in Fabric

Fabric provides first-class support for models exported in the **Open Neural Network Exchange (ONNX)** format, enabling cross-platform deployment, hardware acceleration, and compliance-secure packaging.

## 📦 Why ONNX?

- 🔁 **Framework-agnostic**: Supports PyTorch, TensorFlow, Keras, Scikit-learn, and others.
- ⚡ **Optimized Inference**: Leverages ONNX Runtime, TensorRT, OpenVINO, etc.
- 🔐 **Verifiable Artifacts**: Enables deterministic serialization for provenance hashing.

## 🛠️ Exporting to ONNX

You can export your model using the `torch.onnx` API or `transformers.onnx`.

### PyTorch Example

```python
import torch
from transformers import AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained("path/to/model")
model.eval()

dummy_input = torch.randint(0, 100, (1, 10))
torch.onnx.export(
    model,
    dummy_input,
    "model.onnx",
    input_names=["input_ids"],
    output_names=["logits"],
    dynamic_axes={"input_ids": {0: "batch_size", 1: "sequence"}},
    opset_version=13
)
🧩 Using ONNX Models in Fabric
model.yaml Example
yaml

framework: ONNX
input_schema:
  type: object
  properties:
    input_ids:
      type: array
      items: integer
output_schema:
  type: object
  properties:
    logits:
      type: array
      items:
        type: array
        items: number
Packaging
Place your model.onnx file under:

php-template

models/<name>/<version>/scripts/model.onnx
Include a manifest.json and Dockerfile for runtime.

🚀 Deployment Targets
✅ Edge devices (NVIDIA Jetson, Coral)

✅ WebAssembly runtimes

✅ Kubernetes GPU nodes

✅ Fabric Mesh (via fab model publish)

🧪 Testing
Use onnxruntime to validate locally:

python

import onnxruntime as ort
ort.InferenceSession("model.onnx")
Or through Fabric test harness:

bash

fab model test agent-repacker:1.0.0 --test tests/test_inference.py
✅ Best Practices
Use opset ≥ 13

Avoid dynamic shapes if targeting embedded runtimes

Validate ONNX model with onnx.checker

