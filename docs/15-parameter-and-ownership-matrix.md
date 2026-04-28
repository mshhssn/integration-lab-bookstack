# Parameter and Ownership Matrix

## Scope
Matrix for required parameters, platform prerequisites and ownership responsibilities for integrating the delivered BookStack deployment package.

| Parameter / Artifact | Description | Required? | Category | Supplier | Reviewer / Approver | Target Object / Location | Blocks Deployment if Missing? | Notes |
|---|---|---|---|---|---|---|---|---|
| BOOKSTACK_APP_URL | external application URL | yes | configuration | integration + platform | integration / operations | ConfigMap | yes | must match target ingress/route and DNS |
| TZ | timezone setting | yes | configuration | integration | integration | ConfigMap | no | normal runtime parameter |
| BOOKSTACK_DB_HOST | internal DB service endpoint | yes | configuration | integration / platform design | integration | ConfigMap | yes | should point to internal db service |
| BOOKSTACK_DB_PORT | DB port | yes | configuration | integration | integration | ConfigMap | yes | expected 3306 unless target differs |
| BOOKSTACK_DB_NAME | logical DB name | yes | configuration | app provider / integration | integration | ConfigMap | yes | runtime expectation of the app |
| BOOKSTACK_DB_USER | DB username | yes | configuration | app provider / db owner | integration / operations | ConfigMap or Secret policy-dependent | yes | currently treated as normal config |
| BOOKSTACK_APP_KEY | application key | yes | secret | app provider / operations | operations / security | Secret | yes | security-relevant |
| BOOKSTACK_DB_PASSWORD | application DB password | yes | secret | db owner / operations | operations / security | Secret | yes | app cannot connect without it |
| MARIADB_ROOT_PASSWORD | privileged DB credential | yes | secret | db owner / operations | operations / security | Secret | yes | sensitive admin credential |
| image digests | exact runtime artifacts | yes | platform prerequisite | app provider / package provider | integration / operations | deployment descriptors | yes | pinned runtime references |
| namespace/project | logical target environment | yes | platform prerequisite | platform team | integration / operations | platform object | yes | required before rollout |
| storage class / PVC support | persistent storage capability | yes | platform prerequisite | platform team | integration / operations | platform storage layer | yes | db persistence is mandatory |
| ingress/route model | external exposure method | yes | platform prerequisite | platform team | integration / operations | ingress/route object | yes | target exposure must be known |
| DNS / hostname | external name resolution | yes | platform prerequisite | platform team / operations | integration | DNS / route / ingress | yes | must align with app URL |
| image pull access | registry reachability and permissions | yes | platform prerequisite | platform team | operations / integration | cluster/runtime config | yes | rollout blocked if images cannot be pulled |
| smoke test definition | minimal post-rollout validation | yes | operations definition | integration / operations | operations | operations runbook / checklist | yes | needed for controlled handover |
| rollback approach | revert path for failed rollout | yes | operations definition | operations / integration | operations | runbook / deployment procedure | yes | no controlled deployment without fallback |
| log access path | where to inspect app/db/exposure logs | yes | operations definition | operations / platform team | integration / operations | logging / platform access path | no | required for troubleshooting |
| delivery format | manifests/chart/template/operator | yes | delivery prerequisite | app provider | integration / platform team | handover package | yes | delivery format must be agreed |