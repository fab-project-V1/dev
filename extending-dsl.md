# 🧱 Extending the Fabric DSL

Fabric's DSL is designed for extensibility, enabling advanced users to evolve the language with custom types, keywords, and semantics.

---

## 🧠 Why Extend the DSL?

- Add domain-specific primitives (e.g., "pose", "genome", "threat-level")
- Introduce new execution blocks (`quantum`, `robot`, `bio`, etc.)
- Enforce org-level constraints via new decorators

---

## 📂 Extension Directory Layout

dsl-extension/
├── grammar.ne # Nearley grammar additions
├── transformers.ts # AST transforms or validators
├── keywords.json # Reserved word registry
└── tests/
└── grammar.spec.ts



---

## 🧬 Modifying the Grammar

Fabric uses [Nearley](https://nearley.js.org/) to define its syntax. You can append new rules:

```ne
@builtin "whitespace.ne"

AtomicType -> "genome" {% id %}
             | "pose"   {% id %}
Add to the master grammar using:

bash

fab dsl extend ./dsl-extension/grammar.ne
🚦 AST Transformers
DSL extensions often include AST validators or modifiers:

ts
Copy
Edit
export function transform(ast) {
  walk(ast, (node) => {
    if (node.type === 'PoseType' && node.range > 100) {
      throw new Error("Pose range exceeds safe threshold.");
    }
  });
  return ast;
}
Register with:

bash

fab dsl register-transformer ./dsl-extension/transformers.ts
🔍 Reserved Keywords
Register new keywords to reserve them in the system:

json

["genome", "pose", "reaction", "threat_level"]
Add via:

bash

fab dsl reserve ./dsl-extension/keywords.json
🧪 Testing Extensions
DSL extensions can be tested with:

ts

import { parse } from 'fabric-dsl';
test('custom pose syntax', () => {
  const ast = parse("let p: pose = [0.1, 0.2, 0.3]");
  expect(ast.type).toBe('PoseAssignment');
});
🛡️ Versioning and Compatibility
Extensions must declare a compatible DSL core version (e.g., >=1.0.0 <2.0.0)

All custom types and decorators must be namespaced to avoid global collisions

🧩 Example: Custom Execution Block
ne

CustomBlock -> "bio" _ BlockBody
ts

export function execute_bio(block, context) {
  return simulateBiologicalResponse(block.instructions);
}
Fabric DSL extensions make Fabric not just programmable, but evolutionarily adaptable to any AI domain.


