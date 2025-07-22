Sandbox Examples
Fabric sandbox examples offer interactive, annotated code snippets that let you explore the Fabric DSL and system behavior live or locally via fab run.

✨ What This Covers
Core Fabric blocks (Agent, Exec, If, Emit)

Integrating pre-trained models

Simulating policy logic

Observing provenance flow

🔧 Setup for Live Testing
Clone a Fabric example repo:

bash
Copy
Edit
git clone https://github.com/fab-project-V1/fabric-sandbox-examples
cd fabric-sandbox-examples
Run the CLI sandbox:

bash
Copy
Edit
fab sandbox start
Modify and test .fab files in /examples/ with instant feedback.

🧠 Sample: Minimal Agent
fab
Copy
Edit
Agent HelloAgent:
    input:
        msg: String
    output:
        greeting: String

Exec:
    script: |
        greeting = "Hello, " + msg
💬 Commentary: Demonstrates Agent and Exec block composition with simple string input/output.

📸 Sample: Vision Classifier
fab
Copy
Edit
Agent VisionAgent:
    input:
        image: Image
    output:
        label: String

Exec:
    model: resnet18.onnx
    runtime: onnx
💬 Commentary: Ingests an image and performs ONNX-based inference using a ResNet model.

🛡️ Sample: Conditional Policy Execution
fab
Copy
Edit
If:
    condition: env.power_budget < 20
    Then:
        Emit: "Low power mode activated"
    Else:
        Exec:
            script: run_full_model()
💬 Commentary: Shows dynamic decision-making using environment variables and conditionals.

✅ Next Steps
Add your .fab files to /examples and run fab sandbox test

Use annotations to document block purpose for your team

🔗 Related
DSL Basics

Running Locally
