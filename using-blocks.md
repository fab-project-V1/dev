DSL Mastery: Using Blocks — Control, Execution & Agent Definitions
This tutorial dives into the core Fabric DSL constructs—agent, executionBlock, and control structures—showing you how to compose advanced workflows with clarity and precision.

1. 🧠 Defining Agents
Agents represent model-backed actors in your Fabric mesh.

fab
Copy
Edit
agent FaceRecognizer {
  id:       "uuid-1234-...-abcd"
  model_id: "face-rec-v1:1.0.0"
  inputs:   [CameraFrame@AnyEdge]
  outputs:  [FaceMetadata]
  learns:   none
  explain:  ["trace"]
  device:   any
  policy:   { privacy: anonymized }
}
Key fields:

id and model_id – unique IDs, reference model version.

inputs/outputs – typed channels bound to streams or schemas.

Optional properties: learning mode, explanations, device targeting, privacy policy.

2. 🧩 Creating Execution Blocks
Execution blocks concretize agent behavior in the runtime pipeline.

fab
Copy
Edit
executionBlock FaceDetect {
  id:         "uuid-2345-...-bcde"
  model_id:   "face-rec-v1:1.0.0"
  created_by: "dev@fab"
  timestamp:  "2025-07-20T12:00:00Z"
  policy:     { privacy: anonymized }
  block: {
    type:    inference
    agent:   FaceRecognizer
    entry:   "detectFaces"
    inputs:  [CameraFrame@AnyEdge]
    outputs: [FaceMetadata]
  }
}
block.type indicates operation (e.g., inference, preprocess).

agent and entry specify which code path to run.

Inputs/outputs must match the agent's definition.

3. 🔄 Control Structures
Use imperative constructs inside blocks or workflows.

If / Else:

fab
Copy
Edit
if (FaceMetadata.confidence < 0.5) {
  emit Warning("Low confidence detected")
} else {
  emit Log("High confidence event", FaceMetadata)
}
Looping:

fab
Copy
Edit
for frame in CameraStream {
  let faces = FaceRecognizer.infer(frame)
  emit FrameResults(frame.id, faces.count)
}
Emit Statements:

emit EventName(payload)

Can be used to hook into workflows, audits, or external systems.

4. 🛠 Putting It All Together: A Mini Workflow
fab
Copy
Edit
module FaceModule {
  import core, multimodal

  device AnyEdge { caps: [CPU:4core], policy: { privacy: anonymized } }

  agent FaceRecognizer { ... }

  executionBlock FaceDetect { ... }

  workflow FacePipeline {
    plan: FaceRecognizer -> FaceDetect
    feedback: { metrics: [FaceMetadata.count], interval: "5s" }
  }

  auditTrail FacePipeline {
    snapshotOn: ["planStart", "planCommit", "planFinish"]
    store: ProvenanceLedger
  }
}
This complete example:

Declares a device filter.

Defines an agent and its execution block.

Constructs a workflow plan connecting them.

Configures feedback and auditing to enforce repeatability and traceability.

✅ Next Steps
Deep dive into conditional logic and loop patterns: see [conditional-logic.md].

Want to combine classical and quantum agents? Check out [integrating-quantum.md].

Define your own input/output structures? See [schema-definitions.md].

