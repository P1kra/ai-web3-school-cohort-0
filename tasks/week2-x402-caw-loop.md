# Week 2｜x402 Paywall + CAW Agent Autonomous Payment Loop

## x402 协议解析

x402 是 Coinbase 提出的基于 HTTP 402 Payment Required 状态码的 Web3 支付协议。

### 协议流程

```
1. Agent 请求 API
   GET /api/gpt4 HTTP/1.1
   Host: api.service.com
   
2. 服务端返回 402 + 支付信息
   HTTP/1.1 402 Payment Required
   X-402-Payment: {
     "chainId": 8453,
     "token": "USDC",
     "amount": "0.50",
     "recipient": "0x..."
   }
   
3. Agent 完成支付，拿到 tx hash
   
4. Agent 用 tx hash 换取访问权限
   GET /api/gpt4?tx=0xabc...
   
5. 服务端验证链上支付 → 返回 API 结果
```

### 协议关键特性

- **无许可**：任何 HTTP 服务都可以返回 402
- **链无关**：通过 chainId 指定结算网络
- **无中间人**：支付直接发生在 Agent 和服务商之间
- **可验证**：链上交易任何人可查

## CAW 支付闭环

CAW（Coinbase Agent Wallet / Autonomous Payment）展示了 x402 的完整支付闭环。

### 核心组件

```
┌──────────────────┐
│   AI Agent       │ ← LLM 驱动的对话/任务 Agent
│   (消费者)        │
└────────┬─────────┘
         │ 402 响应
         ▼
┌──────────────────┐
│   PayGuard       │ ← 策略引擎（预算/白名单/审批）
│   (中间件)        │
└────────┬─────────┘
         │ 放行后签名
         ▼
┌──────────────────┐
│   Smart Account  │ ← Safe / Cobo 智能合约钱包
│   (签名层)        │
└────────┬─────────┘
         │ USDC 转账
         ▼
┌──────────────────┐
│   Base L2        │ ← 链上结算
│   (结算层)        │
└────────┬─────────┘
         │ tx hash
         ▼
┌──────────────────┐
│   API Service    │ ← 验证支付 → 返回服务
│   (服务商)        │
└──────────────────┘
```

### 进阶：Agent-to-Agent 支付

如果服务商本身也是一个 AI Agent（比如翻译 Agent、数据分析 Agent），那么 x402 可以实现 Agent 间的自主支付网络：

1. Agent A 需要翻译服务 → 查询链上注册表 → 找到 Agent B
2. Agent A 向 Agent B 发请求 → Agent B 返回 402
3. Agent A 通过 PayGuard 支付 USDC
4. Agent B 验证 → 返回翻译结果
5. 全程无需人类介入（如果金额在预算内）

## 现有方案的局限性

| 局限 | 描述 | 可能的改进 |
|------|------|-----------|
| 无预算管理 | x402 本身不管 Agent 花多少钱 | PayGuard 策略引擎 |
| 无争议机制 | 服务不满意怎么办？ | 托管合约 + 争议期 |
| 无身份验证 | Agent 是谁？ | DID + 链上声誉 |
| 单币种 | 目前主要 USDC | 多代币支持 |
| 无退款 | 链上交易不可逆 | 有条件退款（HTLC） |

## 我计划做的 Demo

用 CAW + x402 跑通一个最小支付闭环：
1. 搭建一个简单的 HTTP API（返回随机数 / 笑话 / 翻译）
2. 配置 402 返回
3. 创建 Agent 操作钱包（Base 测试网）
4. Agent 请求 API → 收到 402 → 支付 → 获得结果
5. 完整记录审计日志
