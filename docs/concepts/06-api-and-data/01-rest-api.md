# API 与数据 — REST API

> 市场 / 订单 / 持仓 / 账户端点

---

## 接入点

| 项目 | 值 |
|------|------|
| 主网 | `https://api.predict.fun/`（需 API Key） |
| 测试网 | `https://api-testnet.predict.fun/`（无需 Key） |
| 备用 UI | `https://api.predict.fun/docs` |
| 速率限制 | 240 请求/分钟 |

## 主要端点

| 分组 | 代表端点 |
|------|---------|
| Categories | `GET /categories`、`GET /tags` |
| Markets | `GET /markets`、`GET /markets/{id}`、`market statistics`、`market timeseries`、`orderbook` |
| Orders | `POST create order`、`remove orders`、`order by hash`、`order match events` |
| Accounts | `connected account`、`account activity`、`set referral` |
| Positions | `GET positions`、`positions by address` |
| Search | `search categories and markets` |
| OAuth | 第三方代下单/查持仓 |

---

> 基于 dev.predict.fun，截至 2026 年 6 月。API 处于 Beta。
