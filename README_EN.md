<p align="center">
  <img src="picture/tgtodrive-brand-en-new.png" alt="TgtoDrive: from cloud transfers to a playable media library" width="100%">
</p>

<p align="center">
  <a href="https://hub.docker.com/r/walkingd/tgto123">
    <img src="https://img.shields.io/docker/pulls/walkingd/tgto123?style=for-the-badge&logo=docker&label=Docker%20Pulls" alt="Docker Pulls">
  </a>
  <a href="https://hub.docker.com/r/walkingd/tgto123">
    <img src="https://img.shields.io/badge/Docker%20Image-walkingd%2Ftgto123-2496ED?style=for-the-badge&logo=docker" alt="Docker Image">
  </a>
  <img src="https://img.shields.io/badge/Version-8.3.17-6C63FF?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/Arch-amd64%20%7C%20arm64-111827?style=for-the-badge" alt="Architecture">
</p>

<p align="center">
  <a href="README.md">中文</a> | English
</p>

<p align="center">
  <strong><span style="font-size: 1.25em;">Telegram Community: <a href="https://t.me/TgtoDriveChat">https://t.me/TgtoDriveChat</a></span></strong>
</p>

<p align="center">
  <strong>An all-in-one cloud-drive media automation platform: from resource discovery, automatic transfer, smart organization and STRM mounting to Emby 302 direct-link playback. It focuses on 115 / 123 / Guangya Cloud Drive organization and transfer, full and incremental 115 / 123 / Guangya STRM generation, and Emby reverse-proxy 302 playback.</strong>
</p>

<p align="center">
  <strong>This software is completely free and will remain free. If this project helps you, please click the ⭐ Star button in the upper-right corner to support it.</strong>
</p>

---

## Overview

TgtoDrive is a Web-console-first automation platform for NAS and home-server media workflows. It connects resource discovery, Telegram monitoring, cloud-drive transfer, media organization, STRM generation, Emby dashboards, and Emby 302 direct-link playback into one continuous workflow.

Typical flow:

```text
Discovery / channel monitoring
        -> Transfer to 123 / 115 / Guangya / Tianyi and other cloud drives
        -> TMDB / AI-assisted media organization
        -> Generate 115 / 123 / Guangya STRM libraries
        -> Emby dashboard and 302 direct-link playback
```

This README is written for Docker image users and focuses on features, deployment, and Web configuration.

## Screenshots

| Emby Dashboard | Emby Reverse Proxy |
| --- | --- |
| ![Emby Dashboard](picture/Emby看板.png) | ![Emby Reverse Proxy](picture/Emby反代.png) |

| 115 Organizer | 123 Organizer |
| --- | --- |
| ![115 Organizer](picture/115网盘-网盘整理功能.png) | ![123 Organizer](picture/123云盘-网盘整理功能.png) |

| Transfer History | Organize History |
| --- | --- |
| ![Transfer History](picture/监控历史.png) | ![Organize History](picture/整理历史.png) |

| Global Settings | Toolbox |
| --- | --- |
| ![Global Settings](picture/全局设置.png) | ![Toolbox](picture/实用工具.png) |

## Key Features

### Cloud-drive accounts and resource entry points

| Feature | Description |
| --- | --- |
| 123 Cloud Drive | Account setup, channel monitoring, share transfer, JSON fast import, offline tasks, STRM generation |
| 115 Cloud Drive | Cookie / QR login, channel monitoring, organization, STRM, shared STRM, link transfer, offline tasks, cleanup |
| Guangya Cloud Drive | SMS login token, channel monitoring, share-link transfer, offline tasks, media organization, STRM generation |
| Tianyi Cloud Drive | Account setup, channel monitoring, link transfer, cleanup |
| HDHive | OAuth authorization, check-in, channel monitoring, transfer workflow, Tianyi-link handling |
| Telegram | Channel monitoring, keyword rules, universal forwarding, scheduled sending, bot notifications |
| Search integrations | Pansou, Nullbr, HDHive and more resource entry points |

