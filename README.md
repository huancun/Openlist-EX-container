# Openlist-EX-container

> 集成 Openlist、Aria2、qBittorrent、Caddy 反向代理，支持多架构一键部署，带导航页和多种 Web 面板，适合离线下载和资源管理。

## [English Version](README-en.md)

---

## 目录
- [项目简介](#项目简介)
- [快速部署](#快速部署)
- [初次使用指南](#初次使用指南)
- [常见问题](#常见问题)
- [更多用法](#更多用法)

---

## 项目简介

本项目基于 [Alist-EX-container](https://github.com/wy580477/Alist-EX-container) 改进，集成了：
- **Openlist**：资源聚合与管理
- **Aria2**：高效离线下载
- **qBittorrent**：BT/PT 下载
- **Caddy**：自动 HTTPS 反向代理
- **AriaNg/VueTorrent**：多种 Web 面板，操作更便捷

支持 AMD64/Arm64/Armv7 架构，自动开启 HTTPS，开箱即用。

---

## 快速部署

1. 下载 [docker-compose.yml](https://github.com/huancun/Openlist-EX-container/blob/main/docker-compose.yml)
2. 按需修改变量，推荐直接使用默认配置
3. 一键启动：
   ```shell
   docker-compose up -d
   ```

---

## 初次使用指南

1. 获取 Openlist 初始密码：
   ```shell
   docker logs openlist-ex
   ```
2. 打开主页面：
   - `http://<你的IP或域名>:<CADDY_WEB_PORT>`
3. 导航页：
   - `http://<你的IP或域名>:<CADDY_WEB_PORT>/portalpage`
4. AriaNg 面板：
   - `http://<你的IP或域名>:<CADDY_WEB_PORT>/ariang`
   - 常规设置 > RPC，填入 RPC 密钥，协议和端口需与浏览器地址栏一致
5. qBittorrent WebUI：
   - `http://<你的IP或域名>:<CADDY_WEB_PORT>/qbitweb`
   - 查看数据目录下 `log/qBittorrent/current` 文件，获得临时密码
   - 默认用户名 `admin`，临时密码登录后建议立即修改为强密码
6. VueTorrent WebUI：
   - `http://<你的IP或域名>:<CADDY_WEB_PORT>/qbitvue`
7. 离线下载设置：
   - Openlist 管理面板 > 设置 > 其它
   - Aria2 地址：`http://localhost:61601/jsonrpc`，填入 Aria2 密钥
   - qBittorrent 链接：`http://<qbit用户名>:<qbit密码>@localhost:61602/`

---

## 常见问题

1. **如何迁移数据？**
   - 直接将数据目录指定为原 openlist 数据目录即可。
2. **Aria2 设置如何持久化？**
   - 修改数据目录下 `aria2/aria2.conf` 文件，重启后生效。
3. **如何设置管理员密码？**
   - 随机生成：
     ```shell
     docker exec openlist-ex openlist admin random
     ```
   - 手动设置：
     ```shell
     docker exec openlist-ex openlist admin set NEW_PASSWORD
     ```
4. **如何查看日志？**
   - 数据目录下 `log` 文件夹可查看 aria2/qBittorrent/caddy 日志。

---

## 更多用法

- AriaNg 面板更改的 Aria2 设置，重启后会失效。建议直接编辑 `aria2/aria2.conf`。
- qBittorrent WebUI 可在 tools > options 更改界面语言。

---


## 更多用法和注意事项

 1. 如果从之前的 openlist 安装迁移，可以直接把数据目录指定到之前的 openlist 数据目录。

 2. AriaNg 面板更改的 Aria2 设置，在 Aria2 重启后会失效。修改数据目录下 aria2/aria2.conf 文件，可以持久更改 Aria2 设置。

 3. 设置管理员密码: 

```
     # 随机生成管理员密码
     docker exec openlist-ex openlist admin random

     # 手动设置管理员密码,`NEW_PASSWORD`是指你需要设置的密码
     docker exec openlist-ex openlist admin set NEW_PASSWORD
```

 4. 在数据目录下 log 目录中，可以查看 aria2/qBittorrent/caddy 的日志。

---

## 致谢

本项目参考并改进自 [Alist-EX-container](https://github.com/wy580477/Alist-EX-container)，感谢原作者的开源贡献。

如需更多帮助或定制，欢迎提交 issue。