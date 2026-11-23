# Shieldon Releases

Shieldon 官方公开下载仓库，提供桌面客户端、服务器部署包、CLI 安装包和校验文件，无需 GitHub 账号即可下载。

## 桌面客户端下载

**Shieldon Desktop 0.1.3 · 正式版**

| 系统 | 安装包 |
| --- | --- |
| Windows x64 | [下载 Windows 安装器（EXE）](https://github.com/basilos-ai/shieldon-releases/releases/download/desktop-v0.1.3/shieldon-desktop-0.1.3-win32-x64-setup.exe) |
| macOS Apple Silicon（M 系列芯片） | [下载 Mac 安装器（DMG）](https://github.com/basilos-ai/shieldon-releases/releases/download/desktop-v0.1.3/shieldon-desktop-0.1.3-darwin-arm64.dmg) |
| macOS Intel | [下载 Mac 安装器（DMG）](https://github.com/basilos-ai/shieldon-releases/releases/download/desktop-v0.1.3/shieldon-desktop-0.1.3-darwin-x64.dmg) |

[版本说明与 ZIP 下载](https://github.com/basilos-ai/shieldon-releases/releases/tag/desktop-v0.1.3) · [SHA-256 校验文件](https://github.com/basilos-ai/shieldon-releases/releases/download/desktop-v0.1.3/desktop-SHA256SUMS)

macOS：打开 DMG，将 Shieldon Desktop 拖入 Applications 后启动。当前安装包未配置开发者签名和 Apple 公证，首次打开可能需要系统确认。连接前请将服务器升级到 Web/backend v0.6.4（仅支持客户端 0.1.3）；已有客户端可使用 Switch Endpoint 切换到新的服务器。Windows 0.1.2 可通过应用内更新升级；0.1.0/0.1.1 用户需手动安装一次新版，之后可在 Settings → Software update 检查兼容更新。默认英语，支持日语和简体中文。未签名 macOS 暂需手动安装，应用内安装会提示验证失败。

**[下载最新 Web / 服务器版本](https://github.com/basilos-ai/shieldon-releases/releases/latest)** · [查看所有版本](https://github.com/basilos-ai/shieldon-releases/releases)

## 服务器部署

最低配置：**4 核 CPU、8 GB 内存、100 GB 存储**，安装 Docker Engine 和 Docker Compose v2（Linux x86_64 / ARM64）。

从同一个版本下载 `shieldon.tar.gz` 和 `shieldon.tar.gz.sha256`，自行选择服务器上的安装位置，新建目录并放入这两个文件，然后在该目录执行：

```sh
set -eu
sha256sum -c shieldon.tar.gz.sha256
test ! -e compose.yaml
test ! -e .env
test ! -e runtime
tar -xzf shieldon.tar.gz --strip-components=1
sha256sum -c SHA256SUMS
chmod 600 .env
```

编辑 `.env` 中的 `SHIELDON_PUBLIC_URL` 和端口，HTTPS 场景设置 `SHIELDON_COOKIE_SECURE=true`，然后启动：

```sh
sh deploy.sh --with-middleware
```

PostgreSQL、Redis、MinIO 是可选安装组件；可以单独部署或连接已有服务。已有 PostgreSQL 和 Redis 时，在 `.env` 填写连接信息后执行 `sh deploy.sh`。应用镜像公开，无需仓库登录。详细配置、升级与备份步骤见包内 `README.md`；部署后文档位于 `/docs/`。

已有安装请使用包内 `update.sh`，不要直接解压覆盖配置和数据。

## CLI

选择对应系统和架构的 `shieldon_<版本>_<系统>_<架构>.zip`：macOS (`darwin`)、Linux、Windows；`amd64` 或 `arm64`。`SHA256SUMS` 和 `manifest.json` 用于校验 CLI 安装包。

---

Public downloads for Shieldon: desktop apps, deployment bundles, CLI installers and checksums.
Use the desktop download links above for Windows and macOS, or the [latest Web / server release](https://github.com/basilos-ai/shieldon-releases/releases/latest) for server and CLI installation files. This repository contains distribution information and release assets; application source code is maintained separately.
