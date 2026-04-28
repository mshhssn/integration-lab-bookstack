# DB StatefulSet Decision

## Decision
The MariaDB workload is no longer modeled as a Deployment in the target architecture.
The preferred target object is now a StatefulSet.

## Reason
MariaDB is a stateful workload.
Its operational behavior depends on persistent data, stable identity and controlled lifecycle behavior.
A Deployment was acceptable for the first technical skeleton, but it is not considered the correct long-term target model.

## Scope Decision
For the current learning stage:
- StatefulSet is introduced
- the DB PVC remains a separate object
- a headless Service is not introduced yet
- detailed health probes are still postponed

## Result
The first platform target model is now closer to a realistic stateful architecture while remaining understandable and compact.