# ZWISERFIT API 可运行代码示例 v0.1

**文档编号:** ZWF-LUNA-API-001  
**版本:** v0.1  
**编制:** Luna（全球开发者生态运营）  
**审核待提交:** Tristan（技术架构官）  
**日期:** 2026-05-14  
**目标:** 为 ZWISERFIT 核心 API 接口提供三语言（curl / Node.js / Python）可运行代码示例

---

## 概述

本文档覆盖 ZWISERFIT AI 门店管理系统最常用的 API 接口。每个接口均提供：
1. 接口说明
2. curl 示例（可复制到终端直接运行）
3. Node.js 示例（含错误处理）
4. Python 示例（含错误处理）
5. 预期响应格式

> ⚠️ 假设 ZWISERFIT 服务运行在 `http://localhost:3000`（开发环境）或 `https://api.zwiserfit.com`（生产环境）
> 可通过环境变量 `ZWISERFIT_API_BASE` 切换。

---

## 0. 前置条件

```bash
# 确保服务在运行
curl -s http://localhost:3000/api/health

# 预期响应:
# {"status":"ok","version":"0.1.0","timestamp":"2026-05-14T00:00:00Z"}
```

---

## 1. 健康检查 — GET /api/health

**用途:** 验证服务是否正常运行 + 获取版本信息

### curl

```bash
curl -s http://localhost:3000/api/health | jq .
```

```json
{
  "status": "ok",
  "version": "0.1.0",
  "timestamp": "2026-05-14T00:00:00Z",
  "uptime": 123456
}
```

### Node.js

```javascript
// health-check.js
const API_BASE = process.env.ZWISERFIT_API_BASE || 'http://localhost:3000';

async function checkHealth() {
  try {
    const response = await fetch(`${API_BASE}/api/health`);
    
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    const data = await response.json();
    console.log('✅ ZWISERFIT 服务状态:');
    console.log(`   状态: ${data.status}`);
    console.log(`   版本: ${data.version}`);
    console.log(`   运行时间: ${data.uptime}s`);
    
    return data;
  } catch (error) {
    console.error('❌ 健康检查失败:', error.message);
    process.exit(1);
  }
}

checkHealth();
```

```bash
# 运行
node health-check.js
```

### Python

```python
# health_check.py
import os
import json
import sys
from urllib.request import Request, urlopen
from urllib.error import URLError

API_BASE = os.getenv('ZWISERFIT_API_BASE', 'http://localhost:3000')

def check_health():
    try:
        req = Request(f'{API_BASE}/api/health')
        with urlopen(req, timeout=10) as resp:
            data = json.loads(resp.read().decode())
            
        print('✅ ZWISERFIT 服务状态:')
        print(f'   状态: {data["status"]}')
        print(f'   版本: {data["version"]}')
        print(f'   运行时间: {data["uptime"]}s')
        
        return data
    except URLError as e:
        print(f'❌ 健康检查失败: {e.reason}')
        sys.exit(1)
    except json.JSONDecodeError:
        print('❌ 响应格式异常')
        sys.exit(1)

if __name__ == '__main__':
    check_health()
```

```bash
# 运行
python health_check.py
```

---

## 2. 获取门店 AI Agent 状态 — GET /api/stores/{storeId}/agents

**用途:** 查询指定门店所有 AI Agent 的运行状态（适合 IoT 仪表盘调用）

### curl

```bash
curl -s http://localhost:3000/api/stores/store-001/agents | jq .
```

```json
{
  "storeId": "store-001",
  "agents": [
    {
      "id": "agent-ordering-001",
      "type": "order_management",
      "status": "active",
      "lastActive": "2026-05-14T00:00:00Z",
      "metrics": {
        "ordersProcessed": 128,
        "avgResponseTimeMs": 342
      }
    },
    {
      "id": "agent-inventory-001",
      "type": "inventory",
      "status": "active",
      "lastActive": "2026-05-14T00:00:00Z",
      "metrics": {
        "stockAlerts": 3,
        "lowStockItems": ["item-042", "item-107"]
      }
    }
  ]
}
```

### Node.js

```javascript
// get-store-agents.js
const API_BASE = process.env.ZWISERFIT_API_BASE || 'http://localhost:3000';
const STORE_ID = process.env.STORE_ID || 'store-001';

async function getStoreAgents(storeId) {
  try {
    const response = await fetch(`${API_BASE}/api/stores/${storeId}/agents`);
    
    if (response.status === 404) {
      console.error(`❌ 门店 ${storeId} 未找到`);
      return null;
    }
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    
    const data = await response.json();
    
    console.log(`📍 门店: ${data.storeId}`);
    console.log(`🤖 Agent 数量: ${data.agents.length}`);
    
    data.agents.forEach(agent => {
      const icon = agent.status === 'active' ? '🟢' : '🔴';
      console.log(`${icon} ${agent.type} (${agent.id})`);
      console.log(`   上次活跃: ${agent.lastActive}`);
    });
    
    return data;
  } catch (error) {
    console.error('❌ 查询失败:', error.message);
    process.exit(1);
  }
}

getStoreAgents(STORE_ID);
```

```bash
# 运行
node get-store-agents.js
```

### Python

```python
# get_store_agents.py
import os
import json
import sys
from urllib.request import Request, urlopen
from urllib.error import HTTPError, URLError

API_BASE = os.getenv('ZWISERFIT_API_BASE', 'http://localhost:3000')
STORE_ID = os.getenv('STORE_ID', 'store-001')

def get_store_agents(store_id):
    try:
        req = Request(f'{API_BASE}/api/stores/{store_id}/agents')
        with urlopen(req, timeout=10) as resp:
            data = json.loads(resp.read().decode())
            
        print(f'📍 门店: {data["storeId"]}')
        print(f'🤖 Agent 数量: {len(data["agents"])}')
        
        for agent in data['agents']:
            icon = '🟢' if agent['status'] == 'active' else '🔴'
            print(f'{icon} {agent["type"]} ({agent["id"]})')
            print(f'   上次活跃: {agent["lastActive"]}')
            
        return data
        
    except HTTPError as e:
        if e.code == 404:
            print(f'❌ 门店 {store_id} 未找到')
        else:
            print(f'❌ HTTP {e.code}: {e.reason}')
        sys.exit(1)
    except URLError as e:
        print(f'❌ 网络错误: {e.reason}')
        sys.exit(1)

if __name__ == '__main__':
    get_store_agents(STORE_ID)
```

```bash
# 运行
python get_store_agents.py
```

---

## 3. 提交订单 — POST /api/orders

**用途:** 通过 AI 店长系统提交新订单（第三方 POS 集成入口）

### curl

```bash
curl -s -X POST http://localhost:3000/api/orders \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ZWISERFIT_API_KEY}" \
  -d '{
    "storeId": "store-001",
    "customerId": "cust-042",
    "items": [
      {"sku": "SKU-001", "name": "经典拿铁", "quantity": 2, "unitPrice": 28.00},
      {"sku": "SKU-003", "name": "牛角包", "quantity": 1, "unitPrice": 15.00}
    ],
    "notes": "少冰"
  }' | jq .
```

```json
{
  "orderId": "ORD-20260514-001",
  "storeId": "store-001",
  "status": "created",
  "totalAmount": 71.00,
  "estimatedWaitMinutes": 5,
  "confirmationMessage": "已收到您的订单，预计5分钟后可取",
  "createdAt": "2026-05-14T00:00:00Z"
}
```

### Node.js

```javascript
// create-order.js
const API_BASE = process.env.ZWISERFIT_API_BASE || 'http://localhost:3000';
const API_KEY = process.env.ZWISERFIT_API_KEY;

async function createOrder(orderData) {
  try {
    const headers = {
      'Content-Type': 'application/json'
    };
    if (API_KEY) {
      headers['X-API-Key'] = API_KEY;
    }
    
    const response = await fetch(`${API_BASE}/api/orders`, {
      method: 'POST',
      headers,
      body: JSON.stringify(orderData)
    });
    
    if (response.status === 401) {
      console.error('❌ API 密钥无效，请检查 ZWISERFIT_API_KEY');
      process.exit(1);
    }
    if (response.status === 422) {
      const errors = await response.json();
      console.error('❌ 参数验证失败:', errors.details);
      process.exit(1);
    }
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    
    const data = await response.json();
    console.log(`✅ 订单创建成功`);
    console.log(`   订单号: ${data.orderId}`);
    console.log(`   金额: ¥${data.totalAmount.toFixed(2)}`);
    console.log(`   预计等待: ${data.estimatedWaitMinutes} 分钟`);
    console.log(`   消息: ${data.confirmationMessage}`);
    
    return data;
  } catch (error) {
    console.error('❌ 订单创建失败:', error.message);
    process.exit(1);
  }
}

// 使用示例
createOrder({
  storeId: 'store-001',
  customerId: 'cust-042',
  items: [
    { sku: 'SKU-001', name: '经典拿铁', quantity: 2, unitPrice: 28.00 },
    { sku: 'SKU-003', name: '牛角包', quantity: 1, unitPrice: 15.00 }
  ],
  notes: '少冰'
});
```

### Python

```python
# create_order.py
import os
import json
import sys
from urllib.request import Request, urlopen
from urllib.error import HTTPError, URLError

API_BASE = os.getenv('ZWISERFIT_API_BASE', 'http://localhost:3000')
API_KEY = os.getenv('ZWISERFIT_API_KEY')

def create_order(order_data):
    headers = {'Content-Type': 'application/json'}
    if API_KEY:
        headers['X-API-Key'] = API_KEY
    
    try:
        req = Request(
            f'{API_BASE}/api/orders',
            data=json.dumps(order_data, ensure_ascii=False).encode(),
            headers=headers,
            method='POST'
        )
        with urlopen(req, timeout=10) as resp:
            data = json.loads(resp.read().decode())
        
        print(f'✅ 订单创建成功')
        print(f'   订单号: {data["orderId"]}')
        print(f'   金额: ¥{data["totalAmount"]:.2f}')
        print(f'   预计等待: {data["estimatedWaitMinutes"]} 分钟')
        print(f'   消息: {data["confirmationMessage"]}')
        
        return data
        
    except HTTPError as e:
        if e.code == 401:
            print('❌ API 密钥无效，请检查 ZWISERFIT_API_KEY')
        elif e.code == 422:
            errors = json.loads(e.read().decode())
            print(f'❌ 参数验证失败: {errors.get("details", errors)}')
        else:
            print(f'❌ HTTP {e.code}')
        sys.exit(1)
    except URLError as e:
        print(f'❌ 网络错误: {e.reason}')
        sys.exit(1)

if __name__ == '__main__':
    create_order({
        'storeId': 'store-001',
        'customerId': 'cust-042',
        'items': [
            {'sku': 'SKU-001', 'name': '经典拿铁', 'quantity': 2, 'unitPrice': 28.00},
            {'sku': 'SKU-003', 'name': '牛角包', 'quantity': 1, 'unitPrice': 15.00}
        ],
        'notes': '少冰'
    })
```

```bash
# 运行
# 1. 先设置 API Key（如不需要则跳过）
export ZWISERFIT_API_KEY="your-api-key-here"
# 2. 运行
python create_order.py
```

---

## 4. 查询门店运营总览 — GET /api/stores/{storeId}/dashboard

**用途:** 开发者整合门店核心运营数据到自建仪表盘

### curl

```bash
curl -s "http://localhost:3000/api/stores/store-001/dashboard?period=24h" \
  -H "X-API-Key: ${ZWISERFIT_API_KEY}" | jq .
```

```json
{
  "storeId": "store-001",
  "period": "24h",
  "summary": {
    "totalOrders": 142,
    "totalRevenue": 3980.50,
    "avgOrderValue": 28.03,
    "peakHour": "12:00-13:00",
    "activeAgents": 4,
    "pendingAlerts": 2
  },
  "topItems": [
    {"sku": "SKU-001", "name": "经典拿铁", "quantity": 58},
    {"sku": "SKU-003", "name": "牛角包", "quantity": 32}
  ],
  "agentHealth": {
    "healthy": 4,
    "degraded": 0,
    "down": 0
  }
}
```

### Node.js

