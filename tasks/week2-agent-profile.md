# Week 2｜Agent Profile and Capability Claim: "PayGuard"

## Agent 身份

- **名称**：PayGuard
- **定位**：AI Agent 支付中间件 — 让 Agent 能花钱，但不乱花钱
- **一句话**：Your AI Agent's financial controller. Spend autonomously, audit always.

## 能力声明

PayGuard 是一个部署在 AI Agent 和区块链之间的支付网关，提供以下核心能力：

### 1. 意图解析（Intent Parsing）
- 输入：AI Agent 的支付意图（自然语言或结构化 JSON）
- 输出：标准化的支付请求（金额、代币、接收方、用途）
- 能力边界：解析但不创造意图 — Agent 决定花不花钱，PayGuard 决定能不能花

### 2. 策略引擎（Policy Engine）
- **预算管理**：按周期（日/周/月）设定总预算，实时追踪剩余额度
- **白名单**：预先批准的接收方地址列表
- **金额分级**：
  - < $1：自动放行
  - $1-$50：策略检查通过后放行
  - > $50：必须人工审批
- **频率限制**：同一接收方 1 小时内最多 10 笔

### 3. 交易执行（Transaction Execution）
- 通过 Smart Account + Session Key 签名
- 支持 USDC（Base / Arbitrum）
- Gas 费自动估算和追加
- 失败自动重试（最多 3 次）

### 4. 审计与告警（Audit & Alert）
- 每笔支付生成人类可读收据
- 日报/周报自动汇总
- 异常检测：金额突变、新地址首付、频率异常

## 能力边界（明确声明不做的事）

- **不保管私钥**：依赖 Smart Account 基础设施
- **不做投资决策**：PayGuard 是支付执行层，不是交易策略层
- **不替代人类审批**：大额交易始终需要人类确认

## 技术依赖

- Smart Account：Safe{Core} 或 Cobo Agentic Wallet
- 支付协议：x402（HTTP 402 Web3 实现）
- 链：Base L2（低 gas，USDC 生态）
- 前端：Telegram Bot / Web Dashboard（人类审批界面）

## 与现有方案的差异

| 对比 | Cobo Agentic Wallet | Capsule | **PayGuard** |
|------|-------------------|---------|-------------|
| 钱包模型 | 智能合约钱包 | MPC EOA | 钱包无关（适配层） |
| 策略执行 | 链上 | 链下 MPC | 链上 + 链下混合 |
| 支付协议 | 无特定协议 | 无特定协议 | x402 native |
| 审计 | 钱包内查看 | 有限 | 完整审计日志 + 告警 |
