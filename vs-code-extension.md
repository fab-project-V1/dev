# Fabric VS Code Extension

The Fabric Visual Studio Code (VS Code) extension provides a powerful, developer-friendly interface for building, testing, and deploying `.fab` modules in real time.

## 🔧 Features

- **Syntax Highlighting** for the Fabric DSL
- **Inline Error Reporting** via the Fabric language server
- **Code Snippets** for common constructs (agents, blocks, observables)
- **Live Compilation & Linting** with `fab-cli`
- **One-click Deploy** to local/edge/cloud environments
- **Integrated Provenance Viewer** for debugging lineage
- **Debug Hooks** for stepping through agent execution

## 📦 Installation

Search for `Fabric Language Tools` in the VS Code Marketplace or install manually:

```sh
code --install-extension fabric-lang-tools.vsix
🛠️ Configuration
After installing, update your workspace .vscode/settings.json:

json

{
  "fabric.languageServerPath": "./tooling/fab-cli/dist/language-server.js",
  "fabric.enableAutoCompile": true
}
🚀 Quickstart
Open a fab-project directory in VS Code.

Create a new .fab file:

bash

mkdir apps/demo && touch apps/demo/Main.fab
Start coding — syntax support and inline errors will appear.

Use the Command Palette:

Fabric: Compile Current File

Fabric: Deploy to Local Mesh

Fabric: Inspect Provenance

🧪 Snippets
Example snippet for an agent block:

fab

agent MyAgent {
  observe Text
  action -> Completion
  using model "text-gen:1.0.0"
}
📡 Debugging
To attach to running agents:

Launch the agent VM with debugging enabled.

From the extension, click "Attach Debugger".

Step through execution line-by-line.

💡 Tips
Enable auto-formatting with Prettier for .fab files.

Use multi-root workspaces to manage different agents/models.

Set up fab-cli tasks in tasks.json for deployment automation.

🧩 Source
The extension source lives under:

bash

tooling/vscode-extension/
├── src/
│   ├── extension.ts
│   ├── language-server/
│   └── snippets/
├── package.json
└── README.md
Contributions and feature requests are welcome!
