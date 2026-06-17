# Predict.fun 知识库

> 本仓库包含 Predict.fun 平台的系统性调研，可作为团队内部的预测市场知识分享和产品设计参考。
> Predict.fun 是 **BNB Chain 原生预测市场**，由 YZi Labs（原 Binance Labs）支持、CZ 公开站台，最大差异化是 **生息抵押品（Venus 路由）** 与 **Binance Wallet 原生 Gasless 集成**。

---

## 目录结构

```
docs/
├── predictfun-basics/              # Predict.fun 基础介绍（按功能模块）
│   ├── 01-platform-overview           # 平台概览与商业模式
│   ├── 02-technical-architecture      # 技术架构与智能合约
│   ├── 03-trading-mechanism           # 交易机制与订单系统
│   ├── 04-wallet-and-assets           # 钱包体系与资产结构
│   ├── 05-api-reference               # API 接口与 SDK 参考
│   ├── 06-settlement-and-oracle       # 结算机制与预言机
│   ├── 07-yield-and-capital-efficiency# 生息抵押与资本效率（核心差异化）
│   ├── 08-binance-wallet-integration  # Binance Wallet 集成（200M+ 用户入口）
│   ├── 09-user-journey-walkthrough    # 用户完整体验流程（含具体数值示例）
│   ├── 10-prediction-market-landscape # 全球预测市场竞争格局对比
│   └── 11-event-market-lifecycle      # 事件与市场完整生命周期
│
└── concepts/                       # 核心概念深度解析（按知识点拆分）
    ├── 01-infrastructure/             # BNB Chain / USDT / Gasless / Rhino Bridge
    ├── 02-tokens-and-assets/          # CTF / ERC-1155 / NegRisk / 生息条件代币
    ├── 03-trading/                    # CLOB / 订单类型 / 概率加权费率 / 价格=概率
    ├── 04-settlement/                 # UMA 兼容 Oracle / 赎回 / 争议
    ├── 05-wallet-and-identity/        # EIP-712 / Privy / ZeroDev / Binance Keyless
    ├── 06-api-and-data/               # REST / WebSocket / SDK / OAuth
    ├── 07-market-operations/          # Event vs Market / 生命周期 / 分类 / Predict Points
    ├── 08-contracts/                  # CTFExchange / 生息合约族 / UMA Adapter
    ├── 09-compliance/                 # 地区限制 / KYC
    └── 10-ecosystem/                  # Binance Wallet / Venus 生息 / 收购 Probable
```

---

## 快速导航

### Predict.fun 基础

| 文档 | 内容 | 推荐阅读顺序 |
|------|------|:---:|
| [平台概览](docs/predictfun-basics/01-platform-overview.md) | 什么是 Predict.fun、商业模式、市场数据、融资历程 | 1 |
| [生息抵押与资本效率](docs/predictfun-basics/07-yield-and-capital-efficiency.md) | 核心差异化：押注期间抵押品经 Venus 生息 | 2 |
| [用户完整体验流程](docs/predictfun-basics/09-user-journey-walkthrough.md) | Leo 视角走完全流程：开户→入金→交易→结算→提现（含具体数值） | 3 |
| [事件与市场生命周期](docs/predictfun-basics/11-event-market-lifecycle.md) | 一个事件从创建到赎回的完整阶段 | 4 |
| [技术架构](docs/predictfun-basics/02-technical-architecture.md) | 混合架构、BNB 链合约族、代币 ID 生成 | 5 |
| [交易机制](docs/predictfun-basics/03-trading-mechanism.md) | 链下 CLOB、订单状态机、概率加权费率 | 6 |
| [钱包与资产](docs/predictfun-basics/04-wallet-and-assets.md) | 账户分层、Privy/Keyless 钱包、USDT 资产、授权机制 | 7 |
| [API 参考](docs/predictfun-basics/05-api-reference.md) | REST/WebSocket 端点、SDK、认证、代码示例 | 8 |
| [结算与预言机](docs/predictfun-basics/06-settlement-and-oracle.md) | UMA 兼容乐观预言机、赎回机制、争议 | 9 |
| [Binance Wallet 集成](docs/predictfun-basics/08-binance-wallet-integration.md) | 200M+ 用户入口、Keyless、Gasless、虚拟盘 | 10 |
| [全球预测市场对比](docs/predictfun-basics/10-prediction-market-landscape.md) | Predict.fun/Polymarket/Kalshi 全维度对比 | 11 |

### 核心概念（按需查阅）

概念文档按知识点拆分为独立小文件，详见 [concepts/README.md](docs/concepts/README.md)。

涵盖：基础设施（BNB Chain/USDT/Gasless）、代币资产（CTF/生息条件代币）、交易机制（CLOB/概率加权费率）、结算（UMA 兼容 Oracle/赎回/争议）、钱包身份（EIP-712/Privy/ZeroDev/Binance Keyless）、API 数据、市场运营、合约地址、合规、生态集成（Binance Wallet/Venus/Probable）。

---

> 数据截至 2026 年 6 月，基于公开信息整理。本知识库仅供研究参考，不构成投资建议。
