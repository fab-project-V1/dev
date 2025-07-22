Using the VSCode Extension
Fabric's official Visual Studio Code extension offers syntax highlighting, schema validation, DSL auto-completion, and live diagnostics for .fab files.

🔧 Installation
Open VSCode

Go to Extensions panel (⇧⌘X)

Search for: "Fabric AI DSL"

Click Install

Or install via CLI:

bash
Copy
Edit
code --install-extension fabric-ai.vscode-fabric
🎨 Features
Syntax Highlighting for .fab files

Auto-Completion for DSL keywords and types

Inline Errors on schema and semantic violations

Snippets for blocks (Agent, Exec, If, Quantum, etc.)

Hover Docs for DSL constructs

Command Palette Integration:

Fabric: Compile

Fabric: Deploy

Fabric: Run in Agent-VM

🧪 Example
As you type:

fab
Copy
Edit
Agent MyVisionAgent:
    input:
        img: Image
You’ll see live suggestions for block structure, types, and annotations.

⚙️ Config Options
Edit .vscode/settings.json:

json
Copy
Edit
{
  "fabric.agentSchema": "fabric-schema.json",
  "fabric.runtimeEndpoint": "http://localhost:7777"
}
🛠 Troubleshooting
Make sure your .fab files are in a recognized project (with fab-project/)

Use fab check to manually verify syntax

Reload window if auto-completion fails: ⇧⌘P > Reload Window

📌 Tips
Use snippet shortcuts like fab-agent, fab-if, fab-quantum

Ctrl+Click on types to view linked documentation

Supports Fabric 1.0.0 and newer

🧭 Related
DSL Basics

CLI Overview
