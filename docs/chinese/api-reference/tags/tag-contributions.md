---
title: Contributions
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: contributions
---

Contributions 数据端点允许您识别用户的社会保险缴费行为。根据数据来源，这个数据可以让您：

- 对用户的收入范围进行计算
- 确定正规就业的规律性

虽然不是收入信息的确切来源，但来自政府服务部门的原始社保缴费数据可以作为评估一个人信用价值的因素。

在菲律宾，SSS、PhilHealth 和 National housing provident fund 平台都有社保缴费数据。

在用户通过 Smile 连接一个 [Account](/v1.0-Chinese/reference/accounts) 后，Smile 从 [Provider](/reference/providers) 检索用户的社保缴费数据并使其可被检索。您可以监听部分事件和 webhooks（概述如下），以确定他们的社保缴费数据何时准备好。

您也可以查看 Smile 提供的用户洞察产品 [Estimated Income](/reference/estimated-incomes)，作为不需要与年度缴费表进行比较便可以快速确定收入的方法。

## 补充数据方式

如果用户提供的数据不够，您也可以利用 Smile 的 [Archive API](/reference/archives) 来鼓励用户上传他们自己的工资单或税务记录。

您也可以从 Smile 的用户洞察产品中查看 [Estimated Income](/reference/estimated-incomes)，了解来自社保缴费的衍生收入。

## 社保缴费对象

| 属性          | 类型     | 详情                                                                  |
|:------------|:-------|:--------------------------------------------------------------------|
| id          | string | Smile Network 上社保缴费信息的唯一 ID                                         |
| date        | string | 社保缴费的日期。当准确日期不可用时，默认为月底                                             |
| currency    | string | 社保缴费捐款的货币，3个字符的 alpha ISO 4217                                      |
| amount      | float  | 汇出的社保缴费数额                                                           |
| referenceId | string | 社保缴费交易的特定参考 ID                                                      |
| metadata    | object | 包含关于这个社保缴费数据端点的数据。见下面的对象 |


### 数据对象

| 属性          | 类型     | 详情                                                            |
| :--------- | :----- |:--------------------------------------------------------------|
| createdAt | date-time | 创建账户记录的日期/时间                                                  |
| itemCreatedAt | date-time | 创建社保缴费记录的日期/时间                                                |
| accountId `Deprecated` | string | 用户在 Smile Network 中的账户 ID                                     |
| sourceId | string | 用户在 Smile Network 中的账户或 archive 的 ID                          |
| sourceType | string | 表示与此对象相关的来源是账户还是 archive 。可能的值：`ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | 用户账户的数据提供商 ID                                                 |
| userId | string | Smile Network 上的用户 ID                                         |


## 社保缴费数据样例

```json
{
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-06-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}
```

## 端点

| 端点                                        | |
|:------------------------------------------| :---- |
| [获取社保缴费列表](/reference/list-contributions) | `GET /contributions` |
| [获取一条社保缴费记录](/reference/get-contribution) | `GET /contributions/{id}` |

## Webhooks

### `CONTRIBUTIONS_ADDED`

添加有关用户的社保缴费数据时，事件发送格式如下：

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "CONTRIBUTIONS_ADDED",
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
      "CONTRIBUTIONS"
    ]
  }
}
```
