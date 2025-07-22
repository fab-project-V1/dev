Running Fabric Locally
This guide walks you through running a standalone Fabric agent using the CLI and Docker—ideal for quick iteration and validation.

🧠 What You’ll Learn
Running agents without Kubernetes

Using Dockerized ONNX or Python agents

Inspecting logs and outputs

🧰 Prerequisites
Fabric CLI (pip install fab-cli)

Docker

A .fab file and any associated model files (e.g., model.onnx)

1️⃣ Start a New Fabric Project
bash
Copy
Edit
mkdir my-local-agent
cd my-local-agent
fab init
2️⃣ Define a Simple Agent
In agent.fab:

fab
Copy
Edit
agent Hello {
  input: string
  output: string

  run {
    return "Hello, " + input + "!"
  }
}
3️⃣ Build the Agent
bash
Copy
Edit
fab build
You’ll get .pkg and .docker/ outputs.

4️⃣ Launch the Agent Container
bash
Copy
Edit
docker build -t hello-agent .docker/
docker run -it hello-agent --input '"World"'
Expected output:

json
Copy
Edit
"Hello, World!"
🧪 Debug Tips
Add --debug to the CLI run for verbose logs.

Mount host directories via -v for live model testing.

Use fab logs (if using fab deploy) to stream output.

🔁 Loop on Code Changes
bash
Copy
Edit
vim agent.fab  # Make edits
fab build
docker run -it hello-agent --input '"again"'
🧩 Summary
Running agents locally gives full control for testing and development without orchestration overhead.

