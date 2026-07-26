<!--
=============================================
  新华云签名 — 完整中文 README
  组织：Xinhua-Cloud-Sign
  仓库：Xinhua-Cloud-Sign/cloud-code-signing-whcp
=============================================
-->

# 🌩 新华云签名

> 零上传云端代码签名，适用于 Windows 驱动与应用。  
> 支持 WHCP、安全启动、SmartScreen 及 360 信任链。  
> **全球独家微软白名单机制。**  
> FIPS 140-3 认证 · 单次签名 28ms · 覆盖 197 国 · 仅传哈希零上传

[![平台](https://img.shields.io/badge/平台-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![安全](https://img.shields.io/badge/安全-FIPS%20140--3-blue)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![WHCP](https://img.shields.io/badge/WHCP-2026%20就绪-green)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![隐私](https://img.shields.io/badge/隐私-零上传-orange)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp)
[![组织](https://img.shields.io/badge/组织-Xinhua--Cloud--Sign-1a1a2e?logo=github)](https://github.com/Xinhua-Cloud-Sign)

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

> *"从 **2026 年 4 月安全更新**起，通过已过期交叉签名程序签名的 kernel 驱动将**默认不再被信任**。"*

**2026 年哪些会失效：**
- ❌ 交叉签名驱动将在 Win 11 24H2+ / Server 2025 上被拦截
- ❌ 传统 EV + USB Key 流程无法满足 WHCP 要求
- ❌ 新内核驱动 ***必须*** 走 WHCP

✅ **新华云签名已接入微软白名单** —— 全球独家。

### 📌 官方链接
- Windows 驱动策略：https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略
- 驱动代码签名要求：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs
- 硬件仪表板入门：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/
- 推进 Windows 驱动安全：https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818

---

## 📄 产品白皮书（PDF）

| 操作 | 链接 |
|--------|------|
| 📖 在线预览 | [Xinhua-Cloud-Sign-WhitePaper.pdf](./docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |
| 📥 直链下载 | [raw 链接](https://raw.githubusercontent.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/main/docs/Xinhua-Cloud-Sign-WhitePaper.pdf) |

---

## 🧰 Windows 安装包

| 文件 | 说明 |
|------|------|
| `CodeSigning_installer.exe` | 云签名客户端 Windows 安装包 |

```bat
:: 以管理员身份运行
CodeSigning_installer.exe

:: 验证安装包签名
sigcheck -v CodeSigning_installer.exe
```

---

## 👥 开发者社区 ——「内核夜校」

> *这里不属于产品经理，只属于那些愿意读 Intel SDM、凌晨两点还在调 BSOD 的人。*

**我们在找这样的人：**
- 🛠 写过 `.sys` 的人
- 🔬 喜欢逆向工程 / 研究 PE 格式的人
- 🛡 研究过 PatchGuard / HVCI 的人
- 🚀 搞 CI/CD 签名自动化的同学

**加入福利：** 免费获赠 1 份正版云签名（类型任选）。

> **不需要填表。不需要转发。不卖课。** 你搞内核，我们送签名。

---

## 🧰 快速开始（CLI）

```text
# 1. 本地计算摘要
sha256sum mydriver.sys > digest.txt

# 2. 发送至云端 HSM
curl -X POST https://api.xinhua-signing.com/v1/sign \
  -H "Authorization: Bearer $TOKEN" -d @digest.txt

# 3. 嵌入签名
codesigning.exe embed mydriver.sys --sig response.sig
```

---

## 📊 关键数据

| 指标 | 数值 |
|--------|-------|
| 🌍 覆盖国家 | **197** |
| ⚡ 中位签名耗时 | **28 ms** |
| 📦 最大单文件 | **数百 GB**（仅哈希） |
| 🔒 文件上传量 | **0** |

---

## 📜 许可证

产品/服务：专有 SaaS。本仓库：**MIT 协议**。

---

## 🔗 相关链接

- [微软 WHCP](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/)
- [驱动签名要求](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows 驱动策略](https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略)

---

> 🧠 *"代码可以不完美，但签名一定要无懈可击。"*  
> —— 新华云签名团队
