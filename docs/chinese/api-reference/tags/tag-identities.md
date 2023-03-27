---
title: Identities
excerpt: ""
category: 62ce2a159aafea009af30dab
slug: identities
---

在大多数情况下，Identities 数据端点包含来自提供商的主要用户数据。将来自不同提供商的各种身份数据放在一起，可以让您更全面地了解用户信息，并有机会跨多个提供者验证他们的数据。

当用户通过 Smile 连接一个 [Account](/reference/accounts) 后，Smile 从 [Provider](/reference/providers) 检索用户的身份数据，并使其可用于检索。您可以监听部分事件和 webhook (下面概述)，以确定何时准备好他们的身份数据。

## 验证用户身份

大多数平台至少包含名字和姓氏，中间名和后缀因平台而异。您可以使用这些信息将客户提供的信息与来自可验证来源(如政府记录和社会保障机构)的数据进行匹配。

## 补充数据方式

如果用户提供的数据不够，您也可以使用 Smile 的 [Archive API](/reference/archives) 鼓励用户上传他们自己的文件。这可以是驾照，护照，甚至银行账单或工资文件。

## 身份对象

| 属性               | 类型     | 详情                                                                                                                     |
|:-----------------|:-------|:-----------------------------------------------------------------------------------------------------------------------|
| id               | string | Smile Network 中身份信息的唯一 ID                                                                                              |
| fullName         | string | 如果可以从提供商获得的话，代表用户的全名，不可用则为 Null                                                                                        |
| firstName        | string | 如果可以从提供商获得的话，代表用户的名字，不可用则为 Null                                                                                        |
| middleName       | string | 如果可以从提供商获得的话，代表用户的中间名，不可用则为 Null                                                                                       |
| lastName         | string | 如果可以从提供商获得的话，代表用户的姓氏，不可用则为 Null                                                                                        |
| suffix           | string | 如果可以从提供商获得的话，代表用户的后缀(如Jr、Ss、MD等)，不可用则为 Null                                                                            |
| gender           | string | 如果可以从提供商获得的话，代表用户的性别，不可用则为 Null，可能值:`Male`, `Female`, `Non-binary`                                                     |
| dob              | date   | 如果可以从提供商获得的话，代表用户的出生日期，不可用则为 Null                                                                                      |
| maritalStatus    | string | 如果可以从提供商获得的话，代表用户的婚姻状况，不可用则为 Null，可能值:`Divorced`, `Lifetime Partner`, `Married`, `Separated`, `Single`, `Widowed`      |
| countryResidence | string | 如果可以从提供商获得的话，代表用户的居住国，不可用则为 Null，以 2 字符 alpha ISO-3166 代码提供，即 `PH`, `ID` 等等。                                           |
| citizenship      | string | 如果可以从提供商获得的话，代表用户在其居住国的公民身份，不可用则为 Null，可能值:`Citizen`, `Resident Alien`, `Non-resident Alien`, `Undocumented`, `Others` |
| photoUrl         | string | 如果可以从提供商获得的话，代表用户的照片或头像的完整的URL，不可用则为 Null                                                                              |
| referenceId      | string | 如果可以从提供商获得的话，代表提供商提供的用户配置文件的引用ID，不可用则为 Null                                                                            |
| profileUrl       | string | 如果可以从提供商获得的话，代表用户与提供商的公共配置文件的完整的 URL，不可用则为 Null                                                                        |
| emails           | array  | 如果可以从提供商获得的话，包含提供商提供的用户电子邮件地址，不可用则为 Null                                                                               |
| phones           | array  | 如果可以从提供商获得的话，包含提供商提供的用户电话号码，不可用则为 Null                                                                                 |
| socialProfiles   | array  | 如果可以从提供商获得的话，包含提供商提供的连接到用户帐户的任何社交资料，不可用则为 Null                                                                         |
| addresses        | array  | 如果可以从提供商获得的话，包含提供程序提供的用户的物理地址，不可用则为 Null                                                                               |
| metadata         | object | 如果可以从提供商获得的话，包含关于此身份数据端点的数据，不可用则为 Null                                                                                 |

### 电子邮件地址对象

| 属性      | 类型     | 详情                                                                                                      |
|:--------|:-------|:--------------------------------------------------------------------------------------------------------|
| address | string | 用户的电子邮件地址                                                                             |
| type    | string | 用户提供的电子邮件地址类型。可选值:`Primary`, `Secondary`, `Work`, `Personal` |


