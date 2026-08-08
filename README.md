## [v3.0.7.1] - 2026-08-08 · Client Slimming & Runtime Efficiency
- **Changed**: Removed redundant init paths; `MyAPI` unified into single off-GUI-thread entry
- **Changed**: Flattened `TTask`/`TThread.Queue` callbacks, eliminated intermediate hash buffers
- **Performance**: Cold-start memory −5~8% vs v3.0.7.0, GUI thread does zero crypto/IO during sign
- **Compatibility**: Fully aligned with v3.0.7.0 server enforcement (≤ v3.0.6.3 still rejected)
- **中文**: 精简客户端冗余代码，统一异步入口；运行期零主线程加密/IO，冷启动内存再降 5–8%；服务端强制策略同 v3.0.7.0
<!--
=============================================
  Xinhua Cloud Signing / 新华云签名
  Main README — Bilingual (EN + 中文)
  Organization: Xinhua-Cloud-Sign
  Repo: Xinhua-Cloud-Sign/cloud-code-signing-whcp
  PDF: docs/Xinhua-Cloud-Sign-WhitePaper.pdf
  Latest Version: v3.0.7.0
=============================================
-->

<p align="center">
  <a href="#-english-version"><img src="https://img.shields.io/badge/🇬🇧-English-dde6ff?style=for-the-badge&labelColor=1a1a2e" alt="English"></a>
  &nbsp;&nbsp;
  <a href="#-中文版本"><img src="https://img.shields.io/badge/🇨🇳-中文-eff6ff?style=for-the-badge&labelColor=7f1d1d" alt="中文"></a>
  &nbsp;&nbsp;
  <a href="./docs/Xinhua-Cloud-Sign-WhitePaper.pdf"><img src="https://img.shields.io/badge/📄-Whitepaper-orange?style=for-the-badge" alt="PDF"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.7.0"><img src="https://img.shields.io/badge/🚀-v3.0.7.0-success?style=for-the-badge" alt="Version"></a>
</p>

---

# 🌩 Xinhua Cloud Signing

> Zero-upload cloud code signing for Windows drivers & apps.  
> Supports WHCP, Secure Boot, SmartScreen & 360.  
> **Global exclusive Microsoft whitelist mechanism.**  
> FIPS 140-3 certified · 28ms per sign · 197 countries · Hash-only (no file upload)

