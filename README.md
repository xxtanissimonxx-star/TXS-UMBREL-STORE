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
### 🔄 Aktuelle Crafty-Version

Die aktuell veröffentlichte Version findest du hier:

[Crafty Releases](https://gitlab.com/crafty-controller/crafty-4/-/releases)


---
