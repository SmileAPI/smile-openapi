---
title: Incomes
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: incomes
---

Incomes 数据端点允许您检索用户可用收入记录，该记录根据提供商的可用数据得到。收入数据主要可以从以下方面获得：

- 选择工资平台
- 选择政府服务平台
- 选择 Gig 平台

来自工资和服务平台的可核实收入是评估一个人信用价值的宝贵的数据端点。

当用户通过 Smile 连接一个 [Account](/reference/accounts)，Smile 从 [Provider](/reference/providers) 检索用户的收入数据，并使其可被检索。您可以监听部分事件和 webhooks（概述如下），以确定何时准备好他们的收入数据。

如果提供商没有提供原始收入数据，Smile 也提供 [Estimated Income](/reference/estimated-incomes) 作为额外的用户洞察。

## 补充数据方式

如果用户提供的来源不够，您可以利用 Smile 的 [Archive API](/reference/archives) 来鼓励用户上传他们自己的工资单或税务记录。

您也可以从 Smile 的用户洞察产品中查看 [Estimated Income](/reference/estimated-incomes)，以了解从现有数据来源得出的收入。

## 收入对象

| 属性          | 类型     | 详情                                                                                                                                       |
|:------------|:-------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| id          | string | Smile Network 上的收入信息的唯一 ID                                                                                                               |
| workItem    | string | 已完成的工作（如自由职业者的工作）                                                                                                                        |
| employer    | string | 雇主姓名                                                                                                                                     |
| startDate   | date   | 收入阶段的开始日期                                                                                                                                |
| endDate     | date   | 收入阶段的结束日期                                                                                                                                |
| currency    | string | 交易的货币，3个字符的阿尔法ISO 4217                                                                                                                   |
| frequency   | string | 收入记录的频率或支付阶段。可能的值：`Hourly`, `Daily`, `Weekly`, `Semimonthly`, `Monthly`, `Bimonthly`, `Quarterly`, `Annually`, `Variable`, `Unspecified` |
| baseAmount  | float  | 已支付收入的基本金额                                                                                                                               |
| grossAmount | float  | 已支付收入的总金额                                                                                                                                |
| netAmount   | float  | 已支付收入的净额                                                                                                           |
| metadata    | object | 包含有关该收入数据端点的数据。见下面的对象                                                                            |


### 数据对象

| 属性          | 类型     | 详情                                                           |
| :--------- | :----- |:-------------------------------------------------------------|
| createdAt | date-time | 创建账户记录的日期/时间                                                 |
| itemCreatedAt | date-time | 创建收入记录的日期/时间                                                 |
| accountId `Deprecated` | string | 用户在 Smile Network 中的账户 ID                                    |
| sourceId | string | 用户在 Smile Network 中的账户或 archive 的 ID                         |
| sourceType | string | 表示与此对象相关的来源是账户还是 archive。可能的值：`ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | 用户账户的数据提供商 ID                                                |
| userId | string | Smile Network 上的用户 ID                                                             |


## 收入数据样例

```json
{
    "id": "inc-123abc456def789abc123def456abc78",
    "startDate": "2022-07-01",
    "endDate": "2022-07-31",
    "workItem": "Regular employment",
    "employer": "ABC Corporation",
    "frequency": "Monthly",
    "currency": "PHP",
    "baseAmount": 8500,
    "grossAmount": 10000,
    "netAmount": 7820.25,
    "metadata": {
        "createdAt": "2022-09-01T01:44:22Z",
        "itemCreatedAt": "2022-09-01T01:54:22Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "inc-123abc456def789abc123def456abc78",
    "startDate": "2022-06-01",
    "endDate": "2022-06-30",
    "workItem": "Regular employment",
    "employer": "ABC Corporation",
    "frequency": "Monthly",
    "currency": "PHP",
    "baseAmount": 8500,
    "grossAmount": 10000,
    "netAmount": 7820.25,
    "metadata": {
        "createdAt": "2022-09-01T01:44:22Z",
        "itemCreatedAt": "2022-09-01T01:54:22Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}
```

## 端点

| 端点                                    | |
|:--------------------------------------| :---- |
| [获取收入数据列表](/reference/list-incomes-1) | `GET /incomes` |
| [获取一条收入记录](/reference/get-income-1)   | `GET /incomes/{id}` |

## Webhooks

### `INCOMES_ADDED`

添加有关用户的收入数据时，事件发送格式如下：

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
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
      "INCOMES"
    ]
  }
}
```
