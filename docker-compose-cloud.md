deployment-patterns/docker-compose-cloud.md
Guide: Running a Fabric Mesh in Docker Compose

✅ Overview
Use Docker Compose to simulate a Fabric runtime including UDAP registry, Agent-VM enclaves, and the provenance ledger—ideal for sandbox testing or CI environments.

🧱 Prerequisites
Docker & Docker Compose installed (v1.29+)

Fabric CLI (fab) built locally

.fab module (e.g., AssistiveVision.fab)

Sample model present: models/edge-vision-v2/1.0.0/model.yaml + weights

🛠️ 1. Project Layout
bash
Copy
Edit
fabric-mesh/
├── docker-compose.yml
├── AssistiveVision.fab
├── models/
│   └── edge-vision-v2/1.0.0/
│       ├── model.yaml
│       └── weights.onnx
└── .env
📝 2. docker-compose.yml
yaml
Copy
Edit
version: "3.8"
services:
  registry:
    image: fab/udap-registry:latest
    ports: ["5000:5000"]
    volumes: ["./models:/models"]

  ledger:
    image: fab/provenance-ledger:latest
    ports: ["6000:6000"]

  agent1:
    image: fab/agent-vm:latest
    depends_on: ["registry", "ledger"]
    environment:
      UDAP_REGISTRY: http://registry:5000
      LEDGER_ENDPOINT: http://ledger:6000
    volumes:
      - ./models:/models
    command: ["fab", "deploy", "--module", "/models/edge-vision-v2/AssistiveVision.fab", "--agent", "VisionAS"]

  agent2:
    image: fab/agent-vm:latest
    depends_on: ["registry", "ledger"]
    environment:
      UDAP_REGISTRY: http://registry:5000
      LEDGER_ENDPOINT: http://ledger:6000
    volumes:
      - ./models:/models
    command: ["fab", "deploy", "--module", "/models/edge-vision-v2/AssistiveVision.fab", "--agent", "Narrator"]
🚀 3. Start the Mesh
bash
Copy
Edit
docker-compose up --build
registry: listens on port 5000

ledger: listens on port 6000

agent1/agent2: deploy Fabric agents within enclaves, register to UDAP, connect to ledger

🔍 4. Interact with Agents
Use CLI or API to:

bash
Copy
Edit
fab monitor --endpoint http://registry:5000
Monitor bid/offer activity

Check provenance entries in the ledger logs

🧪 5. Run Inference
bash
Copy
Edit
fab invoke --agent VisionAS --input examples/sample.jpg
fab invoke --agent Narrator --input '{"detections": [...]}'
Results are logged, and each executionBlock is recorded with block type, timestamp, and content hashes.

🔧 6. Cleanup
bash
Copy
Edit
docker-compose down --volumes
✅ Summary
Spins up all major Fabric runtime components

Enables full lifecycle testing (compile → deploy → invoke)

Replicates on-prem/cloud edge environment in a lightweight containerized setup
