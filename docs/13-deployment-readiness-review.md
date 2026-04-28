# Deployment Readiness Review

## Scope
Review of a delivered deployment package for integration into a target platform environment.

## 1. Delivered Artifacts
| Artifact | Present? | Purpose | Questions / Gaps |
|---|---|---|---|
| container image reference | yes/no | runtime artifact | ... |
| deployment descriptor | yes/no | deployment logic | ... |
| configuration example | yes/no | runtime parameterization | ... |
| secret documentation | yes/no | credential preparation | ... |
| storage requirements | yes/no | persistence planning | ... |
| network / exposure description | yes/no | connectivity planning | ... |
| operations notes | yes/no | operational handover | ... |

## 2. Runtime Assumptions
- expected application endpoint:
- expected database/service dependency:
- expected ports:
- expected persistent storage:
- expected external exposure model:

## 3. Configuration Review
| Variable / Setting | Required? | Secret? | Source | Notes |
|---|---|---|---|---|
| ... | yes/no | yes/no | config/secret/platform | ... |

## 4. Target Environment Readiness
| Area | Ready? | Requirement | Notes / Action |
|---|---|---|---|
| namespace / project | yes/no | ... | ... |
| secrets available | yes/no | ... | ... |
| storage available | yes/no | ... | ... |
| ingress / route / DNS | yes/no | ... | ... |
| internal service connectivity | yes/no | ... | ... |
| image pull access | yes/no | ... | ... |

## 5. Operational Validation
- minimal smoke test:
- relevant logs:
- basic rollback / fallback thought:
- health / readiness expectations:

## 6. Open Issues
1.
2.
3.

## Initial Assessment
- ready for integration: yes/no/partially
- main blockers:
- next actions: