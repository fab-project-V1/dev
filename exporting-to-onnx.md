model-authoring/exporting-to-onnx.md
Title: Exporting Models to ONNX for Fabric Integration

🎯 Objective
Convert trained PyTorch or TensorFlow models to ONNX format for compatibility with Fabric agents and cross-platform deployment.

🔍 Why ONNX?
Cross-framework interoperability

Required for Fabric containerization and inference acceleration

Standardized input/output signatures

🛠 Step 1: Load and Prepare Model
Example: PyTorch model.pt

python
Copy
Edit
import torch
from model_def import MyModel  # your custom class

model = MyModel()
model.load_state_dict(torch.load("model.pt"))
model.eval()
🔧 Step 2: Create Dummy Input
python
Copy
Edit
dummy_input = torch.randn(1, 3, 224, 224)  # shape depends on your model
🔁 Step 3: Export to ONNX
python
Copy
Edit
torch.onnx.export(
    model,
    dummy_input,
    "model.onnx",
    export_params=True,
    opset_version=12,
    input_names=["input"],
    output_names=["output"]
)
🧪 Step 4: Validate Export
bash
Copy
Edit
python -m onnxruntime.tools.convert_onnx_models_to_ort model.onnx
📦 Step 5: Integrate in Fabric
Directory layout after export:

bash
Copy
Edit
models/my-model/1.0.0/
├── model.yaml
├── scripts/
│   └── model.onnx
└── docker/
    └── Dockerfile
Update model.yaml:

yaml
Copy
Edit
name: my-model
version: 1.0.0
format: onnx
entrypoint: scripts/model.onnx
🚀 Optional: TensorFlow Export
python
Copy
Edit
import tf2onnx
import tensorflow as tf

model = tf.keras.models.load_model("saved_model")
spec = (tf.TensorSpec((None, 224, 224, 3), tf.float32, name="input"),)
model_proto, _ = tf2onnx.convert.from_keras(model, input_signature=spec)
with open("model.onnx", "wb") as f:
    f.write(model_proto.SerializeToString())
✅ Done!
Your model is now Fabric-ready as ONNX.

