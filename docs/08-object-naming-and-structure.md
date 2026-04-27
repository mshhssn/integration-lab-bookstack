# Object Naming and Structure

## Namespace
- bookstack-lab

## Core Objects

| Object Type | Name | Purpose |
|---|---|---|
| Namespace | bookstack-lab | logical isolation of the lab environment |
| Deployment | bookstack-app | application workload |
| Service | bookstack-app | internal application access |
| Stateful workload | bookstack-db | database workload |
| Service | bookstack-db | internal database access |
| PVC | bookstack-app-data | persistent app-side storage |
| PVC | bookstack-db-data | persistent database storage |
| ConfigMap | bookstack-config | non-secret runtime configuration |
| Secret | bookstack-secret | credentials and sensitive values |
| Ingress / Route | bookstack-web | external access entry point |

## Label Strategy

### Shared Base Labels
- app.kubernetes.io/name=bookstack
- app.kubernetes.io/part-of=bookstack-lab
- app.kubernetes.io/managed-by=manual-lab
- app.kubernetes.io/environment=lab

### Component Labels
- app.kubernetes.io/component=app
- app.kubernetes.io/component=db
- app.kubernetes.io/component=web

## Dependency View
- bookstack-web -> bookstack-app Service
- bookstack-app -> bookstack-config
- bookstack-app -> bookstack-secret
- bookstack-app -> bookstack-app-data
- bookstack-app -> bookstack-db Service
- bookstack-db -> bookstack-secret
- bookstack-db -> bookstack-db-data

## Proposed Directory Structure
```text
k8s/
├── namespace/
├── config/
├── storage/
├── workloads/
├── services/
└── exposure/