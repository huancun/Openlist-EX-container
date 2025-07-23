
# Openlist-EX-container

> Integrates Openlist, Aria2, qBittorrent, Caddy reverse proxy, supports multi-arch one-click deployment, navigation page and multiple web panels, perfect for offline download and resource management.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Quick Deployment](#quick-deployment)
- [Getting Started](#getting-started)
- [FAQ](#faq)
- [More Usages](#more-usages)

---

## Project Overview

Based on [Alist-EX-container](https://github.com/wy580477/Alist-EX-container), this project integrates:
- **Openlist**: Resource aggregation & management
- **Aria2**: Efficient offline download
- **qBittorrent**: BT/PT download
- **Caddy**: Auto HTTPS reverse proxy
- **AriaNg/VueTorrent/Homer**: Multiple web panels for easy operation

Supports AMD64/Arm64/Armv7 architectures, auto HTTPS, ready to use out of the box.

---

## Quick Deployment

1. Download [docker-compose.yml](https://github.com/huancun/Openlist-EX-container/blob/main/docker-compose.yml)
2. Edit variables as needed, default config is recommended
3. One-click start:
   ```shell
   docker-compose up -d
   ```

---

## Getting Started

1. Get Openlist initial password:
   ```shell
   docker logs openlist-ex
   ```
2. Open main page:
   - `http://<your IP or domain>:<CADDY_WEB_PORT>`
3. Portal page:
   - `http://<your IP or domain>:<CADDY_WEB_PORT>/portalpage`
4. AriaNg panel:
   - `http://<your IP or domain>:<CADDY_WEB_PORT>/ariang`
   - Settings > RPC, fill in RPC Secret Token, protocol and port must match browser address bar
5. qBittorrent WebUI:
   - `http://<your IP or domain>:<CADDY_WEB_PORT>/qbitweb`
   - Check `log/qBittorrent/current` in data directory for temporary password
   - Default username: `admin`, after login please change to a strong password
6. VueTorrent WebUI:
   - `http://<your IP or domain>:<CADDY_WEB_PORT>/qbitvue`
7. Offline download settings:
   - Openlist admin panel > Settings > Other
   - Aria2 address: `http://localhost:61601/jsonrpc`, fill in Aria2 Secret Token
   - qBittorrent link: `http://<qbit username>:<qbit password>@localhost:61602/`

---

## FAQ

1. **How to migrate data?**
   - Bind data directory to your previous openlist data directory.
2. **How to persist Aria2 settings?**
   - Edit `aria2/aria2.conf` in data directory, restart to take effect.
3. **How to set admin password?**
   - Random password:
     ```shell
     docker exec openlist-ex openlist admin random
     ```
   - Set manually:
     ```shell
     docker exec openlist-ex openlist admin set NEW_PASSWORD
     ```
4. **How to check logs?**
   - Check `log` folder in data directory for aria2/qBittorrent/caddy logs.

---

## More Usages

- AriaNg panel changes to Aria2 settings will be lost after restart. Edit `aria2/aria2.conf` for persistent settings.
- qBittorrent WebUI language can be changed in tools > options.
- Homer portal page is customizable, config file: `homer_conf/homer.yml`.

---

## Thanks

This project is based on and improved from [Alist-EX-container](https://github.com/wy580477/Alist-EX-container). Thanks to the original author for their open source contribution.

For more help or customization, feel free to submit an issue.
