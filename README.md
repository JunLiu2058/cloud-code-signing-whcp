<!--
=============================================
  LANGUAGE / 语言选择
  🇬🇧 English  → scroll down to [English Version ↓]
  🇨🇳 中文     → scroll down to [中文版本 ↓]
=============================================
-->

<p align="center">
  <a href="#-english-version"><img src="https://img.shields.io/badge/🇬🇧-English-dde6ff?style=for-the-badge&labelColor=1a1a2e"></a>
  &nbsp;&nbsp;
  <a href="#-中文版本"><img src="https://img.shields.io/badge/🇨🇳-中文-eff6ff?style=for-the-badge&labelColor=7f1d1d"></a>
</p>

---

# 🌩 Xinhua Cloud Signing

> Zero-upload cloud code signing for Windows drivers & apps.  
> Supports WHCP, Secure Boot, SmartScreen & 360.  
> **Global exclusive Microsoft whitelist mechanism.**  
> FIPS 140-3 certified · 28ms per sign · 197 countries · Hash-only (no file upload)

![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![FIPS](https://img.shields.io/badge/security-FIPS%20140--3-blue)
![WHCP](https://img.shields.io/badge/WHCP-2026%20ready-green)
![Privacy](https://img.shields.io/badge/privacy-zero--upload-orange)

---

## 🇬🇧 English Version

### 🚀 Why Xinhua Cloud Signing?

Traditional code signing = **upload entire binary** (GBs) + USB token + local private key risk.  
We do it differently:

| Dimension | Traditional Signing | 🌩 Xinhua Cloud Signing |
|-----------|---------------------|------------------------|
| File transfer | Full binary upload | **Hash only (≤32 B)** |
| Private key | Local / USB token | **HSM-backed, never leaves cloud** |
| Speed | Seconds ~ minutes | **≈28 ms** |
| Max file size | Limited by bandwidth | **Hundreds of GB** (hash only) |
| Compliance | Manual EV + cross-sign | **Microsoft whitelist pre-accessed** |
| 2026 WHCP ready | ❌ Painful | ✅ **Already integrated** |

> 🔐 **Your code never leaves your machine.** Only the file digest (SHA-256) is sent — mathematically impossible to reconstruct the original file.

---

### 🏆 Security Credentials

- ✅ **FIPS 140-3** (U.S. highest crypto module standard, NSA-aligned)
- ✅ **HSM-backed key storage** (FIPS-grade)
- ✅ **SHA-256 / RSA-4096 / ECC P-384**
- ✅ Integrated CAs: **DigiCert · GlobalSign · Sectigo · SSL.com · Certum**

---

### 📦 Signing Types

| # | Type | Secure Boot | WHCP | Game | SmartScreen | 360 |
|---|------|:-----------:|:----:|:----:|:-----------:|:---:|
| 1 | App / Installer Signing | ❌ | ❌ | ❌ | ❌ | ❌ |
| 2 | Driver Signing (basic) | ❌ | ❌ | ❌ | ❌ | ❌ |
| 3 | Driver + Secure Boot | ✅ | ❌ | ❌ | ❌ | ❌ |
| 4 | + **WHCP** | ✅ | ✅ | ❌ | ❌ | ❌ |
| 5 | + Game / Anti-cheat | ✅ | ✅ | ✅ | ❌ | ❌ |
| 6 | + SmartScreen Reputation | ✅ | ✅ | ✅ | ✅ | ❌ |
| 7 | + 360 Trust | ✅ | ✅ | ✅ | ✅ | ✅ |
| 8 | Private Custom (per-day / branded) | ✅ | ✅ | ✅ | ✅ | ✅ |

> 💡 **Type 4+** is what most vendors will *need* after **April 2026**.

---

### ⚠️ Microsoft WHCP & 2026 Policy Change

Microsoft officially announced:

> *"With the **April 2026 security update**, kernel drivers signed via the expired cross-signing program are **no longer trusted by default**."*

**What breaks in 2026:**
- ❌ Cross-signed drivers blocked on Win 11 24H2+ / Server 2025
- ❌ Legacy EV + USB token workflows insufficient for WHCP
- ❌ New kernel drivers → **must go through WHCP**

✅ **Xinhua Cloud Signing already sits on Microsoft's whitelist** — global exclusive.

#### 📌 Official Links
- Windows Driver Policy: https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443
- Advancing Windows Driver Security: https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818
- Driver Code Signing Requirements: https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs
- Hardware Dashboard Getting Started: https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/

---

### 📄 Product Whitepaper (PDF)

Full technical deep-dive — architecture, hash-only flow, WHCP integration, 8-type matrix.  
Optimized for **Adobe Acrobat (flattened / linearized)** — zero rendering lag.

| Action | Link |
|--------|------|
| 📖 Preview | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 Direct Download | [raw link](https://raw.githubusercontent.com/用户名/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

> ⚠️ Replace `用户名` with your GitHub username after push.

---

### 👥 Developer Community — "Kernel Night Lab"

> *Not for product managers. For people who actually read Intel SDM & debug BSOD at 2 AM.*

**We're looking for:**
- 🛠 WDM / WDF driver authors (`.sys` loaded ≥ once)
- 🔬 Reverse engineers / PE format nerds
- 🛡 PatchGuard / HVCI / VBS researchers
- 🚀 CI/CD signing automation folks
- 😤 Anyone rejected by SmartScreen / 360 / WHCP

**What we talk about:**
- Windows kernel internals & IRQL hell
- PatchGuard bypass & defense (research-only)
- Microsoft signing policy change tracking
- Hash-based remote signing architecture
- "That one bug that took 3 nights to find"

#### 🎁 Join Bonus — Free Cloud Signature

Every developer who joins the community gets **1× free production-grade cloud signature** (any type from the table):

- ✅ Zero-upload (hash only)
- ✅ WHCP / Secure Boot / SmartScreen ready
- ✅ Pre-adapted for April 2026 policy
- ✅ No USB token · no private key exposure

> **No forms. No shares. No KPI.**  
> Just: "you hack kernels, we give you signatures."

---

### 🧰 Quick Start

```text
# 1. Compute local digest (NEVER upload the file)
sha256sum mydriver.sys > digest.txt

# 2. Send digest to cloud HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" \
  -d @digest.txt

# 3. Embed returned signature into PE
sign-tool embed mydriver.sys --sig response.sig
```

> Full SDK / CLI will be open-sourced soon — watch this repo ⭐

---

### 📊 Stats Snapshot

| Metric | Value |
|--------|-------|
| 🌍 Countries | **197** |
| ⚡ Median sign time | **28 ms** |
| 📦 Max single-file | **Hundreds of GB** (hash only) |
| 🔒 Files uploaded | **0** |

---

### 📜 License

Product / service: proprietary SaaS.  
This repo (README + docs): **MIT** — feel free to reference / fork the structure.

---

### 🔗 Related

- [Microsoft WHCP / Hardware Dashboard](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/)
- [Driver Signing Requirements](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows Driver Policy (2026)](https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443)

---

> 🧠 *"Code doesn't have to be perfect. But the signature? That has to be bulletproof."*  
> — Xinhua Cloud Signing Team

---

<br><br><br>

---

<p align="center">
  <a href="#-中文版本"><img src="https://img.shields.io/badge/🇨🇳-查看中文版本-eff6ff?style=for-the-badge&labelColor=7f1d1d"></a>
</p>

<br><br>

---

# 🌩 新华云签名

> 零上传云端代码签名，适用于 Windows 驱动与应用。  
> 支持 WHCP、安全启动、SmartScreen 及 360 信任链。  
> **全球独家微软白名单机制。**  
> FIPS 140-3 认证 · 单次签名 28ms · 覆盖 197 国 · 仅传哈希零上传

![平台](https://img.shields.io/badge/平台-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![安全](https://img.shields.io/badge/安全-FIPS%20140--3-blue)
![WHCP](https://img.shields.io/badge/WHCP-2026%20就绪-green)
![隐私](https://img.shields.io/badge/隐私-零上传-orange)

---

## 🇨🇳 中文版本

### 🚀 为什么选新华云签名？

传统签名 = **上传完整文件**（GB 级）+ USB Key + 本地私钥风险。  
我们换了一种方式：

| 对比维度 | 传统签名 | 🌩 新华云签名 |
|-----------|---------------------|------------------------|
| 文件传输 | 完整文件上传 | **仅传哈希（≤32 字节）** |
| 私钥管理 | 本地 / USB Key | **HSM 托管，不出云** |
| 签名速度 | 秒级 ~ 分钟级 | **≈28 毫秒** |
| 最大文件 | 受带宽限制 | **数百 GB**（仅哈希） |
| 合规流程 | 手动 EV + 交叉签名 | **已接入微软白名单** |
| 2026 WHCP 适配 | ❌ 痛苦适配 | ✅ **已集成** |

> 🔐 **你的代码永远不会离开你的机器。** 仅传输文件摘要（SHA-256）—— 数学上无法从哈希还原原始文件。

---

### 🏆 安全资质

- ✅ **FIPS 140-3**（美国最高加密模块标准，对标 NSA）
- ✅ **HSM 硬件安全模块**托管私钥（FIPS 级）
- ✅ **SHA-256 / RSA-4096 / ECC P-384**
- ✅ 集成 CA：**DigiCert · GlobalSign · Sectigo · SSL.com · Certum**

---

### 📦 签名类型一览

| 编号 | 类型 | 安全启动 | WHCP | 游戏 | SmartScreen | 360 |
|---|------|:-----------:|:----:|:----:|:-----------:|:---:|
| 1 | 应用 / 安装包签名 | ❌ | ❌ | ❌ | ❌ | ❌ |
| 2 | 驱动签名（基础） | ❌ | ❌ | ❌ | ❌ | ❌ |
| 3 | 驱动签名（安全启动） | ✅ | ❌ | ❌ | ❌ | ❌ |
| 4 | + **WHCP** 策略签名 | ✅ | ✅ | ❌ | ❌ | ❌ |
| 5 | + 游戏 / 反作弊 | ✅ | ✅ | ✅ | ❌ | ❌ |
| 6 | + SmartScreen 信誉 | ✅ | ✅ | ✅ | ✅ | ❌ |
| 7 | + 360 信任 | ✅ | ✅ | ✅ | ✅ | ✅ |
| 8 | 私人定制（按天/个性名称） | ✅ | ✅ | ✅ | ✅ | ✅ |

> 💡 **类型 4 及以上** 是 2026 年 4 月后大多数厂商的 *刚需*。

---

### ⚠️ 微软 WHCP 与 2026 策略变更

微软官方公告：

> *"从 **2026 年 4 月安全更新**起，通过已过期交叉签名程序签名的 kernel 驱动将**默认不再被信任**。"*

**2026 年哪些会失效：**
- ❌ 交叉签名驱动将在 Win 11 24H2+ / Server 2025 上被拦截
- ❌ 传统 EV + USB Key 流程无法满足 WHCP 要求
- ❌ 新内核驱动 ***必须*** 走 WHCP

✅ **新华云签名已接入微软白名单** —— 全球独家。

#### 📌 官方链接
- Windows 驱动策略：https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443
- 推进 Windows 驱动安全：https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818
- 驱动代码签名要求：https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs
- 硬件仪表板入门：https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/

---

### 📄 产品白皮书（PDF）

完整技术白皮书 —— 架构、仅哈希流程、WHCP 集成、8 类签名矩阵。  
针对 **Adobe Acrobat 扁平化/线性化** 优化，零渲染卡顿。

| 操作 | 链接 |
|--------|------|
| 📖 在线预览 | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 直链下载 | [raw 链接](https://raw.githubusercontent.com/用户名/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

> ⚠️ 推送后请将 `用户名` 替换为你的 GitHub 用户名。

---

### 👥 开发者社区 ——「内核夜校」

> *这里不属于产品经理，只属于那些愿意读 Intel SDM、凌晨两点还在调 BSOD 的人。*

**我们在找这样的人：**
- 🛠 写过 `.sys` 的人（哪怕只成功加载过一次）
- 🔬 喜欢逆向工程 / 研究 PE 格式的人
- 🛡 研究过 PatchGuard / HVCI / VBS 的人
- 🚀 搞 CI/CD 签名自动化的同学
- 😤 被 SmartScreen / 360 / WHCP 拒绝过的人

**我们在聊这些：**
- Windows 内核原理 & IRQL 地狱
- PatchGuard 对抗与防御（仅研究用途）
- 微软签名策略变化追踪
- 基于哈希的远程签名架构
- "那个花了三个晚上才找到的 Bug"

#### 🎁 加入福利：免费云签名

所有加入社区的开发者，**免费获赠 1 份正版云签名**（类型任选）：

- ✅ 零上传（仅哈希）
- ✅ WHCP / 安全启动 / SmartScreen 全支持
- ✅ 提前适配 2026 年 4 月策略
- ✅ 无需 USB Key · 私钥不出云

> **不需要填表。不需要转发。不卖课。**  
> 你搞内核，我们送签名。

---

### 🧰 快速开始

```text
# 1. 本地计算摘要（绝不上传文件）
sha256sum mydriver.sys > digest.txt

# 2. 将摘要发送至云端 HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" \
  -d @digest.txt

# 3. 将返回的签名嵌入 PE 文件
sign-tool embed mydriver.sys --sig response.sig
```

> 完整 SDK / CLI 即将开源 —— 点个 Star 关注本仓库 ⭐

---

### 📊 关键数据

| 指标 | 数值 |
|--------|-------|
| 🌍 覆盖国家 | **197** |
| ⚡ 中位签名耗时 | **28 ms** |
| 📦 最大单文件 | **数百 GB**（仅哈希） |
| 🔒 文件上传量 | **0** |

---

### 📜 许可证

产品/服务：专有 SaaS。  
本仓库（README + 文档）：**MIT 协议** —— 可自由引用或 Fork 结构。

---

### 🔗 相关链接

- [微软 WHCP / 硬件仪表板](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/)
- [驱动签名要求](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows 驱动策略](https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略)

---

> 🧠 *"代码可以不完美，但签名一定要无懈可击。"*  
> —— 新华云签名团队

<br><br><br>

---

<p align="center">
  <a href="#-english-version"><img src="https://img.shields.io/badge/🇬🇧-Back%20to%20English-dde6ff?style=for-the-badge&labelColor=1a1a2e"></a>
  &nbsp;&nbsp;
  <a href="#-中文版本"><img src="https://img.shields.io/badge/🇨🇳-返回中文-eff6ff?style=for-the-badge&labelColor=7f1d1d"></a>
</p>
