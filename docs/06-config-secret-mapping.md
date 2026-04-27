# Config and Secret Mapping

## Source Values from Current Lab

- COMPOSE_PROJECT_NAME
- TZ
- BOOKSTACK_APP_URL
- BOOKSTACK_APP_KEY
- BOOKSTACK_DB_HOST
- BOOKSTACK_DB_PORT
- BOOKSTACK_DB_NAME
- BOOKSTACK_DB_USER
- BOOKSTACK_DB_PASSWORD
- MARIADB_ROOT_PASSWORD

## Classification Table

| Variable | Category | Future Target | Reason | Keep as-is? |
|---|---|---|---|---|
| COMPOSE_PROJECT_NAME | local/compose-specific | none | only relevant for local Compose naming | no |
| TZ | configuration | ConfigMap | normal runtime setting, not secret | yes |
| BOOKSTACK_APP_URL | configuration | ConfigMap | external application URL, not secret | yes |
| BOOKSTACK_APP_KEY | secret | Secret | security-relevant application key | yes |
| BOOKSTACK_DB_HOST | configuration | ConfigMap | internal service target, not secret | yes |
| BOOKSTACK_DB_PORT | configuration | ConfigMap | technical connection parameter | yes |
| BOOKSTACK_DB_NAME | configuration | ConfigMap | database name is not secret | yes |
| BOOKSTACK_DB_USER | configuration | ConfigMap | username is usually not treated as secret in this context | yes |
| BOOKSTACK_DB_PASSWORD | secret | Secret | database credential | yes |
| MARIADB_ROOT_PASSWORD | secret | Secret | privileged database credential | yes |

## Resulting Split

### Configuration Values
- TZ
- BOOKSTACK_APP_URL
- BOOKSTACK_DB_HOST
- BOOKSTACK_DB_PORT
- BOOKSTACK_DB_NAME
- BOOKSTACK_DB_USER

### Secret Values
- BOOKSTACK_APP_KEY
- BOOKSTACK_DB_PASSWORD
- MARIADB_ROOT_PASSWORD

### Local-Only / Not Needed on Target Platform
- COMPOSE_PROJECT_NAME

## Notes
- A weak password used in a lab is still a secret.
- Compose convenience values are not automatically useful on a target platform.
- Config and secret separation improves clarity, access control and change management.

## Initial Platform Decision

For the current learning path, runtime values will be separated conceptually into:
- configuration values for normal operational settings
- secret values for credentials and security-relevant keys

This separation is considered mandatory for a later target platform design.