### Transfer and monitoring

- Monitor Telegram channels for 123, 115, Guangya, Tianyi and HDHive resources.
- Use Douban / Maoyan ranking lists and keyword allowlists to trigger transfers.
- Configure blocklists, second-level routing, channel IDs and target folders.
- Transfer Guangya share links directly, including fallback expansion for share folders that cannot be restored from their root item.
- Monitor 123 share links for incremental updates.
- Manage transfer history, logs and organization history from the Web console.

### Media library organization

TgtoDrive can turn transferred files into a cleaner media library for Emby, Jellyfin or Plex.

| Capability | Description |
| --- | --- |
| Recognition | Match media items with filenames, TMDB, media info and AI assistance |
| Classification | Movies, TV shows, anime, documentaries and variety shows |
| Region grouping | Mainland China, western, Japanese / Korean and other regions |
| Year grouping | Optional year-based subfolders |
| Naming normalization | Standardize movie, season, episode and subtitle naming |
| Upgrade rules | Prefer Remux / Blu-ray, resolution, Dolby and file-size policies |
| Multi-version strategy | Keep Dolby and non-Dolby versions when needed |
| STRM sync | Refresh STRM output after organization changes |

### STRM generation and maintenance

| Capability | Description |
| --- | --- |
| 123 STRM | Generate STRM files from 123 cloud-drive folders |
| 115 STRM | Generate STRM files from 115 cloud-drive folders |
| Guangya STRM | Generate STRM files from Guangya cloud-drive folders through `/playgy/` playback links |
| Shared STRM | Generate and organize STRM files from shared 115 resources |
| Metadata sync | Sync subtitles, posters, NFO files and related assets |
| Invalid cleanup | Remove invalid STRM files and empty directories |
| Deep delete | Trigger cloud-drive cleanup after media deletion in Emby |

### Emby integration

| Feature | Description |
| --- | --- |
| Emby Dashboard | Library statistics, latest media, continue watching and activity views |
| Emby Reverse Proxy | Manage multiple Emby reverse-proxy instances |
| 302 Direct Link Playback | Rewrite playback requests to cloud-drive direct links |
| Playback Records | Inspect reverse-proxy playback records |
| Poster Refresh | Detect and refresh missing Emby posters |
| Metadata Cleanup | Utility workflow for Emby metadata cleanup |

### Operations and utilities

- Global proxy, TMDB key and Telegram main-bot settings.
- Web SSH terminal.
- Pansou aggregation search configuration.
- WeCom notification settings.
- Server connectivity checks.
- Local-file fast import to 123 / 115.
- Multi-protocol offline tasks for 123 / 115 / Guangya.
- Bilibili / Douyin video download.
- Community posting settings.
- 123 cloud-drive API rate-limit toolbox.

## Quick Start

### 1. Requirements

- Docker 20.10+.
- Docker Compose 2.x.
- A NAS or Linux server that can run continuously.
- Telegram API connectivity if you need Telegram-related workflows.

### 2. Create a deployment folder

```bash
mkdir -p tgtodrive
cd tgtodrive
mkdir -p db downloads strm
```

### 3. Create `docker-compose.yml`

```yaml
version: '3'

services:
  tgtodrive-service:
    image: walkingd/tgto123:latest
    container_name: TgtoDrive
    network_mode: host  # 推荐 host 模式以简化端口映射和直链访问
    environment:
      # --- 基础配置 ---
      - TZ=Asia/Shanghai
      # 必填：WEB管理页面的登录账号密码
      - ENV_WEB_PASSPORT=admin
      - ENV_WEB_PASSWORD=password
    volumes:
      # 数据库与日志持久化，右侧固定为/app/db
      - ./db:/app/db
      # STRM输出目录：用于保存 /app/strm 下生成内容,/vol1/1000/Emby/strm 改成你的目录，右侧固定为/app/strm
      - /vol1/1000/Emby/strm:/app/strm
      # [可选] B站、抖音等视频下载保存路径，不需要可去掉：右侧固定为/app/downloads
      - ./downloads:/app/downloads
      # [可选] 本地文件无限尝试秒传网盘路径：左侧填NAS本地路径，不需要可去掉：右侧固定为/app/upload
      - /vol3/1000/Video/MoviePilot/transfer:/app/upload

    restart: always
```

