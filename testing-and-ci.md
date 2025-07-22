# ✅ Testing and CI for Fabric Modules

Fabric provides a structured testing and CI ecosystem for DSL modules, models, and plugin components.

---

## 🧪 Test Types

### 1. **DSL Unit Tests**
Validate syntax trees, semantic rules, and runtime evaluation:

```ts
test('agent block compiles', () => {
  const ast = parse('agent Test { input: String; output: String; }');
  expect(ast.type).toBe('AgentDecl');
});
Use the built-in runner:

bash

fab test
2. Model Inference Tests
Ensure trained models behave as expected:

ts

test('model returns JSON', async () => {
  const result = await runModel('agent-repacker:1.0.0', { text: "hello" });
  expect(result.Completion).toBeDefined();
});
3. Compliance Tests
Automatically validate privacy, energy, and fairness constraints:

bash

fab compliance test model.yaml
⚙️ CI Setup
Use GitHub Actions to automate tests and model validation:

.github/workflows/ci.yml

yaml

name: Fabric CI

on:
  push:
    paths:
      - "models/**"
      - "modules/**"
      - "dsl/**"

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Fabric
        run: npm install -g fab-cli
      - name: Run tests
        run: fab test
📦 Testing Plugins
All plugin SDKs include a Jest harness for logic verification and coverage:

bash

cd plugins/my-plugin
npm run test
🧠 Best Practices
Ensure every module has tests/ with semantic coverage

Use mock inputs/outputs to avoid external dependencies

Track compliance/ test outcomes in CI

Fabric's test tooling supports correctness, compliance, and reproducibility for every module, agent, and model.


