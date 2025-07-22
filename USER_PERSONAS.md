This document outlines key user personas for the Fabric ecosystem. These profiles guide documentation, UX design, CLI affordances, and platform feature prioritization.

🧑‍💻 Developer
Description
Builds Fabric models, agents, workflows using the DSL and CLI.

Goals
Write .fab modules for audio, vision, or quantum tasks.

Test and debug locally.

Push compliant models to the registry.

Tools Used
fab-cli, VS Code extension, Docker, ONNX, Git

Needs
Robust DSL reference

End-to-end examples

Easy local dev + test

Performance tuning guides

🧑‍🔧 Operator
Description
Deploys and manages Fabric applications across environments.

Goals
Install and monitor runtime components.

Tune scheduler, ledger, and policy kernel.

Apply security, observability, and rollback strategies.

Tools Used
K8s, Helm, fab deploy, Grafana, Prometheus

Needs
System architecture diagrams

Deployment recipes (edge/cloud/local)

Logs, metrics, and alerting integration

🤝 Integrator
Description
Connects Fabric agents into external systems or legacy stacks.

Goals
Wrap Fabric output into REST, ROS, or gRPC

Ensure schema compatibility

Automate packaging and CI/CD

Tools Used
ROS, GitHub Actions, Docker Compose, Fabric Plugin SDK

Needs
SDK usage patterns

External integration examples

CI-compatible packaging and testing flows

