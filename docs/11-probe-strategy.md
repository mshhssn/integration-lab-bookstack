# Probe Strategy

## Goal
Introduce a first meaningful health model for the platform target design.

## BookStack Application
- startupProbe: enabled
- readinessProbe: enabled
- livenessProbe: enabled

Reason:
The application exposes HTTP endpoints and can be checked in a platform-friendly way via HTTP.
A startup probe protects slower initialization.
Readiness controls traffic admission.
Liveness provides a controlled restart mechanism.

## MariaDB
- startupProbe: enabled
- readinessProbe: enabled
- livenessProbe: postponed

Reason:
MariaDB is a stateful workload and should not receive an aggressive restart policy too early.
A readiness model is important so the application only connects once the DB is really available.
A liveness probe may be added later with more caution.

## Initial Probe Target Choices
- BookStack app: HTTP GET on /login
- MariaDB: exec-based mariadb-admin ping

## Design Note
Probe behavior depends on workload type.
Stateless web workloads and stateful database workloads should not be treated the same way.