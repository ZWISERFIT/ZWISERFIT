# 🔬 KinTwin SDK · Personalized Health Metabolics Engine

> **🟡 SDK 开源 · 核心闭源 | YC RFS Direction 3: AI-Native Personalized Medicine**
>
> 门店→行为流→哈希存证→应用层。
> 用户通过 DID 持有自己的数据。保险和医药从 KinTwin 读取的是密码学证明，而非盲信。

[![License](https://img.shields.io/badge/License-MIT_(SDK)-green.svg)](./LICENSE)
[![YC RFS](https://img.shields.io/badge/YC_RFS-Direction_3_(AI_Personalized_Medicine)-blue)]()

---

## 什么是 KinTwin？

**KinTwin = 人体行为数据代谢底座**

```
Momo（数据采集） + Nova（连续行为流） + Ethan（哈希确权） + 自研硬件三件套
                              ↓
                    KinTwin — 行为数据代谢引擎
                              ↓
          DID 确权 → PoPB 存证 → 保险定价 / 医药研发
```

| 组件 | 说明 | 开源策略 |
|:--|:--|:--|
| **Hardware API** | 门禁/摄像头/体测仪 SDK 接口 | 🟢 MIT 开放 |
| **Data Format Specs** | ZWF-20 健康行为数据标准 | 🟢 MIT 开放 |
| **Integration Examples** | 硬件集成示例代码 | 🟢 MIT 开放 |
| **Nova Behavior Stream** | 连续行为流算法 | 🔒 闭源 |
| **Ethan Hash Protocol** | 数据哈希存证协议 | 🔒 闭源 |
| **Firmware** | 硬件固件 | 🔒 闭源 |

---

## 目录结构

```
kin-twin-sdk/
├── api/             # Hardware API 规范 · DID 接口
├── examples/        # 集成示例 · 数据采集 pipeline
├── specs/           # ZWF-20 标准 · 数据格式规范
└── README.md        # 本文件
```

---

## 快速开始

```python
# 安装 KinTwin SDK
pip install kintwin-sdk

# 连接门禁设备
from kintwin import GateClient
gate = GateClient(device_id="gym-gate-001")
gate.connect()

# 读取行为流
stream = gate.get_behavior_stream()
for event in stream:
    print(f"User {event.did[:8]}... → {event.action} @ {event.timestamp}")

# 验证存证
from kintwin.attest import verify_hash
assert verify_hash(event.hash, event.data)
```

---

## 数据主权

KinTwin 的核心原则：**用户拥有自己的数据。平台在技术上无法访问。**

- ✅ 用户通过 DID 持有数据密钥
- ✅ MPC 分布式密钥管理 → 平台无法单方解密
- ✅ 所有数据访问需用户签名授权
- ✅ 存证链公开可验证 — SHA-256 → 链上锚定

这是架构保证，不是商业承诺。

---

## 开源策略

KinTwin 是 ZWISERFIT 分层开源策略的 **🟡 SDK开放层**：

| 层级 | 开源策略 | 说明 |
|:--|:--|:--|
| 🟢 Saros Open | MIT 完全开源 | 应用层 · 任何健身房可部署 |
| 🟡 **KinTwin SDK** | SDK开源·核心闭源 | 硬件API开放 · 算法/协议闭源 |
| 🔴 Zeus Protocols | 极小开放·协议文档 | Agent通信标准 · Oracle闭源 |
| ⚫ 9-Agent Kernel | 全闭源·架构图纸 | 调度器·审计引擎·四流拓扑 |

---

> **KinTwin · Dongguan, Guangdong, China**
> *你的数据归你。这是架构，不是承诺。*
> ⭐ [Star ZWISERFIT](https://github.com/ZWISERFIT/ZWISERFIT)

📄 MIT (SDK) / Proprietary (Core)
