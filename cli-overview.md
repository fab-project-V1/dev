# 🛠️ Fabric CLI Overview

The Fabric Command Line Interface (`fab`) is the primary tool for managing and operating Fabric AI systems.

---

## 📦 Installation

After installing Fabric:

```bash
fab --version
📁 Project Setup
bash

fab init my-project
cd my-project
Creates a new Fabric project scaffold.

🧱 Build Models
Compile all .fab modules:

bash

fab build
To build a specific file:

bash

fab build path/to/module.fab
🧪 Simulation
Run a .fab module locally:

bash

fab simulate EchoAgent.fab
📤 Publish Models
Push a fully packaged model to the Fabric registry:

bash

fab model publish models/my-model/1.0.0/model.yaml
🔍 Monitor
Observe deployed models and agents:

bash

fab monitor
🧰 Additional Commands
Command	Description
fab deploy	Deploy compiled model to runtime target
fab model push	Push model to public model Git registry
fab test	Run test suite for model behaviors
fab compliance verify	Validate model against policies/profiles

📚 Help
Use --help for any command:

bash

fab build --help
The CLI is designed for productivity, scriptability, and integration into any CI/CD pipeline.
