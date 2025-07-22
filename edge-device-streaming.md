deployment-patterns/edge-device-streaming.md
Title: Real-Time Streaming from Edge Sensors into Fabric Agents

🎯 Objective
Demonstrate how to capture data from edge devices (camera/microphone), stream it to a Fabric agent over HTTP/gRPC/WebSocket, and perform live inference or processing.

🧰 Prerequisites
A camera or microphone connected to a device (e.g. Raspberry Pi, Jetson, phone, or laptop)

Python 3.8+ with opencv-python, sounddevice, websockets, or ffmpeg

Fabric agent accepting input on HTTP or WebSocket

🎥 Step 1: Capture and Stream Video
python
Copy
Edit
# capture_stream.py
import cv2
import requests

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break
    _, jpeg = cv2.imencode('.jpg', frame)
    requests.post("http://<agent-ip>:<port>/infer", files={"image": jpeg.tobytes()})
Replace <agent-ip> with your deployed agent service URL.

🎙️ Step 2: Stream Audio to Agent
python
Copy
Edit
# audio_stream.py
import sounddevice as sd
import numpy as np
import requests

def callback(indata, frames, time, status):
    audio_bytes = indata.astype(np.float32).tobytes()
    requests.post("http://<agent-ip>:<port>/infer-audio", data=audio_bytes)

stream = sd.InputStream(callback=callback)
stream.start()
Ensure your agent has a route for /infer-audio.

🤖 Step 3: Receive Stream in Agent
In your .fab module:

yaml
Copy
Edit
agent EdgeReceiver:
  input: image/jpeg
  execution:
    run: vision_model
    on_receive: save_to_tmp + run_onnx
🌍 Step 4: Remote Deployment
Package and push the agent:

bash
Copy
Edit
fab model publish models/edge-receiver/1.0.0/model.yaml
Deploy on device or central mesh.

🧪 Validation
View inference logs from agent

Check streamed results in provenance ledger

Inspect frame/audio lag (ensure <200ms for real-time)

⚠️ Notes
Consider bandwidth-limited codecs (e.g. H.264)

Use UDP/WebRTC for low-latency streaming

Deploy agents closer to edge for minimal RTT

✅ Summary
Connected physical sensors to Fabric

Enabled real-time inference pipeline

Works across private/remote edge networks
