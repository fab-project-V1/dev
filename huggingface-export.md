# Hugging Face Export in Fabric

Fabric supports streamlined export of Hugging Face Transformers models into compliant, reproducible, and deployable formats across edge, cloud, and mesh environments.

## 🤗 Why Hugging Face?

- 🌍 Largest NLP model hub
- 📚 Rich ecosystem of tokenizers, pipelines, and trainers
- 🔄 Supports conversion to ONNX, TorchScript, and SafeTensors

---

## 🚢 Export Workflow

### 1. Choose a Base Model

```bash
transformers-cli login
transformers-cli repo clone EleutherAI/pythia-70m
Or programmatically:

python

from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("EleutherAI/pythia-70m")
tokenizer = AutoTokenizer.from_pretrained("EleutherAI/pythia-70m")
2. Convert to ONNX
bash

transformers onnx --model=EleutherAI/pythia-70m onnx-export
This generates model.onnx, tokenizer.json, config.json.

3. Save as SafeTensors
python

model.save_pretrained("./safe", safe_serialization=True)
tokenizer.save_pretrained("./safe")
Ensure reproducibility and deterministic hashing with:

bash

sha256sum safe/model.safetensors
📦 Fabric Integration
Place exported files under:

pgsql

models/<name>/<version>/training/output/
├── model.safetensors
├── tokenizer.json
├── config.json
├── tokenizer_config.json
And declare in model.yaml:

yaml

framework: ONNX
training_config: training/config_1_0_0.yaml
provenance:
  training_data_hash: sha256:...
  training_commit: ...
🧪 Fabric Test Inference
Create a test file:

python

from transformers import AutoTokenizer, AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained("training/output")
tokenizer = AutoTokenizer.from_pretrained("training/output")

inputs = tokenizer("The future of AI is", return_tensors="pt")
output = model.generate(**inputs)
print(tokenizer.decode(output[0]))
Run with:

bash

fab model test <name>:<version>
🧬 Best Practices
Pin Hugging Face version (e.g., transformers==4.41.0)

Always export tokenizer alongside model

Use SafeTensors over .bin for compliance and determinism
