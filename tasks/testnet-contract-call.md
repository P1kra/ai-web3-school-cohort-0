# 测试网智能合约调用 — WETH on Sepolia

## 基本信息

| 项目 | 内容 |
|------|------|
| 测试网 | Sepolia (Ethereum Testnet) |
| 合约地址 | `0xfFf9976782d46CC05630D1f6eBAb18b2324d6B14` |
| 合约名称 | Wrapped Ether (WETH) |
| 区块浏览器 | [Sepolia Etherscan](https://sepolia.etherscan.io/address/0xfFf9976782d46CC05630D1f6eBAb18b2324d6B14#readContract) |
| 当前区块 | 10,916,627 |
| Gas Price | ~1.0 gwei |

## 读函数调用结果

我通过 Python web3.py 库，使用公共 RPC (`ethereum-sepolia.publicnode.com`) 连接到 Sepolia 测试网，调用了 WETH 合约的以下只读函数：

### 1. `name()` — 合约名称
```
Wrapped Ether
```

### 2. `symbol()` — 代币符号
```
WETH
```

### 3. `decimals()` — 小数位数
```
18
```

### 4. `totalSupply()` — 总供应量
```
221,224.13 WETH
```

### 5. `balanceOf(address)` — 查询某地址余额
查询地址：`0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045`（vitalik.eth）
余额：`0.0545 WETH`

## 执行过程说明

1. **在哪里发起调用**：在服务器终端通过 web3.py 脚本发起 RPC 调用
2. **调了什么**：WETH 合约的 5 个只读函数（name / symbol / decimals / totalSupply / balanceOf）
3. **读 vs 写的区别**：所有调用都是 **只读（read）** 操作，不需要钱包签名、不需要支付 gas、不改变链上状态。写操作（如 transfer、approve）则需要钱包签名 + 支付 gas + 人工确认
4. **如何验证**：通过 [Sepolia Etherscan](https://sepolia.etherscan.io/address/0xfFf9976782d46CC05630D1f6eBAb18b2324d6B14#readContract) 的 Read Contract 页面可以独立验证所有返回值
5. **哪些步骤需要人工确认**：
   - ✅ 只读调用：无需确认，AI Agent 可自动执行
   - ⚠️ 如果做写操作（转账/授权/部署）：必须在钱包中手动签名确认，Agent 不能代签

## 关键理解

- **合约地址** = 合约在链上的"门牌号"，所有交互都通过这个地址
- **读函数** = 免费查询，不消耗 gas，不需要私钥签名
- **写函数** = 改变链上状态，消耗 gas，需要私钥签名 → 必须人工确认
- **区块浏览器** = 链上数据的"搜索引擎"，可以验证任何交易和合约状态
- **RPC 节点** = 连接区块链的"入口"，可以自建或用公共节点

## 代码

```python
from web3 import Web3

w3 = Web3(Web3.HTTPProvider("https://ethereum-sepolia.publicnode.com"))
contract = w3.eth.contract(
    address="0xfFf9976782d46CC05630D1f6eBAb18b2324d6B14",
    abi=[...],  # WETH ABI
)
name = contract.functions.name().call()  # 只读，无需签名
```

## AI 辅助说明

- AI 帮我查找了 Sepolia 上的 WETH 合约地址和 ABI
- AI 编写了 web3.py 调用脚本
- 所有只读调用由 AI 自动完成（不涉及资金）
- 本任务未进行写操作，如后续需要部署合约或转账，我会手动确认签名
