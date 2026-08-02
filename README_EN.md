<!--
=============================================
  Xinhua Cloud Signing — Full English README
  Organization: Xinhua-Cloud-Sign
  Repo: Xinhua-Cloud-Sign/cloud-code-signing-whcp
  Latest Version: v3.0.6.2
=============================================
-->

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
[![Version](https://img.shields.io/badge/version-3.0.6.2-success)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.6.2)

---

## 🚀 Latest Release — v3.0.6.2 · Performance Overhaul

> **200% faster startup · AI-assisted refactoring · Security hardening**

This release focuses on **two non-negotiables**: extreme performance and operational security.

### ⚡ Performance Breakthrough
- **Startup time improved by up to 200%** (cold boot: ~1.2s → ~0.4s)
- UI thread workload reduced by **~70%**
- Core signing path fully refactored for low-latency execution
- Background tasks moved to **anonymous threads / TTask**, eliminating GUI stalls

### 🤖 AI-Assisted Code Optimization
Large portions of the codebase were **analyzed, restructured, and optimized with AI assistance**:
- Threading model redesigned (strict UI / Worker separation)
- Heavy cryptographic routines isolated from the message loop
- Redundant initialization paths removed
- PDF loading, certificate refresh, and history I/O significantly streamlined

### 🧱 Architectural Improvements
- Lazy initialization for EdgeBrowser / WebView2
- Deferred PDF loading until idle / tab activation
- `MyAPI` and other CPU-intensive logic executed asynchronously
- Improved exception safety across background workers

### 📊 Real-World Impact

| Scenario | Before | After |
|--------|--------|-------|
| Cold start | ~1.2s | **~0.4s** |
| Sign request (cached) | ~320ms | **~95ms** |
| PDF tab switch | noticeable delay | **instant** |
| UI responsiveness | occasional stalls | **smooth drag / resize** |

---

## 🛡️ Security Notice (2026‑08‑01 Incident)

On August 1, 2026, our infrastructure detected a coordinated attack targeting user accounts:

- Attackers enumerated user IDs to trigger bulk password reset emails
- Attempted credential stuffing against the web console
- Tried to compromise linked email accounts as a pivot point

✅ **Core signing services were not compromised**  
✅ **Private keys remained secure and offline**  
✅ **Attack vectors have been mitigated at the infrastructure level**

### 🔐 Mandatory Security Recommendations

We strongly advise **all users** to take immediate action:

1. **Enable TOTP / Google Authenticator 2FA** on your Cloud Signing account
2. **Change your signing console password** to a 16+ character strong passphrase
3. **Change your linked email password** (and ensure it is unique)
4. **Never click suspicious links in emails** — always navigate manually to the console

### ⚠️ Responsibility Boundary

Xinhua Cloud Signing secures the infrastructure, HSMs, and signing pipelines.  
**Account security (passwords, 2FA, email hygiene) remains the responsibility of the user.**

If an account is compromised due to weak credentials, missing 2FA, or email breach, **the account holder assumes all risks and liabilities**.

---

## 🚀 Why Xinhua Cloud Signing?

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

## 🏛 Security Credentials

- ✅ **FIPS 140-3** (U.S. highest crypto module standard, NSA-aligned)
- ✅ **HSM-backed key storage** (FIPS-grade hardware security module)
- ✅ **SHA-256 / RSA-4096 / ECC P-384**
- ✅ Integrated CAs: **DigiCert · GlobalSign · Sectigo · SSL.com · Certum**

---

## 📦 Signing Types

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

## ⚠️ Microsoft WHCP & 2026 Policy Change

Microsoft officially announced:

> *"With the **April 2026 security update**, kernel drivers signed via the expired cross-signing program are **no longer trusted by default**."*

**What breaks in 2026:**
- ❌ Cross-signed drivers blocked on Win 11 24H2+ / Server 2025
- ❌ Legacy EV + USB token workflows insufficient for WHCP
- ❌ New kernel drivers → **must go through WHCP**

✅ **Xinhua Cloud Signing already sits on Microsoft's whitelist** — global exclusive.

### 📌 Official Links
- Windows Driver Policy: https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443
- Advancing Windows Driver Security: https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818
- Driver Code Signing Requirements: https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs
- Hardware Dashboard: https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/

---

## 📄 Product Whitepaper (PDF)

Full technical deep-dive — architecture, hash-only flow, WHCP integration, 8-type matrix.  
Optimized for **Adobe Acrobat (flattened / linearized)** — zero rendering lag.

| Action | Link |
|--------|------|
| 📖 Preview | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 Download | [raw link](https://raw.githubusercontent.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

---

## 🧰 Windows Installer

| Asset | Description |
|-------|-------------|
| `Xinhua_EVCS_v3.0.6.2_setup.exe` | Offline full installer v3.0.6.2 (Windows x64) |

```bat
:: Run as Administrator
Xinhua_EVCS_v3.0.6.2_setup.exe

:: Verify signature
sigcheck -v Xinhua_EVCS_v3.0.6.2_setup.exe
```

> 💡 After install, CLI available as `codesigning.exe` in PATH.

---

## 👥 Developer Community — "Kernel Night Lab"

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

### 🎁 Join Bonus — Free Cloud Signature

Every developer who joins the community gets **1× free production-grade cloud signature** (any type from the table):

- ✅ Zero-upload (hash only)
- ✅ WHCP / Secure Boot / SmartScreen ready
- ✅ Pre-adapted for April 2026 policy
- ✅ No USB token · no private key exposure

> **No forms. No shares. No KPI.**  
> Just: *"you hack kernels, we give you signatures."*

### 💬 Telegram
| Channel | Group |
|---------|-------|
| 📢 @XinhuaCloudSign_News (announcements) | 💬 @XinhuaCloudSign (discussion) |

---

## 🧰 Quick Start (CLI)

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

## 📊 Stats Snapshot

| Metric | Value |
|--------|-------|
| 🌍 Countries | **197** |
| ⚡ Median sign time | **28 ms** |
| 📦 Max single-file | **Hundreds of GB** (hash only) |
| 🔒 Files uploaded | **0** |

---

## 📜 License

Product / service: proprietary SaaS.  
This repo (README + docs): **MIT** — feel free to reference / fork the structure.

---

## 🔗 Related

- [Microsoft WHCP / Hardware Dashboard](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/)
- [Driver Signing Requirements](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows Driver Policy (2026)](https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443)
- **Signotaur** (self-hosted code signing service, supports YubiKey / SafeNet / PKCS#11 HSM / .pfx / Windows Cert Store; gRPC signing + HTTP/1.1 dashboard)

---

> 🧠 *"Code doesn't have to be perfect. But the signature? That has to be bulletproof."*  
> — Xinhua Cloud Signing Team