### 4. Start the service

```bash
docker-compose pull  # Pull the latest image
docker-compose up -d # Start in the background
```

Open the Web console:

```text
http://YOUR_SERVER_IP:12366
```

Log in with `ENV_WEB_PASSPORT` and `ENV_WEB_PASSWORD` from your compose file.

## Recommended Web Setup Order

1. Open Global Settings and configure proxy, TMDB key and the Telegram main bot.
2. Configure 115, 123, Guangya and Tianyi accounts.
3. Configure channel monitoring: channel IDs, target folders, keywords and blocklists.
4. Configure organizer pages: scan folders, target folders, naming rules and upgrade policies.
5. Configure STRM generation: cloud-drive folders and playback base URL.
6. Configure Emby reverse proxy: Emby URL, API key and listen port.
7. Save settings, wait for the service to restart, then inspect Logs, Transfer History and Organize History.

## Common Commands

Check status:

```bash
docker compose ps
```

Follow logs:

```bash
docker compose logs -f
```

Update:

```bash
docker compose pull
docker compose up -d
```

Stop:

```bash
docker compose down
```

Recommended backup items:

- `db/`: configuration, history, logs and task state.
- `strm/`: generated STRM media library.

## Feature Screenshots

### System Tools

#### Emby Dashboard

Shows Emby-related service status, media-library information and playback workflow visibility, so you can quickly check whether the media stack is healthy.

![Emby Dashboard](picture/Emby看板.png)

#### Emby Reverse Proxy

Configures Emby reverse-proxy instances, including Emby URL, API key, listen port and 302 direct-link playback options.

![Emby Reverse Proxy](picture/Emby反代.png)

#### Global Settings

Centralizes proxy settings, Telegram main-bot settings, TMDB key and channel-monitoring polling options.

![Global Settings](picture/全局设置.png)

#### Logs

Displays service logs, task execution records and errors. This is the primary place to troubleshoot transfers, organization, STRM generation and reverse-proxy playback.

![Logs](picture/日志中心.png)

#### Transfer History

Shows resources matched by channel monitoring, their transfer status, message sources and handling results.

![Transfer History](picture/监控历史.png)

#### Organize History

Shows media recognition, classification, renaming, upgrade and move records from cloud-drive organization tasks.

![Organize History](picture/整理历史.png)

#### Toolbox

Provides manual utility actions and maintenance tasks for troubleshooting or one-off resource handling.

![Toolbox](picture/实用工具.png)

### 115 Cloud Drive

#### 115 Account

Configures 115 account login, Cookie, QR login and account status checks. It is the base for 115 transfer, organization, STRM and direct-link workflows.

![115 Account](picture/115网盘-115账号配置.png)

#### HDHive Account

Configures HDHive account information for resource search, channel monitoring, link transfer and points-threshold controls.

![HDHive Account](picture/115网盘-影巢账号配置.png)

#### 115 Channel Monitoring

Configures 115 resource-channel monitoring rules, including channel IDs, target folders, keyword allowlists, blocklists and routing rules.

![115 Channel Monitoring](picture/115网盘-115频道监控配置.png)

#### HDHive Channel Monitoring

Configures HDHive channel monitoring and transfer rules, including keywords, target folders and trigger conditions.

![HDHive Channel Monitoring](picture/115网盘-影巢频道监控配置.png)

#### Organizer

Scans 115 cloud-drive media folders and uses TMDB recognition to classify, rename, archive and upgrade media files.

![115 Organizer](picture/115网盘-网盘整理功能.png)

