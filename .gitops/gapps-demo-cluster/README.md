# GitOps Deployment Manifests - gapps-demo-cluster

This directory contains declarative Kubernetes and Crossplane manifests for cluster `gapps-demo-cluster`.

## Structure

```
gapps-demo-cluster/
├── infrastructure/           # Cluster-wide Crossplane CRDs
│   ├── artifact-registry.yaml
│   └── storage-bucket.yaml
├── dev/                      # Development environment
│   ├── applications/         # Application Kubernetes manifests
│   ├── databases/            # Database CRDs (Cloud SQL)
│   └── redis/                # Redis CRDs (Memorystore)
├── staging/                  # Staging environment
│   └── ...
└── prod/                     # Production environment
    └── ...
```

## Resource Types

### Infrastructure (cluster-wide)
- **Artifact Registry**: Container image registry
- **Storage Buckets**: Cloud Storage buckets

### Per-Environment Resources
- **Applications**: Deployments, Services, ConfigMaps, HPA, Network Policies
- **Databases**: Cloud SQL instances (PostgreSQL, MySQL)
- **Redis**: Memorystore instances

## How It Works

These manifests are automatically applied to your Kubernetes cluster by ArgoCD.

1. **Infrastructure First**: Crossplane provisions GCP resources from `infrastructure/` CRDs
2. **Environment Resources**: Database/Redis CRDs are applied per environment
3. **Applications**: Kubernetes manifests are applied once infrastructure is ready
4. **Continuous Sync**: ArgoCD monitors and syncs changes automatically

## Namespaces

| Resource Type | Namespace |
|--------------|-----------|
| Infrastructure | `crossplane-resources` |
| Applications | `{env}` (dev, staging, prod) |
| Databases | `{env}-database` |
| Redis | `{env}-redis` |

## Managed by

Generated and managed by **Syncable Deployment Platform**
- Documentation: https://docs.syncable.dev
- Support: support@syncable.dev
