# TXS Umbrel Store

Eigener Umbrel App Store für Apps, die ich auf meinem Umbrel-Server verwenden möchte.

---

## 📦 Apps

| App | Beschreibung |
|---|---|
| 🎮 **Crafty Controller** | Minecraft Server Management |

---

## 📁 Repository-Struktur

```text
TXS-UMBREL-STORE/
├── umbrel-app-store.yml
│
└── txs-crafty/
    ├── umbrel-app.yml
    ├── docker-compose.yml
    └── exports.sh
```

---

## ➕ Apps hinzufügen

Für jede neue App wird ein eigener Ordner angelegt:

```text
txs-appname/
├── umbrel-app.yml
├── docker-compose.yml
└── exports.sh
```

Die **App-ID muss mit der Store-ID `txs` beginnen**.

### Beispiele

```text
txs-jellyfin/
txs-adguard/
txs-nginx/
```

Anschließend wird die App im GitHub-Repository hinterlegt.

Umbrel kann die App anschließend über den **TXS Umbrel Store** installieren.

---

# 🔄 Updates

Updates der Apps werden über dieses GitHub-Repository verwaltet.

Bei einem Update müssen grundsätzlich zwei Dinge angepasst werden:

### 1. TXS-App-Version

In der Datei:

```text
umbrel-app.yml
```

wird die Version der eigenen Umbrel-App geändert:

```yaml
version: "1.0.1"
```

Diese Version beschreibt die **Version der TXS-Umbrel-App** und nicht zwingend die Version der eigentlichen Software.

---

### 2. Docker-Image

In:

```text
docker-compose.yml
```

wird die verwendete Version der eigentlichen Software geändert.

Beispiel für Crafty:

```yaml
image: registry.gitlab.com/crafty-controller/crafty-4:4.10.9
```

Damit wird Crafty auf Version `4.10.9` aktualisiert.

---

### 📝 Release Notes

Änderungen können zusätzlich in `umbrel-app.yml` dokumentiert werden:

```yaml
releaseNotes: >-
  Updated Crafty Controller to 4.10.9.
```

---

## 📊 Beispiel für Crafty-Versionen

| TXS-App-Version | Crafty-Version |
|---|---|
| `1.0.0` | `4.10.8` |
| `1.0.1` | `4.10.9` |
| `1.0.2` | `4.10.10` |
| `1.1.0` | `4.11.x` |

Die **TXS-App-Version** und die **Software-Version** werden bewusst getrennt.

---

# 💾 Was passiert beim Update?

Beim Aktualisieren wird der bisherige Docker-Container durch einen Container mit dem neuen Image ersetzt.

Die persistenten Daten bleiben erhalten, da sie außerhalb des Containers über Docker Volumes gespeichert werden.

Bei Crafty werden die wichtigen Daten beispielsweise hier gespeichert:

```yaml
volumes:
  - ${APP_DATA_DIR}/backups:/crafty/backups
  - ${APP_DATA_DIR}/logs:/crafty/logs
  - ${APP_DATA_DIR}/servers:/crafty/servers
  - ${APP_DATA_DIR}/config:/crafty/app/config
  - ${APP_DATA_DIR}/import:/crafty/import
```

Dadurch bleiben unter anderem erhalten:

- 🖥️ Minecraft-Server
- 🌍 Welten
- ⚙️ Serverkonfigurationen
- 💾 Backups
- 🔧 Crafty-Konfiguration
- 📋 Logs

> **⚠️ Wichtig:** Vor größeren Updates sollte trotzdem ein Backup der wichtigen Daten vorhanden sein.

---

# 🔢 Versionsschema

Für die TXS-Apps wird **Semantic Versioning** verwendet:

```text
MAJOR.MINOR.PATCH
```

Beispiele:

```text
1.0.0
1.0.1
1.1.0
2.0.0
```

### PATCH

Kleine Änderungen und Fehlerbehebungen.

```text
1.0.0 → 1.0.1
```

### MINOR

Neue Funktionen oder größere Änderungen ohne grundlegende Inkompatibilität.

```text
1.0.1 → 1.1.0
```

### MAJOR

Größere Änderungen, die möglicherweise inkompatibel sind.

```text
1.1.0 → 2.0.0
```

---

# 🎮 Crafty Controller

Crafty Controller wird aktuell über das Docker-Image betrieben:

```text
registry.gitlab.com/crafty-controller/crafty-4
```

### Webinterface

Crafty verwendet:

```text
8443
```

Das Webinterface läuft über **HTTPS**.

### Dynmap

Der Dynmap-Port wird auf dem Umbrel-Host über Port `8523` bereitgestellt:

```text
8523 → 8123
```

Dadurch gibt es keinen Konflikt mit anderen Anwendungen, die bereits Port `8123` verwenden.

### Minecraft Java

Minecraft Java Server können über den Portbereich:

```text
25500-25600
```

erreicht werden.

### Minecraft Bedrock

Bedrock verwendet:

```text
19132/udp
```

---

# 🚀 Ziel

Der **TXS Umbrel Store** soll langfristig eine eigene Sammlung von Apps enthalten, die speziell für den eigenen Umbrel-Server angepasst und gepflegt werden.

## Geplante Apps

- 🎮 Crafty Controller
- 🎬 Jellyfin
- 🛡️ AdGuard Home
- 🌐 Nginx Proxy Manager
- 📦 weitere benötigte Server-Anwendungen

---

## 📌 Hinweis

Der Store befindet sich derzeit im Aufbau.

Neue Apps und Updates werden direkt über dieses GitHub-Repository verwaltet.