#### STRM

Generates STRM files from 115 folders with full scans, incremental refresh, metadata sync and invalid-item cleanup.

![115 STRM](picture/115网盘-STRM生成.png)

#### Shared STRM

Generates and organizes STRM files from shared 115 resources, bringing shared links into the local media-library playback workflow.

![115 Shared STRM](picture/115网盘-分享STRM生成与整理.png)

#### Link Transfer

Handles 115 shared links and saves resources to target folders, then passes them into the organization workflow when needed.

![115 Link Transfer](picture/115网盘-链接转存.png)

#### Offline Settings

Configures 115 offline-download options for magnet, ed2k and torrent tasks. ED2K and magnet/torrent handling have separate switches.

![115 Offline Settings](picture/115网盘-离线设置.png)

#### Cleanup

Configures automatic cleanup rules for expired, invalid or no-longer-needed 115 resources and folders.

![115 Cleanup](picture/115网盘-自动清理.png)

### 123 Cloud Drive

#### 123 Account

Configures 123 account credentials, token, folders and status checks. It is the base for 123 transfer, fast import, organization and STRM workflows.

![123 Account](picture/123云盘-123账号配置.png)

#### Channel Monitoring

Configures 123 resource-channel monitoring rules and automatically transfers Telegram channel resources to target 123 folders.

![123 Channel Monitoring](picture/123云盘-频道监控配置.png)

#### Organizer

Scans 123 cloud-drive media resources and uses TMDB recognition to classify, rename, archive and upgrade media files.

![123 Organizer](picture/123云盘-网盘整理功能.png)

#### STRM

Generates STRM files from 123 folders for Emby, Jellyfin, Plex and other media-library tools.

![123 STRM](picture/123云盘-STRM生成.png)

#### Transfer and JSON Fast Import

Configures 123 share-link transfer and JSON fast-import workflows for batch importing existing resource lists.

![123 Transfer and JSON Fast Import](picture/123云盘-转存与秒传JSON.png)

#### Offline Settings

Configures 123 offline-download tasks for magnet, ed2k and torrent links.

![123 Offline Settings](picture/123云盘-离线设置.png)

#### Fast Import from 115 and Tianyi

Configures cross-drive fast import from 115, Tianyi and related sources into 123 Cloud Drive.

#### Share Monitor

Monitors incremental changes in 123 share links and automatically transfers newly added files to target folders.

![123 Share Monitor](picture/123云盘-分享转存监控.png)

#### Share Generation

Generates 123 Cloud Drive share links for search, forwarding and resource-publishing workflows.

![123 Share Generation](picture/123云盘-分享链接生成.png)

### Guangya Cloud Drive

#### Login and Token

Uses SMS verification to log in to Guangya Cloud Drive, then persists the access token and refresh token for share transfer, channel monitoring and organization workflows.

![Guangya Login and Token](picture/光鸭云盘-登录与Token.png)

#### Channel Monitoring

Configures Guangya resource-channel monitoring for public Telegram channels and TG API channel IDs. Keyword allowlists, blocklists, Douban / Maoyan rankings and second-level routing can all be used to decide what gets transferred.

![Guangya Channel Monitoring](picture/光鸭云盘-频道监控配置.png)

#### Link Transfer

Handles Guangya share links and saves shared files or folders into the configured account folder. For shares whose root folder cannot be restored directly, TgtoDrive expands the folder and transfers child files as a fallback.

![Guangya Link Transfer](picture/光鸭云盘-链接转存.png)

#### Offline Settings

Configures Guangya offline tasks for magnet links, torrents converted to magnet links, and best-effort ED2K submission. ED2K availability depends on the live Guangya cloud-add API; failures are reported separately and do not block 115 submissions.

#### Organizer

Scans Guangya media folders and uses TMDB, media info and AI-assisted recognition to classify, rename, archive and upgrade media files, following the same organization model used by 123 and 115.

