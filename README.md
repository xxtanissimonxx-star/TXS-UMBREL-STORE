# TXS Umbrel Store

Eigener Umbrel App Store für Apps, die ich auf meinem Umbrel-Server verwenden möchte.

## Apps

- Crafty Controller – Minecraft Server Management

## Struktur


```text
TXS-UMBREL-STORE/
├── umbrel-app-store.yml
│
└── txs-crafty/
    ├── umbrel-app.yml
    ├── docker-compose.yml
    └── exports.sh
```

## Apps hinzufügen

Für jede neue App wird ein eigener Ordner angelegt:

txs-appname/
├── umbrel-app.yml
├── docker-compose.yml
└── exports.sh

Die App-ID muss mit der Store-ID "txs" beginnen.

Beispiele:

txs-jellyfin/
txs-adguard/
txs-nginx/

Anschließend wird die App im GitHub-Repository hinterlegt. Umbrel kann sie anschließend über den TXS Umbrel Store installieren.

---

# Updates

Updates der Apps werden über dieses GitHub-Repository verwaltet.

Bei einem Update müssen grundsätzlich zwei Dinge angepasst werden:

## 1. App-Version

In "umbrel-app.yml":

version: "1.0.1"

Die Versionsnummer beschreibt die Version der TXS-Umbrel-App.

## 2. Docker-Image

In "docker-compose.yml" wird die verwendete Version der eigentlichen Software geändert.

Beispiel:

image: registry.gitlab.com/crafty-controller/crafty-4:4.10.9

Damit wird Crafty auf Version 4.10.9 aktualisiert.

Optional können die Änderungen in "releaseNotes" dokumentiert werden:

releaseNotes: >-
  Updated Crafty Controller to 4.10.9.

## Beispiel für Crafty-Updates

TXS-App-Version    Crafty-Version
1.0.0               4.10.8
1.0.1               4.10.9
1.0.2               4.10.10
1.1.0               4.11.x

Die TXS-App-Version und die Software-Version werden dabei bewusst getrennt.

---

# Was passiert beim Update?

Beim Aktualisieren wird der bisherige Docker-Container durch einen Container mit dem neuen Image ersetzt.

Die persistenten Daten bleiben erhalten, da sie außerhalb des Containers über Docker Volumes gespeichert werden.

Bei Crafty befinden sich die wichtigen Daten beispielsweise hier:

volumes:
  - ${APP_DATA_DIR}/backups:/crafty/backups
  - ${APP_DATA_DIR}/logs:/crafty/logs
  - ${APP_DATA_DIR}/servers:/crafty/servers
  - ${APP_DATA_DIR}/config:/crafty/app/config
  - ${APP_DATA_DIR}/import:/crafty/import

Dadurch bleiben unter anderem:

- Minecraft-Server
- Welten
- Serverkonfigurationen
- Backups
- Crafty-Konfiguration
- Logs

bei einem Container-Update erhalten.

Wichtig: Vor größeren Updates sollte trotzdem ein Backup der wichtigen Daten vorhanden sein.

---

# Versionsschema

Für die TXS-Apps wird grundsätzlich Semantic Versioning verwendet:

MAJOR.MINOR.PATCH

Beispiele:

1.0.0
1.0.1
1.1.0
2.0.0

## PATCH

Kleine Änderungen oder Fehlerbehebungen:

1.0.0 → 1.0.1

## MINOR

Neue Funktionen oder größere Änderungen ohne grundlegende Inkompatibilität:

1.0.1 → 1.1.0

## MAJOR

Größere Änderungen, die möglicherweise inkompatibel sind:

1.1.0 → 2.0.0

---

# Crafty

Crafty Controller wird aktuell über das offizielle Crafty-Docker-Image betrieben:

registry.gitlab.com/crafty-controller/crafty-4

Die Weboberfläche läuft intern auf:

8443

und verwendet HTTPS.

Der Dynmap-Port wird auf dem Umbrel-Host über 8523 bereitgestellt:

8523 → 8123

Dadurch gibt es keinen Konflikt mit anderen Anwendungen, die bereits Port 8123 verwenden.

Minecraft Java Server können über den Portbereich:

25500-25600

erreicht werden.

Bedrock verwendet:

19132/udp

---

# Ziel

Der TXS Umbrel Store soll langfristig eine eigene Sammlung von Apps enthalten, die speziell für den eigenen Umbrel-Server angepasst und gepflegt werden.

Geplante Apps können beispielsweise sein:

- Crafty Controller
- Jellyfin
- AdGuard Home
- Nginx Proxy Manager
- weitere benötigte Server-Anwendungen
