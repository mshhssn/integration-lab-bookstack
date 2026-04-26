# Platform Mapping

## Current Stack
- bookstack-app
- bookstack-db
- bookstack-proxy
- app volume
- db volume
- .env runtime configuration
- nginx proxy configuration
- external access via localhost:8080

## Mapping Table

| Compose Component | Function | Future Platform Object | Reason | Open Questions |
|---|---|---|---|---|
| bookstack-app | application workload | Deployment + Service | main application runtime | how much persistence is really needed? |
| bookstack-db | database | StatefulSet + PVC | stateful data component | cluster DB or later externalized? |
| bookstack-proxy | entry point / reverse proxy | Deployment + Service or later Ingress/Route replacement | external access and routing | keep proxy or replace with ingress? |
| app volume | uploads/config/runtime persistence | PVC | persistent app-side data | which contents are truly persistent? |
| db volume | database persistence | PVC | durable data storage | backup/restore later in platform context |
| .env | mixed runtime configuration | ConfigMap + Secret | must be separated by sensitivity | which values belong where? |
| nginx config | proxy configuration | ConfigMap | externalized configuration | how much proxy logic remains later? |
| port 8080 | external exposure | Service + Ingress/Route | platform-native exposure model | ingress or route in target platform? |

## State Classification
- bookstack-app: partially stateful
- bookstack-db: stateful
- bookstack-proxy: stateless
- app volume: persistent storage
- db volume: persistent storage
- .env: mixed config + secrets

## Open Architecture Questions
1. Does the future platform need a dedicated reverse proxy container?
2. Which files in the app volume are truly persistent and business-relevant?
3. Should the database run inside the cluster or be external later?
4. Which runtime values belong into ConfigMap and which into Secret?
5. What would a meaningful application-level health check look like?

## Minimal Target State

| Component | Needed on target platform? | Target Object | Priority | Reason |
|---|---|---|---|---|
| BookStack application | yes | Deployment | required | main application workload |
| App internal access | yes | Service | required | stable service discovery inside platform |
| MariaDB database | yes | Stateful workload | required | persistent stateful data component |
| DB persistence | yes | PVC | required | data must survive workload restarts |
| App persistence | maybe | PVC | optional | depends on required uploads/config persistence |
| Runtime config (non-secret) | yes | ConfigMap | required | separate operational configuration |
| Runtime config (secret) | yes | Secret | required | protect passwords and keys |
| External access | yes | Ingress or Route | required | platform-native exposure instead of host port |
| Dedicated reverse proxy | maybe | Deployment + Service | optional | only if ingress/route is not sufficient |
| Health checks | yes | readiness/liveness probes | later | needed for more robust platform operation |
| Monitoring integration | yes | platform/tool integration | later | useful but not part of first minimal rollout |

Dedicated reverse proxy on target platform: optional.
Reason: The local reverse proxy is useful for learning external/internal separation and routing, but on a target platform this responsibility can often be handled by Ingress or Route.