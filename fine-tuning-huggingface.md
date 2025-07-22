model-authoring/fine-tuning-huggingface.md
Title: Fine-Tuning HuggingFace Transformers for Fabric Agents

🎯 Objective
Customize a pre-trained LLM from HuggingFace for a domain-specific Fabric agent. We'll use distilbert-base-uncased on a small classification task.

🔧 Step 1: Install Requirements
bash
Copy
Edit
pip install transformers datasets evaluate torch
📂 Step 2: Load a Pre-trained Model
python
Copy
Edit
from transformers import AutoModelForSequenceClassification, AutoTokenizer

model_name = "distilbert-base-uncased"
model = AutoModelForSequenceClassification.from_pretrained(model_name, num_labels=2)
tokenizer = AutoTokenizer.from_pretrained(model_name)
🧪 Step 3: Prepare Dataset
python
Copy
Edit
from datasets import load_dataset

dataset = load_dataset("imdb", split="train[:2%]").train_test_split(test_size=0.2)
def tokenize_fn(example): return tokenizer(example["text"], truncation=True, padding="max_length")
dataset = dataset.map(tokenize_fn, batched=True)
🏋️ Step 4: Train
python
Copy
Edit
from transformers import TrainingArguments, Trainer

args = TrainingArguments("hf-agent-output", evaluation_strategy="epoch", per_device_train_batch_size=4)

trainer = Trainer(model=model, args=args, train_dataset=dataset["train"], eval_dataset=dataset["test"])
trainer.train()
💾 Step 5: Save Model for Fabric
bash
Copy
Edit
trainer.save_model("models/sentiment-agent/1.0.0/training/output")
tokenizer.save_pretrained("models/sentiment-agent/1.0.0/training/output")
📦 Step 6: Export to ONNX (Optional)
bash
Copy
Edit
pip install optimum
python -m optimum.exporters.onnx --model models/sentiment-agent/1.0.0/training/output --task text-classification models/sentiment-agent/1.0.0/scripts/model.onnx
🧾 Step 7: Define model.yaml
yaml
Copy
Edit
name: sentiment-agent
version: 1.0.0
format: onnx
entrypoint: scripts/model.onnx
metadata:
  domain: nlp
  license: apache-2.0
✅ Done!
Your fine-tuned HuggingFace model is now Fabric-compatible.
