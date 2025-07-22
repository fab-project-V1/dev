DSL Mastery: Agent Chaining in Fabric Workflows
Agent chaining connects multiple Fabric agents together so that outputs from one become inputs to another. This is essential for building modular, scalable workflows.

1. 🔗 Basic Chain with Compatible Schemas
fab
Copy
Edit
agent ImagePreprocessor {
  outputs: [clean_image: ImageTensor]
  ...
}

agent ObjectDetector {
  inputs: [image: ImageTensor]
  outputs: [detections: List<BoundingBox>]
  ...
}

workflow VisionFlow {
  step preprocess: ImagePreprocessor
  step detect: ObjectDetector <- preprocess.clean_image
}
Fabric ensures type compatibility across chained outputs and inputs at compile time.

2. 🧱 Using Intermediate Variables
Chain with variable captures to reference or inspect data:

fab
Copy
Edit
workflow ExtendedVision {
  step pre: ImagePreprocessor
  let img = pre.clean_image

  step detect: ObjectDetector <- img
}
3. 🔁 Chain Multiple Agents with Transformations
Use transformation agents or logic blocks in between:

fab
Copy
Edit
agent NMS {
  inputs: [raw_detections: List<BoundingBox>]
  outputs: [filtered: List<BoundingBox>]
  ...
}

workflow ChainedFlow {
  step detect: ObjectDetector
  step refine: NMS <- detect.detections
}
4. 🧩 Chaining Across Modalities
Fabric supports multimodal workflows:

fab
Copy
Edit
agent AudioEncoder {
  outputs: [features: FloatTensor]
}

agent MultimodalFusion {
  inputs: [image_feats: FloatTensor, audio_feats: FloatTensor]
  ...
}
🔍 Tips for Debugging Chains
Use fab validate to trace type mismatches

Use let to log intermediate data during test runs

Make use of optional fields and fallbacks for resilience

