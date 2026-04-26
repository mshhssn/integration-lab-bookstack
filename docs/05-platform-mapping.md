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
