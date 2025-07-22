# 📘 DSL Basics: Writing Your First Fabric Module

The Fabric DSL is a high-level, compositional language designed to express multimodal, privacy-conscious, and edge-deployable AI logic. It compiles to secure enclaves and quantum-compatible IR.

---

## 🧩 Module Anatomy

Every `.fab` file begins with metadata and `agent` or `module` definitions.

```fab
module HelloAgent:
  version: 1.0.0
  author: "Ada Lovelace <ada@fabric.ai>"
  tags: ["intro", "hello-world"]
👩‍💻 Agents & Execution
Fabric programs define agents:

fab

agent Greeter:
  input: { name: string }
  output: { greeting: string }

  run:
    let msg = "Hello, " + name
    return { greeting: msg }
Agents are stateless by default, deterministic, and executable locally or on-mesh.

🛠 Types & Structs
The DSL supports primitive types, arrays, and custom structs.

fab

struct User:
  name: string
  email: string

agent Welcome:
  input: User
  output: string

  run:
    return "Welcome, " + input.name
🔁 Conditionals & Loops
fab

run:
  if user.name == "":
    return "Invalid user"
  else:
    return "Hi, " + user.name
For loops are restricted to bounded iteration for auditability.

⚡ Inference Calls
Fabric supports calling ML models:

fab

model Completion@1.0.0

agent CompletePrompt:
  input: { prompt: string }
  output: { text: string }

  run:
    return Completion.run({ prompt: prompt })
🔒 Privacy & Provenance
You can annotate sensitive fields:

fab

input: { email: string @private }
And enable audit trails:

fab

@provenance track
✅ Compile and Run
Use the CLI to compile and test:

bash

fab compile modules/HelloAgent.fab
fab test modules/HelloAgent.fab
🧠 Next Up
Explore:

agent-blocks.md for composable AI pipelines

quantum-modules.md for QIR integration

Fabric DSL is where semantics meet safety, composability meets compliance.
