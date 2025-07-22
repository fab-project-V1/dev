# 🖥️ Local Deployment Guide

Running Fabric locally is ideal for development, debugging, and small-scale experiments. This guide walks you through setting up the complete Fabric runtime stack on your machine.

---

## ✅ Prerequisites

Ensure the following are installed:

- [Docker](https://www.docker.com/)
- [Node.js](https://nodejs.org/) (v18+)
- [Python](https://www.python.org/) (3.9+)
- [Fab CLI](../tooling/fab-cli/README.md)
- [VS Code](https://code.visualstudio.com/) with Fabric Extension

---

## 📦 Step 1: Bootstrap the Environment

Clone the Fabric repository and install dependencies:

```bash
git clone https://github.com/fab-project-V1/fabric.git
cd fabric
npm install -g ./tooling/fab-cli
Create a local project:

bash

fab init my-local-project
cd my-local-project
🧱 Step 2: Launch Core Services
Start the full local stack using Docker Compose:

bash

docker compose -f config/docker-compose.yml up -d
This includes:

Agent VM Runtime

UDAP Registry

Scheduler + Policy Kernel

Provenance Ledger

Plugin Manager

Check status:

bash

docker ps
🧪 Step 3: Run and Debug a Model
Compile and run a sample:

bash

fab build modules/MyModel.fab
fab run modules/MyModel.fab
Use fab monitor to observe inference, logs, and policy evaluations.

Attach debugger in VS Code using the provided launch configuration.

🔄 Step 4: Develop Iteratively
Update .fab code → rebuild → rerun:

bash

fab build
fab run
Live reload is supported via fab watch.

📁 Local Output Structure
perl

my-local-project/
├── modules/
├── build/
├── logs/
├── registry/
└── .fab-cache/
🧼 Cleanup
To stop and remove containers and volumes:

bash

docker compose down -v
To clear Fabric build and registry cache:

bash

fab clean
🧰 Tips
Use FABRIC_DEBUG=true for verbose logs.

fab shell opens a local REPL with Fabric runtime bindings.

Create mock inputs using fab gen input-schema.

🧱 Next Steps
Edge Deployment

Cloud Deployment

Writing Secure Agents

perl
Copy
Edit
