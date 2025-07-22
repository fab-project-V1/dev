# 🔌 Plugin SDK

The **Fabric Plugin SDK** allows developers to extend the Fabric runtime with custom functionality—ranging from hardware accelerators to compliance policies—without modifying the core system. Plugins can hook into Fabric’s compiler, runtime, compliance engine, and ledger.

---

## 🧩 Plugin Types

| Plugin Type       | Description                                      | Path                                  |
|-------------------|--------------------------------------------------|---------------------------------------|
| Compiler Plugin   | Extend DSL parsing, IR passes, or backend targets | `compiler/plugins/`                   |
| Runtime Plugin    | Hook into agent-vm or scheduler execution flow   | `daemon/plugins/`                     |
| Compliance Plugin | Inject policies or monitor data access           | `compliance/plugins/`                 |
| Ledger Plugin     | Provide custom consensus mechanisms              | `daemon/provenance-ledger/plugins/`   |

---

## ⚙️ Plugin Lifecycle

Each plugin follows this lifecycle:

1. **Registration:** Loaded at runtime via plugin manifest or CLI.
2. **Activation:** Hooks into the appropriate subsystem (e.g., parser, scheduler).
3. **Invocation:** Called by Fabric when the relevant event occurs.
4. **Unloading:** Cleaned up at shutdown or hot-swap.

---

## 🏗️ Creating a Plugin

Here’s a basic example of a compliance plugin in TypeScript:

```ts
// compliance/plugins/gdpr-check.ts
export function register() {
  return {
    name: "GDPR-Check",
    onDataAccess: (record) => {
      if (record.region === "EU" && !record.userConsent) {
        throw new Error("GDPR consent required.");
      }
    }
  }
}
Register it in your model.yaml:

yaml

policy:
  plugins:
    - path: compliance/plugins/gdpr-check.ts
🔍 Plugin Manifest
Each plugin must include a manifest (plugin.json):

json

{
  "name": "tensor-fuser",
  "version": "0.1.0",
  "type": "compiler",
  "entry": "compiler/plugins/tensor-fuser.py",
  "description": "Fuses multiple tensor operations into a single ONNX op."
}
🧪 Testing Plugins
Use the CLI to test:


fab plugin test compiler/plugins/tensor-fuser.py
Or run a simulated inference with plugin enabled:


FABRIC_PLUGINS="compliance/plugins/gdpr-check.ts" fab run model.fab
🔒 Security and Sandboxing
Plugins are sandboxed using:

VM isolation (agent-vm)

Signature verification (manifest + content hash)

Limited API access based on type

📦 Publishing Plugins
To share plugins:


fab plugin publish plugins/my-plugin/
This publishes to the Fabric plugin registry with cryptographic signing.

📚 Related Topics
Policy Kernel

Provenance Ledger

Compliance Engine


