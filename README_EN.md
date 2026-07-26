<!--
=============================================
  Xinhua Cloud Signing — Full English README
  Organization: Xinhua-Cloud-Sign
  Repo: Xinhua-Cloud-Sign/cloud-code-signing-whcp
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

## 🏆 Security Credentials

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

| Action | Link |
|--------|------|
| 📖 Preview | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 Download | [raw link](https://raw.githubusercontent.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

---

## 🧰 Windows Installer

| Asset | Description |
|-------|-------------|
| `CodeSigning_installer.exe` | Windows installer for cloud signing client |

```bat
:: Run as Administrator
CodeSigning_installer.exe

:: Verify signature
sigcheck -v CodeSigning_installer.exe
```

---

## 👥 Developer Community — "Kernel Night Lab"

> *Not for product managers. For people who actually read Intel SDM & debug BSOD at 2 AM.*

**We're looking for:**
- 🛠 WDM / WDF driver authors
- 🔬 Reverse engineers
- 🛡 PatchGuard / HVCI researchers
- 🚀 CI/CD signing automation folks

**Join bonus:** 1× free production-grade cloud signature (any type).

> **No forms. No shares. No KPI.** Just: *"you hack kernels, we give you signatures."*

---

## 🧰 Quick Start (CLI)

```text
# 1. Compute digest
sha256sum mydriver.sys > digest.txt

# 2. Send to cloud HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" -d @digest.txt

# 3. Embed signature
codesigning.exe embed mydriver.sys --sig response.sig
```

---

## 📊 Stats

| Metric | Value |
|--------|-------|
| 🌍 Countries | **197** |
| ⚡ Sign time | **28 ms** |
| 📦 Max file | **Hundreds of GB** |
| 🔒 Uploaded | **0** |

---

## 📜 License

Product: proprietary SaaS. This repo: **MIT**.

---

## 🔗 Related

- [Microsoft WHCP](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/)
- [Driver Signing Requirements](https://learn.microsoft.com/en-us/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows Driver Policy](https://support.microsoft.com/en-us/topic/the-windows-driver-policy-ecd2a78c-750c-415d-93f2-e37302ce0443)

---

> 🧠 *"Code doesn't have to be perfect. But the signature? That has to be bulletproof."*  
> — Xinhua Cloud Signing Team
