# Minimal Platform Target

## Goal
Define the first minimal platform-oriented target model for the current BookStack stack without writing full platform manifests yet.

## Minimal Required Objects

| Object | Component | Required? | Reason |
|---|---|---|---|
| Deployment | BookStack application | yes | main application workload |
| Service | BookStack application | yes | stable internal access |
| Stateful workload | MariaDB | yes | stateful data component |
| Service | MariaDB | yes | stable internal database access |
| PVC | MariaDB | yes | persistent database storage |
| PVC | BookStack app | yes for current lab model | app-side persistent files/uploads/config currently exist |
| ConfigMap | BookStack runtime config | yes | non-secret operational configuration |
| Secret | App and DB credentials | yes | passwords and keys must be separated |
| Ingress / Route | External exposure | yes | platform-native external access |
| Dedicated reverse proxy | optional | no for first target model | local learning component, not required in first platform design |

## Initial Target Architecture
- External traffic enters through Ingress or Route.
- Traffic is forwarded to the BookStack application Service.
- The BookStack application runs as a Deployment.
- The application reads non-secret configuration from ConfigMap.
- The application reads secret values from Secret.
- The application connects internally to MariaDB through a DB Service.
- MariaDB runs as a stateful workload with persistent storage.
- App-side persistence remains included in the first target model because the current lab uses persistent app data.

## Deliberately Excluded for Now
- detailed probes
- monitoring integration
- autoscaling
- network policies
- TLS details
- backup/restore platform design
- CI/CD rollout logic
- Terraform integration

## Initial Design Decision
For the first platform target model, the dedicated nginx reverse proxy is not included.
Reason: External exposure and routing should first be modeled in a platform-native way via Ingress or Route.