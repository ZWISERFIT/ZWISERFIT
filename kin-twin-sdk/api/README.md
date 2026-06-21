# KinTwin Hardware API

> 🟡 MIT (API) | 门禁/摄像头/体测仪 SDK 接口规范

本目录存放 KinTwin 硬件层的 API 规范和接口文档。

## API 模块

- **Gate API** — 人脸识别门禁接口
- **Camera API** — 多摄像头行为采集接口
- **BodyScanner API** — 体测仪数据接口
- **DID Bridge** — DID 身份绑定接口

## 设计原则

- 硬件无关性 — API 规范不绑定特定硬件厂商
- 密码学不可否认性 — 每一条数据采集记录都有签名
- 实时流式 — WebSocket + gRPC 双向流

## 许可证

MIT (API specification) / Proprietary (implementation)
