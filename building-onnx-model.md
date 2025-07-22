model-authoring/building-onnx-model.md
Title: Building an ONNX Model for Fabric Agents

🎯 Objective
Train a basic model (e.g. image classifier), export it to ONNX format, and prepare it for deployment in a Fabric agent.

🛠️ Step 1: Train a PyTorch Model
python
Copy
Edit
import torch
import torch.nn as nn
import torchvision.transforms as transforms
import torchvision.datasets as datasets

model = nn.Sequential(
    nn.Flatten(),
    nn.Linear(28*28, 128),
    nn.ReLU(),
    nn.Linear(128, 10)
)

# MNIST dataset
train_loader = torch.utils.data.DataLoader(
    datasets.MNIST('.', train=True, download=True, transform=transforms.ToTensor()),
    batch_size=64, shuffle=True)

optimizer = torch.optim.Adam(model.parameters())
loss_fn = nn.CrossEntropyLoss()

for epoch in range(3):
    for imgs, labels in train_loader:
        output = model(imgs)
        loss = loss_fn(output, labels)
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
📦 Step 2: Export to ONNX
python
Copy
Edit
dummy_input = torch.randn(1, 1, 28, 28)
torch.onnx.export(model, dummy_input, "model.onnx", opset_version=11)
🔍 Step 3: Validate the ONNX Model
bash
Copy
Edit
pip install onnx onnxruntime
python -c "
import onnx, onnxruntime
model = onnx.load('model.onnx')
onnx.checker.check_model(model)
sess = onnxruntime.InferenceSession('model.onnx')
print(sess.get_inputs()[0].shape)
"
📁 Step 4: Create Fabric Agent Directory
bash
Copy
Edit
mkdir -p models/mnist-classifier/1.0.0
mv model.onnx models/mnist-classifier/1.0.0/
🧾 Step 5: Write the model.yaml
yaml
Copy
Edit
name: mnist-classifier
version: 1.0.0
format: onnx
entrypoint: model.onnx
metadata:
  domain: vision
  license: Apache-2.0
✅ Done!
You’ve built and validated an ONNX model for use in Fabric agents.
