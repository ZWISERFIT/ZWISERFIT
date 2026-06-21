# 🏪 Saros Open · AI Store Digital Co-Founder

> **🟢 MIT 完全开源 | YC RFS Direction 2: AI-Native Service**
>
> 传统SaaS把工具卖给人，人自己当大脑。Saros把大脑+工具一起交付。
> **SaaS第一次有了会用工具的人。**

[![License](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![YC RFS](https://img.shields.io/badge/YC_RFS-Direction_2_(AI_Native_Service)-blue)]()

---

## 什么是 Saros？

**Saros = Momo（门店大脑） + SaaS Stack（执行手脚）**

| 组件 | 说明 | 开源策略 |
|:--|:--|:--|
| **Momo OS** | 门店运营操作系统 · 7年认知编码 | 🟢 MIT 完全开源 |
| **SaaS Stack** | POS/CRM/排课/进销存/会员管理 | 🟢 MIT 完全开源 |
| **Deploy Scripts** | 一键部署脚本 · Docker Compose | 🟢 MIT 完全开源 |
| **Docs** | 商户文档 · API参考 · 部署手册 | 🟢 MIT 完全开源 |
| **Community** | 贡献指南 · 社区治理 · RFC流程 | 🟢 MIT 完全开源 |

---

## 目录结构

```
saros-open/
├── momo-saas/       # Momo 门店大脑 + SaaS 栈源码
├── deploy/          # 部署脚本 · Docker · K8s
├── docs/            # 商户文档 · API参考 · 最佳实践
├── community/       # 贡献指南 · 社区治理 · RFC
└── README.md        # 本文件
```

---

## 快速开始

```bash
# 部署 Momo + SaaS 栈
git clone https://github.com/ZWISERFIT/ZWISERFIT.git
cd ZWISERFIT/saros-open/deploy
docker-compose up -d

# 或安装 OpenClaw Agent 运行 Momo
npm install -g openclaw
openclaw init --profile momo-store
openclaw agent start momo --capabilities store-ops,member-mgmt,daily-report
```

> 📖 [完整部署文档 →](./docs/)

---

## 开源策略

Saros 是 ZWISERFIT 分层开源策略的 **🟢 完全开放层**：

| 层级 | 开源策略 | 说明 |
|:--|:--|:--|
| 🟢 **Saros Open** | MIT 完全开源 | 任何健身房/工作室可自由部署和定制 |
| 🟡 **KinTwin SDK** | SDK开源·核心闭源 | 硬件API开放·行为流算法闭源 |
| 🔴 **Zeus Protocols** | 极小开放·协议文档 | Agent通信标准·Oracle解码器闭源 |
| ⚫ **9-Agent Kernel** | 全闭源·架构图纸 | 调度器·审计引擎·四流拓扑 |

---

## 贡献

欢迎开发者、健身房运营者、AI 研究者：

1. 🐛 发现 Bug？→ [提交 Issue](https://github.com/ZWISERFIT/ZWISERFIT/issues/new)
2. 💡 有想法？→ [发起 Discussion](https://github.com/ZWISERFIT/ZWISERFIT/discussions)
3. 🔧 准备写代码？→ [挑选 Good First Issue](https://github.com/ZWISERFIT/ZWISERFIT/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

详见 [`./community/CONTRIBUTING.md`](./community/)

---

> **Saros · Dongguan, Guangdong, China**
> *SaaS第一次有了会用工具的人。*
> ⭐ [Star ZWISERFIT](https://github.com/ZWISERFIT/ZWISERFIT)

📄 MIT
