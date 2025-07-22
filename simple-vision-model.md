Simple Vision Model
This tutorial demonstrates how to integrate an ONNX-based image classifier into a Fabric agent. We'll use a pre-trained MobileNet model and wrap it in a .fab module.

🧠 What You’ll Learn
Downloading and using ONNX models

Writing an image classification Fabric agent

Running inference on sample images

🧰 Prerequisites
Fabric CLI installed (pip install fab-cli)

Docker (for ONNX runtime sandbox)

Python 3.x

Image file (e.g., cat.jpg)

1️⃣ Create Project Directory
bash
Copy
Edit
mkdir simple-vision-model
cd simple-vision-model
fab init
2️⃣ Download Pre-trained ONNX Model
bash
Copy
Edit
mkdir model
wget https://github.com/onnx/models/raw/main/vision/classification/mobilenet/model/mobilenetv2-7.onnx -O model/mobilenetv2.onnx
3️⃣ Define the Fabric Agent
Edit project.fab:

fab
Copy
Edit
agent ImageClassifier {
  input: image
  output: string

  weights: "model/mobilenetv2.onnx"

  run {
    let probs = infer(image)
    let label = argmax(probs)
    return label
  }
}
4️⃣ Compile the Agent
bash
Copy
Edit
fab build
You should see ✔ Build succeeded.

5️⃣ Run Inference
bash
Copy
Edit
fab run ImageClassifier --input "@cat.jpg"
Output should be something like:

json
Copy
Edit
"tabby cat"
🧪 Tip: Swap Models
You can replace the ONNX file with any compatible model. Update the weights: path and ensure input format matches.

🧩 Summary
You've created a vision model agent using ONNX in Fabric, suitable for image classification and extensible to edge or web deployment.

