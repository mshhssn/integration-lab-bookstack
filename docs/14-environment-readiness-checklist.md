# Environment Readiness Checklist

## Scope
Checklist to verify whether a target platform environment is ready to receive and operate the delivered BookStack deployment package.

| Area | Check Item | Required? | Status | Ownership | Notes / Action |
|---|---|---|---|---|---|
| platform base | target namespace / project exists | yes | open | platform team / integration | create dedicated namespace/project |
| platform base | naming conventions are aligned | yes | open | integration | confirm object naming and environment naming |
| image access | all required images are reachable from target platform | yes | open | platform team | verify registry reachability and pull access |
| image access | digest-based image references are accepted | yes | open | platform team / operations | confirm deployment policy for pinned images |
| configuration | all non-secret runtime values are known | yes | open | integration / app provider | finalize operational config values |
| secrets | all required secrets are available | yes | open | app provider / operations / security | confirm provisioning and ownership |
| secrets | secret rotation responsibility is defined | no | open | operations / security | clarify later operational ownership |
| storage | persistent storage for database is available | yes | open | platform team / storage team | confirm storage class and quota |
| storage | app-side persistent storage is available if required | yes | open | platform team / integration | validate whether app persistence remains needed |
| storage | PVC sizing is aligned with platform expectations | yes | open | integration / platform team | review requested storage sizes |
| networking | internal service-to-service communication is allowed | yes | open | platform team | app must reach db internally |
| networking | external exposure model is defined (ingress or route) | yes | open | platform team / integration | confirm target exposure method |
| networking | hostname / DNS is defined | yes | open | platform team / operations | confirm target application URL |
| networking | TLS responsibility is defined | no | open | platform team / operations | clarify certificate handling |
| operations | log access path is known | yes | open | operations | define where app/db/exposure logs are reviewed |
| operations | smoke test is defined | yes | open | integration / operations | define minimum post-deployment checks |
| operations | readiness expectations are defined | yes | open | integration / operations | confirm traffic admission expectations |
| operations | rollback approach is known | yes | open | operations / integration | define revert path for failed rollout |
| governance | deployment ownership is defined | yes | open | integration / operations | who executes rollout? |
| governance | incident ownership is defined | yes | open | operations / app provider / platform team | who handles failures in which layer? |
| governance | delivery format is agreed | yes | open | app provider / integration | manifests, chart, template, other |