![Guangya Organizer](picture/光鸭云盘-网盘整理功能.png)

#### STRM Generation

Generates STRM files for Guangya Cloud Drive folders. Playback links use `/playgy/` and can be mounted into Emby, Jellyfin or Plex.

### Tianyi Cloud Drive and Other Integrations

#### Tianyi Account

Configures Tianyi account login information for Tianyi transfer, monitoring and cleanup workflows.

![Tianyi Account](picture/天翼云盘-天翼账号配置.png)

#### Tianyi Channel Monitoring

Configures Tianyi resource-channel monitoring and transfers Tianyi shared resources to target folders.

![Tianyi Channel Monitoring](picture/天翼云盘-频道监控配置.png)

#### Tianyi Link Transfer

Handles Tianyi Cloud Drive shared links and transfers linked resources into the configured account.

![Tianyi Link Transfer](picture/天翼云盘-链接转存.png)

#### Tianyi Cleanup

Configures automatic cleanup rules for expired Tianyi resources or temporary files.

![Tianyi Cleanup](picture/天翼云盘-自动清理.png)

#### SSH Terminal

Connects to remote servers from the Web console, making it easier to inspect the deployment environment, container state and mounted folders.

![SSH Terminal](picture/SSH终端.png)

#### Universal Forwarding and TG API

Configures Telegram API and universal forwarding so private, restricted or user-forwarded messages can still enter the automation workflow.

![Universal Forwarding and TG API](picture/万能转发与TGAPI配置.png)

#### Pansou Aggregation Search

Configures Pansou aggregation search for keyword-based discovery across multiple cloud-drive resource sources.

![Pansou Aggregation Search](picture/Pansou聚合搜索配置.png)

#### WeCom Notifications

Configures WeCom notifications for transfer results, organization results, task completion and error messages.

![WeCom Notifications](picture/微信通知配置.png)

#### Community Posting

Configures resource-community posting so organized resource information can be published according to rules.

![Community Posting](picture/资源社区配置.png)

#### Local File Fast Import

Scans local PT or download folders and attempts fast import into 123 / 115 to reduce repeated upload traffic.

![Local File Fast Import](picture/本地文件秒传配置.png)

#### Emby Missing Poster Refresh

Detects media items with missing posters in Emby and triggers refresh tasks to improve library presentation.

![Emby Missing Poster Refresh](picture/Emby缺失海报检测与刷新.png)

#### Server Connectivity Checks

Tests network connectivity from the server to Telegram, cloud drives, TMDB, Emby and other key services.

![Server Connectivity Checks](picture/服务器连通性检测.png)

#### Video Download

Configures and runs video download tasks, saving downloaded files into mapped container folders for later organization or library import.

![Video Download](picture/视频下载功能.png)

## FAQ

### Why do some features not work?

Most workflows depend on account, folder, proxy, bot and TMDB settings in the Web console. Save the relevant configuration first, then check the Logs page.

### Why is channel monitoring not picking up messages?

Check Telegram connectivity, channel ID, keyword rules, blocklists, target folders and polling interval. For private or restricted channels, universal forwarding may be a better fit.

### STRM files are generated, but Emby cannot play them. What should I check?

Make sure the STRM playback base URL is reachable from the Emby server, the 115 / 123 / Guangya account is still valid, the Emby reverse-proxy instance is running, and the required ports are not blocked.

### What if the 115 Cookie expires?

Open the 115 account page and update the Cookie, or use the QR-login workflow from the Web console.

### How should organizer folders be configured?

The scan folder and target folder should not be the same. The target folder should not be placed inside the scan folder, otherwise repeated scans or organization loops may happen.

## Disclaimer

- TgtoDrive is intended for personal cloud-drive file management, automated organization and media-library maintenance.
- Make sure you have the legal right to use the relevant accounts, resources and media files.
- Follow your local laws, cloud-drive service terms and third-party service rules.
- Account, data, network and copyright risks are the user's responsibility.
