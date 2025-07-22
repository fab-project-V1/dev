# ⚙️ Model Quantization in Fabric

Quantization reduces the numerical precision of model weights and activations, enabling faster, smaller, and more energy-efficient inference—critical for edge and real-time AI.

---

## 🎯 What Is Quantization?

Quantization converts model parameters from 32-bit floating point (FP32) to lower-bit representations like:

| Format   | Bit Width | Use Case                  |
|----------|-----------|---------------------------|
| FP16     | 16-bit    | Speed boost, same accuracy |
| INT8     | 8-bit     | Edge deployment, low power |
| INT4     | 4-bit     | Max compression, some tradeoff |

---

## ⚡ Benefits

- 🚀 **Speedup:** Reduced computational demand
- 📦 **Size reduction:** Smaller model binaries
- 🔋 **Energy savings:** Especially on mobile/IoT
- 🌍 **Latency improvement:** Faster responses

---

## 🧰 Quantizing in Fabric

Fabric supports quantization via the `fab optimize` tool:

```bash
fab optimize quantize --model models/agent-repacker/1.0.0 --precision int8
Outputs a quantized/ folder alongside original weights.

🛠 Supported Formats
Framework	Quantization APIs
ONNX	ONNX Runtime QDQ/ORT tools
PyTorch	torch.quantization or optimum
TensorFlow	Post-training quantization via TFLite

Fabric's optimizer selects the correct backend automatically.

📉 Accuracy vs Compression Tradeoff
Format	Compression	Accuracy Impact
FP16	~2x	Negligible
INT8	~4x	Minor (<1%)
INT4	~8x	Moderate (2–5%)

Evaluate quantized models using:

bash

fab benchmark agent agent-repacker --quantized
🔒 Compliance Notes
Quantized models must retain original provenance

Include a new parameter_count in your model.yaml

You may sign separately with:

bash

fab model sign --variant quantized
🧪 Hybrid and Layer-wise Quantization
Advanced users can:

Mix FP16 and INT8 per layer

Preserve attention or embedding layers in FP32

Use per-channel vs per-tensor quantization

Fabric does not yet support mixed-precision auto-tuning, but it's planned for v1.2.

Quantization is a powerful knob—use it wisely to balance performance and model fidelity.
