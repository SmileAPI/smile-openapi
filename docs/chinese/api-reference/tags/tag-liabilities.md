---
title: Liabilities
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: liabilities
---


Liabilities 数据端点允许您在几秒内检索到特定提供商的贷款数据，该项数据可以帮助您决策以及核保。目前，这些数据都来自于为公民提供贷款服务的政府机构。
 
在菲律宾，贷款支持由 SSS 提供。即将加入的 Pag-IBIG 及其他来源也是我们规划中的一部分。

当用户通过 Smile 连接一个 [Account](/reference/accounts)  后，Smile 从  [Provider](/reference/providers) 检索用户的贷款数据并使其可被检索。您可以监听部分事件和 webhooks（概述如下），以确定何时准备好他们的贷款数据。

## 补充数据方式

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload relevant documentation.

## 贷款对象

| 属性                    | 类型     | 详情                                                                                                                                         |
|:----------------------|:-------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | string | Smile Network 上的贷款信息的唯一 ID                                                                                                                 |
| type                  | string | 贷款类型，取决于提供商                                                                                                                                |
| referenceId           | string | 提供商网络上贷款的唯一参考 ID                                                                                                                           |
| startDate             | date   | 贷款的开始日期                                                                                                                                    |
| endDate               | date   | 贷款的结束日期。如果没有或仍在进行，则为空                                                                                                                      |
| firstAmortizationDate | date   | 首次分期还款的日期                                                                                                                                  |
| amortizationFrequency | string | 分期还款的频率。可能的值：`Hourly`, `Daily`, `Weekly`, `Semimonthly`, `Monthly`, `Bimonthly`, `Quarterly`, `Annually`, `Variable`, `Unspecified`        |
| currency              | string | 贷款的货币，3个字符的阿尔法ISO 4217                                                                                                                     |
| loanAmount            | float  | 贷款的金额                                                                                                                                      |
| amortizationAmount    | float  | 根据 `amortizationFrequency` 值支付的分期还款金额                                                                                                      |
| outstandingBalance    | float  | 仍未偿还的贷款金额                                                                                                                                  |
| nextPaymentAmount     | float  | 下一次分期还款的贷款金额。可能包括逾期的金额                                                                                                                     |
| overduePaymentAmount  | float  | 逾期的贷款金额。不包括尚未过期的预期还款。                                                                                                                      |
| metadata              | object | 包含关于这个贷款数据端点的数据。见下面的对象                                                                         |


### 数据对象

| 属性                    | 类型     | 详情                                                            |
| :--------- | :----- |:--------------------------------------------------------------|
| createdAt | date-time | 创建账户记录的日期/时间                                                  |
| itemCreatedAt | date-time | 创建贷款记录的日期/时间                                                  |
| accountId `Deprecated` | string | 用户在 Smile Network 中的账户 ID                                     |
| sourceId | string | 用户在 Smile Network 中的账户或 archive 的 ID                          |
| sourceType | string | 表示与此对象相关的来源是账户还是 archive 。可能的值：`ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | 用户账户的数据提供商 ID                                                              |
| userId | string |  Smile Network 上的用户 ID                    |


## 贷款数据样例

```json
[{
    "id": "lia-123abc456def789abc123def456abc78",
    "type": "Salary Loan",
    "startDate": "2022-10-06",
    "amortizationFrequency": "Monthly",
    "currency": "PHP",
    "loanAmount": 16000,
    "referenceId": "SL201601011234567",
    "endDate": "2023-10-06",
    "firstAmortizationDate": "2022-11-06",
    "amortizationAmount": 738.32,
    "outstandingBalance": 14599.76,
    "nextPaymentAmount": 732.38,
    "overduePaymentAmount": 0,
    "metadata": {
        "createdAt": "2022-11-01T01:01:01Z",
        "itemCreatedAt": "2022-11-01T01:11:01Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "xyzservice",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```

## 端点

| 端点                                      | |
|:----------------------------------------| :---- |
| [获取贷款数据列表](/reference/list-liabilities) | `GET /liabilities` |
| [获取一条贷款记录](/reference/get-liabilities)  | `GET /liabilities/{id}` |

## Webhooks

### `LIABILITIES_ADDED`

添加有关用户的贷款数据时，事件发送格式如下：

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LIABILITIES_ADDED",
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
  "id": "et-123abc456def789abc123def456abc78",
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
      "LIABILITIES"
    ]
  }
}
```