```javascript
// get-dashboard.js
const API_BASE = process.env.ZWISERFIT_API_BASE || 'http://localhost:3000';
const API_KEY = process.env.ZWISERFIT_API_KEY;
const STORE_ID = process.env.STORE_ID || 'store-001';

async function getDashboard(storeId, period = '24h') {
  const url = new URL(`${API_BASE}/api/stores/${storeId}/dashboard`);
  url.searchParams.set('period', period);
  
  const headers = {};
  if (API_KEY) headers['X-API-Key'] = API_KEY;
  
  try {
    const response = await fetch(url.toString(), { headers });
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    
    const data = await response.json();
    console.log(`📊 ${storeId} 运营总览 (${period})`);
    console.log(`━━━━━━━━━━━━━━━━━━━━━`);
    console.log(`订单数:   ${data.summary.totalOrders}`);
    console.log(`营收:     ¥${data.summary.totalRevenue.toFixed(2)}`);
    console.log(`客单价:   ¥${data.summary.avgOrderValue.toFixed(2)}`);
    console.log(`高峰期:   ${data.summary.peakHour}`);
    console.log(`Agent健康: 🟢${data.agentHealth.healthy} 🟡${data.agentHealth.degraded} 🔴${data.agentHealth.down}`);
    
    return data;
  } catch (error) {
    console.error('❌ 查询失败:', error.message);
    process.exit(1);
  }
}

getDashboard(STORE_ID, '24h');
```

### Python

```python
# get_dashboard.py
import os
import json
import sys
from urllib.request import Request, urlopen
from urllib.error import HTTPError, URLError
from urllib.parse import urlencode

API_BASE = os.getenv('ZWISERFIT_API_BASE', 'http://localhost:3000')
API_KEY = os.getenv('ZWISERFIT_API_KEY')
STORE_ID = os.getenv('STORE_ID', 'store-001')

def get_dashboard(store_id, period='24h'):
    params = urlencode({'period': period})
    url = f'{API_BASE}/api/stores/{store_id}/dashboard?{params}'
    
    headers = {}
    if API_KEY:
        headers['X-API-Key'] = API_KEY
    
    try:
        req = Request(url, headers=headers)
        with urlopen(req, timeout=10) as resp:
            data = json.loads(resp.read().decode())
        
        print(f'📊 {store_id} 运营总览 ({period})')
        print('━━━━━━━━━━━━━━━━━━━━━')
        print(f'订单数:   {data["summary"]["totalOrders"]}')
        print(f'营收:     ¥{data["summary"]["totalRevenue"]:.2f}')
        print(f'客单价:   ¥{data["summary"]["avgOrderValue"]:.2f}')
        print(f'高峰期:   {data["summary"]["peakHour"]}')
        health = data['agentHealth']
        print(f'Agent健康: 🟢{health["healthy"]} 🟡{health["degraded"]} 🔴{health["down"]}')
        
        return data
        
    except HTTPError as e:
        print(f'❌ HTTP {e.code}: {e.reason}')
        sys.exit(1)
    except URLError as e:
        print(f'❌ 网络错误: {e.reason}')
        sys.exit(1)

if __name__ == '__main__':
    get_dashboard(STORE_ID, '24h')
```

```bash
# 运行
python get_dashboard.py
```

---

## 错误处理速查表

所有 API 接口遵循统一错误响应格式：

```json
{
  "error": {
    "code": "INVALID_STORE_ID",
    "message": "门店 ID 'invalid-999' 不存在",
    "status": 404,
    "details": ["possible typo in storeId"]
  }
}
```

| HTTP Status | Error Code | 含义 | 常见原因 |
|:---:|-----------|------|---------|
| 400 | BAD_REQUEST | 请求格式错误 | JSON 解析失败 |
| 401 | UNAUTHORIZED | 未认证 | API Key 缺失/无效 |
| 404 | NOT_FOUND | 资源不存在 | 门店/订单 ID 错误 |
| 422 | VALIDATION_ERROR | 参数验证失败 | 缺少必填字段 |
| 429 | RATE_LIMITED | 频率限制 | 超过 100 req/min |
| 500 | INTERNAL_ERROR | 服务端错误 | 联系维护者 |

---

## 环境变量

```bash
# 在 .env 文件中设置
ZWISERFIT_API_BASE=http://localhost:3000       # API 地址
ZWISERFIT_API_KEY=your-api-key-here           # API 密钥（如有）
STORE_ID=store-001                              # 默认门店 ID
```

---

## 下一步

1. ✅ 覆盖 4 个核心接口 × 3 语言 = 12 个可运行示例
2. ⬜ Tristan 审核 API 路径与实际部署是否一致
3. ⬜ 部署后进行逐个接口的 e2e 验证
4. ⬜ 集成到 API 文档网站（生成 OpenAPI 3.0 规范）

---

*LUNA-0514-001 · ZWISERFIT API 可运行代码示例 v0.1*  
*编制: Luna 🌙*  
*待审核: Tristan（技术架构官）*  
*2026-05-14 · 天使轮冲刺 Day 4*
