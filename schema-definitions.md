DSL Mastery: Schema Definitions for Agents
Structured schemas define the shape, type, and semantics of inputs and outputs across Fabric agents. This tutorial walks through declaring, importing, and enforcing typed schemas in Fabric DSL.

1. 📦 Declaring a Custom Schema
Use record to define a reusable input/output structure:

fab
Copy
Edit
record VisionInput {
  image: ImageTensor
  timestamp: DateTime
  location: optional<GeoPoint>
}
Supports basic types: Int, Float, String, Bool

Composite types: List, Map, Tuple, optional<>

Multimedia types: ImageTensor, AudioTensor, VideoTensor, TextTokenStream

2. 🔄 Using Schemas in Agents
Reference records directly in agent inputs/outputs:

fab
Copy
Edit
agent EdgeVision @target(cuda) {
  id:        "agent-edge-vision"
  model_id:  "edge-vision-v2:1.1.0"
  inputs:    [frame: VisionInput]
  outputs:   [detections: List<BoundingBox>]
  postprocess: { normalize: true }
}
Define associated types:

fab
Copy
Edit
record BoundingBox {
  label: String
  confidence: Float
  box: Tuple<Float, Float, Float, Float>
}
3. 📁 External Schema Imports
Schemas can be shared across modules:

fab
Copy
Edit
import schema "common/schemas/vision-types.fab"
This promotes modularity and reuse.

4. ✅ Validation & Enforcement
When compiled:

Input/output schema mismatches are caught statically

Validation ensures schema compatibility between chained agents

optional<> and defaults help support graceful degradation

✅ Related Concepts
agent-chaining.md: See schema alignment in chained workflows

using-blocks.md: Declare schema-constrained control blocks

