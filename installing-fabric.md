# 🚀 Installing Fabric

Get started with Fabric by setting up the CLI, runtime, and developer environment locally.

---

## 🛠️ Prerequisites

- **Node.js** (>= 18)
- **Python** (>= 3.10)
- **Docker** (for containerized apps)
- **Git**
- (Optional) **Visual Studio Code**

---

## 📦 Installing Fabric CLI

Install the Fabric CLI globally:

```bash
npm install -g @fabric-compiler/fab-cli
Verify installation:

bash

fab --version
🧪 Initialize a Project
Create your first Fabric project:

bash

fab init my-first-app
cd my-first-app
This scaffolds a working Fabric project structure.

🐍 Set Up Python Environment
Recommended setup:

bash

python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
🧱 Build and Run
To compile and simulate:

bash

fab build
fab simulate
To launch your app (if it includes an agent service):

bash

fab run
🧩 VSCode Extension (Optional)
Enable syntax highlighting, snippets, and inline validation:

bash

code --install-extension fabric-labs.vscode-fabric
🧭 What's Next?
Write your first model in first-model.md

Explore command line tooling in cli-overview.md


