deployment-patterns/k8s-mesh-rollout.md
Title: Deploying Fabric Mesh on Kubernetes

🧭 Objective
Set up a production-grade Fabric mesh on Kubernetes using kubectl, optional Helm charts, and a UDAP service mesh registry.

📦 Prerequisites
Kubernetes cluster (minikube, Kind, GKE, etc.)

kubectl CLI installed

Optional: Helm 3.x

Fabric agents packaged as Docker images

A registry.yaml and provenance-ledger.yaml deployment file

🗂️ Directory Layout
Copy
Edit
k8s/
├── udap-registry-deployment.yaml
├── provenance-ledger-deployment.yaml
├── agent-visionas-deployment.yaml
├── agent-narrator-deployment.yaml
├── services/
│   ├── registry-service.yaml
│   ├── ledger-service.yaml
│   └── agents-service.yaml
🔧 Step 1: Deploy Core Fabric Services
bash
Copy
Edit
kubectl apply -f k8s/udap-registry-deployment.yaml
kubectl apply -f k8s/provenance-ledger-deployment.yaml
kubectl apply -f k8s/services/
Check pods:

bash
Copy
Edit
kubectl get pods
🛠️ Step 2: Define and Deploy Agents
Each agent gets its own deployment:

bash
Copy
Edit
kubectl apply -f k8s/agent-visionas-deployment.yaml
kubectl apply -f k8s/agent-narrator-deployment.yaml
Each deployment connects via environment variables to UDAP and LEDGER.

Example snippet:

yaml
Copy
Edit
env:
  - name: UDAP_REGISTRY
    value: http://registry:5000
  - name: LEDGER_ENDPOINT
    value: http://ledger:6000
🧪 Step 3: Invoke Agents Remotely
Once agents are exposed via LoadBalancer or NodePort, invoke with:

bash
Copy
Edit
fab invoke --agent VisionAS --input sample.jpg
Use internal DNS or service endpoints like http://visionas.default.svc.cluster.local.

📈 Step 4: Monitor Mesh
Enable Prometheus, Grafana, or Kiali:

bash
Copy
Edit
kubectl apply -f monitoring/fabric-prometheus.yaml
Observe:

Agent bids/offers

Resource usage

Provenance logs

🧹 Cleanup
bash
Copy
Edit
kubectl delete -f k8s/
✅ Summary
Leverages native Kubernetes primitives

Supports auto-scaling and service discovery

Ideal for high-availability production topologies

