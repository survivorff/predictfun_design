# Predict.fun 平台深度调研知识库

> **持续更新中** | 调研启动：2026-06-17 | 数据来源：predict.fun 官网与开发者文档（dev.predict.fun）、BNB Chain 链上合约、YZi Labs/Binance 公告、各加密媒体报道

本项目对 **predict.fun**——BNB Chain 原生预测市场平台——进行系统性深度调研，涵盖市场情况、业务架构、技术架构、用户体验路径、核心功能与交易技术壁垒、商业模式、代币/积分/空投、竞争格局等维度，所有图表使用 Mermaid 绘制。

> ⚠️ 调研内容仅供研究参考，不构成任何投资建议。部分数据为基于公开信息的推断，已在文中明确标注。

---

## 📌 一句话定位

**predict.fun 是由 YZi Labs（原 Binance Labs）支持、CZ 公开站台的 BNB Chain 原生预测市场，最大差异化是「DeFi 原生资本效率」——用户押注期间的抵押资金可同时赚取 DeFi 收益（Yield-Bearing Collateral）。**

口号：*"The BNB-native information market where it pays to be right."*

---

## 📊 核心数据速览（截至 2026 Q2，多来源汇总）

| 指标 | 数值 | 来源/备注 |
|------|------|-----------|
| 上线时间 | 2025-12-16（CZ 于 12-04 预告） | CoinDesk / ainvest |
| 累计交易量 | **$1.8B+** | cryptorank（YZi 复投公告） |
| 注册用户 | **130,000+** | cryptorank |
| 撮合订单数 | **4,000,000+** | cryptorank |
| 赚取收益的用户资金 | **$20M+** | cryptorank |
| TVL | **~$16.9M** | DefiLlama |
| 主要投资方 | YZi Labs（原 Binance Labs）、Susquehanna Crypto | cryptobriefing |
| 战略收购 | Probable（2026-03，PancakeSwap + YZi Labs 孵化） | blockonomi |
| 世界杯活动峰值 | 3 天内 2 万 DAU、18 万笔/日 | odaily |

> 注：交易量/用户数随时间快速增长，不同时间点口径不同（上线初 $300k → 收购 Probable 时 $1.5B → YZi 复投时 $1.8B+）。

---

## 🗂️ 目录结构

```
predictfun_design/
├── README.md                         ← 本文件
└── research/
    ├── README.md                     ← 调研总览与快速导航
    ├── 01_predictfun/
    │   └── analysis.md               ← 深度分析报告（8 大标准化章节）
    └── summary/
        ├── overview.md               ← 全景汇总报告
        ├── open_questions.md         ← 待确认问题清单
        └── limitations.md            ← 调研局限性说明
```

> 目录结构与参考项目 `polymarket_research` 对齐：**每个被调研对象一个文件夹，内含单个 `analysis.md`**，市场/业务/技术/UX 等所有维度作为编号章节集中在该文件内。

---

## 🔍 核心发现（TL;DR）

1. **「会生息的抵押品」是最大护城河**：predict.fun 在 Polymarket 式的 CLOB + 条件代币（CTF）架构之上，额外构建了一套 **Yield-Bearing 合约族**（`YieldBearingConditionalTokens` / `YieldBearingWrappedCollateral`）。用户下注的 USDT 在持仓期间被包装为生息抵押品，路由进 **Venus Protocol**（BNB Chain 最大借贷市场），理论年化 5–15%。这是当前唯一对闲置抵押提供收益的主要预测市场（相对 Polymarket 抵押品闲置的结构性创新）。

2. **背靠 Binance 全家桶**：YZi Labs（原 Binance Labs）领投并多次复投，CZ 亲自预告站台，创始人 @dingalingts 为前 Binance 研究负责人。更关键的是 **Binance Wallet 原生集成**——用户用 Keyless Wallet 一键开户、Binance 代付 Gas、完全 Gasless，把数千万 Binance 用户变成潜在流量池。

3. **技术上是 Polymarket 的「BNB 改良分叉」**：同样使用 Gnosis 条件代币框架（CTF）、CTFExchange 链下订单簿撮合 + 链上结算、NegRisk 多结果市场、UMA 兼容乐观预言机（`UmaCompatibleOptimisticOracle`）解决结果。差异在于 **链选 BNB（非 Polygon）+ 生息抵押 + ZeroDev/Privy 账户抽象（Predict Account 智能钱包）**。

4. **「东方野心」明确**：主基础设施部署在 `ap-northeast-1`（东京），收购 Probable 并由岳小鱼（@yuexiaoyu）出任亚太负责人，重点吃下中文/亚洲社区——这是 Polymarket/Kalshi 相对薄弱的市场。

5. **积分驱动增长（Predict Points）**：尚未发币，靠 PP 积分 + 空投预期拉新。积分来自交易量、做市（提供流动性）、持仓、邀请（10% 永久返佣）。做市积分按「订单距中点距离、订单规模、是否双边挂单」每分钟快照计分——这是典型的「为未来代币空投预埋」打法。

6. **赛事场景验证渠道**：2026 世界杯「$2M Predict Cup」通过 Binance Wallet 入口 + 200 万美元奖池，3 天做到 2 万 DAU、18 万笔/日，验证了「大事件 + Binance 渠道 + 奖励」的增长飞轮。

---

## 📋 报告包含的内容

调研沿用参考项目（Polymarket Builder 生态调研）的标准化结构——单份 `analysis.md` 含以下 8 大编号章节：

1. **市场情况**：定位、市场规模与轨迹、品类覆盖、竞争格局、融资与收购
2. **业务架构**：五大核心模块、市场生命周期、资金流、双边市场、利益相关者
3. **用户体验路径**：双入口对比 + 注册/入金/交易/持仓/结算/提现完整 Mermaid 流程
4. **技术架构**：技术栈、链上合约族、Venus 生息机制、数据流、关键 API 端点
5. **核心功能与交易技术壁垒**：功能详解 + 壁垒评分表 + 与 Polymarket 对照
6. **商业模式**：费率数学、收入测算、单位经济性、商业画布、增长飞轮、代币/积分/空投
7. **待确认问题**：明确标注哪些是推测、哪些待验证
8. **总结**：核心判断

---

## 🛠️ 调研方法

| 方法 | 用途 |
|------|------|
| 官方开发者文档（dev.predict.fun） | API 端点、SDK、链上合约地址、订单簿机制 |
| BNB Chain 链上合约 | 验证 CTF / Yield-Bearing / UMA Adapter / FeeModule 部署 |
| Web 检索 + 媒体交叉验证 | 融资、收购、交易量、用户数等市场数据 |
| Binance/YZi Labs 官方公告 | 投资、Binance Wallet 集成、世界杯活动 |
| 竞品文档（Polymarket/UMA） | 对照印证架构与结算机制 |

---

## ⚠️ 局限性说明

- 收益分配（Yield）具体路由到哪些 DeFi 协议（Venus / Lista / 其他）官方未完全公开，文中为合理推断
- 费率「2% 基础费、随价格偏离 50% 递减」来自第三方媒体口径，未经官方费率表逐项核验
- 交易量/用户数为不同时间点的公开口径，存在快照差异
- 尚未发币，代币经济（Tokenomics）为基于积分与空投预期的推断
- 详见 [limitations.md](./research/summary/limitations.md)

---

## 🔄 更新日志

| 日期 | 更新内容 |
|------|----------|
| 2026-06-17 | 初始版本：完成 predict.fun 平台 8 大维度深度调研 + 全景汇总 |

---

## 📄 License

MIT — 调研内容仅供参考，不构成投资建议。
