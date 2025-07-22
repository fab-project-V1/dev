# ⏱ Latency Tuning in Fabric

Latency is a key performance metric for deployed Fabric agents and models, particularly in real-time and edge scenarios.

---

## 🔍 Sources of Latency

| Source               | Description                                |
|----------------------|--------------------------------------------|
| Model size           | Larger models yield longer inference times |
| Token length         | Autoregressive generation scales with input size |
| Execution overhead   | Includes model loading and pre/postprocessing |
| Mesh hops            | Distributed executions may incur network delays |
| Container cold start | For dynamically provisioned agents         |

---

## 🧪 Measuring Latency

Use the built-in Fabric benchmarking module:

```bash
fab benchmark agent agent-repacker
Outputs metrics like:

mean_latency: average per-call time

p95_latency: 95th percentile latency

warmup_time: container spin-up time (if cold)

🧰 Strategies to Reduce Latency
1. Model Optimization
Use smaller architectures (e.g., distilled models)

Prune unnecessary attention layers

Export to ONNX + enable inference providers (e.g., TensorRT)

2. Token Efficiency
Use stop tokens or max_tokens to bound generation

Limit prompt size via token filters

3. Runtime Controls
Enable caching for repeated calls

Co-locate mesh agents to reduce network latency

Pin models in RAM using warm_start: true

🧬 Latency Budgeting in model.yaml
Define latency expectations in your manifest:

yaml

performance:
  metrics:
    - name: latency
      value: 80
      dataset: internal-benchmark
policy:
  energy_budget: "15J/per_call"
The value is interpreted in milliseconds.

📉 Tradeoffs
Reducing latency may:

Lower model accuracy (if pruning or quantizing)

Increase energy draw (for pinned or accelerated inference)

Require mesh resource reservations

Balance against your SLA and energy/fairness constraints.

🛠 Tools
Tool	Purpose
fab benchmark	Profile deployed agents or models
fab optimize	Apply pruning, distillation, ONNX
Fabric mesh UI	Visualize agent call latency
