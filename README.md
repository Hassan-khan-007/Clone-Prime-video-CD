# ⚙️ Prime Video Clone - GitOps CD Repository

This repository functions as the **Single Source of Truth (SSOT)** for continuous delivery. It contains pure Kubernetes deployment manifests that are automatically synchronized to a local **Kind** (Kubernetes in Docker) cluster using **Argo CD**.

---

## 🎯 Architecture & Workflow (CD Phase)
1. **Decoupled Configuration:** Unlike traditional setups, application source code is strictly separated from deployment configurations.
2. **Automated CI Handshake:** Upon a successful build and security scan in the CI repository, Jenkins automatically clones this CD repository, updates the image tag inside `manifests/deployment.yaml` using `sed`, and pushes the commit back.
3. **GitOps Reconciliation:** **Argo CD** (running in the `argocd` namespace of the Kind cluster) polls or receives webhooks from this repository, automatically pulling the fresh image from Docker Hub and deploying it to the local cluster with zero manual intervention.

---

## 📁 Repository Structure
```text
.
└── manifests/
    ├── deployment.yaml   # Kubernetes Deployment (Image tag dynamically updated by CI)
    └── service.yaml      # Kubernetes Service (Exposes application on port 3000)
