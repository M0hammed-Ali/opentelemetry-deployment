# 🌌 OpenTelemetry Astronomy Shop — Microservices Demo with CI/CD and GitOps

This repository contains a fork of the **OpenTelemetry Astronomy Shop**, a distributed, microservices-based application built to demonstrate observability using OpenTelemetry. We’ve extended the original system by adding:

- ✅ Kubernetes deployment configurations
- ⚙️ CI/CD automation with GitHub Actions
- 🚀 GitOps deployment using ArgoCD

---

## 🎯 Project Goals

1. **Showcase Real-World Observability**  
   Demonstrates OpenTelemetry instrumentation across a realistic multi-service system.

2. **Enable Tooling Integration**  
   Provides a testbed for vendors and tool authors to showcase OpenTelemetry integrations.

3. **Support OpenTelemetry Testing**  
   Acts as a living system for contributors to validate and evolve OpenTelemetry APIs and SDKs.

4. **Production-Style Deployment Pipeline**  
   Adds Kubernetes-native deployment using GitHub Actions + ArgoCD, simulating modern delivery pipelines.

---

## 🧱 Architecture Overview

This project is built on a microservice architecture, including:

- Product Catalog
- Checkout Service
- Recommendation Engine
- Frontend UI
- Ad Service
- Cart Service
- Email, Payment, and Shipping Services

All services are instrumented with **OpenTelemetry** and communicate over gRPC or HTTP.

---

## 🚀 Deployment

### 🔧 Prerequisites

- Kubernetes Cluster (local via Minikube or cloud)
- `kubectl` and `kustomize` installed
- ArgoCD (for GitOps deployment)
- GitHub Actions enabled on your fork

### 📦 Step 1: CI with GitHub Actions

Push code or config changes to any branch and GitHub Actions will:
- Lint YAML and code
- Build and push Docker images
- Update Kubernetes manifests (optional)
- Trigger ArgoCD sync (if configured)

CI workflows are defined in `.github/workflows/`.

### 📦 Step 2: GitOps Deployment with ArgoCD

Set up ArgoCD to track the Kubernetes manifests in the `/k8s/` directory of this repo.

Example ArgoCD `Application` manifest:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: astronomy-shop
  namespace: argocd
spec:
  source:
    repoURL: https://github.com/<your-username>/otel-astronomy-shop
    path: k8s
    targetRevision: main
  destination:
    server: https://kubernetes.default.svc
    namespace: astronomy
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
