# ⚡ 闪传 · Flashdrop (v8.0)

<p align="center">
  <strong><a href="#-闪传-简体中文">🇨🇳 简体中文文档</a></strong> &nbsp;|&nbsp; <strong><a href="#-flashdrop-english">🇺🇸 English Documentation</a></strong>
</p>

<p align="center">
  🌐 <strong>立即在线使用 / Launch Web App:</strong> <a href="https://bibubibu1106.github.io/flashdrop/"><strong>https://bibubibu1106.github.io/flashdrop/</strong></a>
</p>

---

# 🇨🇳 闪传 (简体中文)

## 一、项目简介

**《闪传》（英文名：Flashdrop）** 是一款零配置、免安装 App、端到端加密的跨生态极速互传 Web PWA 工具。  
专为 **🍎 苹果（iPhone / iPad） ⇄ 🤖 安卓（手机 / 平板） ⇄ 💻 电脑（Mac / Windows）** 打造，支持苹果开热点给安卓免流直传、同 Wi‑Fi 局域网直连、以及 5G 异网穿透互传，内置 **简体中文 / English** 双语实时切换。

### 🚀 3 步极速上手
1. **打开网页**：在需要互传的手机、平板或电脑浏览器中打开 [https://bibubibu1106.github.io/flashdrop/](https://bibubibu1106.github.io/flashdrop/)（点击右上角 **下载图标** 可查看「添加到主屏幕」引导；点击 **设置图标** 可切换中/英文与夜间模式）。
2. **扫码或输入配对码（仅首次需要）**：点击顶部的「配对码 / 扫码换码」，让多台设备使用同一个 **6 位配对码**（自动保存在本机，下次打开自动秒连）。
3. **开始互传**：
   - **传文字/链接/验证码**：点击「一键读取本机剪贴板并发送」或在输入框长按粘贴。
   - **传照片/视频/文件**：点击「发照片 / 视频」相册多选，或点击「发原文件 (原图)」无损保留拍摄时间与定位信息（电脑/平板可直接拖拽文件到页面或按 `Ctrl+V` 粘贴截图）。

---

## 二、核心亮点与技术架构

### ✨ 功能亮点
- **🌐 中英双语自由切换**：在右上角「⚙️ 设置」中支持一键切换 **🇨🇳 简体中文（闪传）** 与 **🇺🇸 English（Flashdrop）**，全站所有界面、弹窗、状态提示及系统反馈均支持双语实时热切换。
- **📶 热点 / 同 Wi-Fi 零流量极速直传**：当苹果开热点给安卓（或两台设备连同一 Wi-Fi）时，自动匹配局域网内网 IP 建立 WebRTC P2P 通道，原画无损、不耗费手机流量。
- **🌍 5G 异网自动穿透与可靠中继**：当设备处于完全不同的移动网络时，自动经由国内高速 STUN 节点（腾讯 / 小米 / Cloudflare）穿透或走端到端加密滑动窗口中继。
- **📱 多设备同时在线（4+ 台设备协同）**：支持苹果手机、安卓手机、平板（iPad / 安卓平板）、电脑（Mac / Windows）同时在线，可一键 **「📡 全部设备」群发** 或 **单选指定设备私发**。
- **🔄 个人常用码 ⇄ 朋友临时码一键切换**：平时使用个人专属 6 位常用码自动秒连；分享网址给朋友时可一键生成「临时新码」面对面互传，传完一键切回个人常用码，频道与密钥 100% 隔离。
- **📋 文字 / 剪贴板直传 & 智能提取**：
  - 自动识别文本中的 **4~8 位验证码（OTP）** 与 **网址链接**，生成「复制验证码」「打开链接」快捷按钮。
  - 支持输入框「长按粘贴即自动发送」、电脑端全局 `Ctrl+V` / `Cmd+V` 粘贴截图或文件即刻秒传。
  - 支持 iPhone 快捷指令 **`?sendText=` 轻点手机背面两下秒传剪贴板**。
- **🖼️ 原图时间保留 & 批量无损打包**：
  - 内置 JPEG EXIF 时间戳解析与恢复引擎（`exifHelper`），解决安卓发图给苹果相册后拍摄时间变成当天的问题。
  - 支持收到多张照片/多个文件后一键 **「📦 打包 ZIP」** 无损合并下载，或 iOS 一键批量存相册。
  - 支持音视频页面内直接预览播放、大文件传输防自动息屏（WakeLock）、断网一键「🔄 重发」、浅色/夜间深色模式切换。

### 🏗️ 隐私与底层架构
- **完全独立运行（Serverless 单文件架构）**：前端打包为零外部运行时依赖的单文件 `index.html`，托管于 GitHub Pages，不绑定任何私有后端，任何时候打开网址即可使用。
- **端到端加密（PBKDF2 + AES-256-GCM）**：所有配对握手信令、剪贴板文字与中继分片均使用基于当前 6 位配对码本地派生的 AES-256-GCM 密钥在设备本地加解密，服务器不留存任何用户数据。
- **双通道自适应传输引擎**：优先建立 WebRTC DataChannel 局域网/P2P 高速直连；在严格对称型 NAT 防火墙下自动无感回退至「QoS 1 + 8KB 分片 + 240KB 滑动窗口分段签收与漏包精准重传」加密中继通道，确保 100% 传输成功率。

---

## 三、常见问题与原理解答（Q&A）

### Q1：为什么有时候传图片很快（几秒一张），有时候却比较慢（几百 KB/s）？限制传输速率的原因是什么？

传图片速度差异的核心在于**当时两台设备走的是哪一条传输通道**（可在接收记录中观察是否带有黄色的 **「加密中继」** 标签）：

1. **最常见的原因：退化到了「保底加密中继」通道（约 150 ~ 220 KB/s）**
   - 当两台手机因为网络防火墙拦截，没能建立点对点直连（WebRTC P2P）时，为了保证 **100% 一定能传过去**，软件会自动切换到公共免费信令服务器（EMQX / HiveMQ）做「加密中继」。
   - **为什么中继会限速？** 免费公共 MQTT 服务器对单设备的消息频率有限流保护（发太快会被服务器直接断开或丢包）。因此在 v6.0 滑动窗口协议中，中继通道设定了流控保护：**每片切分 8 KB + 每片间隔 35 毫秒 + 每发送 240 KB（30 片）暂停并等待接收方核对签收一次**。理论最高速率为 `8 KB ÷ 0.035 s ≈ 220 KB/s`，传输一张 3~4 MB 的原图大约需要 15~20 秒。
2. **为什么有时候没能走上「高速直连（5 ~ 30 MB/s）」？**
   - **两边各自使用 5G/4G 移动流量（运营商对称型 NAT 防火墙）**：国内三大运营商的 5G 基站普遍采用对称型 NAT，严禁外部设备直接往手机打洞连入。此时若未配置中转服务器（TURN），就无法建立 P2P 直连，只能回退到慢速的加密中继。
   - **苹果 iOS Safari 与部分安卓浏览器（如夸克）的「私有地址隐藏（mDNS）」**：现代手机浏览器出于隐私保护，有时会把局域网真实 IP（如 `172.20.10.1`）隐藏为虚拟域名（`xxxx.local`），而部分安卓浏览器内核无法解析苹果的 `.local` 地址，导致局域网直连握手失败，退回到了慢速中继。
   - **还没等 P2P 握手完成就立刻点了发送**：刚打开网页的前 1~3 秒，「信令在线」已经先连上了，但底层的「局域网/P2P 高速管道」还在后台打洞协商。如果第 1 秒就立刻选图发送，当时高速管道尚未打通，就会直接走慢速中继通道。
3. **💡 怎么让它每次都跑满高速直连？**
   - **看一眼顶部状态或设备名旁边的绿字标签**：等顶部连接状态变成 **「热点 / 局域网极速直连」** 或 **「跨网 P2P 点对点高速直连」**（或设备名旁边出现绿色的 **「免流 / 直连」** 小标）后再点发图；若未出现，点击旁边的 **「🔄 刷新连接」** 即可重新触发打洞。
   - **苹果开热点给安卓时**：连上热点后点一下顶部的 **「刷新连接」**，让两台手机在热点局域网内重新交换一次内网地址，速度立刻可飙升至几 MB/s 到几十 MB/s。
   - **纯 5G 异网传大视频/大量原图时**：可在右上角 **「⚙️ 设置 → 高级：自定义异网大文件 TURN 节点」** 中填入免费的 Cloudflare TURN 凭证，即可在纯 5G 异网下也跑满高速带宽。

---

### Q2：我之前有时候会通过两台手机之间的蓝牙传输数据，这种是什么？和「闪传 Flashdrop」有什么区别？

日常所说的手机「蓝牙传文件」，其实分为**两种完全不同的底层技术**（一种是真蓝牙，非常慢；另一种是「披着蓝牙外衣的隐藏 Wi‑Fi 直连」，速度极快）：

1. **第一种：真正的「纯蓝牙传输」（Bluetooth OPP 协议）—— 速度很慢**
   - **底层原理**：数据完全走蓝牙无线电波（2.4GHz 窄频通道）。
   - **实际速度**：经典蓝牙（Bluetooth EDR）的实际文件传输速率只有 **150 ~ 250 KB/s**（和闪传的「保底加密中继」速度差不多），传一张 5 MB 的原图需要 20 多秒，传视频则需要数分钟。
   - **为什么苹果和安卓之间不能用？** 苹果出于安全与生态限制，**将 iPhone 的蓝牙文件传输协议（OPP）直接阉割封死**——iPhone 的蓝牙只允许连接耳机、手表、键盘，不允许和安卓手机配对传照片或文件。
2. **第二种：苹果「隔空投送 (AirDrop)」或安卓「互传联盟 (Quick Share / 小米华为互传)」—— 表面用蓝牙，实际走隐藏 Wi-Fi**
   - **真实原理（蓝牙握手 + 隐藏 Wi-Fi Direct 传输）**：
     1. **蓝牙只负责「打招呼」**：两台手机靠近时，先用低功耗蓝牙（BLE）互相发现对方，交换加密密钥和临时无线网卡地址（耗时约 0.5 秒）。
     2. **后台偷偷开启「隐藏热点」传数据**：握手成功的瞬间，两台手机的 Wi‑Fi 芯片会在后台建立一条点对点的隐藏无线通道（苹果叫 **AWDL**，安卓叫 **Wi‑Fi Direct / P2P**），速度高达 **20 ~ 80 MB/s**（比纯蓝牙快 100 倍以上）。
   - **为什么苹果和安卓之间不能直接用？** 苹果的 AWDL 协议与安卓的互传协议互不兼容，且手机浏览器出于沙箱安全限制无法直接调用底层的隐藏 Wi‑Fi Direct 芯片。
3. **💡 这跟我们的「闪传 Flashdrop」是什么关系？**
   - **闪传（Flashdrop）本质上就是用 Web 技术复刻了一套跨系统的 AirDrop（隔空投送）**：

| 对比维度 | 苹果 AirDrop / 安卓互传 | ⚡ 闪传 Flashdrop |
| :--- | :--- | :--- |
| **第 1 步：怎么找到对方（打招呼）** | 靠 **蓝牙** 近距离广播握手 | 靠 **6 位配对码 + 云端加密信令** 握手（不限距离） |
| **第 2 步：怎么高速传大图/大文件** | 手机自动拉起 **隐藏 Wi‑Fi 直连** | 苹果开热点给安卓（或同 Wi‑Fi）走 **WebRTC 局域网直连** |
| **跨系统能力** | ❌ 苹果 ⇄ 安卓互相封闭不通 | ✅ **苹果 ⇄ 安卓 ⇄ 平板 ⇄ 电脑 全通** |
| **距离限制** | ❌ 必须在几米之内 | ✅ 热点直连免流量，异地 5G 也能跨网传 |

---

### Q3：那还有没有别的办法，能像闪传一样在「苹果 ⇄ 安卓 ⇄ 平板 ⇄ 电脑」之间互传内容，甚至更快、更安全、更好？

如果不局限于「免装 App 的纯网页（Web PWA）」，愿意在每台设备上**安装一个专门的原生 App**，业界有以下 3 种能突破浏览器沙箱限制、做到**更快（跑满无线网卡物理极限 50~100 MB/s）、更稳、甚至完全断网离线也能传**的进阶方案：

1. **方案一：LocalSend（开源跨平台「真·隔空投送」原生 App 天花板）**
   - **为什么比网页版更快、更稳？** 作为安装在系统里的原生客户端（iOS App Store 免费下载，Android / macOS / Windows 全平台支持），能直接获取设备真实局域网 IP（不受浏览器 `.local` mDNS 隐私屏蔽影响），并直接在手机本地启动底层 **HTTPS / TCP 高速服务器**。同 Wi‑Fi 或苹果开热点给安卓时速率稳定在 **40 ~ 90 MB/s**，批量发送数百张原图可直接流式写入苹果相册，且 **100% 纯离线可用**。
   - **局限性**：每台设备均需预先安装客户端，且**不支持异地 / 5G 异网互传**（仅限同局域网或热点）。
2. **方案二：Tailscale（组建个人专属「WireGuard 加密虚拟局域网」）**
   - **核心原理（系统级内网穿透）**：在苹果、安卓、平板、电脑上安装 **Tailscale**（个人免费版支持 100 台设备），在操作系统虚拟网卡层为每台设备分配固定虚拟内网 IP，并通过底层 UDP 端口打洞将全球各地的设备拉入同一个加密局域网。
   - **自带「Taildrop」跨网投送**：无论两台设备是否在同一城市、连的是 Wi‑Fi 还是 5G，直接在系统分享菜单选择 **Tailscale** 即可点对点直传原图与大文件，采用 WireGuard 军工级端到端加密，异网直连速率可跑满 5G 上传带宽（**5 ~ 30 MB/s**）。
3. **方案三：Syncthing / 私有 NAS（全自动无感后台同步）**
   - 在安卓、苹果（Möbius Sync）、电脑上配置同一个共享同步目录。手机拍完照片或放入文件夹后，只要连上热点或家里的 Wi‑Fi，后台即自动静默增量同步到苹果与电脑硬盘中。

#### 📊 四大跨端方案终极横评：不同场景怎么选？

| 方案名称 | 最佳适用场景 | 实际速率表现 | 是否需装 App | 能否 5G 异网传 | 临时传给朋友便捷度 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **⚡ 闪传 Flashdrop (本项目)** | **日常文字/验证码/几张原图秒传、临时与朋友或新电脑互传** | 热点直连 **5~25 MB/s**<br>中继保底 **0.2 MB/s** | **✅ 免安装**<br>（打开网址即用） | **✅ 支持** | **⭐⭐⭐⭐⭐**<br>（扫码即传，无需装软件） |
| **🟢 LocalSend (原生 App)** | **同 Wi-Fi / 热点下批量传几百张原图、数 GB 大视频** | **40 ~ 90 MB/s**<br>（跑满网卡极限） | ❌ 需每台设备装 App | ❌ 不支持<br>（仅限同局域网/热点） | ⭐⭐<br>（需对方先下载安装 App） |
| **🛡️ Tailscale (虚拟专网)** | **个人名下多台设备异地 5G 互传大文件 / 远程访问电脑** | **10 ~ 80 MB/s** | ❌ 需装 App 并登同一号 | **✅ 极强**<br>（系统级底层穿透） | ⭐<br>（仅限本人设备） |
| **🔌 Type-C 双头闪存盘/数据线** | **一次性导出几十 GB 的 4K / ProRes 原片素材** | **100 ~ 1000 MB/s** | ✅ 插线即读 | ❌ 需物理连接 | ⭐⭐⭐⭐ |

- **💡 黄金组合建议**：日常传文字/验证码/链接、随手传几张照片、或跟朋友/同事电脑临时互传直接用 **`闪传 Flashdrop`**；外出旅行拍了几百张原图 + 十几个 4K 大视频需要一次性导素材时搭配 **`LocalSend`**，两者互补就是最完美的跨生态方案。

---

## 四、升级版本演进（v1.0 → v8.0）

- **🌱 v1.0（基础原型）**：实现苹果⇄安卓热点免流直连与异网穿透双模架构、6 位私密配对码与二维码秒绑、以及基于配对码的 PBKDF2 + AES-256-GCM 端到端加密传输。
- **🚀 v2.0（系统级直达与多媒体）**：新增安卓 PWA 系统分享菜单直发（`share_target` + Service Worker + IndexedDB 收件箱）、iPhone 快捷指令 `?sendText=` 轻点背面两下秒传剪贴板、4~8 位验证码与网址智能提取按钮、以及音视频页面内直接预览播放。
- **🖥️ v3.0（多端协同与临时码隔离）**：突破一对一限制，升级支持 **iPhone + 安卓手机 + 平板 + 电脑** 4 台及以上设备同时在线（支持群发全部设备或单选私发）；加入电脑端拖拽上传与全局 `Ctrl+V` 截图粘贴秒传；配对弹窗新增 **「个人常用码 ⇄ 朋友临时新码」** 一键切换。
- **🛠️ v4.0（连接防抖与原图时间恢复）**：移除国内不通的 Google STUN，切换为 **腾讯（`stun.qq.com`）、小米（`stun.miwifi.com`）与 Cloudflare** 高速节点；采用每设备独立私信收件箱频道与后台静默心跳，根治「连接中 ⇄ 已连接」反复横跳；内置纯前端 JPEG EXIF 时间戳解析与恢复引擎（`exifHelper`），解决安卓发图给苹果相册后拍摄时间变成当天的问题。
- **🛡️ v5.0 ~ v6.0（滑动窗口可靠传输与夸克浏览器兼容）**：修复夸克浏览器 WebRTC `RTCSessionDescription`/`RTCIceCandidate` 序列化为空 `{}` 的兼容 Bug；选图首毫秒读入 `Uint8Array` 内存快照防止切后台文件句柄失效；加入局域网 ICE 候选缓存队列；保底加密中继升级为 **QoS 1 + 8KB 分片 + 35ms 流控 + 每 30 片（240KB）滑动窗口分段签收与漏包精准补发协议**（通过 33% 强丢包自动化测试）。
- **✨ v6.5（日常高频实用增强）**：新增 Screen WakeLock 防传大文件自动息屏锁屏、传输失败/取消后一键「🔄 重发」、前端零依赖多文件无损「📦 打包 ZIP」下载、以及右上角浅色/夜间深色模式切换。
- **🎨 v7.0（全端响应式双栏工作台与半透明磨砂 Bento 美学）**：全站图标锁定 `1:1` 正方形防挤压，平板横屏/电脑宽屏（`≥ 768px`）自动切换为左右双栏工作台；彻底移除全局 `...`（`truncate`/`line-clamp`）文字省略截断，改为自然换行完整呈现；合并右上角浅灰下载图标按钮并在 iOS/安卓常驻显示；三大操作按钮升级为 iOS 风格半透明磨砂玻璃色卡；底部新增 GitHub 仓库入口胶囊。
- **🌐 v8.0（中英双语国际化与独立品牌命名 · 最新版）**：中文模式应用名独立显示为 **「闪传」**，英文模式独立显示为 **「Flashdrop」**；在「设置」顶部新增 **「界面语言 / Language」** 实时分段切换器（`🇨🇳 简体中文` / `🇺🇸 English`），实现全站所有界面、弹窗、网络状态及动态 Toast 提示 100% 双语化。

---

<br/>

# 🇺🇸 Flashdrop (English)

## 1. Introduction

**Flashdrop** (Chinese brand name: **闪传**) is a zero-config, app-free, end-to-end encrypted cross-device instant transfer Web PWA.  
Built specifically for **🍎 Apple (iPhone / iPad) ⇄ 🤖 Android (Phone / Tablet) ⇄ 💻 PC (Mac / Windows)**, it supports zero-data direct transfer over Personal Hotspot or same Wi-Fi LAN, cross-network 5G P2P traversal, and instant **English / 简体中文** language switching.

### 🚀 3-Step Quick Start
1. **Open the Web App**: Visit [https://bibubibu1106.github.io/flashdrop/](https://bibubibu1106.github.io/flashdrop/) on your phones, tablet, or computer (tap the top-right **Download icon** to add to your Home Screen; tap the **Settings gear icon** to switch between English and Simplified Chinese or toggle Dark Mode).
2. **Pair Once**: Tap the Pair Code bar to scan the QR code or enter the same **6-digit Pair Code** across your devices (saved locally for automatic reconnection).
3. **Transfer Instantly**:
   - **Text / OTP / Links**: Tap `Read & Send Local Clipboard` or paste into the input box.
   - **Photos / Videos / Original Files**: Tap `Photos / Videos` for multi-select gallery upload, or `Original Files` to preserve full EXIF metadata (drag & drop or `Ctrl+V` paste on Tablet/PC).

---

## 2. Key Highlights & Technical Architecture

### ✨ Key Highlights
- **🌐 Instant Bilingual Switching**: Seamlessly switch between **🇺🇸 English (Flashdrop)** and **🇨🇳 简体中文 (闪传)** inside **⚙️ Settings**. Every screen, modal, status indicator, and toast notification updates in real time without page reload.
- **📶 Zero-Data Hotspot & LAN Direct Transfer**: When an iPhone shares its Personal Hotspot with an Android device (or when devices share the same Wi-Fi), Flashdrop automatically discovers local LAN ICE candidates for high-speed WebRTC P2P transfer with zero cellular data consumption.
- **🌍 Cross-Network 5G P2P & Reliable Sliding-Window Relay**: Automatically traverses NAT via high-speed STUN nodes (Tencent / Xiaomi / Cloudflare) or falls back to an AES-256-GCM encrypted sliding-window relay channel with 100% delivery verification.
- **📱 Multi-Device Mesh (4+ Simultaneous Devices)**: Connect iPhone, Android phone, iPad/Android tablet, and Mac/Windows PC simultaneously. Broadcast to **📡 All Devices** at once or select a single target device.
- **🔄 Personal Home Code ⇄ Temporary Friend Code**: Use your persistent 6-digit Home Code for instant daily auto-connect, or generate a one-tap **Temp Code** when sharing with friends face-to-face—100% isolated channels and encryption keys.
- **📋 Instant Text / Clipboard Transfer & Smart Extraction**:
  - Automatically detects **4–8 digit OTP verification codes** and **URLs**, rendering one-tap `Copy Code` and `Open Link` buttons.
  - Supports **Auto-Send on Paste**, desktop `Ctrl+V` / `Cmd+V` screenshot/file paste, and iOS **`?sendText=` Back-Tap Shortcut** instant clipboard sharing.
- **🖼️ Original EXIF Date Preservation & Lossless ZIP Archiving**:
  - Built-in binary JPEG EXIF parser & injector (`exifHelper`) restores `DateTimeOriginal` timestamps so photos sent from Android to iPhone appear at their original capture date in Apple Photos.
  - One-tap **📦 ZIP All** lossless archive download for multiple received files, built-in video/audio preview player, Screen WakeLock, one-tap retry, and Dark Mode.

### 🏗️ Privacy & Technical Architecture
- **100% Standalone Serverless Single-File Architecture**: Packaged as a self-contained single-file `index.html` hosted on GitHub Pages with zero proprietary backend dependencies.
- **End-to-End Encryption (PBKDF2 + AES-256-GCM)**: All signaling handshakes, clipboard texts, and relay chunks are encrypted locally on your device using keys derived from your 6-digit Pair Code. No data is ever stored on any server.
- **Dual-Path Adaptive Transport Engine**: Prioritizes direct WebRTC DataChannel over Hotspot/LAN/P2P; seamlessly falls back under strict Symmetric NAT firewalls to a **QoS 1 + 8KB chunked + 240KB sliding-window ACK & selective retransmission** encrypted relay protocol for 100% delivery reliability.

---

## 3. Frequently Asked Questions (Q&A)

### Q1: Why is photo transfer sometimes super fast (several MB/s) and sometimes slower (~200 KB/s)? What limits the transfer speed?

The speed difference depends on **which transport channel your devices are currently using** (check if the transfer item shows a yellow **`Encrypted Relay`** badge):

1. **Fallback to the "Encrypted Relay" Channel (~150–220 KB/s)**:
   - When strict network firewalls prevent a direct WebRTC P2P connection, Flashdrop automatically falls back to public serverless MQTT brokers (EMQX / HiveMQ) to guarantee **100% delivery success**.
   - Public MQTT brokers enforce strict rate limits per client. To prevent disconnection or packet loss, v6.0 uses flow control: **8 KB per chunk + 35 ms pacing + sliding-window verification every 240 KB (30 chunks)**, yielding a theoretical maximum of `8 KB ÷ 0.035 s ≈ 220 KB/s` (~15–20 seconds for a 3–4 MB original photo).
2. **Why High-Speed Direct P2P (5–30 MB/s) Sometimes Doesn't Connect**:
   - **Cellular 5G/4G Symmetric NAT**: Mobile carriers often use Symmetric NAT firewalls that block incoming direct UDP hole-punching unless a TURN relay server is configured.
   - **Browser mDNS Local IP Masking (`.local`)**: iOS Safari and some Android browsers (such as Quark) sometimes mask private LAN IPs (e.g., `172.20.10.1`) with `.local` mDNS hostnames that the other browser cannot resolve.
   - **Sending Before P2P Handshake Finishes**: Signaling connects in <1 second, while WebRTC ICE negotiation takes 1–3 seconds in the background.
3. **💡 How to Maximize High-Speed Direct Transfer**:
   - Wait until the top banner shows **`Hotspot / LAN Direct`** or **`Cross-Network P2P Direct Connected`** before selecting files, or tap **`🔄 Reconnect`** after joining a Personal Hotspot.
   - For frequent large video transfers over separate 5G networks, add a free Cloudflare TURN credential under **`⚙️ Settings → Advanced TURN Server`**.

---

### Q2: Sometimes I transfer data between two phones via Bluetooth—what is that under the hood, and how does it compare to Flashdrop?

Mobile "Bluetooth file transfer" actually refers to **two completely different technologies**:

1. **Classic Pure Bluetooth Transfer (Bluetooth OPP) — Very Slow**:
   - Uses 2.4GHz classic Bluetooth radio directly (`150–250 KB/s`). Furthermore, **Apple completely blocks Bluetooth OPP file transfer on iOS**, so iPhones cannot send or receive files with Android via classic Bluetooth.
2. **Apple AirDrop & Android Quick Share — Bluetooth Handshake + Hidden Wi-Fi Direct**:
   - When same-brand phones transfer photos at `20–80 MB/s`, Bluetooth (BLE) is only used for the first 0.5 seconds to discover nearby devices and exchange keys. The actual file transfer runs over a hidden peer-to-peer Wi-Fi channel (**AWDL** on Apple, **Wi-Fi Direct** on Android). Because Apple's AWDL and Android's Quick Share are proprietary and incompatible, they cannot talk to each other.
3. **💡 How Flashdrop Compares**:
   - **Flashdrop is essentially a cross-platform, web-based AirDrop**:

| Comparison | Apple AirDrop / Android Quick Share | ⚡ Flashdrop |
| :--- | :--- | :--- |
| **Step 1: Device Discovery** | Nearby **Bluetooth (BLE)** broadcast | **6-digit Pair Code + Encrypted Cloud Signaling** (No distance limit) |
| **Step 2: High-Speed Data Transfer** | Hidden **Wi-Fi Direct / AWDL** | **WebRTC LAN Direct** over Personal Hotspot or same Wi-Fi |
| **Cross-Ecosystem Support** | ❌ Incompatible between iOS & Android | ✅ **iPhone ⇄ Android ⇄ Tablet ⇄ PC** |
| **Distance Limit** | ❌ Within a few meters | ✅ Zero-data over Hotspot/LAN, plus remote 5G transfer |

---

### Q3: Are there other ways to transfer content across Apple ⇄ Android ⇄ Tablet ⇄ PC that are even faster or better?

If you are willing to **install a dedicated native app** on every device (rather than using a zero-install Web PWA), here are the 3 best native alternatives and how they compare:

1. **LocalSend (Best Native Open-Source Cross-Platform AirDrop)**:
   - Runs a native local HTTPS/TCP server bypassing browser sandboxes and mDNS masking, reaching **40–90 MB/s** over Wi-Fi or Hotspot and working **100% offline** (even on an airplane with no internet). Requires installing the app on every device and only works on the same LAN/Hotspot.
2. **Tailscale (Personal Encrypted WireGuard Mesh VPN + Taildrop)**:
   - Connects all your personal devices across different cities/5G networks into a virtual private LAN using OS-level WireGuard UDP hole-punching (`5–30+ MB/s` over 5G). Requires logging into the same account on all devices.
3. **Syncthing / Private NAS (Automated Background Folder Sync)**:
   - Automatically syncs designated folders in the background whenever devices connect to Wi-Fi or Hotspot without manual sending.

| Solution | Best Use Case | Real-World Speed | App Install Required? | Works Over 5G Cross-Network? | Sharing with Friends |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **⚡ Flashdrop (This Project)** | **Instant text/OTP/photo sharing, temporary sharing with friends or new PCs** | Hotspot LAN **5–25 MB/s**<br>Relay **0.2 MB/s** | **✅ No Install**<br>(Open URL & use) | **✅ Yes** | **⭐⭐⭐⭐⭐**<br>(Scan QR & send) |
| **🟢 LocalSend (Native App)** | **Bulk transferring hundreds of RAW photos or multi-GB 4K videos on LAN/Hotspot** | **40–90 MB/s**<br>(Max Wi-Fi speed) | ❌ Install on all devices | ❌ No<br>(Same LAN/Hotspot only) | ⭐⭐<br>(Friend must install app) |
| **🛡️ Tailscale (Mesh VPN)** | **Personal devices frequently transferring large files over remote 5G** | **10–80 MB/s** | ❌ Install & same login | **✅ Excellent**<br>(OS-level NAT traversal) | ⭐<br>(Personal devices only) |
| **🔌 Dual-Plug USB-C Drive/Cable** | **Offloading tens of GBs of ProRes / 4K video footage** | **100–1000 MB/s** | ✅ Plug & play | ❌ Physical cable | ⭐⭐⭐⭐ |

- **💡 Best Combo Recommendation**: Use **`Flashdrop`** for daily text/OTP/link sharing, quick photo transfers, and instant sharing with friends' phones or computers without installing software; pair it with **`LocalSend`** when offloading ratusan of RAW photos or multi-gigabyte 4K videos over a hotspot.

---

## 4. Version Evolution Changelog (v1.0 → v8.0)

- **🌱 v1.0 (Core Prototype)**: WebRTC P2P direct transfer across iOS & Android over Hotspot/LAN and cross-network; 6-digit pair code, QR code binding, and PBKDF2 + AES-256-GCM end-to-end encryption.
- **🚀 v2.0 (System-Level Shortcuts & Media)**: Android PWA `share_target` system share-sheet integration, iOS `?sendText=` Back-Tap clipboard shortcut, smart OTP/URL extraction, and inline video/audio preview.
- **🖥️ v3.0 (Multi-Device Mesh & Temp Code Isolation)**: Upgraded from 1-on-1 to 4+ simultaneous devices (Phone + Tablet + PC), broadcast/targeted sending, desktop `Ctrl+V` screenshot paste, and one-tap switching between `Personal Home Code` and `Temporary Friend Code`.
- **🛠️ v4.0 (Connection Stability & EXIF Preservation)**: Replaced blocked Google STUN with high-speed domestic/global STUN nodes (`stun.qq.com`, `stun.miwifi.com`, Cloudflare), dedicated per-device private signaling inbox topics, silent background heartbeats, and automatic JPEG EXIF `DateTimeOriginal` restoration.
- **🛡️ v5.0 ~ v6.0 (Sliding-Window Reliable Transfer & Quark Browser Fix)**: Fixed WebRTC `RTCSessionDescription`/`RTCIceCandidate` empty `{}` serialization bug on Quark Browser, first-millisecond `Uint8Array` memory snapshot on file selection, early LAN ICE candidate queueing, and a **30-chunk (240KB) sliding-window ACK + selective retransmission protocol** verified under 33% simulated packet loss.
- **✨ v6.5 (Daily Quality-of-Life Enhancements)**: Screen WakeLock API to prevent sleep during large transfers, one-tap `Retry / Resend`, zero-dependency client-side `ZIP All` bundler, and Dark Mode.
- **🎨 v7.0 (Responsive Dual-Column Workspace & Frosted Bento UI)**: Responsive 12-column desktop/tablet dual-pane layout (`≥768px`), `1:1` aspect-square icon locks, complete removal of `...` (`truncate`/`line-clamp`) text truncation in favor of natural wrapping, unified top-right action icons, translucent frosted glass Bento action cards, and footer GitHub repository link.
- **🌐 v8.0 (Bilingual i18n Edition — `闪传` / `Flashdrop` · Latest)**: Independent brand naming (**`闪传`** in Simplified Chinese, **`Flashdrop`** in English), live language switcher in Settings (`🇨🇳 简体中文` / `🇺🇸 English`), and 100% bilingual coverage across all UI components, modals, status banners, and toast notifications.
