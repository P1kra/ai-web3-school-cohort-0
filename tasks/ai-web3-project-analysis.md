# AI × Web3 项目分析报告

> 分析日期：2026年5月23日
> 关注方向：Agent Wallet + Agent Payment Commerce

---

## 项目一：Cobo Agentic Wallet（CAW）

### 一句话总结

**Cobo Agentic Wallet 是全球首个基于 MPC（多方计算）的 AI Agent 专用钱包，让 AI Agent 可以在用户设定的"契约"范围内自主进行链上交易和支付。**

---

### 1. 项目概述

Cobo 成立于 2017 年，是一家总部位于新加坡的数字资产托管和钱包基础设施公司。在此之前，Cobo 已经服务了大量机构客户，累计安全保障了 **超过 3.8 万亿美元**资产、创建了 **2 亿+ 个钱包**、支持 **80+ 条公链**，历史上 **零安全事故**。

CAW 于 2026 年 4 月 20 日正式发布，是一个专门为 AI Agent 打造的下一代钱包产品。它的核心理念是：**给 Agent 一份"契约"（Pact），而不是把私钥直接交出去。**

---

### 2. AI 部分：Agent 如何"使用"这个钱包

#### 2.1 自然语言驱动的任务委托

用户用自然语言告诉 AI Agent 想做什么，比如：

- "帮我在 30 天内用 1 万 USDC 定投 ETH"
- "把 5 万 USDC 放到不同 DeFi 协议里优化收益"
- "每天处理不超过 500 美元的小额支付"

Agent 收到指令后，会**自动起草一份 Pact（契约）**，里面包含：
- **Intent**（意图）：要完成什么目标
- **Execution Plan**（执行计划）：具体怎么做
- **Policies**（策略限制）：单笔限额、日限额、白名单地址/协议等
- **Completion Conditions**（结束条件）：时间到期 / 预算花完 / 目标达成

用户审核通过后，Agent 就开始自主执行，不需要每笔交易都让人手动点"确认"。

#### 2.2 Recipe（技能配方）系统

CAW 内置了一套 **Recipe 库**——相当于给 Agent 的"操作手册"。预制 Recipe 覆盖了：

| 类别 | 具体 Recipe |
|------|------------|
| 交易 | Uniswap V3 Swap、Jupiter Swap（Solana）、Hyperliquid 现货交易 |
| 策略 | DCA 定投、网格交易 |
| DeFi | Aave V3 借贷、Compound V3 借贷、WETH 包装 |
| 支付 | Token 转账、Superfluid 流支付、x402 支付、Stripe 小额支付 |
| 预测市场 | Polymarket 下单 |

因为有 Recipe，Agent **不再"幻觉"**——它不会瞎编合约地址、不会搞错 ABI 参数。每一步都走已验证的路径。

#### 2.3 框架兼容性

CAW 原生集成主流 AI 框架：**LangChain、OpenAI Agents SDK、Claude MCP、Agno、CrewAI**。开发者一条 `npx skills` 命令就能接入：

```bash
npx skills add CoboGlobal/cobo-agentic-wallet --skill cobo-agentic-wallet --yes --global
```

---

### 3. Web3 部分：链上安全和去中心化控制

#### 3.1 MPC 私钥分片（核心安全机制）

CAW 不使用传统的单一私钥模式，而是用 **MPC（多方计算）** 把私钥拆成多个"碎片"，分布在三个角色之间：

```
Agent 密钥碎片  +  Cobo 密钥碎片  →  Pact 授权的交易自动签名
用户密钥碎片   +  Cobo 密钥碎片  →  高价值操作审批 & 治理
```

关键点：
- **任何单一方都不能独立签名**——即使 Agent 被黑了、LLM 被注入了恶意指令，没有 Cobo 那半边碎片也动不了钱
- **用户可以随时恢复完整的私钥控制权**——备份自己的碎片，脱离 Cobo 也能独立恢复，这是真正的自托管（non-custodial）

#### 3.2 Pact = 链上可执行的授权协议

Pact 不仅是软件层面的"权限设置"，而是被 MPC 基础设施**在签名层面强制执行**的。这意味着 Agent 就算"想"超额转账，MPC 签名环节就不让它过。

Pact 生命周期：
```
提交 → 用户审批 → 执行中（实时可监控）→ 自动完成/到期销毁
```

用户可以随时在手机 App 上一键冻结所有正在执行的 Pact。

