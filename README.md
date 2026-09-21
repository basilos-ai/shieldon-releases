# Shieldon Releases

Shieldon 官方公开下载仓库，提供部署包、CLI 安装包和校验文件，无需 GitHub 账号即可下载。

**[下载最新版本](https://github.com/basilos-ai/shieldon-releases/releases/latest)** · [查看所有版本](https://github.com/basilos-ai/shieldon-releases/releases)

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

Public downloads for Shieldon: deployment bundles, CLI installers and checksums.
Use the [latest release](https://github.com/basilos-ai/shieldon-releases/releases/latest) for installation files. This repository contains distribution information and release assets; application source code is maintained separately.
