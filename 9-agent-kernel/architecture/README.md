# 9-Agent Kernel Architecture

> ⚫ Proprietary (Reference Only) | 四流拓扑 · Agent拓扑图 · 数据流图

## 架构文档

- `four-stream-topology.md` — 四流架构拓扑
- `agent-topology.md` — 9-Agent 拓扑关系图
- `data-flow.md` — 全链路数据流图
- `trust-layer.md` — 信任层架构

## 设计原则

- **每个Agent是独立OS** — 有自己的调度器、文件系统、协议栈
- **四流并行** — 认知→资产生产→运营→审计 24×7 并行
- **自愈闭环** — Watchdog 三级闭环 + Escalation L1→L3
- **Stella独立审计** — 免疫系统，对指挥层和执行层均有独立审计权

## 注意事项

⚠️ 本目录文档仅供架构参考。核心调度器、审计引擎、四流拓扑代码全闭源。

## 许可证

Proprietary — Architecture diagrams for reference only
