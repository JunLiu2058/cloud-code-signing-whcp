<!--
=============================================
  Xinhua Cloud Signing — Full English README
  Organization: Xinhua-Cloud-Sign
  Repo: Xinhua-Cloud-Sign/cloud-code-signing-whcp
  Latest Version: v3.0.6.3
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
[![Version](https://img.shields.io/badge/version-3.0.6.3-success)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.6.3)

---

## 🚀 Latest Release — v3.0.6.3 · Client Kernel Upgrade & Server Parity

> **Client kernel rewritten · Byte-level server parity · Hardened security · TSA on .NET 10**

This release is **not about surface features** — it is about **correctness, consistency, and trust**.

### ⚙️ Client Kernel Upgrade
- Core signing runtime rewritten for tighter alignment with the server-side trust chain
- Digest computation, session handshake, and TSA chaining now follow the **exact same state machine** as the backend
- Improved edge-case handling for:
  - PE files with dual code directories
  - Drivers crossing WHCP 2026 policy boundaries
  - Non-standard section alignment

### 🔗 Server Consistency (Parity)
- Client no longer "guesses" backend behavior — all responses validated against server schema
- Hash submission, session resume, and signature embedding verified byte-for-byte against server reference
- Offline mode degrades gracefully instead of producing silently broken signatures

### 🛡 Security Hardening
- Hardened local key-cache isolation (digest-only workflow, no plaintext private material)
- Strict certificate chain validation before embedding (CN → CA → Root → TSA)
- Replay protection on session tokens
- Hardened `MyAPI` decoding path (still async, still off GUI thread)
- **Custom TSA backend migrated to .NET 10** — improved high-concurrency stability

### ✨ Functional Improvements
- Faster cold start (carried over from v3.0.6.2, further trimmed)
- More accurate progress reporting during hash → sign → embed pipeline
- Better error differentiation: network / server / PE-format / chain-trust
- Verbose log mode for CI/CD debugging

### 📊 Real-World Impact

| Scenario | v3.0.6.2 | v3.0.6.3 |
|--------|--------|-------|
| Cold start | ~0.4s | **~0.3s** |
| Sign request (cached) | ~95ms | **~70ms** |
| Server parity | Partial | **Byte-level** |
| TSA stability (concurrent) | .NET 4.8 | **.NET 10** |
| UI responsiveness | smooth | **smoother** |

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
| `Xinhua_EVCS_v3.0.6.3_setup.exe` | Offline full installer v3.0.6.3 (Windows x64) |

```bat
:: Run as Administrator
Xinhua_EVCS_v3.0.6.3_setup.exe

:: Verify signature
sigcheck -v Xinhua_EVCS_v3.0.6.3_setup.exe
```

> 💡 After install, CLI available as `codesigning.exe` in PATH.

---

## 🛰 TSA Infrastructure Upgrade

The custom RFC 3161 timestamp server has been upgraded:

- Runtime migrated from **.NET Framework 4.8 → .NET 10**
- Improved high-concurrency handling and request queuing
- Reduced clock drift sensitivity under sustained load
- No breaking changes, no client reconfiguration required

✅ Already deployed to production  
📊 Monitoring active

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

---

> 🧠 *"A signature is only as trustworthy as the client that produced it. v3.0.6.3 makes the client speak the server's language."*  
> — Xinhua Cloud Signing Team