#### 3.3 双模式支持

- **MPC 模式**（已上线）：高安全场景，AI Agent 自动签名 + 用户可冻结
- **托管模式**（即将上线）：高频低延迟场景（如微支付、自动打赏）

#### 3.4 多链多资产支持

支持 Ethereum、Base、Arbitrum、Optimism、Polygon、Solana 等 **80+ 条链**，**3000+ 种代币**。

---

### 4. 可验证材料

| 材料类型 | 内容 |
|----------|------|
| 产品页面 | https://www.cobo.com/agentic-wallet |
| 官方发布公告 | https://www.cobo.com/post/cobo-launches-agentic-wallet-how-ai-agents-interact-on-chain（2026.4.20） |
| 技术深度文章 | https://www.cobo.com/post/agentic-wallet-ai-crypto-wallet-guide（2026.4.28） |
| GitHub | https://github.com/CoboGlobal/cobo-agentic-wallet |
| 开发者文档 | https://www.cobo.com/products/agentic-wallet/manual |
| Recipe 库 | https://www.cobo.com/agentic-wallet/recipes |
| 网安战绩 | 8 年零安全事故，ISO 27001 + AICPA SOC 认证 |
| 移动端 | iOS App Store + Google Play 均已上架 |

---

### 5. 我的判断与收获

**为什么这个项目值得关注：**

1. **它解决了 Agent × Payment 的核心矛盾。** 之前 AI Agent 要做支付，要么把私钥给 Agent（极度危险），要么每次人工确认（效率极低）。CAW 的 Pact 机制找到了"可控自主"的平衡点——Agent 能自主干活，但跑不出你画的圈。

2. **"契约"这个概念非常妙。** Pact 不是传统的"权限开关"（要么全开要么全关），而是每个任务一张"临时通行证"，任务完成就自动过期。这在 DeFi、DAO 财库管理、Agent-to-Agent 商务场景中有极大的想象空间。

3. **Recipe 体系降低了门槛。** 非技术用户不需要写代码，Agent 自己就知道怎么去 Uniswap 换币、去 Aave 存款。这解决了"Agent 有权限但不知道怎么操作"的尴尬。

4. **MPC 是真正的差异化。** 市面上大多数 agentic wallet 用 TEE（可信执行环境）或 API 密钥，本质上是软件级安全。MPC 是数学级安全——和 Cobo 服务 3.8 万亿资产的机构安全体系是同源的。

**我的疑问：**

- 目前 CAW 还处于邀请制早期阶段，实际用户规模和生态成熟度有待观察
- Agent-to-Agent 支付真的跑通了吗？比如两个不同框架的 Agent 之间能否互相支付？
- 如果 Cobo 的 MPC 服务宕机，虽然用户不会丢钱，但 Agent 是不是就停摆了？

---

### 6. 来源链接

- Cobo Agentic Wallet 官网：https://www.cobo.com/agentic-wallet
- 官方发布稿（2026.4.20）：https://www.cobo.com/post/cobo-launches-agentic-wallet-how-ai-agents-interact-on-chain
- Agentic Wallet 技术详解：https://www.cobo.com/post/agentic-wallet-ai-crypto-wallet-guide
- 开发者快速入门：https://www.cobo.com/products/agentic-wallet/manual/developer/quickstart-overview
- GitHub 开源仓库：https://github.com/CoboGlobal/cobo-agentic-wallet
- Recipe 用例库：https://www.cobo.com/agentic-wallet/recipes

---

## 项目二：Phala Network — TEE 驱动的 AI 协处理器

### 一句话总结

**Phala Network 是一个基于 TEE（可信执行环境）的去中心化 AI 协处理器，让智能合约能安全、私密地调用链下 AI Agent 执行计算，并为 AI Agent 提供可验证的"黑箱"运行环境。**

---

### 1. 项目概述

Phala Network 最初在 2020 年启动，最初是 Polkadot 生态的隐私计算平行链。经过多年演进，现已转型为聚焦 **AI × Web3 的协处理器（Coprocessor）**——你可以把它理解成区块链的"AI 外挂"：

- 智能合约天然不适合跑 AI（算力贵、速度慢、链上数据全公开）
- Phala 在链下运行 AI 计算，但把**计算结果的可验证证明**送回链上
- 所有计算在 TEE 硬件加密环境中完成，连节点运营者也看不到里面跑了什么

