# Integration Lab 1 – BookStack + MariaDB + Reverse Proxy

## Ziel
Betriebsnaher Multi-Service-Stack mit bestehender Anwendung, Datenbank, Reverse Proxy und Persistenz.

## Architektur
- bookstack-proxy veröffentlicht Port 8080
- bookstack-app nur intern erreichbar
- bookstack-db nur intern erreichbar
- internes Netzwerk: bookstack_internal
- persistente Volumes:
  - bookstack_db_data
  - bookstack_app_config

## Pre-Flight Checks
- Docker erreichbar
- Port 8080 frei
- .env vorhanden
- APP_KEY gesetzt
- compose config erfolgreich

## Start
docker compose up -d

## Prüfung
curl -i http://localhost:8080/health
Browser: http://localhost:8080

## Wichtige Dateien
- compose.yml
- .env
- proxy/nginx.conf
- proxy/conf.d/default.conf

## Persistenz
- DB in Volume bookstack_db_data
- App-Konfiguration in Volume bookstack_app_config

## Wichtige Fehlerbilder
- APP_KEY fehlt/ungültig
- DB_HOST falsch
- DB-Credentials geändert, aber bestehendes DB-Volume
- APP_URL falsch gesetzt