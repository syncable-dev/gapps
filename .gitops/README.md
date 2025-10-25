# GitOps Deployment Manifests

This directory contains declarative Kubernetes and Crossplane manifests for your application deployment.

## Structure

- **infrastructure/**: Crossplane Custom Resource Definitions (CRDs) for GCP infrastructure provisioning
  - Database instances (Cloud SQL)
  - Redis caches (Memorystore)
  - Storage buckets (Cloud Storage)
  - Pub/Sub topics and subscriptions

- **applications/**: Kubernetes manifests for application workloads
  - Deployments
  - Services
  - ConfigMaps
  - Horizontal Pod Autoscalers
  - Network Policies

## How It Works

These manifests are automatically applied to your Kubernetes cluster by ArgoCD.

1. **Infrastructure First**: Crossplane provisions GCP resources from `infrastructure/` CRDs
2. **Applications Second**: Kubernetes applies `applications/` manifests once infrastructure is ready
3. **Continuous Sync**: ArgoCD continuously monitors this directory and syncs changes automatically

## ⚠️ Important

- Do not manually edit these files unless you know what you're doing
- All changes are tracked in git history for rollback capability
- Infrastructure changes trigger GCP resource provisioning/updates
- Application changes trigger rolling updates to your services

## Managed by

Generated and managed by **Syncable Deployment Platform**
- Documentation: https://docs.syncable.dev
- Support: support@syncable.dev
