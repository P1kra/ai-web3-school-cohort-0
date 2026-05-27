# Week 2｜Direction Deep-Dive Pack: AI Agent Payment Commerce

## 概述

本文档整合 Week 2 所有 Module 任务的分析成果，形成完整的"AI Agent Payment Commerce"方向深度分析包。

## 一句话定位

**PayGuard**：部署在 AI Agent 和区块链之间的支付中间件，让 Agent 能自主花钱但不乱花钱。目标是成为 Agent 经济的基础设施层。

## 为什么选这个方向

### 市场时机
- AI Agent 已经开始产生真实消费需求（API 费用、数据采购、算力租赁）
- 每日数十亿次 Agent-to-API 调用中，缺乏原生的 Web3 支付方案
- x402 协议提供了一个开放标准，但缺少中间件层

### 个人契合度
- 6 年 Web3 经验，理解钱包、交易、Gas 等概念
- 云服务运营经验，理解计费、订阅、API 定价模型
- 不需要深度 AI 技术背景，聚焦在支付基础设施层

### 竞争格局
- Cobo Agentic Wallet：钱包层，策略驱动
- Capsule：MPC 层，私钥管理
- x402：协议层，支付标准
- **PayGuard 的机会**：中间件层，连接协议、钱包和 Agent

## 技术架构

```
┌─────────────────────────────────────────┐
│              Human Interface             │
│     (Telegram / Dashboard / Email)       │
│     审批大额 ｜ 查看报告 ｜ 调整策略      │
└─────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────┐
│             PayGuard Core               │
│  ┌──────────┐ ┌──────────┐ ┌─────────┐ │
│  │ Intent   │ │ Policy   │ │ Audit   │ │
│  │ Parser   │ │ Engine   │ │ Logger  │ │
│  └──────────┘ └──────────┘ └─────────┘ │
└─────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────┐
│           Wallet Abstraction            │
│     Safe SDK ｜ Cobo SDK ｜ MPC SDK      │
└─────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────┐
│           Blockchain Layer              │
│        Base L2 (USDC Settlement)        │
└─────────────────────────────────────────┘
```

## 关键设计决策

| 决策 | 选择 | 理由 |
|------|------|------|
| 结算网络 | Base L2 | 低 gas、Coinbase 支持、USDC 流动性 |
| 钱包方案 | Smart Account (Safe) | 可编程权限、Session Key、gas 抽象 |
| 支付协议 | x402 | 开放标准、HTTP-native |
| 策略引擎 | 链下检查 + 链上约束 | 灵活且安全 |
| 人类界面 | Telegram Bot | 用户已经在用的平台 |

## 风险与缓解

| 风险 | 严重性 | 缓解 |
|------|--------|------|
| Prompt 注入导致恶意支付 | 高 | 策略引擎强制检查，大额人工审批 |
| Session Key 泄露 | 高 | 短有效期、资金隔离、异常检测 |
| x402 协议未被广泛采用 | 中 | 适配多种支付协议，不绑定单一标准 |
| 合规风险（MSB 牌照等） | 中 | 初期不托管资金，纯中间件模式 |
| Agent 经济未如预期爆发 | 中 | 模块化设计，可单独用于人类支付场景 |

## 下一步（Week 3-4 计划）

1. **技术验证**（Week 3）：
   - 部署 Safe 智能账户到 Base 测试网
   - 跑通 CAW + x402 最小支付闭环
   - 实现基础策略引擎（预算上限、白名单）

2. **产品成型**（Week 4）：
   - 开发 Telegram Bot 审批界面
   - 实现审计日志和日报生成
   - Hackathon Demo 准备

3. **生态对接**（Week 5+）：
   - 开源 PayGuard SDK
   - 文档和开发者指南
   - 寻找首批合作 Agent 项目

## 附录：Week 2 任务清单

| 任务 | 文档 | 状态 |
|------|------|------|
| Direction Research | week2-direction-research.md | ✅ |
| Payment Flow | week2-payment-flow.md | ✅ |
| Agent Profile | week2-agent-profile.md | ✅ |
| Wallet Permission | week2-wallet-permission.md | ✅ |
| Security Threat Model | week2-security-threat-model.md | ✅ |
| Governance/Coordination | week2-governance-coordination.md | ✅ |
| x402 + CAW Loop | week2-x402-caw-loop.md | ✅ |
| Final Deliverable | 本文档 | ✅ |
