# Deploy Scripts

> 🟢 MIT | 一键部署 · Docker · K8s · 运维脚本

本目录存放 Saros 的部署和运维脚本。

## 内容规划

- `docker-compose.yml` — 单机部署（Momo + SaaS + 依赖服务）
- `k8s/` — Kubernetes 部署配置
- `scripts/` — 运维脚本（备份/恢复/健康检查/日志轮转）
- `env.example` — 环境变量模板

## 快速部署

```bash
git clone https://github.com/ZWISERFIT/ZWISERFIT.git
cd ZWISERFIT/saros-open/deploy
cp env.example .env
# 编辑 .env 填入你的配置
docker-compose up -d
```

## 许可证

MIT
