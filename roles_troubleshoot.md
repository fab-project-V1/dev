Persona-Based Troubleshooting Guide
Fabric supports multiple roles in the AI system lifecycle. This guide maps common issues and diagnostics by persona to streamline debugging and resolution.

👨‍💻 Developer
Scope: Model design, agent logic, .fab syntax, DSL integration.

Issue	Symptoms	Actions
DSL syntax error	fab compile fails	Run fab lint, check line/column in error output
Agent not producing output	Silent inference or null return	Use fab test, enable --debug, inspect execution block logs
Import resolution	Unknown module error	Verify relative imports and module path casing

⚙️ Operator
Scope: Deployment, runtime orchestration, container integrity, hardware allocation.

Issue	Symptoms	Actions
Container crash	Agent VM not spawning	Run docker logs <container>, check Dockerfile consistency
GPU not utilized	Inference slow, CPU bound	Validate runtime spec includes gpu: true, monitor nvidia-smi
Agent unreachable	404 or timeout	Check UDAP registry, firewall, fab ps for live agents

🔌 Integrator
Scope: External APIs, SDK hooks, ROS/K8s bridging.

Issue	Symptoms	Actions
Webhook failure	No response, HTTP 500	Enable HTTP logs in fab-daemon, test manually with curl
ROS agent not publishing	Empty /agent_topic	Confirm topic subscription in .fab, run rostopic echo
ONNX export mismatch	Inference results differ	Recheck opset version, use onnxruntime.InferenceSession(..., providers=...)

🔒 Compliance Lead
Scope: Policy enforcement, data lineage, audit trail.

Issue	Symptoms	Actions
Provenance error	"Missing commit hash"	Check training_commit in model.yaml, validate registry tag
Privacy violation flagged	PII detected	Ensure anonymization pipeline in preprocess.py and config
Signature mismatch	Registry rejects model	Re-sign with fab sign --private-key, confirm key matches signed_by field
