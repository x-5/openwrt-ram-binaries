# OpenWrt RAM-Mode Pre-compressed Binaries

[![Sync Upstream and UPX Compress](https://github.com/x-5/openwrt-ram-binaries/actions/workflows/sync-and-compress.yml/badge.svg)](https://github.com/x-5/openwrt-ram-binaries/actions/workflows/sync-and-compress.yml)

自动化跟踪上游官方 Release，进行极限 **UPX (`--best --lzma`)** 压缩与多架构发布的仓库。

专门适配小内存、小 Flash 闪存（如 16MB/32MB Flash、128MB/256MB RAM）的 OpenWrt 路由器（如 **小米 CR8809、移动 RD103、联发科 MT7620 / MT7628 / MT7621**）。

---

## 平台与制品矩阵

| 目标平台 | 适用代表机型 | CPU 架构与特性 | NetBird 制品 (UPX 极限压缩) | DStatus 制品 (UPX 极限压缩) |
| :--- | :--- | :--- | :--- | :--- |
| **ARMv7 / ARMv6** | **小米 CR8809** (IPQ5000), 树莓派, RD103 等 | 32位 ARMv7-A / ARMv6 (Cortex-A7) | `netbird_linux_armv6` (**~6.2 MB**, 原版 28.3MB) | `dstatus-agent_linux_arm7` (**~2.6 MB**, 原版 9.9MB) |
| **MIPSEL (Softfloat)** | **MT7620A/N**, MT7628, MT7621 | 32位 MIPS 24KEc Little-Endian (无硬件 FPU) | `netbird_linux_mipsle` (**~6.1 MB**, 原版 32.3MB) | `dstatus-agent_linux_mipsle` (**~2.6 MB**, 原版 11.7MB) |

> [!NOTE]
> MT7620 / MT7628 芯片无硬件 FPU 单元，本仓库选取的 NetBird 包特地基于 **Softfloat（软浮点）** 构建，避免出现 `Illegal instruction` 崩溃。

---

## 下载地址与加速镜像

### 1. 最新版本固定直链 (Latest Release)

#### 🇨🇳 国内加速直链 (推荐)
* **NetBird (ARMv7 / CR8809)**:
  `https://ghproxy.net/https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/netbird_linux_armv6`
* **NetBird (MIPSEL / MT7620)**:
  `https://ghproxy.net/https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/netbird_linux_mipsle`
* **DStatus (ARMv7 / CR8809)**:
  `https://ghproxy.net/https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/dstatus-agent_linux_arm7`
* **DStatus (MIPSEL / MT7620)**:
  `https://ghproxy.net/https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/dstatus-agent_linux_mipsle`

#### 🌐 官方 GitHub 直链
* `https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/netbird_linux_armv6`
* `https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/netbird_linux_mipsle`
* `https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/dstatus-agent_linux_arm7`
* `https://github.com/x-5/openwrt-ram-binaries/releases/download/latest/dstatus-agent_linux_mipsle`

---

## 自动化追更机制

* GitHub Actions 定时任务每 6 小时自动查询上游 `netbirdio/netbird` 和 `fev125/dstatus` 最新版本。
* 当探测到新版本时，自动拉取制品、进行 UPX 压缩、生成 `SHA256SUMS` 并推送到 GitHub Releases。
* 支持通过 `workflow_dispatch` 手动一键触发同步。
