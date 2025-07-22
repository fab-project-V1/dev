# ⚛️ Quantum Modules in Fabric

Fabric supports hybrid classical-quantum execution by embedding quantum kernels as first-class modules. These are executed via quantum simulators or real QPUs using Fabric's Quantum Runtime.

---

## 🧬 What is a Quantum Module?

A `quantum` block in Fabric defines:

- A register layout
- A quantum circuit (QASM/QIR/Quil)
- Measurement outputs
- Optional classical post-processing

---

## ✨ Example: Bell State Circuit

```fab
quantum BellExperiment:
  qubits: 2
  outputs: { result: array<boolean, 2> }

  circuit:
    h 0
    cx 0 1
    measure 0 -> 0
    measure 1 -> 1
This declares a 2-qubit quantum experiment producing a 2-bit output.

🔗 Classical Integration
Quantum modules can be invoked from agents:

fab

agent EntangleAndClassify:
  input: {}
  output: { category: string }

  run:
    let q = BellExperiment.run({})
    return ResultClassifier.run({ bits: q.result })
🛠️ Supported Backends
Qiskit (via QASM)

Rigetti/QCS (via Quil)

IonQ and Braket

Fabric Quantum Simulator (FQS)

Set backend via Fabric deployment config or runtime policy.

📜 Circuit Formats
Fabric supports multiple intermediate representations:

.qasm (OpenQASM)

.quil (Rigetti Quil)

.qir.mlir (Microsoft QIR dialect)

.qmod.fab (Native Fabric DSL block)

Conversion between formats is handled by the Fabric Compiler.

🔐 Provenance + Verification
Quantum executions include:

Input/output bitstring hashes

Device metadata

Circuit checksum (SHA256)

Quantum signature (if applicable)

🔄 Hybrid Quantum-Classical Chains
Quantum modules can be chained in agent logic:

fab

run:
  let bits = QKernel.run({}).result
  return Decoder.run({ bits })
🔬 Debugging & Simulation
Run quantum modules locally via:

bash

fab simulate QuantumModule.fab
This will use the local simulator and output measurement histograms.

🛤️ Next Steps
See training.md for integrating quantum models into pipelines

Visit governance.md for certifying quantum workloads


