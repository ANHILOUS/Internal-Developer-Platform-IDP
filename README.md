Internal Developer Platform (IDP) - Platform Engineering Catalyst

## 🚧 Status: In Active Development 🚧

This project is currently under active development as part of an advanced academic focus on Platform Engineering. While not yet production-ready, the core architecture is finalized, and component integration is in progress.

---

## Executive Summary

The objective of this project is to architect and implement a comprehensive **Internal Developer Platform (IDP)** based on modern "Golden Path" principles. This platform aims to slash developer onboarding time, remove infrastructure bottlenecks, and reduce cognitive load by providing a self-service interface for service scaffolding and cloud provisioning.

This implementation utilizes the **"BACK" stack** (Backstage, ArgoCD, Crossplane, and Kubernetes) to establish Kubernetes as the universal control plane for both application and infrastructure lifecycles.

## Core Problem Solved

Traditional DevOps models often suffer from ticketing bottlenecks where application developers must wait for operations teams to provision databases, storage, or secrets. This project aims to replace that manual workflow with automated, self-service governance.

## Technical Architecture (The "Golden Path")

The platform integrates several cloud-native tools into a cohesive workflow.

### Architecture Diagram

<img width="1254" height="1254" alt="image-idp" src="https://github.com/user-attachments/assets/0b3e57be-b288-464d-9490-9fda18f7d08f" />

### Component Breakdown

1.  **Platform Control Plane (Kubernetes):** The backbone hosting the entire solution. All platform components run as native Kubernetes resources.
2.  **Developer Portal (Backstage):** The "Storefront." This provides the UI/CLI for developers to discover existing services, view API documentation, and use Software Templates to scaffold new projects.
3.  **Infrastructure-as-Code (Crossplane):** The cloud abstraction layer. Instead of direct Terraform, we use Crossplane to define Composite Resources (XRDs) (e.g., `CompositePostgresInstance`). Developers submit simple Kubernetes "Claims" to provision complex cloud resources (e.g., AWS RDS) without needing cloud credentials.
4.  **GitOps & Continuous Deployment (ArgoCD):** The delivery engine. When Backstage creates a new repo, ArgoCD automatically detects and synchronizes the desired state between Git and the Kubernetes cluster, enforcing automated deployment and drift detection.

## The Developer Workflow

The engineered workflow is designed to minimize friction:

* **Step 1:** Developer requests a "New Backend Service" via a form in the Backstage portal.
* **Step 2:** Backstage scaffolds the repository (e.g., Go/Python) and commits the necessary GitOps YAML (for ArgoCD) and Infrastructure Claims (for Crossplane) to a config repo.
* **Step 3:** ArgoCD detects the change and synchronizes the environment, deploying the application and triggering Crossplane.
* **Step 4:** Crossplane provisions the requested cloud infrastructure (e.g., an RDS Database) and injects the credentials back into the application namespace as a Secret.

## Tech Stack

* **Container Orchestration:** Kubernetes
* **Developer Portal:** Backstage
* **Infrastructure Provisioning:** Crossplane
* **GitOps & CD:** ArgoCD
* **Package Management:** Helm
* **Version Control & CI:** GitHub

## Project Roadmap / Future Goals

1.  [ ] **Phase 1: Foundation (In Progress):** Deploy management cluster, establish namespaces, and install core operator stack (Helm/Crossplane).
2.  [ ] **Phase 2: Scaffolding:** Define Backstage Software Templates for a standardized Go microservice and a generic RDS database claim.
3.  [ ] **Phase 3: Integration:** Configure ArgoCD ApplicationSets to auto-deploy new services based on Git folder structure.
4.  [ ] **Phase 4: Optimization (Future):** Integrate **Prometheus/Grafana** for observability in the Backstage portal and **Kyverno** for Policy-as-Code governance.
