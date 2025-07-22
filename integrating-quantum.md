DSL Mastery: Integrating Quantum Modules
This tutorial shows how to embed quantum simulation and hybrid workflows using Fabric's quantum-enhanced DSL features.

1. 🧬 Defining Quantum Types
First, introduce quantum types:

fab
Copy
Edit
type Qubit
type QReg = Qubit[4]
type HybridTensor = union(RealTensor, QReg)
Use them to represent quantum states or hybrid data structures.

2. 🕹️ Quantum Agent Block
Define an agent that runs a quantum circuit in simulation:

fab
Copy
Edit
agent QuantumSampler @target(simulator) {
  id:        "uuid-quantum-1234"
  model_id:  "quantum-sampler:0.1"
  inputs:    [Params:RealTensor<4>]
  outputs:   [Counts:Map]
  quantum: {
    regs: qr[4]
    circuit:
      H(qr[0]);
      RX(qr[1], Params[1]);
      CNOT(qr[1], qr[2]);
      U3(qr[3], θ, φ, λ)
    measure: bits = MEASURE(qr)
  }
  fallback:  ClassicalApprox { state: reset }
  policy:    { error_correction: on }
}
Key components:

@target(simulator) designates execution environment.

quantum block specifies registers, gates, and measurement.

fallback ensures deterministic behavior when a real QPU is unavailable.

3. 🌐 Hybrid Workflow Composition
Combine quantum and classical agents:

fab
Copy
Edit
workflow QuantumLoop {
  plan: ParamGen -> QuantumSampler -> ClassicalOptimizer
  coordination: { consensus: true }
  feedback: { metrics: [loss], interval: "30s" }
}
This pattern supports iterative quantum-classical loops.

4. 🔧 Exporting Quantum IR
To emit OpenQASM or Quil:

bash
Copy
Edit
fab build my_quantum_module.fab --emit=qasm
fab build my_quantum_module.fab --emit=quil
Generated QASM/Quil files can target real quantum backends.

✅ Next Tutorials
Define structured I/O with schema-definitions.md

Learn agent chaining patterns → agent-chaining.md

