# Predict.fun 概念科普目录

> 系统性理解 Predict.fun（BNB Chain 原生预测市场）的业务与技术概念

---

## 01 基础设施 (Infrastructure)

| 文档 | 主题 |
|------|------|
| [01-bnb-chain.md](01-infrastructure/01-bnb-chain.md) | BNB Chain：Chain ID 56、低 Gas、EVM 兼容、主服务器东京 |
| [02-usdt-collateral.md](01-infrastructure/02-usdt-collateral.md) | USDT：Predict.fun 的交易资产与结算货币 |
| [03-gasless-meta-tx.md](01-infrastructure/03-gasless-meta-tx.md) | Gasless：Binance 代付 Gas + 账户抽象，用户无需持有 BNB |
| [04-rhino-bridge.md](01-infrastructure/04-rhino-bridge.md) | Rhino Bridge：资产如何跨链进入 BNB Chain |

## 02 代币与资产 (Tokens & Assets)

| 文档 | 主题 |
|------|------|
| [01-conditional-token-framework.md](02-tokens-and-assets/01-conditional-token-framework.md) | Gnosis CTF：条件代币框架，YES/NO 代币的铸造与赎回 |
| [02-erc1155-standard.md](02-tokens-and-assets/02-erc1155-standard.md) | ERC-1155：多代币标准 |
| [03-yield-bearing-tokens.md](02-tokens-and-assets/03-yield-bearing-tokens.md) | 生息条件代币：YieldBearingConditionalTokens（核心差异化） |
| [04-negrisk-multi-outcome.md](02-tokens-and-assets/04-negrisk-multi-outcome.md) | NegRisk：多结果市场机制 |

## 03 交易机制 (Trading)

| 文档 | 主题 |
|------|------|
| [01-clob-order-matching.md](03-trading/01-clob-order-matching.md) | CLOB：链下撮合 + 链上原子结算的混合架构 |
| [02-order-types.md](03-trading/02-order-types.md) | 订单类型：市价 / 限价 |
| [03-probability-weighted-fees.md](03-trading/03-probability-weighted-fees.md) | 概率加权费率：~2% 峰值随价格偏离 50% 递减 |
| [04-price-equals-probability.md](03-trading/04-price-equals-probability.md) | 价格 = 概率：隐含概率机制 |
| [05-orderbook-yes-no-complement.md](03-trading/05-orderbook-yes-no-complement.md) | 订单簿：只存 YES、NO 取补、深度与价差 |

## 04 结算与预言机 (Settlement)

| 文档 | 主题 |
|------|------|
| [01-uma-compatible-oracle.md](04-settlement/01-uma-compatible-oracle.md) | UMA 兼容乐观预言机：乐观提交 + DVM 仲裁 |
| [02-resolution-redeem.md](04-settlement/02-resolution-redeem.md) | 结果上链与赎回：份额兑付 $1 / 归零 |
| [03-dispute-mechanism.md](04-settlement/03-dispute-mechanism.md) | 争议机制：质押挑战 + UMA 投票裁决 |

## 05 钱包与身份 (Wallet & Identity)

| 文档 | 主题 |
|------|------|
| [01-eip712-non-custodial.md](05-wallet-and-identity/01-eip712-non-custodial.md) | 非托管交易 + EIP-712 签名订单 |
| [02-predict-account-privy.md](05-wallet-and-identity/02-predict-account-privy.md) | Predict Account：基于 Privy 的智能钱包 |
| [03-zerodev-account-abstraction.md](05-wallet-and-identity/03-zerodev-account-abstraction.md) | ZeroDev 账户抽象：Gasless 交易与提现 |
| [04-binance-keyless-wallet.md](05-wallet-and-identity/04-binance-keyless-wallet.md) | Binance Keyless Wallet：无私钥一键开户 |
| [05-api-key-auth.md](05-wallet-and-identity/05-api-key-auth.md) | API 认证：auth message → EIP-712 → JWT |

## 06 API 与数据 (API & Data)

| 文档 | 主题 |
|------|------|
| [01-rest-api.md](06-api-and-data/01-rest-api.md) | REST API：市场/订单/持仓/账户端点 |
| [02-websocket.md](06-api-and-data/02-websocket.md) | WebSocket：实时订单簿与成交推送 |
| [03-sdk.md](06-api-and-data/03-sdk.md) | SDK：TypeScript 与 Python |
| [04-oauth-integration.md](06-api-and-data/04-oauth-integration.md) | OAuth：第三方代用户下单 |

## 07 市场运营 (Market Operations)

| 文档 | 主题 |
|------|------|
| [01-event-vs-market.md](07-market-operations/01-event-vs-market.md) | Event vs Market：数据结构关系 |
| [02-market-lifecycle.md](07-market-operations/02-market-lifecycle.md) | 市场生命周期：完整状态机 |
| [03-market-categories.md](07-market-operations/03-market-categories.md) | 市场分类：加密/体育/政治/宏观/娱乐/AI |
| [04-predict-points-rewards.md](07-market-operations/04-predict-points-rewards.md) | Predict Points 与做市奖励：每分钟快照计分 |

## 08 链上合约 (Contracts)

| 文档 | 主题 |
|------|------|
| [01-ctf-exchange.md](08-contracts/01-ctf-exchange.md) | CTFExchange：订单结算合约（生息 + 非生息双轨） |
| [02-yield-bearing-contracts.md](08-contracts/02-yield-bearing-contracts.md) | 生息合约族：YieldBearingConditionalTokens / WrappedCollateral |
| [03-uma-adapter.md](08-contracts/03-uma-adapter.md) | UMA Adapter：预言机适配器 |

## 09 合规与风控 (Compliance)

| 文档 | 主题 |
|------|------|
| [01-geo-restrictions.md](09-compliance/01-geo-restrictions.md) | 地区访问限制 |
| [02-kyc.md](09-compliance/02-kyc.md) | KYC：身份验证与 Binance 集成 |

## 10 生态与集成 (Ecosystem)

| 文档 | 主题 |
|------|------|
| [01-binance-wallet-integration.md](10-ecosystem/01-binance-wallet-integration.md) | Binance Wallet 集成：触达 200M+ 用户 |
| [02-venus-yield-integration.md](10-ecosystem/02-venus-yield-integration.md) | Venus 生息集成：抵押品收益来源 |
| [03-probable-acquisition.md](10-ecosystem/03-probable-acquisition.md) | 收购 Probable：整合亚洲流动性与社区 |