### 电话号码对象

| 属性     | 类型     | 详情                                                                                           |
|:-------|:-------|:---------------------------------------------------------------------------------------------|
| number | string | 国际E.164格式的用户电话号码                                      |
| type   | string | 用户提供的电话号码类型。可选值:`Mobile`, `Fixed`, `Unspecified` |


### 社交资料对象

| 属性        | 类型     | 详情                                                           |
|:----------|:-------|:-------------------------------------------------------------|
| socialUrl | string | 用户的公共社交媒体的完整的 URL 页面                                         |
| type      | string | 用户的社交媒体账户提供商。可能值:`Twitter`, `Facebook`, `LinkedIn`, `Others` |


### 地址对象

| 属性          | 类型     | 详情                                                 |
|:------------|:-------|:---------------------------------------------------|
| fullAddress | string | 用户的完整物理地址                                          |
| line1       | string | 用户地址的第一行，即街道地址                                     |
| line2       | string | 用户地址的第二行                                           |
| city        | string | 用户地址所在城市                                           |
| region      | string | 用户地址的地理区域，如州或省                                     |
| zip         | string | 用户地址的邮政编码                                          |
| country     | string | 用户地址所在国家。以2字符 alpha ISO-3166 代码提供，即 `PH`, `ID` 等等。 |
| latitude    | string | 用户地址的纬度坐标                                          |
| longitude   | string | 用户地址的经度坐标                                          |
| type        | string | 用户提供的地址类型。可选值: `Primary`, `Secondary`              |


### 数据对象

| 属性                     | 类型        | 详情                                                            |
|:-----------------------|:----------|:--------------------------------------------------------------|
| createdAt | date-time | 创建账户记录的日期/时间                                                  |
| itemCreatedAt | date-time | 创建身份记录的日期/时间                                                  |
| accountId `Deprecated` | string    | 用户在 Smile Network 中的账号 ID                                     |
| sourceId               | string    | Smile Network 中用户帐户或 archive 的 ID                             |
| sourceType             | string    | 指示与此对象关联的来源是帐户还是 Archive 。可选值: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId             | string    | 用户帐户的数据提供商的 ID                                                |
| userId                 | string    | Smile Network 中的用户 ID                                         |


## 身份数据样例

```json
{
  "id": "i-123abc456def789abc123def456abc78",
  "fullName": "George Cimafranca Palomero, Jr",
  "firstName": "George",
  "middleName": "Cimafranca",
  "lastName": "Palomero",
  "suffix": "Jr",
  "gender": "Male",
  "dob": "1970-08-24",
  "maritalStatus": "Married",
  "countryResidence": "PH",
  "citizenship": "Citizen",
  "photoUrl": "https://cdn.smileapi.io/image/avatar/v20211115191600/george.jpg",
  "referenceId": null,
  "profileUrl": null,
  "emails": [
    {
      "address": "gpalomero1234@smileapi.io",
      "type": "Primary"
    }
  ],
  "phones": [
    {
      "number": "+639559991234",
      "type": "Mobile"
    }
  ],
  "socialProfiles": [
    {
      "socialUrl": "https://www.facebook.com/gpalomero1234",
      "type": "Facebook"
    }
  ],
  "addresses": [
    {
      "fullAddress": "12 Maybunga St, Barangay Paraiso, Pasig City, NCR, 1600, PH",
      "line1": "12 Maybunga St",
      "line2": "Barangay Paraiso",
      "city": "Pasig City",
      "region": "NCR",
      "zip": "1600",
      "country": "PH",
      "latitude": "14.573454",
      "longitude": "121.085042",
      "type": "Primary"
    }
  ],
  "metadata": {
    "createdAt": "2022-08-19T07:29:08Z",
    "itemCreatedAt": "2022-08-24T05:24:37Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```

## 端点

| 端点                                       | |
|:-----------------------------------------| :---- |
| [获取身份数据列表](/reference/list-identities-1) | `GET /identities` |
| [获取一条身份记录](/reference/get-identity-1)    | `GET /identities/{id}` |

## Webhooks

### `IDENTITY_ADDED`

添加有关用户的身份数据时，事件发送格式如下：

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
      "INCOMES"
    ]
  }
}
```
