model-authoring/repackaging-thirdparty.md
Title: Repackaging PyTorch / TensorFlow Models into Fabric Agents

🎯 Objective
Wrap an existing PyTorch or TensorFlow model (trained outside of Fabric) into a standardized Fabric model directory with manifest, container, and DSL bindings.

🛠 Step 1: Identify Model
Assume you have:

model.pt (PyTorch)

or saved_model/ (TensorFlow)

Plus custom inference.py file with a callable predict(input) function

🗂 Step 2: Scaffold Fabric Directory
bash
Copy
Edit
fab init model sentiment-wrapper --version 1.0.0
This generates:

pgsql
Copy
Edit
models/sentiment-wrapper/1.0.0/
├── model.yaml
├── scripts/
│   ├── predict.py
│   └── manifest.json
└── docker/
    └── Dockerfile
📜 Step 3: Write predict.py
python
Copy
Edit
import torch
from transformers import AutoTokenizer

model = torch.load("model.pt")
tokenizer = AutoTokenizer.from_pretrained("distilbert-base-uncased")

def predict(text):
    inputs = tokenizer(text, return_tensors="pt")
    with torch.no_grad():
        logits = model(**inputs).logits
    return logits.argmax().item()
🧾 Step 4: Define model.yaml
yaml
Copy
Edit
name: sentiment-wrapper
version: 1.0.0
format: python
entrypoint: scripts/predict.py
metadata:
  source: huggingface
  original_framework: pytorch
  domain: nlp
  license: apache-2.0
🐳 Step 5: Dockerize (Optional)
Dockerfile
Copy
Edit
FROM python:3.10-slim
COPY . /app
WORKDIR /app
RUN pip install torch transformers
ENTRYPOINT ["python", "scripts/predict.py"]
🔏 Step 6: Validate
bash
Copy
Edit
fab model validate models/sentiment-wrapper/1.0.0/model.yaml
✅ Done!
Your PyTorch or TensorFlow model is now repackaged as a Fabric model.

