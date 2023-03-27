---
title: Documents
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: documents
---


Documents 数据端点包含有价值的官方文件相关信息，这些信息可以从提供商那里获得，如：

- 经核实的政府身份证号码，如社会保险等。
- 用于刑事检查的许可文件信息
- 证书和执照信息
- 工资单文件信息

虽然一些文件可能有与之相关的附件，但这些附件不应该与用户上传的 [Archives](/reference/archives) 相混淆。

在用户通过 Smile 连接一个 [Account](/reference/accounts) 后，Smile 从  [Provider](/reference/providers) 检索任何可用的文件数据并使其可被检索。您可以监听部分事件和 webhooks（概述如下），以确定他们的文件数据何时准备好（如果适用）。

## 补充数据方式

如果用户提供的数据不够，您也可以利用 Smile 的 [Archive API](/reference/archives) 来鼓励用户上传他们自己的文件，可以是驾驶执照，护照，甚至是银行或工资单据。

## 文件对象

| 属性           | 类型     | 详情                                                                                  |
|:-------------|:-------|:------------------------------------------------------------------------------------|
| id           | string | Smile Network 上的文件信息的唯一 ID                                                          |
| name         | string | 文件的名称，如 *NBI Clearance document*，*SSS Number* 等。                                    |
| docId        | string | 文件的唯一标识符                                                                            |
| status       | string | 如果可以从提供商得到的话，代表文件状态，目前只有 NBI Clearance 在使用，如果不可用，则为空。可能的值：`VALID`, `HIT`, `EXPIRED` |
| documentType | string | 文件的类型。可能的值: `IDENTIFICATION`, `PAYSLIP`, `CLEARANCE`, `CERTIFICATE`                 |
| issueDate    | date   | 文件签发的日期。如果没有，则为空。                                                                   |
| expiryDate   | date   | 文件到期的日期。如果没有，则为空。                                                                   |
| fileUrl      | string | 文件的完全格式化URL参考附件。如果没有，则为空。                                                           |
| metadata     | object | 包含关于此文件数据端点的数据。见下面的对象                                                               |

### 数据对象

| 属性                     | 类型     | 详情                                                             |
|:-----------------------| :----- |:---------------------------------------------------------------|
| createdAt              | date-time | 创建账户记录的日期/时间                                                   |
| itemCreatedAt          | date-time | 创建文件记录的日期/时间                                                   |
| accountId `Deprecated` | string | 用户在 Smile Network中的账户 ID                                                                                                                                  |
| sourceId               | string | 用户在 Smile Network 中的账户或 archive 的 ID                           |
| sourceType             | string | 表示与此对象相关的来源是账户还是 archive 。可能的值: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId             | string | 用户账户的数据提供商 ID                                                  |
| userId                 | string | Smile Network 上的用户 ID                                          |


## 文件数据样例

```json
{
  "id": "d-123abc456def789abc123def456abc78",
  "name": "NBI Clearance",
  "docId": "A123BCDE45-AA123456",
  "status": "VALID",
  "documentType": "CLEARANCE",
  "issueDate": "2022-06-06",
  "expiryDate": "2023-06-06",
  "fileUrl": null,
  "metadata": {
    "createdAt": "2022-08-19T07:29:08Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```

## 端点

| 端点                                      | |
|:----------------------------------------| :---- |
| [获取文件数据列表](/reference/list-documents-1) | `GET /documents` |
| [获取一条文件记录](/reference/get-document-1)   | `GET /documents/{id}` |

## Webhooks

### `DOCUMENTS_ADDED`

添加有关用户的文件数据时，事件发送格式如下：

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "DOCUMENTS_ADDED",
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
      "DOCUMENTS"
    ]
  }
}
```
