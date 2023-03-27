---
title: Transactions
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: transactions
---

Transactions 数据端点可用于许多 gig 平台，可能包含收入、支出交易以及电子钱包存款或提款的信息。

在某些情况下，Smile 还通过其 [Estimated Income](/reference/estimated-incomes) 从交易中得出月收入信息。

在用户通过 Smile 连接一个 [Account](/reference/accounts) 后，Smile 从 [Provider](/reference/providers) 检索用户的交易数据并使其可被检索。您可以监听部分事件和 webhooks（概述如下），以确定何时准备好他们的交易数据。

## 补充数据方式

如果用户提供的数据不够，您也可以利用 Smile 的 [Archive API](/reference/archives) 来鼓励用户上传他们的工资单文件。

## 交易对象

| 属性          | 类型     | 详情                        |
|:------------|:-------|:--------------------------|
| id          | string | Smile Network 上交易项目的唯一 ID |
| date        | date   | 交易日期                      |
| description | string | 交易的详情                     |
| currency    | string | 交易的货币，符合3字符阿尔法 ISO 4217   |
| amount      | number | 交易金额                      |
| referenceId | string | 来自提供商的交易参考 ID             |
| metadata    | object | 包含关于此交易数据端点的数据。见下面的对象     |

### 数据对象

| 属性                     | 类型        | 详情                                                           |
|:-----------------------|:----------|:-------------------------------------------------------------|
| createdAt | date-time | 创建账户记录的日期/时间                                                 |
| itemCreatedAt | date-time | 创建交易记录的日期/时间                                                 |
| accountId `Deprecated` | string    | 用户在 Smile Network 中的账户 ID                                    |
| sourceId               | string    | 用户在 Smile Network 中的账户或 archive 的 ID                         |
| sourceType             | string    | 表示与此对象相关的来源是账户还是archive。可能的值: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId             | string    | 用户账户的数据提供商 ID                                                |
| userId                 | string    | Smile Network 上的用户 ID                                        |

## 交易数据样例

```json
{
    "id": "einc-123abc456def789abc123def456abc78",
    "month": "2022-06",
    "currency": "PHP",
    "baseAmount": 8510.50,
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
        "itemCreatedAt": "2022-08-24T05:24:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}
```

## 端点

| 端点                                         | |
|:-------------------------------------------| :---- |
| [获取交易数据列表](/reference/list-transactions-1) | `GET /transactions` |
| [获取一条交易记录](/reference/get-transaction-1)   | `GET /transactions/{id}` |

## Webhooks

### `TRANSACTIONS_ADDED`

添加有关用户的交易数据时，事件发送格式如下：

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "IDENTITY_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "identityId": "i-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `TASK_FINISHED`

用户账户的数据同步进程结束时，事件发送格式如下：

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TASK_FINISHED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ],
    "datapoints": [
      "IDENTITIES",
      "TRANSACTIONS"
    ]
  }
}
```
