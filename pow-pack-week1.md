# Week 1 Proof-of-Work Pack

> 皮卡（P1kra）· AI × Web3 School Cohort 0 · 2026-05-18 ~ 05-23

---

## 📋 提交清单

### 🤖 AI 学习

| 产出 | 链接 | 积分 |
|------|------|------|
| AI 基础概念卡片（6 个） | [daily/2026-05-19.md](daily/2026-05-19.md) | 10 |
| Learning Agent Setup 记录 | [daily/2026-05-18.md](daily/2026-05-18.md) | 20 |
| AI 可交互学习产物 | *(未完成)* | 30 |

### ⛓️ Web3 学习

| 产出 | 链接 | 积分 |
|------|------|------|
| Web3 基础概念卡片（8 个） | [daily/2026-05-20.md](daily/2026-05-20.md) | 10 |
| Sepolia 测试网交易 | [daily/2026-05-20.md](daily/2026-05-20.md) | 20 |
| EOA / 智能账户 / 多签对比 | [tasks/eoa-comparison.md](tasks/eoa-comparison.md) | 30 |

### 🔀 AI × Web3 综合

| 产出 | 链接 | 积分 |
|------|------|------|
| 受限 Web3 助手 Workflow 设计 | [tasks/restricted-web3-assistant.md](tasks/restricted-web3-assistant.md) | 40 |
| AI × Web3 项目拆解（Cobo + Phala） | [tasks/ai-web3-project-analysis.md](tasks/ai-web3-project-analysis.md) | 30 |
| Week 1 学习总结 | [learning-summary-week1.md](learning-summary-week1.md) | 20 |

### 🎙️ 线上活动（实时参加）

| 活动 | 日期 | 链接 | 积分 |
|------|------|------|------|
| 开营仪式 | 5/18 | [daily/2026-05-18.md](daily/2026-05-18.md) | 20 |
| Hermes Agent 入门 | 5/19 | *(待补)* | 20 |
| Web3 运行原理 | 5/20 | *(待补)* | 20 |
| AI 下乡计划 | 5/21 | *(待补)* | 20 |
| Co-learning | 5/22 | [daily/2026-05-22.md](daily/2026-05-22.md) | 20 |
| Week 1 例会 | 5/22 | [daily/2026-05-22.md](daily/2026-05-22.md) | 20 |
| Open Agentic Economy | 5/23 | [daily/2026-05-23.md](daily/2026-05-23.md) | 20 |

---

## ❌ 一个失败/卡点记录

**问题：** WCB API 的 `tasks.listForLearner` 只传 `programId` 不传 `trackId` 会静默返回空数组 `[]`，导致多次以为"没有任务"。排查了很久才从 API 文档里发现必须同时传 `trackId`。

**解决：** 通过 `program.getById` 获取 `curriculumWeeks[0].trackId`，然后用 `tasks.listForLearner(programId, trackId)` 拿到完整任务列表。

**教训：** API 不报错不代表用对了，静默返回空值比报错更坑。

---

## 🔢 积分汇总

| 类别 | 已提交 | 可获积分 |
|------|--------|----------|
| 前置准备 | 5/7 | 65 |
| AI 向 | 2/3 | 30 |
| Web3 向 | 3/4 | 60 |
| AI × Web3 综合 | 3/3 | 90 |
| 发布 & 观察 | 1/2 | 20 |
| 线上活动（实时） | 5/10 | 100 |
| 线上活动（回放） | 0/7 | 0 |
| **合计** | **19/36** | **365** |

---

> 📦 完整仓库：[github.com/P1kra/ai-web3-school-cohort-0](https://github.com/P1kra/ai-web3-school-cohort-0)
