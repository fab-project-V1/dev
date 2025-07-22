# Fabric DSL Reference

This document provides a structured lookup for the Fabric DSL—used to describe AI systems, agents, workflows, and compliance rules.

---

## 🧩 Core Constructs

### `agent`
Defines an autonomous component that can perform tasks or inference.

```yaml
agent:
  name: ImageAnalyzer
  inputs: [image]
  outputs: [classification]
  model: edge-vision-v2@1.1.0
workflow
Describes an orchestrated sequence of agents and dataflows.

yaml

workflow:
  name: RepackPipeline
  steps:
    - use: TextSanitizer
    - use: CompletionEngine
import
Pulls external models or libraries into context.

yaml

import:
  - edge-vision-v2@1.1.0
  - shared/vision-utils.fab
🔁 Block Types
compute
Executes deterministic logic or invokes a model.

yaml

compute:
  using: PythiaModel
  input: user_query
  output: completion
control
Applies decision logic (if/else, switch, loop).

yaml

control:
  if: user.intent == 'help'
  then:
    - emit: 'How can I assist you?'
observe
Gathers telemetry or logs signals.

yaml

observe:
  signal: cpu_usage
  tag: inference_start
assert
Validates policy or runtime invariants.

yaml

assert:
  energy < 20J
  privacy == 'anonymized'
bind
Creates a variable from upstream output.

yaml

bind:
  as: cleaned_text
  from: TextSanitizer.output
emit
Yields final output from the workflow.

yaml

emit: final_summary
🧪 Type System
string, integer, float, boolean

array<type>, object, binary

yaml

input_schema:
  type: object
  properties:
    image:
      type: string
      format: binary
🔐 Compliance Directives
policy
yaml

policy:
  privacy: anonymized
  energy_budget: "30J/inference"
  fairness:
    weighted:
      user: 0.6
      system: 0.4
provenance
yaml

provenance:
  training_data_hash: sha256:abcd...
  training_commit: abc123...
  training_config: training/config.yaml
🔍 Metadata Blocks
yaml

author: "Alex Doe <alex@fabric.dev>"
created_at: "2025-07-22T08:00:00Z"
license: "Apache-2.0"
tags: [vision, edge, quantized]
🔧 Execution Metadata
yaml

framework: "ONNX"
parameter_count: 7000000000
signatures:
  artifact_sig: abc123...
  manifest_sig: def456...
This DSL reference evolves with each Fabric version. For changes, consult /CHANGELOG.md.


