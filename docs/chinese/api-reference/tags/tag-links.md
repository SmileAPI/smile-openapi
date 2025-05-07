---
title: 账户多头申请警告（MAW）
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: links
---

当潜在借款人向多家金融机构申请贷款时，贷款机构会收到多头申请警告（MAW）通知。有了 MAW，贷款机构在评估风险时就能利用借款人在整个网络中的行为信息做出更明智的决策。

通过 MAW 服务，一旦您的用户经由 Wink Widget SDK 连接了账户，您就会收到用户是否已与 Smile 网络中的其他贷款人和机构进行了连接的通知。

为您的账户激活 MAW 有下列多种好处：

- **实时通知** 当借款人申请多笔贷款时收到通知，以便进行主动风险管理和及时决策。
- **加强风险评估** 降低向信用压力过大或行为可疑的借款人发放贷款的风险，减少潜在损失，提高贷款组合质量。
- **欺诈检测** 通过识别试图同时获得多笔贷款的借款人，发现潜在的欺诈活动，最大限度地降低向欺诈性申请人提供贷款的风险。
- **网络效应** 受益于贷款机构所参与的网络不断扩大，Smile 为加强风险评估和欺诈防范提供更丰富、更准确的数据。

账户激活 MAW 后，您可以通过两种方式接收或检索用户之前在网络上的贷款行为数据：

1. 通过 ``GET /links`` 端点
2. 通过监听 ``LINK_ADDED``webhook

这样，您就可以根据自己的需要，通过多种方式检索数据。

## Link 对象

| 属性        | 类型               | 详情                               |
|:----------|:-----------------|:---------------------------------|
| id        | string           | 该 Link 记录的唯一 ID                  |
| startDate | date-time        | 用户的 Link 数据分析开始的时间，通常为账户连接前的730天 |
| endDate   | date-time        | 用户的 Link 数据分析结束的时间，通常是在连接账户时     |
| records   | array of objects | 包含 Link 记录的数组    |

### Records 对象

| 属性        | 类型               | 详情                                            |
| :----- | :----- |:----------------------------------------------|
| count | number | 在``startDate``到``endDate``期间，该帐户连接过的其他贷款组织的数量 |
| linkedAt | array of date-time | 账户连接到其他贷款机构的日期/时间值                            |

## 用户对象示例

```json
{
    "id": "link-123abc456def789abc123def456abc78",
    "startDate": "2022-03-20T01:27:26Z",
    "endDate": "2022-09-20T01:27:26Z",
    "records": [
        {
          "count" : 3,
          "linkedAt" : [
            "2022-04-20T01:27:26Z",
            "2022-04-21T12:00:00Z",
            "2022-06-01T01:00:00Z"
          ]
        }
    ]
}
```

## 端点

| 端点                                      |                      |
|:----------------------------------------| :------------------- |
| [获取 Link 数据列表](/reference/list-links) | `GET /links`      |
| [获取一条 Link 记录](/reference/get-link)   | `GET /links/{id}` |

## Webhooks

### `LINK_ADDED`

添加有关用户的 Link 数据时，事件发送格式如下：

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LINK_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "id": "link-ef789aabc41236abc7856df45bc123de",
    "providers": [
      "abccorp"
    ]
  }
}
```
