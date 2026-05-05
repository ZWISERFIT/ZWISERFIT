# 贡献指南 | Contributing to ZWISERFIT

> 🫂 **你不是在"帮我"——你是在建设自己未来会用到的基础设施。**
> 每一位贡献者都是 ZWISERFIT 开源生态的共建者。

感谢你来到 ZWISERFIT！本项目以 **线下实体门店为根基**，致力于共建健康行为数据资产化开源协议层。无论你是嵌入式工程师、前端开发者、AI 研究员、健身行业从业者，还是对项目感兴趣的普通用户——这里都有你能参与的切入点。

阅读我们的[社区宪法](./CONSTITUTION.md)了解项目核心原则。

---

## 📋 目录

- [行为准则](#行为准则)
- [如何参与](#如何参与)
  - [报告 Bug](#报告-bug)
  - [功能请求](#功能请求)
  - [文档改进](#文档改进)
  - [代码贡献](#代码贡献)
- [Pull Request 流程](#pull-request-流程)
- [分支命名规范](#分支命名规范)
- [Commit Message 格式](#commit-message-格式)
- [代码风格](#代码风格)
- [开发环境搭建](#开发环境搭建)
- [沟通渠道](#沟通渠道)
- [首次贡献者友好指南](#首次贡献者友好指南)
- [贡献者认可](#贡献者认可)

---

## 行为准则

本项目遵循 [贡献者公约 2.1](./CODE_OF_CONDUCT.md)。参与即表示你同意遵守其条款。我们致力于为每一位参与者营造**尊重、包容、诚实、协作**的社区环境。

---

## 如何参与

### 报告 Bug 🐛

发现 Bug？太好了——说明你在认真使用我们的项目。

**提交 Bug 报告前：**
1. 🔍 搜索 [已有 Issues](https://github.com/ZWISERFIT/ZWISERFIT/issues)，确认 Bug 未被报告
2. 📖 检查文档确认该行为是否按设计工作

**提交 Bug 报告时：**
- 使用 `Bug report` Issue 模板
- 包含**环境信息**（操作系统、OpenClaw 版本、Hermes Agent 版本）
- 提供**最小复现步骤**
- 描述**预期行为**与**实际行为**
- 附上相关日志或截图

### 功能请求 💡

有改进想法？我们非常欢迎！ZWISERFIT 正在攻克人脸机数据通路、POS 对接等核心难题——你的功能建议可能正巧能解决某个关键阻碍。

**提交功能请求时：**
- 使用 `Feature request` Issue 模板
- 描述**该功能解决什么问题**
- 说明**期望的方案**
- 列出**备选方案**（如果有）
- 添加相关上下文（行业背景、技术限制等）

### 文档改进 📝

文档是 ZWISERFIT 的第一公民，不是事后补充。我们尤其欢迎：
- 中文翻译优化（项目采用中英双语）
- 操作手册补充（Momo 部署指南、ZWF-20 配置说明）
- 架构图与流程图更新
- 多语言翻译贡献

文档贡献可直接提交 PR，无需先开 Issue。

### 代码贡献 💻

#### 当前急需贡献方向

| 🏷️ 标签 | 方向 | 说明 |
|:---|:---|:---|
| `help wanted` | 嵌入式/IoT | 人脸机数据对接、RS-485/MQTT 中间件 |
| `good first issue` | 入门友好 | 文档修复、小功能增强 |
| `data-pipeline` | 数据管线 | ZWF-20 标准实现、数据脱敏工具 |
| `momo-core` | AI 店长 | Hermes Agent 场景增强 |
| `security` | 安全审计 | 权限模型、数据加密 |

---

## Pull Request 流程

1. **Fork** 本仓库并 Clone 到本地
2. 从 `main` 分支创建你的功能分支（参考[分支命名规范](#分支命名规范)）
3. 编写代码并添加必要的测试
4. 确保 commit message 符合[规范](#commit-message-格式)
5. 推送分支并创建 Pull Request
6. 在 PR 描述中填写 [PR 模板](./.github/PULL_REQUEST_TEMPLATE.md)
7. 等待 Code Review，回应反馈

**PR 审查标准：**
- ✅ 代码逻辑清晰、有适当注释
- ✅ 变更范围聚焦，一个 PR 解决一个问题
- ✅ 文档已同步更新
- ✅ 数据相关变更必须声明数据来源级别（L1/L2/L3）

---

## 分支命名规范

```
<type>/<short-description>
```

| Type | 用途 | 示例 |
|:---|:---|:---|
| `feat/` | 新功能 | `feat/momo-daily-report` |
| `fix/` | Bug 修复 | `fix/data-pipeline-timeout` |
| `docs/` | 文档更新 | `docs/api-reference` |
| `refactor/` | 代码重构 | `refactor/auth-module` |
| `test/` | 测试相关 | `test/face-recognition` |
| `chore/` | 构建/工具链 | `chore/update-deps` |

**示例：** `feat/zwf20-face-data-import`、`fix/momo-hallucination-filter`

---

## Commit Message 格式

我们遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

**Type：**
- `feat` — 新功能
- `fix` — Bug 修复
- `docs` — 文档变更
- `style` — 代码格式（不影响功能）
- `refactor` — 重构
- `test` — 测试
- `chore` — 构建/工具

**示例：**
```
feat(momo): 新增会员训练报告自动生成

基于 Hermes Agent 实现每日训练报告自动生成与企微推送。
数据来源：L1 实测数据（人脸机打卡）+ L2 测试记录。

Closes #42
```

```
fix(data-pipeline): 修复高并发下数据脱敏竞态条件

数据脱敏模块在 >1000 QPS 场景下偶现未脱敏字段泄漏。
根因：shared buffer 未加同步锁。现已增加 mutex 保护。

Fixes #58
```

---

## 代码风格

- **Markdown**：中文为主，关键术语中英双语（如：数据管道 Data Pipeline）
- **配置/YAML**：2 空格缩进
- **Python**：遵循 PEP 8，使用 Black 格式化
- **Shell**：使用 `#!/bin/bash`，通过 ShellCheck 检查
- **注释**：关键逻辑必须有注释，尤其是数据脱敏/合规相关代码

---

## 开发环境搭建

### 基础环境

```bash
# 1. 克隆仓库
git clone https://github.com/ZWISERFIT/ZWISERFIT.git
cd ZWISERFIT

# 2. 安装 OpenClaw 框架
npm install -g openclaw

# 3. 配置 Hermes Agent（参考 docs/ 目录下的部署指南）

# 4. 验证环境
openclaw --version
```

### 数据相关贡献者额外步骤

如果你参与数据管线相关开发，请先阅读：
- [CONSTITUTION.md](./CONSTITUTION.md) — 数据主权条款（Article I）
- ZWF-20 数据标准文档（`standards/` 目录）

---

## 沟通渠道

| 渠道 | 用途 | 链接 |
|:---|:---|:---|
| **GitHub Issues** | Bug 报告、功能请求、技术讨论 | [Issues](https://github.com/ZWISERFIT/ZWISERFIT/issues) |
| **GitHub Discussions** | 社区交流、想法分享、Q&A | [Discussions](https://github.com/ZWISERFIT/ZWISERFIT/discussions) |
| **企业微信群** | 实时沟通、紧急问题 | 联系 founder@zwiserfit.com 获取邀请 |
| **邮件** | 生态合作、投资接洽 | [founder@zwiserfit.com](mailto:founder@zwiserfit.com) |

> ⚠️ 邮件标题请注明 `[ZWISERFIT合作] - 您的公司/姓名`。

---

## 首次贡献者友好指南

**第一次参与开源？** 这里是你的起点：

### 🟢 零门槛入门（无需编程）

1. **阅读并反馈**：浏览 [README.md](./README.md) 和 [CONSTITUTION.md](./CONSTITUTION.md)，标注不清晰的地方
2. **文档纠错**：发现错别字、链接失效？提交一个小 PR 修复它
3. **翻译贡献**：帮助将文档翻译为英文或其他语言
4. **使用反馈**：部署 Momo 数字店长后，分享你的使用体验

### 🟡 初级贡献（少量编程）

1. 查看带 `good first issue` 标签的 Issue
2. 从文档改进或简单 Bug 修复入手
3. 在 Issue 评论区留言表明你正在处理（我们会保留给你）

### 🟠 进阶贡献（需要专业背景）

1. **嵌入式/IoT**：人脸识别终端数据对接
2. **AI/ML**：Hermes Agent 场景增强
3. **数据工程**：ZWF-20 标准实现
4. **安全审计**：全链路安全加固

### 💡 贡献小贴士

- 📖 **先看宪法**：[CONSTITUTION.md](./CONSTITUTION.md) 定义了项目核心价值观
- 🔍 **搜索已有 Issue**：避免重复劳动
- 💬 **大胆提问**：在 Issue 下留言，我们乐意帮助新贡献者
- 🚫 **不必完美**：你的第一个 PR 不必完美——Code Review 会帮助你改进
- 🎯 **从小做起**：一个 typo 修复也是有价值的贡献

---

## 贡献者认可

我们珍视每一位贡献者。贡献者将在以下方面获得认可：

- 🏆 **Contributors 榜单**：所有代码贡献者列入项目 README 和官网
- 📜 **数据贡献者署名**：数据相关贡献在 SOURCE.md 中署名
- 🎖️ **核心维护者晋升**：持续高质量贡献者可晋升为核心维护者
- 📝 **社区宪法签名**：重要贡献者将被邀请在 CONSTITUTION.md 签署

---

> 📄 本项目以 Apache 2.0 协议开源。贡献者保留其贡献的全部权利。
> 项目原创架构、AI角色体系、商业模式与 ZXF-20/ZWF-20 数据标准归创始人莫淑瑜独家原创所有。

> **Last Updated / 最后更新：** 2026-05-05
