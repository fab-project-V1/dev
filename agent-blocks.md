# 🔗 Agent Blocks: Composing Modular AI Logic

Agent blocks in Fabric are composable building blocks for secure, multimodal AI applications. They enable logic chaining, reusability, and distributed execution.

---

## 🧱 What Are Agent Blocks?

Each `agent` in Fabric defines:
- A schema-bound **input**
- A validated **output**
- A **run** section (or block) expressing execution logic

Blocks may call models, other agents, conditionals, or structural compositions.

---

## ➕ Composing Agents

```fab
agent ClassifyAndRespond:
  input: { text: string }
  output: { label: string, response: string }

  run:
    let category = Classifier.run({ text }).label
    let reply = Responder.run({ category }).text
    return { label: category, response: reply }
Each run step may invoke an agent or model, and their results are directly accessible.

🔄 Control Flow Blocks
fab

run:
  if input.age < 18:
    return MinorResponder.run({ name: input.name })
  else:
    return AdultResponder.run({ name: input.name })
You can chain multiple conditional branches or loop through bounded sequences.

🪢 Nested Blocks
Blocks may contain sub-blocks:

fab

run:
  let stage1 = Tokenizer.run({ text: input.text })
  let stage2 = Summarizer.run({ tokens: stage1.tokens })
  return { summary: stage2.summary }
🧩 Agent Libraries
You can import agents:

fab

import AssistantUtils from "lib/assistive-utils.fab"

run:
  return AssistantUtils.Normalize.run({ name: input.name })
🔒 Policy-Aware Blocks
Agent blocks respect declared policies:

fab

agent Redactor:
  input: { document: string }
  output: { redacted: string }

  policy:
    privacy: anonymized
    audit: required

  run:
    return PII_Remover.run({ document: input.document })
Policies are enforced across any downstream block.

🧠 Block Execution Semantics
Pure: Deterministic, replayable

Traceable: Block IDs and signatures recorded

Composable: Nested calls or block libraries supported

Auditable: Block-level provenance recorded automatically

🧪 Test Blocks with CLI
bash

fab test modules/RespondWithLabel.fab
You can mock sub-agents using stubs for fast development.

🛤️ Next Steps
Explore:

quantum-modules.md for quantum circuit and hybrid execution

training.md for how blocks link to trained models


