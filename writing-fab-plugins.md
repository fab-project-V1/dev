# 🧩 Writing FAB Plugins

Fabric supports a modular plugin system for extending core functionalities such as DSL semantics, model hooks, runtime behaviors, and audit logic.

---

## 🧬 Plugin Anatomy

A Fabric plugin consists of:

my-plugin/
├── plugin.json # Metadata manifest
├── index.ts # Entry point
├── handlers/ # Lifecycle and compiler hooks
│ ├── onCompile.ts
│ └── onDeploy.ts
└── tests/
└── plugin.spec.ts

yaml
Copy
Edit

---

## 📜 plugin.json Manifest

```json
{
  "name": "privacy-enhancer",
  "version": "1.0.0",
  "description": "Adds token anonymization checks to Fabric compiler.",
  "entry": "index.ts",
  "hooks": ["compile", "deploy"]
}
🔧 Hook Example: onCompile
ts

export function onCompile(ast, options) {
  if (ast.containsPII()) {
    throw new Error("PII detected in DSL source.");
  }
  return ast;
}
🚀 Registering the Plugin
bash

fab plugin add ./my-plugin
Registered plugins are listed in:

bash

fab plugin list
🧪 Testing Your Plugin
Each plugin can include CI-enforced test specs:

ts

import { testPlugin } from 'fab-sdk';

testPlugin('privacy-enhancer', () => {
  const sample = loadAST('examples/leaky.fab');
  expect(() => plugin.onCompile(sample)).toThrow();
});
Run tests with:

bash

npm test
🛠 Use Cases
Type	Use Case
Compiler Hook	Custom AST transforms
Runtime Hook	Logging, rate-limiting, obfuscation
Audit Hook	Custom compliance or fairness logic
UI Plugin	Extend VSCode/CLI interactions

🔐 Plugin Isolation
Plugins run in a sandboxed VM for security. No access to host FS or network is permitted unless explicitly granted via:

json

"permissions": ["filesystem", "net"]
Plugins are the foundation for Fabric ecosystem extensibility—use them to encode your innovation directly into the system pipeline!
