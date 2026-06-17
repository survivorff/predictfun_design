# Predict.fun 深度调研项目

> 调研日期：2026-06-17
> 数据来源：predict.fun 官网与开发者文档、BNB Chain 链上合约、YZi Labs/Binance 公告、加密媒体报道
> 调研对象：**单一平台深度剖析**（区别于参考项目的「生态横向调研」）

---

## 目录结构

```
research/
├── 01_market/                 # 市场情况：定位 / 规模 / 融资 / 收购 ✅
├── 02_business_architecture/  # 业务架构：核心模块与价值链 ✅
├── 03_tech_architecture/      # 技术架构：CLOB + CTF + UMA + Yield ✅
├── 04_user_experience/        # 用户体验：注册/入金/交易/提现/结算 ✅
├── 05_core_features_moat/     # 核心功能与交易技术壁垒 ✅
├── 06_business_model/         # 商业模式：费率/收入测算/画布 ✅
├── 07_token_points_airdrop/   # 代币 / Predict Points / 空投 ✅
├── 08_competitive_landscape/  # 竞争格局：vs Polymarket / Kalshi ✅
└── summary/
    ├── overview.md            # 全景汇总报告
    ├── open_questions.md      # 待确认问题清单
    └── limitations.md         # 调研局限性说明
```

---

## 报告导航

| # | 维度 | 核心内容 | 报告 |
|---|------|----------|------|
| 01 | 市场情况 | BNB 原生定位、$1.8B+ 交易量、YZi/Susquehanna 融资、收购 Probable | [查看](./01_market/analysis.md) |
| 02 | 业务架构 | 交易/收益/结算/增长四大模块 | [查看](./02_business_architecture/analysis.md) |
| 03 | 技术架构 | 链下 CLOB + 链上 CTF + UMA 预言机 + Yield-Bearing 合约族 + 账户抽象 | [查看](./03_tech_architecture/analysis.md) |
| 04 | 用户体验 | Web / Binance Wallet 双入口注册、入金、交易、提现、结算全流程 | [查看](./04_user_experience/analysis.md) |
| 05 | 核心功能与壁垒 | 生息抵押、Gasless 交易、智能钱包、做市积分 + 壁垒评分 | [查看](./05_core_features_moat/analysis.md) |
| 06 | 商业模式 | 2% 概率加权费率、收入测算、商业画布 | [查看](./06_business_model/analysis.md) |
| 07 | 代币/积分/空投 | Predict Points 机制、做市积分快照、空投预期 | [查看](./07_token_points_airdrop/analysis.md) |
| 08 | 竞争格局 | vs Polymarket（Polygon）/ Kalshi（合规）/ BNB 生态站位 | [查看](./08_competitive_landscape/analysis.md) |

---

## 核心发现（TL;DR）

1. **生息抵押品（Yield-Bearing Collateral）** 是结构性创新——押注期间资金不闲置，链上已部署专门的 `YieldBearingConditionalTokens` 合约族佐证。
2. **Binance 全家桶背书** ——YZi Labs 多次投资、CZ 站台、Binance Wallet 原生 Gasless 集成、创始人前 Binance 背景。
3. **技术是 Polymarket 的 BNB 改良分叉** ——同样 CTF + CLOB + UMA 兼容预言机，差异在链选、生息、账户抽象。
4. **东方野心** ——主服务器东京、收购 Probable、岳小鱼任亚太负责人，重点吃中文/亚洲市场。
5. **积分驱动增长** ——Predict Points + 空投预期，做市积分每分钟快照计分。
6. **大事件渠道飞轮** ——世界杯 $2M 奖池 + Binance 入口，3 天 2 万 DAU。

---

## 调研方法

- **官方开发者文档（dev.predict.fun）**：API、SDK、链上合约地址、订单簿计价机制
- **链上合约核验**：CTF / Yield-Bearing / UMA Adapter / NegRisk / FeeModule 部署地址
- **多来源交叉验证**：融资、收购、交易量、用户数
- **竞品对照**：Polymarket / UMA 官方文档印证架构

## 调研局限性

- 收益路由的具体 DeFi 协议未完全公开（推断）
- 费率细节来自第三方口径，未逐项官方核验
- 交易量/用户数为不同时间点快照
- 尚未发币，代币经济为推断

详见 [summary/limitations.md](./summary/limitations.md)
