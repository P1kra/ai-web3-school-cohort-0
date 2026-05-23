# Week 1 学习总结：AI × Web3 的第一次碰撞

## 一个 AI 概念我有了新理解

**Agent（智能体）**。进营之前我以为 Agent 就是"能聊天的 AI 助手"，但这周接触了 Hermes 之后才意识到，Agent 的核心是 **工具调用 + 自主决策**，不是单轮问答。一个真正的 Agent 能自己查资料、搜网页、执行命令、调用 API，还能在失败时自己换方案。尤其是了解了 MCP（模型上下文协议）后，发现 Agent 的可扩展性远超想象——接入不同 MCP Server 就能获得新能力，像搭积木一样。

## 一个 Web3 概念我有了新理解

**智能账户（Smart Account）**。做了 EOA vs 智能账户 vs 多签的对比后，发现 ERC-4337 的账户抽象不是"另一个钱包"，而是从根本上改变了"谁控制资产"这个模型。EOA 是单点私钥控制，丢了就没了；智能账户可以设限额、多人共管、恢复机制——这让 AI Agent 安全地管理链上资产成为可能，也是 Agent Payment 方向的基础设施。

## 一个 AI × Web3 交叉问题

**Agent 能不能自己发起支付？** 这周的讲座和任务让我理清了一个关键点：Agent 可以准备交易数据、估算 gas、检查余额——但不能代签。签名必须在用户本地完成，私钥不能离开用户设备。这意味着 Agent Wallet 的设计不是"让 AI 花钱"，而是"AI 提案 + 人类审批"的安全模式，或者通过智能账户的权限策略实现有限自治。

## 本周完成的 PoW

- 搭建了 GitHub 学习仓库，用 Learning Agent 管理学习流程
- 整理了 AI 基础概念卡片（LLM / Prompt / Context / Agent / MCP / Tool Use）
- 整理了 Web3 基础概念卡片（Wallet / Gas / Smart Contract / Testnet 等）
- 在 Sepolia 测试网完成了一笔测试转账
- 参加了 5 场实时讲座和 Co-learning
- 写了 EOA/智能账户/多签对比笔记
- 拆解了 AI×Web3 项目（Cobo Agentic Wallet 等）
- 设计了一个受限 Web3 助手 workflow

🔗 完整记录：[GitHub Repo](https://github.com/P1kra/ai-web3-school-cohort-0)

## 一个未解决的问题或 Week 2 想深入的方向

**如何验证 AI 的执行结果？** 这周学到链上操作可以用 tx hash + 区块浏览器验证，但如果 AI 帮你做了链下决策（比如"这个项目值得投资"），怎么验证它的推理过程？Week 2 想深入 Agent 的可验证性方向，结合 ZK / TEE 看看有没有成熟的方案。
