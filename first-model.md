# ✨ Your First Fabric Model

This tutorial walks you through creating and deploying a minimal Fabric AI model.

---

## 🎯 Goal

Build a simple agent that takes text input and returns a transformed string.

---

## 📁 Step 1: Create a Fabric Module

Create a new file: `EchoAgent.fab`

```fab
agent EchoAgent {
  input: {
    message: String
  }

  output: {
    reply: String
  }

  execute {
    reply = "Echo: " + message
  }
}
This defines an EchoAgent that echoes any incoming message.

🔨 Step 2: Compile the Model
bash

fab build
Fabric will validate and compile the .fab file into IR for execution.

🚀 Step 3: Simulate Locally
bash

fab simulate EchoAgent.fab
Provide input:

json

{ "message": "Hello Fabric!" }
Expected output:

json

{ "reply": "Echo: Hello Fabric!" }
📦 Step 4: Package for Deployment
Generate a container image and config:

bash

fab package
📤 Step 5: Publish (Optional)
Push your model to the public Fabric registry:

bash

fab model publish models/echo-agent/1.0.0/model.yaml
Make sure to define model.yaml and version your directory properly.

🧪 Test Integration
Try calling your deployed model from a Fabric app or via HTTP API if exposed.

You're now ready to build more complex agents, integrate sensors, or wrap transformers!