[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![FIPS](https://img.shields.io/badge/security-FIPS%20140--3-blue)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![WHCP](https://img.shields.io/badge/WHCP-2026%20ready-green)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![Privacy](https://img.shields.io/badge/privacy-zero--upload-orange)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![Org](https://img.shields.io/badge/Org-Xinhua--Cloud--Sign-1a1a2e?logo=github)](https://github.com/Xinhua-Cloud-Sign)
[![Version](https://img.shields.io/badge/version-3.0.7.0-success)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.7.0)

---

## 🇬🇧 English Version {#english-version}

### 🚀 Latest Release — v3.0.7.0 · Server Enforces Client Minimum — Legacy Versions Deprecated

> **Breaking Change · Security Enforcement · Legacy Client Cut‑off · TSA on .NET 10**

This release is a **security-driven mandatory upgrade**. The server will **no longer accept any client below v3.0.7.0**.

#### ⚠️ Breaking Change (Server‑Side)

Starting the v3.0.7.0 rollout, the cloud signing backend **rejects all requests from client versions < v3.0.7.0**:

- v3.0.6.x and earlier are **no longer accepted** by the signing gateway
- Requests with stale session schemas, old TSA chains, or pre‑parity digest formats return `403 ClientTooOld`
- This is a **security enforcement**, not a feature removal

| Client | Server Status |
|--------|:---:|
| ≤ v3.0.6.3 | ❌ Rejected |
| **v3.0.7.0** | ✅ Only accepted version |

👉 **All users must upgrade before the cutoff date** or signing requests will fail.

#### 🛡 Why This Is Happening

Over the past weeks we observed **sustained targeted intrusion attempts** against the signing infrastructure:

- ID enumeration → bulk password‑reset floods
- Credential stuffing against the web console
- Attempts to abuse legacy client handshake quirks as pivot points

Legacy clients (< v3.0.7.0) carry:

- weaker session token derivation
- pre‑hardening key‑cache behavior
- non‑byte‑aligned parity with the current server trust state machine

Keeping them compatible would mean **keeping known attack surface alive**. We chose to close it.

#### ⚙️ Client Kernel Upgrade (from v3.0.6.3)

- Core signing runtime rewritten for tighter alignment with the server-side trust chain
- Digest computation, session handshake, and TSA chaining follow the **exact same state machine** as the backend
- Improved edge-case handling for:
  - PE files with dual code directories
  - Drivers crossing WHCP 2026 policy boundaries
  - Non-standard section alignment

#### 🔗 Server Consistency (Parity)

- Client no longer "guesses" backend behavior — all responses validated against server schema
- Hash submission, session resume, and signature embedding verified byte-for-byte against server reference
- Offline mode degrades gracefully instead of producing silently broken signatures

#### 🛡 Security Hardening

- Hardened local key-cache isolation (digest-only workflow, no plaintext private material)
- Strict certificate chain validation before embedding (CN → CA → Root → TSA)
- Replay protection on session tokens
- Hardened `MyAPI` decoding path (still async, still off GUI thread)
- **Custom TSA backend on .NET 10** — improved high-concurrency stability
- **Server-side reject list** for pre‑v3.0.7.0 user‑agent + session magic

#### ✨ Functional Improvements

- Faster cold start (carried over from v3.0.6.3, further trimmed)
- More accurate progress reporting during hash → sign → embed pipeline
- Better error differentiation: network / server / PE-format / chain-trust
- Verbose log mode for CI/CD debugging

#### 📊 Real-World Impact

| Scenario | v3.0.6.2 | v3.0.6.3 | v3.0.7.0 |
|--------|--------|-------|-------|
| Cold start | ~0.4s | ~0.3s | **~0.2s** |
| Sign request (cached) | ~95ms | ~70ms | **~50ms** |
| Server parity | Partial | Byte-level | **Enforced** |
| TSA stability (concurrent) | .NET 4.8 | .NET 10 | **.NET 10 (hardened)** |
| UI responsiveness | smooth | smoother | **smoothest** |
| Legacy client support | ✅ | ✅ | **❌ Removed** |
| Session replay protection | ❌ | Partial | **✅ Full** |

---

### 🛡️ Security Notice (2026‑08‑01 Incident)

On August 1, 2026, our infrastructure detected a coordinated attack targeting user accounts:

- Attackers enumerated user IDs to trigger bulk password reset emails
- Attempted credential stuffing against the web console
- Tried to compromise linked email accounts as a pivot point

✅ **Core signing services were not compromised**  
✅ **Private keys remained secure and offline**  
✅ **Attack vectors have been mitigated at the infrastructure level**

#### 🔐 Mandatory Security Recommendations

We strongly advise **all users** to take immediate action:

1. **Upgrade to v3.0.7.0 immediately** — older versions will be rejected by the server
2. **Enable TOTP / Google Authenticator 2FA** on your Cloud Signing account
3. **Change your signing console password** to a 16+ character strong passphrase
4. **Change your linked email password** (and ensure it is unique)
5. **Never click suspicious links in emails** — always navigate manually to the console

#### ⚠️ Responsibility Boundary

Xinhua Cloud Signing secures the infrastructure, HSMs, and signing pipelines.  
**Account security (passwords, 2FA, email hygiene) remains the responsibility of the user.**

If an account is compromised due to weak credentials, missing 2FA, or email breach, **the account holder assumes all risks and liabilities**.

---

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
- ✅ **HSM-backed key storage** (FIPS-grade hardware security module)
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
| 📖 Preview (inline) | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 Direct Download | [raw link](https://raw.githubusercontent.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

---

### 🧰 Windows Installer

| Asset | Description |
|-------|-------------|
| `Xinhua_EVCS_v3.0.7.0_setup.exe` | Offline full installer v3.0.7.0 (Windows x64) |

#### Quick Install
```bat
:: Run as Administrator
Xinhua_EVCS_v3.0.7.0_setup.exe

:: Verify signature
sigcheck -v Xinhua_EVCS_v3.0.7.0_setup.exe
```

> 💡 After install, CLI available as `codesigning.exe` in PATH.

---

### 🛰 TSA Infrastructure Upgrade

The custom RFC 3161 timestamp server has been upgraded:

- Runtime migrated from **.NET Framework 4.8 → .NET 10**
- Improved high-concurrency handling and request queuing
- Reduced clock drift sensitivity under sustained load
- Hardened against timestamp forgery and replay attacks
- No breaking changes for v3.0.7.0+ clients

✅ Already deployed to production  
📊 Monitoring active

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
> Just: *"you hack kernels, we give you signatures."*

#### 💬 Telegram
| Channel | Group |
|---------|-------|
| 📢 @XinhuaCloudSign_News (announcements) | 💬 @XinhuaCloudSign (discussion) |

---

### 🧰 Quick Start (CLI)

```text
# 1. Compute local digest (NEVER upload the file)
sha256sum mydriver.sys > digest.txt

# 2. Send digest to cloud HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" \
  -d @digest.txt

# 3. Embed returned signature into PE
codesigning.exe embed mydriver.sys --sig response.sig
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
| 🛡 Min client version | **v3.0.7.0** |

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

> 🧠 *"Compatibility is a luxury you can't afford with a signing root. v3.0.7.0 closes the door on everything that predates the threat model we now run."*  
> — Xinhua Cloud Signing Team

<br><br>

---

<p align="center">
  <a href="#-中文版本"><img src="https://img.shields.io/badge/🇨🇳-查看中文版本-eff6ff?style=for-the-badge&labelColor=7f1d1d"></a>
</p>

<br><br>

---

# 🌩 新华云签名 {#中文版本}

> 零上传云端代码签名，适用于 Windows 驱动与应用。  
> 支持 WHCP、安全启动、SmartScreen 及 360 信任链。  
> **全球独家微软白名单机制。**  
> FIPS 140-3 认证 · 单次签名 28ms · 覆盖 197 国 · 仅传哈希零上传

[![平台](https://img.shields.io/badge/平台-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![安全](https://img.shields.io/badge/安全-FIPS%20140--3-blue)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![WHCP](https://img.shields.io/badge/WHCP-2026%20就绪-green)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![隐私](https://img.shields.io/badge/隐私-零上传-orange)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![组织](https://img.shields.io/badge/组织-Xinhua--Cloud--Sign-1a1a2e?logo=github)](https://github.com/Xinhua-Cloud-Sign)
[![版本](https://img.shields.io/badge/版本-3.0.7.0-success)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.7.0)

---

## 🚀 最新版本 — v3.0.7.0 · 服务器强制最低版本 · 旧客户端停用

> **破坏性变更 · 安全驱动 · 弃用旧版客户端 · TSA 升级 .NET 10**

本版本是**安全驱动的强制升级**。服务器将**不再接受任何低于 v3.0.7.0 的客户端**。

#### ⚠️ 破坏性变更（服务器端）

自 v3.0.7.0 上线起，云签名后端**拒绝所有 < v3.0.7.0 的客户端请求**：

- v3.0.6.x 及更早版本**不再被签名网关接受**
- 使用旧会话 schema、旧 TSA 链或非一致性摘要格式的请求将返回 `403 ClientTooOld`
- 这是**安全强制措施**，不是功能移除

| 客户端版本 | 服务器状态 |
|--------|:---:|
| ≤ v3.0.6.3 | ❌ 已拒绝 |
| **v3.0.7.0** | ✅ 唯一接受版本 |

👉 **所有用户必须在截止日期前升级**，否则签名请求将失败。

#### 🛡 为什么做出这个决定

过去数周，我们持续观测到针对签名基础设施的**定向渗透攻击**：

- ID 枚举 → 批量密码重置邮件轰炸
- 针对 Web 控制台的凭证填充攻击
- 试图利用旧客户端握手缺陷作为入侵跳板

旧版客户端（< v3.0.7.0）存在：

- 较弱的会话令牌派生机制
- 加固前的密钥缓存行为
- 与当前服务器信任状态机不对齐

保留兼容性 = **保留已知攻击面**。我们选择关闭它。

#### ⚙️ 客户端内核升级（延续自 v3.0.6.3）

- 签名运行时重写，与服务器端信任链严格对齐
- 摘要计算、会话握手、TSA 链式调用与后端**共享同一套状态机**
- 改善以下边缘情况的处理：
  - 含双代码目录的 PE 文件
  - 跨越 WHCP 2026 策略边界的驱动
  - 非标准节对齐

#### 🔗 服务器端一致性（Parity）

- 客户端不再"猜测"后端行为——所有响应按服务端 schema 校验
- 哈希提交、会话恢复、签名嵌入均与服务器参考实现**逐字节验证**
- 离线模式优雅降级，不再产生"看似签了但链不对"的废品

#### 🛡 安全加固

- 本地密钥缓存隔离加强（摘要工作流，无明文私钥）
- 嵌入前严格校验证书链（CN → CA → Root → TSA）
- Session Token 重放保护
- `MyAPI` 解码路径加固（仍异步、仍不卡 UI）
- **自定义 TSA 后端已迁移至 .NET 10**——高并发稳定性大幅提升
- **服务端拒绝列表**：拦截 pre‑v3.0.7.0 的 User‑Agent + Session Magic

#### ✨ 功能增强

- 冷启动再提速（延续 v3.0.6.3 并进一步压缩）
- 哈希→签名→嵌入 全链路进度反馈更精准
- 错误分类更清晰：网络 / 服务端 / PE 格式 / 链信任
- 新增 CI/CD 详细日志模式

#### 📊 实际效果对比

| 场景 | v3.0.6.2 | v3.0.6.3 | v3.0.7.0 |
|--------|--------|-------|-------|
| 冷启动 | ~0.4s | ~0.3s | **~0.2s** |
| 签名请求（缓存） | ~95ms | ~70ms | **~50ms** |
| 服务器一致性 | 部分对齐 | 字节级一致 | **强制校验** |
| TSA 并发稳定性 | .NET 4.8 | .NET 10 | **.NET 10（加固）** |
| UI 响应 | 丝滑 | 更丝滑 | **最丝滑** |
| 旧客户端支持 | ✅ | ✅ | **❌ 已移除** |
| 会话重放保护 | ❌ | 部分 | **✅ 完整** |

---

## 🛡️ 安全公告（2026‑08‑01 事件）

2026 年 8 月 1 日，系统管理员日志确认云签名服务遭遇外部定向攻击：

- 攻击者通过循环枚举用户 ID，批量触发密码重置邮件
- 尝试通过弱密码爆破入侵云签名后台
- 试图入侵用户邮箱系统作为跳板

✅ **核心签名服务未被攻破**  
✅ **私钥保持安全离线状态**  
✅ **攻击向量已在基础设施层面封堵**

#### 🔐 强制安全建议（请立即执行）

强烈建议 **所有用户** 立即采取行动：

1. **立即升级到 v3.0.7.0**——旧版本将被服务器拒绝
2. **开启 TOTP / Google Authenticator 二次验证**
3. **修改云签名登录密码**为 16 位以上强密码
4. **同步修改绑定邮箱密码**（确保与签名系统不同）
5. **切勿点击邮件内可疑链接**，手动输入官网地址登录

#### ⚠️ 责任声明

新华云签名负责保护基础设施、HSM 和签名管道安全。  
**账户安全（密码、2FA、邮箱卫生）由用户自行负责。**

若因用户使用弱密码、未启用二次验证、或关联邮箱被入侵导致证书被恶意签发，**所有损失及法律后果由账户持有者自行承担**。

---

## 🚀 为什么选新华云签名？

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

## 🏆 安全资质

- ✅ **FIPS 140-3**（美国最高加密模块标准，对标 NSA）
- ✅ **HSM 硬件安全模块**托管私钥（FIPS 级）
- ✅ **SHA-256 / RSA-4096 / ECC P-384**
- ✅ 集成 CA：**DigiCert · GlobalSign · Sectigo · SSL.com · Certum**

---

## 📦 签名类型一览

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

## ⚠️ 微软 WHCP 与 2026 策略变更

微软官方公告：

> *"从 **2026 年 4 月安全更新**起，通过已过期交叉签名程序签名的 kernel 驱动将**默认不再被信任**。"*

**2026 年哪些会失效：**
- ❌ 交叉签名驱动将在 Win 11 24H2+ / Server 2025 上被拦截
- ❌ 传统 EV + USB Key 流程无法满足 WHCP 要求
- ❌ 新内核驱动 ***必须*** 走 WHCP

✅ **新华云签名已接入微软白名单** —— 全球独家。

#### 📌 官方链接
- Windows 驱动策略：https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略
- 驱动代码签名要求：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs
- 硬件仪表板入门：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/
- 推进 Windows 驱动安全：https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818

---

## 📄 产品白皮书（PDF）

完整技术白皮书 —— 架构、仅哈希流程、WHCP 集成、8 类签名矩阵。  
针对 **Adobe Acrobat 扁平化/线性化** 优化，零渲染卡顿。

| 操作 | 链接 |
|--------|------|
| 📖 在线预览 | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 直链下载 | [raw 链接](https://raw.githubusercontent.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

---

## 🧰 Windows 安装包

| 文件 | 说明 |
|------|------|
| `Xinhua_EVCS_v3.0.7.0_setup.exe` | 离线完整安装包 v3.0.7.0（Windows x64） |

#### 安装步骤
```bat
:: 以管理员身份运行
Xinhua_EVCS_v3.0.7.0_setup.exe

:: 验证安装包签名
sigcheck -v Xinhua_EVCS_v3.0.7.0_setup.exe
```

> 💡 安装后命令行工具 `codesigning.exe` 自动加入 PATH，可直接在 CMD/PowerShell 调用。

---

## 🛰 自定义 TSA 升级公告

自定义 RFC 3161 时间戳服务器已完成基础架构升级：

- 运行时从 **.NET Framework 4.8 迁移至 .NET 10**
- 优化高并发场景下的请求排队与处理能力
- 降低持续峰值负载下的时钟漂移敏感性
- 加固防时间戳伪造与重放攻击
- v3.0.7.0+ 客户端无破坏性变更

✅ 生产环境已全量上线  
📊 监控数据正常

---

## 👥 开发者社区 ——「内核夜校」

> *这里不属于产品经理，只属于那些愿意读 Intel SDM、凌晨两点还在调 BSOD 的人。*

**我们在找这样的人：**
- 🛠 写过 `.sys` 的人（哪怕只成功加载过一次）
- 🔬 喜欢逆向工程 / 研究 PE 格式的人
- 🛡 研究过 PatchGuard / HVCI 的人
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

#### 💬 Telegram
| 频道 | 群组 |
|------|------|
| 📢 @XinhuaCloudSign_News（官方公告） | 💬 @XinhuaCloudSign（技术交流） |

---

## 🧰 快速开始（CLI）

```text
# 1. 本地计算摘要（绝不上传文件）
sha256sum mydriver.sys > digest.txt

# 2. 将摘要发送至云端 HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" \
  -d @digest.txt

# 3. 将返回的签名嵌入 PE 文件
codesigning.exe embed mydriver.sys --sig response.sig
```

> 完整 SDK / CLI 即将开源 —— 点个 Star 关注本仓库 ⭐

---

## 📊 关键数据

| 指标 | 数值 |
|--------|-------|
| 🌍 覆盖国家 | **197** |
| ⚡ 中位签名耗时 | **28 ms** |
| 📦 最大单文件 | **数百 GB**（仅哈希） |
| 🔒 文件上传量 | **0** |
| 🛡 最低客户端版本 | **v3.0.7.0** |

---

## 📜 许可证

产品/服务：专有 SaaS。  
本仓库（README + 文档）：**MIT 协议** —— 可自由引用或 Fork 结构。

---

## 🔗 相关链接

- [微软 WHCP / 硬件仪表板](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/)
- [驱动签名要求](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows 驱动策略](https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略)

---

> 🧠 *"兼容性是你负担不起的奢侈品，当你手里握着签名根密钥的时候。v3.0.7.0 关上了所有不符合当前威胁模型的门。"*  
> —— 新华云签名团队

<br><br>

---

<p align="center">
  <a href="#-english-version"><img src="https://img.shields.io/badge/🇬🇧-Back%20to%20English-dde6ff?style=for-the-badge&labelColor=1a1a2e"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.7.0"><img src="https://img.shields.io/badge/🚀-Download%20v3.0.7.0-success?style=for-the-badge" alt="Download"></a>
  &nbsp;&nbsp;
  <a href="https://t.me/XinhuaCloudSign_News"><img src="https://img.shields.io/badge/📢-Telegram%20News-26A5E4?style=for-the-badge&logo=telegram&logoColor=white"></a>
</p>
