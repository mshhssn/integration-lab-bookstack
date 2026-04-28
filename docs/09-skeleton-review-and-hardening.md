# Skeleton Review and Hardening

## Review Summary
The initial platform skeleton is considered valid as a first technical target model.
It already separates workloads, services, storage, configuration, secrets and external exposure in a clean way.

## What Is Already Good
- namespace is defined
- config and secret are separated
- application and database are modeled separately
- internal services exist for app and db
- persistence is modeled with PVCs
- external exposure is modeled via ingress
- image references are pinned by digest
- object naming and labels are consistent

## Known Simplifications
- MariaDB is currently modeled as a Deployment
- no readiness/liveness probes are defined
- no resource requests/limits are defined
- no securityContext is defined
- no storage class is defined
- no TLS handling is modeled
- no route alternative is modeled yet
- app persistence is still broad and not yet refined

## Hardening Decisions
- MariaDB should be treated as a stateful workload in the next maturity step
- readiness and liveness behavior should be introduced next
- resource requests and limits should be added later
- app persistence should be reviewed and narrowed where possible
- ingress remains the neutral external exposure model
- an OpenShift route variant can be added later
- the dedicated reverse proxy remains excluded from the first platform target model
- MariaDB is no longer treated as a long-term Deployment target.
- The target design for MariaDB is now a StatefulSet.
- For the current learning stage, the DB PVC remains a separate object instead of using volumeClaimTemplates.
- A headless Service is not introduced yet because the first target model focuses on clear internal connectivity for the application.

## Next Maturity Focus
1. convert DB design direction from Deployment to StatefulSet
2. introduce readiness/liveness thinking
3. add basic resource requests and limits
4. review app-side persistence
5. prepare ingress-to-route comparison for OpenShift