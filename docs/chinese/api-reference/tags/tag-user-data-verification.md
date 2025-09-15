---
title: Data Verification
excerpt: ''
category: 64c78531461848004b92b92f
slug: user-data-verification
---

无需用户登录，Smile Snap Data Verification API 允许开发人员根据官方数据源检索个人数据。这项服务还有一个查询模式，请参阅 [概况数据](https://docs.getsmileapi.com/reference/query-identity) 。

该 API 可用于验证个人提供的数据，以核对准确性并最大限度地减少欺诈行为。Smile 目前支持通过 Social Security ID 编号进行验证。其他数据源也将很快加入。

查询所需的数据如下：

1. ID Type
2. ID Number
3. First Name

然后，您可以发送其他信息（请参阅 Verify Identity 端点），以便在所提供的数据与官方数据源的数据相匹配时接收信息。

在继续进行验证匹配之前，Smile 会根据所提供的 ID 类型和编号检查姓名匹配度是否达到 80%。

## 结果对象

| 属性                   | 类型      | 详情                       |
|:---------------------|:--------|:-------------------------|
| nameMatchScore       | number  | 与所提供姓名的匹配度百分比            |
| dobMatched           | boolean | 出生日期的匹配结果。如果查询中没有列出，则为空  |
| mobileMatched        | boolean | 手机号码的匹配结果。如果查询中未列出，则为空   |
| emailMatched         | boolean | 电子邮件地址的匹配结果。如果查询中未列出，则为空 |
| genderMatched        | boolean | 性别匹配结果。如果查询中没有列出，则为空     |
| maritalStatusMatched | boolean | 婚姻状况的匹配结果。如果查询中未列出，则为空   |

## 样例结果数据

### 数据匹配

如果名字和姓氏的组合与提供的 ID 编号所登记的姓名至少有 80% 的匹配度，则将返回匹配结果。

下面的样例结果假定查询时只发送了手机号码和电子邮件。

```json
  "data": {
    "hit": true,
    "message": "SUCCESS",
    "result": {
      "nameMatchScore": 92,
      "dobMatched": null,
      "mobileMatched": false,
      "emailMatched": true,
      "genderMatched": null,
      "maritalStatusMatched": null
    }
  }
```

### 数据不匹配

如果名字和姓氏的组合与提供的 ID 编号所登记的姓名匹配度低于 80%，则不会返回匹配结果。

```json
  "data": {
    "hit": true,
    "message": "First name or last name not matched.",
    "result": {
      "nameMatchScore": 77,
      "dobMatched": null,
      "mobileMatched": null,
      "emailMatched": null,
      "genderMatched": null,
      "maritalStatusMatched": null
    }
  }
```

## 端点

| 端点                                                    | |
|:------------------------------------------------------| :---- |
| [验证身份](/reference/verify-profile-identity) | `GET /profiles/-/identities/verify` |
