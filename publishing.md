# 🚀 Publishing Models to Fabric

Publishing is the final step where your packaged model is signed, registered, and made available in the Fabric public model registry.

---

## 📦 Pre-Publish Checklist

Ensure your model directory includes:

models/
└── my-model/
└── 1.0.0/
├── model.yaml
├── scripts/
│ ├── model.onnx
│ └── manifest.json
├── training/
└── evaluation/



---

## 🧾 model.yaml Metadata

Sample:

```yaml
name: my-model
version: 1.0.0
serial_id: my-model@1.0.0#<SHA256>
framework: ONNX
parameter_count: 70000000
license: Apache-2.0
input_schema:
  type: object
  properties:
    input: { type: string }
output_schema:
  type: object
  properties:
    output: { type: string }
performance:
  metrics:
    - name: accuracy
      value: 0.93
      dataset: internal-test
signatures:
  artifact_sig: <generated>
  manifest_sig: <generated>
signed_by: "<name/email>"
sign_date: "YYYY-MM-DD"
✍️ Signing Artifacts
Fabric CLI will sign and validate model files:

bash

fab model sign models/my-model/1.0.0/model.yaml
This command generates the artifact_sig and manifest_sig fields based on SHA-256 hashes and appends signed_by and sign_date.

📤 Publishing to Registry
bash

fab model publish models/my-model/1.0.0/model.yaml
This:

Validates schema compliance

Commits the model to the public Git registry

Registers it in the UDAP index

✅ Confirmation
Look for:

perl

📦 Publishing my-model:1.0.0...
✅ Model my-model:1.0.0 pushed successfully.
✅ Publish succeeded
Your model will be discoverable via:

bash

fab model list
fab model info my-model@1.0.0
🔁 Updating Models
Use semantic versioning (1.0.1, 1.1.0) for changes

Re-sign and re-publish each version

All versions are immutable once published