截至 2024 年 Q4（Messari 报告数据）：
- 全年处理了 **超过 2.7 亿次**合约执行
- 部署了 **4,991 个** AI Agent Contract
- 节点网络约 **17,420 个**活跃 Worker（Phala 链）
- 12 月月度活跃用户达 **1,125** 人（历史新高，同比增长 63%）

---

### 2. AI 部分：Agent 如何在 TEE 中运行

#### 2.1 TEE = AI Agent 的"防作弊黑箱"

TEE（Trusted Execution Environment）是 CPU/GPU 内部的一个硬件级安全区域。在 TEE 里运行的代码和数据，**连机器的物理管理员都看不到**。

对 AI Agent 的意义：
- Agent 的代码和关键数据（比如私钥、API 密钥、交易策略）在 TEE 里跑 → 加密保护
- 任何人——包括运行节点的矿工——都无法窃取 Agent 的"大脑"
- 远程验证（Remote Attestation）机制可以证明 Agent 确实在真实 TEE 硬件里跑，没有被篡改

#### 2.2 AI Agent Contract：用 TypeScript 写链下 AI

Phala 的 AI Agent Contract 是一套让开发者用 **TypeScript/JavaScript** 编写链下 AI 程序的框架。智能合约发起请求 → Phala 的 Worker 节点在 TEE 里执行 → 结果回链上。

这意味着：
- 一个 DeFi 智能合约可以调用 TEE 里的 AI 模型做风险评估
- 一个 NFT 合约可以调用 TEE 里的 AI 做图片生成
- AI Agent 可以在 TEE 里持有私钥、自主交易，外界无法干预

#### 2.3 GPU TEE 基准测试：AI 推理几乎无损

Phala 在 NVIDIA H100 和 H200 GPU 上做了 TEE 性能测试：
- H100：典型 LLM 推理任务的开销 **低于 5%**
- H200：典型 LLM 推理任务的开销 **低于 7%**
- 大模型（如 Llama-3.1-70B）的开销几乎为零

这意味着在 TEE 里跑 AI 模型的**安全和隐私几乎不影响性能**。

#### 2.4 关键合作：ai16z × Eliza 框架

2024 年底，Phala 与 **ai16z（Shaw 团队）** 合作，将 TEE 能力集成到了 **Eliza**——目前最火的 Web3 AI Agent 开源框架。Eliza Agent 的 RAG 记忆系统、媒体分析、自主交易等功能都在 TEE 里执行，实现了我前面说的"防作弊黑箱"。

基于此衍生出的 **Spore.fun** 是一个实验性项目：AI Agent 自己在 Solana 上发币、交易、繁殖——用赚到的钱支付 Phala 的 TEE 服务器租金，实现自给自足的数字生命。

---

### 3. Web3 部分：去中心化协处理器网络

#### 3.1 三重安全架构：ZKP + TEE + MPC

Phala 的安全不是单一技术，而是三层叠加：

| 技术层 | 做什么 | 解决什么问题 |
|--------|--------|------------|
| **TEE**（Intel TDX + NVIDIA GPU TEE） | 计算在加密硬件里执行 | 代码和数据私密性、可验证性 |
| **ZKP**（零知识证明） | 证明计算正确但不泄露内容 | 隐私交易验证 |
| **MPC**（多方计算） | 多方协作计算、互不暴露数据 | 跨机构数据协作 |

#### 3.2 去中心化节点网络

全球任何人可以部署 TEE 兼容硬件，成为 Worker 节点提供算力，赚取 PHA 代币奖励。节点运营者看不到租户的计算内容，这构成了一个 **去中心化的保密云计算市场**。

- 能管理多达 **100 万 CPU 核心**、超过 10 万个节点
- 支持 PHA 代币质押机制（StakePool）确保节点经济安全

#### 3.3 向以太坊生态的战略迁移

2024 年底，Phala 宣布**放弃 Polkadot 平行链（Khala），整体迁移至以太坊**。原因：
- Intel 将于 2025 年停止 SGX 支持，Khala 链上的 SGX 节点将无法运行
- 转向 Intel TDX 和 NVIDIA GPU TEE 等下一代平台
- 在以太坊上建设 Layer 2 Rollup（Op-Succinct 方案）+ TEE 市场

这是一次重大的生态战略调整，从 Polkadot 的独立链变成以太坊生态的基础设施层。

#### 3.4 DStack：TEE 应用的 Docker

