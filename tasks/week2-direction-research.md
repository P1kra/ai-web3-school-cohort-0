# Week 2｜Direction Research: AI × Web3 Problem Map & Main Direction Selection

**方向：AI Native Wallet + Agent Payment Commerce**

## 1. AI × Web3 问题地图

### 1.1 核心矛盾
AI Agent 在 Web3 场景中面临一个根本张力：**自主性 vs 安全性**。

- Agent 需要自主执行链上操作（支付、签名、合约交互），但私钥一旦完全交给 Agent，就失去了人类对资产的最终控制
- 现有的解决方案（EOA 私钥托管、MPC 分片、Smart Account）各有权衡，没有一个"银弹"

### 1.2 问题空间分解

| 层级 | 问题 | 当前状态 | 机会 |
|------|------|----------|------|
| 身份层 | Agent 如何证明"我是谁" | DID/VC 方案碎片化 | Agent 可验证身份 + 声誉系统 |
| 权限层 | Agent 能花多少钱、调哪些合约 | 大多靠人类预授权 | 可编程策略引擎（时间窗口、预算上限、合约白名单） |
| 执行层 | Agent 如何安全签名交易 | EOA 托管 / Smart Account | 条件签名、多签 Agent、意图（Intent）模式 |
| 验证层 | 人类如何确认 Agent 没乱来 | 大多靠事后查账 | 实时监控 + 异常告警 + 可撤回机制 |
| 结算层 | Agent 间如何完成支付 | 传统支付网关 | x402、Agent-to-Agent 微支付 |

### 1.3 三条技术路径对比

| 路径 | 代表方案 | 优点 | 缺点 |
|------|----------|------|------|
| **Smart Account + Session Key** | Cobo Agentic Wallet, Safe{Core} | 灵活，可编程 | 需要智能合约钱包生态支持 |
| **MPC + Policy Engine** | Capsule, Lit Protocol | 不依赖合约钱包，兼容现有 EOA | 策略执行在链下，有信任假设 |
| **Intent + Solver 网络** | Anoma, Essential | 解耦意图表达与执行，隐私友好 | 生态还在早期，Solver 集中化风险 |

### 1.4 我选择的方向：Agent Payment Commerce

**为什么选这个方向：**

1. **需求真实且紧迫**：AI Agent 已经开始产生消费需求（API 调用费、数据采购、算力租赁），但支付基础设施完全跟不上
2. **技术栈在成熟**：x402 协议提供了 HTTP 402 Payment Required 的 Web3 实现，Cobo 的 Agentic Wallet 提供了策略层，CAW 提供了 Agent 自主支付的参考实现
3. **差异化空间大**：当前方案要么太偏技术（x402 纯协议层），要么太偏托管（Cobo 中心化钱包），缺少一个"开发者友好的 Agent 支付中间件"
4. **个人优势**：Web3 交易经验 6 年，理解支付场景的痛点；有云服务运营经验，理解 B2B 计费模型

**我计划探索的方向：** 一个面向 AI Agent 的支付网关，让 Agent 能：
- 用可编程预算自主完成小额支付
- 人类设置"护栏"（每日上限、白名单、审批阈值）
- 所有操作链上可审计

## 2. 关键项目 / 论文跟踪

- **x402 (Coinbase)**：HTTP 402 协议 Web3 实现，让 API 可以原生接受 USDC 支付
- **Cobo Agentic Wallet**：策略驱动的智能合约钱包，支持 Session Key + 预算控制
- **CAW (Agent Autonomous Payment)**：x402 + 钱包的完整支付闭环示范
- **Safe{Core}**：模块化智能账户基础设施
- **Capsule**：MPC 钱包 + 可编程策略

## 3. 下一步

- 深入理解 x402 协议规范
- 搭建 CAW demo 跑通支付闭环
- 设计自己的"Agent 支付网关"最小可行方案
