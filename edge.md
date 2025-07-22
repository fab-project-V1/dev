# 🌐 Edge Deployment Guide

Fabric supports lightweight, containerized edge deployments for models that require low-latency, on-device execution. This guide details how to prepare, optimize, and deploy Fabric modules to edge devices.

---

## ✅ Prerequisites

Before deploying to edge:

- Fabric model is compiled and exported (e.g. ONNX)
- Docker is installed on your edge device (or Podman)
- Device has support for required runtimes (TensorRT, OpenVINO, etc.)
- SSH or physical access to device
- `fab-cli` is installed on your dev machine

---

## 🛠️ Step 1: Optimize the Model

Use Fabric’s packaging tools to convert and compress:

```bash
fab model export modules/MyModel.fab --format onnx
fab model quantize output/model.onnx --backend tensorrt
Validate on local device before transfer.

📦 Step 2: Build Edge Container
Create a minimal runtime image:

bash

fab model package modules/MyModel.fab --target edge --output container.tar.gz
This includes:

Inference code (ONNX or compiled WASM)

Model weights

Minimal runtime

Edge-compatible Dockerfile

Optional: edit training/docker/Dockerfile to use platform-specific base images (e.g., Jetson).

🚚 Step 3: Transfer to Device
Copy the container to the edge device:

bash

scp container.tar.gz user@edge-device:/tmp/
Or push to a private container registry.

🚀 Step 4: Run Inference on Device
SSH into the device and load the container:

bash

tar -xzf /tmp/container.tar.gz -C /tmp/container
cd /tmp/container
docker build -t mymodel-edge .
docker run --rm mymodel-edge
For streaming inputs (e.g., camera or sensor):

bash

docker run --rm -v /dev/video0:/dev/video0 mymodel-edge
Use fab monitor to stream logs and results remotely if connected.

🛡️ Step 5: Secure and Monitor
Add policy restrictions (e.g., anonymization):

yaml

policy:
  privacy: anonymized
  energy_budget: 10J/per_call
Use Fabric's remote monitor module or connect to the Provenance Ledger node via mesh VPN.

📱 Edge Device Compatibility
Fabric edge containers run on:

NVIDIA Jetson (Nano, Xavier, Orin)

Raspberry Pi (4/5 with GPU/NPU)

Intel NUC

Coral Edge TPU

Any Linux SBC with Docker

Use fab edge detect to auto-profile hardware.

🧱 Next Steps
Local Deployment

Cloud Deployment

Hardware Adaptation SDK


