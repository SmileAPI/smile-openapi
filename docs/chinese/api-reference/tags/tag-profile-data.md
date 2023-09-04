---
title: Profile Data
excerpt: ''
category: 64c78531461848004b92b92f
slug: profile-data
---

无需用户登录，Smile Snap Profile Data API 即可允许开发人员根据官方数据源检索个人数据。该个人资料数据可用于以下情况：

- 检索用户的其他信息
- 预填的用户基本信息
- 验证提供的数据（另请参阅 [验证数据](https://docs.getsmileapi.com/v1.0-Chinese/reference/verify-profile-identity) ）

通过提供个人的 ID 类型、ID 编号和姓名，如果姓名与通过 ID 编号识别的个人信息至少有 80% 的匹配度（见下文），则可以检索到用户的其他基本信息。否则，将不会返回任何信息。

Smile 目前支持通过 SSS ID 编号进行查询。其他数据源也将很快加入。

如果您需要比 Smile Snap 提供的更详细的用户信息，可以通过 Wink Widget SDK 以用户认证的方式获取。

### 结果对象

| 属性                         | 类型     | 详情                                                                                                         |
|:---------------------------|:-------|:-----------------------------------------------------------------------------------------------------------|
| nameMatchScore             | number | 与所提供姓名的匹配度百分比                                                                                              |
| firstName                  | string | 此人的名字                                                                                                      |
| lastName                   | string | 此人的姓氏                                                                                                      |
| middleName                 | string | 此人的中间名                                                                                                     |
| suffix                     | string | 此人的姓名后缀                                                                                                    |
| dob                        | date   | 此人的出生日期，格式为 YYYY-MM-DD                                                                                     |
| mobile                     | string | 此人的手机号码                                                                                                    |
| email                      | string | 此人的电子邮件地址                                                                                                  |
| gender                     | string | 此人的性别，可能的值有 ``Male``, ``Female``, ``Non-binary``                                                           |
| maritalStatus              | string | 此人的婚姻状况，可能是以下情况之一： ``Divorced``, ``Married``, ``Separated``, ``Single``, ``Widowed``, ``Lifetime Partner`` |
| homeTelephone              | string | 此人的家庭电话号码                                                                                                  |
| address                    | object | 此人的地址                                                                                                      |
| socialSecurityCoverageType | string | 此人的社会保险类型，可以是以下类型之一： ``EMPLOYEE``, ``VOLUNTARY``, ``SELF EMPLOYED``, ``FOR EMPLOYMENT``                    |
| socialSecurityCoverageDate | string | 此人参加社会保障的日期                                                                                                |
| totalEmploymentReportCount | number | 此人就业记录的数量                                                                                                  |
| firstEmploymentReportDate  | date   | 此人首次就业记录的日期                                                                                                           |
| latestEmploymentReportDate | date   | 此人最后一次就业记录的日期                                                   |

#### 地址对象

| 属性          | 类型     | 详情                                               |
|:------------|:-------|:-------------------------------------------------|
| fullAddress | string | 用户的详细地址                                          |
| line1       | string | 用户地址的第一行，即街道地址                                   |
| line2       | string | 用户地址的第二行                                         |
| city        | string | 用户地址所在的城市                                        |
| region      | string | 用户地址所在的区域，如州或省                                   |
| zip         | string | 用户地址的邮编或邮政编码                                     |
| country     | string | 用户地址所在的国家。以 2 个字符的字母 ISO-3166 代码提供，如`PH`、`ID`等。  |

### 样例 Profile 数据

### 数据匹配

如果名字和姓氏的组合与所提供 ID 编号登记的名字有至少 80% 的匹配度，则将返回该用户的数据。

```json
  "data": {
    "hit": true,
    "message": "SUCCESS",
    "result": {
      "nameMatchScore": 92,
      "firstName": "George",
      "lastName": "Palomero",
      "middleName": "Cimafranca",
      "suffix": "Jr",
      "dob": "1970-08-24",
      "mobile": "+639559991234",
      "email": "gpalomero1234@smileapi.io",
      "gender": "Male",
      "maritalStatus": "Married",
      "homeTelephone": null,
      "address": null,
      "socialSecurityCoverageType": "EMPLOYEE",
      "socialSecurityCoverageDate": "2020-05-01",
      "totalEmploymentReportCount": 5,
      "firstEmploymentReportDate": "2000-02-01",
      "latestEmploymentReportDate": "2022-12-01"
    }
  }
```

### 数据不匹配

如果名字和姓式的组合与所提供 ID 编号登记的姓名的匹配度低于 80%，则不会返回该用户的数据。

```json
  "data": {
    "hit": true,
    "message": "First name or last name not matched.",
    "result": {
      "nameMatchScore": 77,
      "firstName": null,
      "lastName": null,
      "middleName": null,
      "suffix": null,
      "dob": null,
      "mobile": null,
      "email": null,
      "gender": null,
      "maritalStatus": null,
      "homeTelephone": null,
      "address": null,
      "socialSecurityCoverageType": null,
      "socialSecurityCoverageDate": null,
      "totalEmploymentReportCount": null,
      "firstEmploymentReportDate": null,
      "latestEmploymentReportDate": null
    }
  }
```

## 端点

| 端点 | |
| :------- | :---- |
| [查询身份](/reference/query-profile-identity) | `GET /profiles/-/identities/query` |