Phala 推出了 **DStack**——一个让开发者像用 Docker 一样部署 TEE 应用的平台。支持一键部署 Docker 镜像到加密虚拟机（CVM），实时监控，信任验证。

---

### 4. 可验证材料

| 材料类型 | 内容 |
|----------|------|
| 官网 | https://phala.network |
| Messari 研报（Q4 2024） | https://messari.io/report/state-of-phala-q4-2024 |
| TEE 安全框架白皮书 | https://phala.network/posts/coprocessor-security-verification-framework |
| NEAR AI × Phala TEE SDK | https://near.ai/blog/building-next-gen-near-ai-infrastructure-with-tees |
| NVIDIA H100 TEE 基准测试 | https://phala.network/posts/confidential-computing-on-nvidia-h100-gpu-a-performance-benchmark-study |
| ai16z × Phala 合作 | 集成到 Eliza 框架，2024 Q4 |
| 2025 路线图 | Phala 2.0：GPU TEE + Op-Succinct L2 + Phala Cloud |
| GitHub | https://github.com/Phala-Network |

---

### 5. 我的判断与收获

**为什么这个项目值得关注：**

1. **"AI 协处理器"这个定位很精准。** 它不试图让区块链本身运行 AI（不现实），而是做链和 AI 之间的"桥梁"——智能合约说"我需要 AI 做个判断"，Phala 帮它跑完再把结果公证回链上。

2. **TEE 解决了一个真实痛点：Agent 的"不透明性"。** 如果一个 AI Agent 帮你管钱，你怎么知道它的代码没有被节点运营者偷偷改了？TEE + 远程验证让你能证明 Agent 跑的代码就是开源的、没被篡改的那一份。这个能力在 Agent 管钱的场景中是底层刚需。

3. **GPU TEE 性能损失很小（<7%）是一个关键数据点。** 它说明隐私计算不是"安全但慢到没法用"的东西，实际部署是可行的。

4. **和 Eliza/ai16z 的合作让 Phala 找到了 PMF（产品市场契合）。** Eliza 是目前 Web3 AI Agent 的事实标准框架，把这个集成做了，等于把生态的"高速公路入口"占了。

**我的疑问：**

- TEE 的安全性高度依赖 Intel/NVIDIA 的硬件，如果硬件有漏洞（比如之前的 SGX 侧信道攻击），整个系统的安全假设会崩塌吗？
- 从 Polkadot 迁移到以太坊虽然是理性的技术选择，但会不会导致原有生态用户流失？
- Phala 是"AI Agent 的基础设施"，它本身不直接做 Agent Wallet。它和 Cobo 这类 Agent Wallet 产品是互补关系——Phala 提供 TEE 运行环境，Cobo 提供 MPC 签名授权——但用户需要理解这两层的关系，这对非技术用户有门槛。

---

### 6. 来源链接

- Phala Network 官网：https://phala.network
- Messari Q4 2024 研报：https://messari.io/report/state-of-phala-q4-2024
- TEE 安全验证框架：https://phala.network/posts/coprocessor-security-verification-framework
- NEAR AI × Phala TEE SDK 发布：https://near.ai/blog/building-next-gen-near-ai-infrastructure-with-tees
- Phala AI Agent Contract 文档：https://docs.phala.network/ai-agent-contract/getting-started
- DStack 技术文档：https://docs.phala.network/overview/phala-network/dstack

---

## 两个项目的互补关系总结

放到 **Agent Wallet + Agent Payment Commerce** 这个视角下，这两个项目实际上解决的是同一问题的两个不同层面：

```
┌─────────────────────────────────────────────────┐
│                 AI Agent 要做支付                 │
├─────────────────────────────────────────────────┤
│  Cobo Agentic Wallet                             │
│  → "支付授权"层：谁批准？花多少？往哪花？            │
│  → MPC 签名 + Pact 策略 + Recipe 执行              │
├─────────────────────────────────────────────────┤
│  Phala Network                                   │
│  → "运行环境"层：Agent 的代码安全吗？没被篡改吗？     │
│  → TEE 加密执行 + 远程验证 + 隐私保护               │
└─────────────────────────────────────────────────┘
```

一个负责 **"Agent 有没有权限做这件事"**，另一个负责 **"Agent 本身是不是可信的"**。两者结合才是完整的 Agent 安全支付方案。

---

> **作者备注**：本文档基于公开资料整理分析，数据截至 2026 年 5 月。文中所有判断和疑问仅代表个人研究观点，不构成投资建议。
