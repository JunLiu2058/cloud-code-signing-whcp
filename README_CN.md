<!--
=============================================
  新华云签名 — 完整中文 README
  组织：Xinhua-Cloud-Sign
  仓库：Xinhua-Cloud-Sign/cloud-code-signing-whcp
  最新版本：v3.0.6.2
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
[![版本](https://img.shields.io/badge/版本-3.0.6.2-success)](https://github.com/Xinhua-Cloud-Sign/cloud-code-signing-whcp/releases/tag/v3.0.6.2)

---

## 🚀 最新版本 — v3.0.6.2 · 性能全面重构

> **启动速度提升 200% · AI 辅助代码重构 · 安全加固**

本版本聚焦两件事：**极致性能** 与 **运行安全**。

### ⚡ 性能突破
- **启动速度提升最高 200%**（冷启动 ~1.2s → ~0.4s）
- UI 线程负载下降约 **70%**
- 核心签名路径全面重构，执行效率显著提升
- AI 辅助重构大量代码，线程模型更合理
- PDF / 证书 / 历史记录全部懒加载
- `MyAPI` 等重计算逻辑全部移至后台线程

### 🤖 AI 辅助代码优化
大量代码经 **AI 分析、重构与优化**：
- 线程模型重设计（UI / Worker 严格分离）
- 重密码学例程从消息循环中隔离
- 冗余初始化路径移除
- PDF 加载、证书刷新、历史 I/O 大幅精简

### 🧱 架构改进
- EdgeBrowser / WebView2 懒初始化
- PDF 延迟到空闲期 / Tab 激活时才加载
- `MyAPI` 等 CPU 密集型逻辑异步执行
- 后台任务异常安全性全面提升

### 📊 实际效果对比

| 场景 | 优化前 | 优化后 |
|--------|--------|-------|
| 冷启动 | ~1.2s | **~0.4s** |
| 签名请求（缓存） | ~320ms | **~95ms** |
| PDF 页签切换 | 明显延迟 | **瞬时完成** |
| UI 响应 | 偶发卡顿 | **丝滑拖动/缩放** |

---

## 🛡️ 安全公告（2026‑08‑01 事件）

2026 年 8 月 1 日，系统管理员日志确认云签名服务遭遇外部定向攻击：

- 攻击者通过循环枚举用户 ID，批量触发密码重置邮件
- 尝试通过弱密码爆破入侵云签名后台
- 试图入侵用户邮箱系统作为跳板

✅ **核心签名服务未被攻破**  
✅ **私钥保持安全离线状态**  
✅ **攻击向量已在基础设施层面封堵**

### 🔐 强制安全建议（请立即执行）

强烈建议 **所有用户** 立即采取行动：

1. **开启 TOTP / Google Authenticator 二次验证**
2. **修改云签名登录密码**为 16 位以上强密码
3. **同步修改绑定邮箱密码**（确保与签名系统不同）
4. **切勿点击邮件内可疑链接**，手动输入官网地址登录

### ⚠️ 责任声明

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

## 🏛 安全资质

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

### 📌 官方链接
- Windows 驱动策略：https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略
- 驱动代码签名要求：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs
- 硬件仪表板入门：https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/
- 推进 Windows 驱动安全：https://techcommunity.microsoft.com/blog/windows-itpro-blog/advancing-windows-driver-security-removing-trust-for-the-cross-signed-driver-pro/4504818
- **Signotaur**（自托管代码签名服务，支持 YubiKey / SafeNet / PKCS#11 HSM / .pfx / Windows 证书存储；gRPC 签名 + HTTP/1.1 管理面板）

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
| `Xinhua_EVCS_v3.0.6.2_setup.exe` | 离线完整安装包 v3.0.6.2（Windows x64） |

### 安装步骤
```bat
:: 以管理员身份运行
Xinhua_EVCS_v3.0.6.2_setup.exe

:: 验证安装包签名
sigcheck -v Xinhua_EVCS_v3.0.6.2_setup.exe
```

> 💡 安装后命令行工具 `codesigning.exe` 自动加入 PATH，可直接在 CMD/PowerShell 调用。

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

### 🎁 加入福利：免费云签名

所有加入社区的开发者，**免费获赠 1 份正版云签名**（类型任选）：

- ✅ 零上传（仅哈希）
- ✅ WHCP / 安全启动 / SmartScreen 全支持
- ✅ 提前适配 2026 年 4 月策略
- ✅ 无需 USB Key · 私钥不出云

> **不需要填表。不需要转发。不卖课。**  
> 你搞内核，我们送签名。

### 💬 Telegram
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

---

## 📜 许可证

产品/服务：专有 SaaS。  
本仓库（README + 文档）：**MIT 协议** —— 可自由引用或 Fork 结构。

---

## 🔗 相关链接

- [微软 WHCP / 硬件仪表板](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/)
- [驱动签名要求](https://learn.microsoft.com/zh-cn/windows-hardware/drivers/dashboard/code-signing-reqs)
- [Windows 驱动策略](https://support.microsoft.com/zh-cn/windows/windows-驱动程序策略)
- **Signotaur**（自托管代码签名服务，支持 YubiKey / SafeNet / PKCS#11 HSM / .pfx / Windows 证书存储；gRPC 签名 + HTTP/1.1 管理面板）

---

> 🧠 *"代码可以不完美，但签名一定要无懈可击。"*  
> —— 新华云签名团队
