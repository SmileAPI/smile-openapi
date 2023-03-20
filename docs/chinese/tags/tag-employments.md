---
title: Employments
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: employments
---

Employments 数据端点包含用户就业状况的信息。就业数据最常从政府服务和机构以及由您的用户连接到 Smile 的薪资平台获取。

Smile 从平台上原封不动地返回就业信息，如开始和结束日期、雇主名称、工作职位和其他信息。从政府服务部门获取经核实的数据，并将其与工资平台的信息整合，可以让您对用户的就业状况有一个确切的了解。

就业数据不包括在 Gig 平台上从事的工作，如骑行共享应用程序等。

在用户通过 Smile 连接一个[ Account ](/reference/accounts)后，Smile 从[ Provider ](/reference/providers)检索用户的就业数据并使其可被重组。您可以监听部分事件和 webhooks（概述如下），以确定他们的就业数据何时准备好。

## 验证就业情况

大多数平台至少会包含一个开始日期和雇主名称。如果从社会保障账户中评估就业状况，您可以将这些与社保缴费进行比对，以核实就业时间和当前状况。

## 补充数据方式

如果用户提供的数据不够， 您也可以利用 Smile 的[ Archive API ](/reference/archives)来鼓励用户上传工资单或公司 ID。

## 就业数据对象

| 属性             | 类型     | 详情                                                                      |
|:---------------|:-------|:------------------------------------------------------------------------|
| id             | string | Smile Network 上就业信息的唯一 ID                                               |
| name           | string | 如果可以从提供商得到的话，代表所做的工作。如果没有，则为空                                           |
| description    | string | 如果可以从提供商得到的话，代表对所做工作的描述。如果没有，则为空                                        |
| jobTitle       | string | 如果可以从提供商得到的话，代表雇主的职称或职位。如果不能提供，则为空                                      |
| department     | string | 如果可以从提供商得到的话，代表用户被雇佣的部门。如果没有，则为空                                        |
| employeeNumber | string | 如果可以从提供商得到的话，代表用户与雇主的雇员编号。如果没有，则为空                                      |
| employer       | string | 如果可以从提供商得到的话，代表雇主的公司或企业名称。如果没有，则为空。可能的值： `Male`, `Female`, `Non-binary` |
| status         | string | 如果可以从提供商得到的话，代表用户的就业状况。如果没有，则为空                                         |
| startDate      | date   | 如果可以从提供商得到的话，代表用户在雇主处开始工作的日期。如果没有，则为空                                   |
| endDate        | date   | 如果可以从提供商得到的话，代表用户在雇主处结束工作的日期。如果没有，则为空                                   |
| metadata       | object | 包含有关该就业数据端点的数据。见下面的对象                                                   |


### 数据对象

| 属性                     | 类型        | 详情                                                           |
|:-----------------------|:----------|:-------------------------------------------------------------|
| createdAt              | date-time | 创建就业数据的日期/时间                                                 |
| accountId `Deprecated` | string    | 用户在 Smile Network 中的账户 ID                                    |
| sourceId               | string    | 用户在 Smile Network 中的账户或 archive 的 ID                         |
| sourceType             | string    | 表示与此对象相关的来源是账户还是 archive。可能的值：`ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId             | string    | 用户账户的数据提供商的 ID                                               |
| userId                 | string    | Smile Network 上用户的 ID                  |


## 就业数据样例

``` json
{
    "id": "e-123abc456def789abc123def456abc78",
    "startDate": "2022-07-01",
    "name": "Security",
    "description": null,
    "jobTitle": "Security Guard",
    "department": null,
    "employeeNumber": "EMP-123456",
    "employer": "ABC Corporation",
    "status": "Permanent",
    "endDate": "2022-07-31",
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}
```

## 端点

| 端点                                        | |
|:------------------------------------------| :---- |
| [获取就业数据列表](/reference/list-employments-1) | `GET /employments` |
| [获取一条就业记录](/reference/get-employment-1)   | `GET /employments/{id}` |

## Webhooks

### `EMPLOYMENTS_ADDED`

添加有关用户的就业数据时，事件发送格式如下：

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "EMPLOYMENTS_ADDED",
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

``` json
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
      "EMPLOYMENTS"
    ]
  }
}
```
