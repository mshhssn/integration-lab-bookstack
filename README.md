# **BookStack Local Delivery Package**

## **Zweck**
Lokales, produktionsnahes Delivery-Paket für BookStack mit MariaDB, Reverse Proxy und Persistenz auf Basis von Docker Compose.

## **Aktive Laufzeitkomponenten**
- `bookstack-app`
- `bookstack-db`
- `bookstack-proxy`

## **Aktive operative Dateien**
- `compose.yml`
- `.env`
- `.env.example`
- `proxy/nginx.conf`
- `proxy/conf.d/default.conf`

## **Aktive Architektur**
- `bookstack-proxy` veröffentlicht Port `8080`
- `bookstack-app` ist nur intern erreichbar
- `bookstack-db` ist nur intern erreichbar
- internes Netzwerk: `bookstack_internal`
- persistente Volumes:
  - `bookstack-app-config`
  - `bookstack-db-data`

## **Nicht aktiv in der aktuellen Laufzeit**
- `k8s/` enthält Zielplattform-Vorbereitung und wird aktuell nicht angewendet
- `docs/` enthält Begleitmaterial, Reviews und Notizen

## **Voraussetzungen**
- Docker verfügbar
- Docker Compose verfügbar
- lokaler Port `8080` frei
- gültige `.env` vorhanden

## **Konfiguration**
Die lokale Laufzeitkonfiguration erfolgt über `.env`.

Neue lokale Konfiguration aus Vorlage erzeugen:

```bash
cp .env.example .env
```

**Wichtige Variablen**:

- TZ
- BOOKSTACK_APP_URL
- BOOKSTACK_APP_KEY
- BOOKSTACK_DB_HOST
- BOOKSTACK_DB_PORT
- BOOKSTACK_DB_NAME
- BOOKSTACK_DB_USER
- BOOKSTACK_DB_PASSWORD
- MARIADB_ROOT_PASSWORD

## **Pre-Deployment Quick Check**:
```bash
docker --version
docker-compose --version
docker compose config > /tmp/compose-validated.yml
```

**Pflichtwerte prüfen**:

- .env vorhanden
- BOOKSTACK_APP_KEY gesetzt
- BOOKSTACK_APP_URL plausibel
- BOOKSTACK_DB_HOST=bookstack-db
- Proxy-Dateien vorhanden

## **Rollout**
**Standard-Rollout**:
```bash
docker-compose -f compose.yml up -d
```
**Kontrollierter Recreate-Rollout**:
```bash
docker-compose -f compose.yml up -d --force-recreate
```
**Statusprüfung**
```bash
docker-compose -f compose.yml ps
```
**Smoke Test**

Technischer Check:
```bash
curl -i http://localhost:8080/health
curl -I http://localhost:8080/
```
Manuelle Prüfung im Browser:
- Login-Seite erreichbar
- Login funktioniert
- vorhandene Inhalte sichtbar
- Inhalte lassen sich öffnen
- Änderungen lassen sich speichern

**Logs prüfen**:
```bash
docker compose logs --tail=50 bookstack-proxy
docker compose logs --tail=50 bookstack-app
docker compose logs --tail=50 bookstack-db
```
**Stoppen**
```bash
docker-compose -f compose.yml down
```
**Persistenz prüfen**
```bash
docker volume ls
docker volume inspect bookstack-app-config
docker volume inspect bookstack-db-data
```
Persistente Laufzeitdaten liegen in Docker Volumes:
+ App-seitig: bookstack-app-config
+ DB-seitig: bookstack-db-data

Wichtige bekannte Fehlerbilder
- BOOKSTACK_APP_KEY fehlt oder ist ungültig
- BOOKSTACK_DB_HOST ist falsch gesetzt
- BOOKSTACK_DB_PASSWORD oder BOOKSTACK_DB_USER sind falsch
- BOOKSTACK_APP_URL passt nicht zur Zielumgebung
- Proxy-Upstream in default.conf zeigt auf falsches Ziel
- bestehendes DB-Volume kollidiert mit geänderten Initialwerten

Hinweise
- Die Images sind per Digest gepinnt.
- Der aktuell aktive Delivery Flow ist Compose-basiert.
- Kubernetes-Dateien sind vorbereitet, aber derzeit nicht Teil der aktiven lokalen Laufzeit.