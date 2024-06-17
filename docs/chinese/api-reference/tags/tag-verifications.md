---
title: Verification
excerpt: ""  
category: 64c78531461848004b92b92f
slug: verification
---

Snap Verifications 帮助企业改进身份验证流程。客户只需输入用户的身份详细信息（如姓名、联系信息和 ID 号码），Snap Verification 就会将这些信息与可靠的数据源进行匹配和验证，并输出每个属性的验证状态。

Snap Verification API 至少需要三项信息：

1. 用户的姓名
2. 用户的 ID 或电子邮件（请参阅下面的受支持 ID 列表）
3. 用户的授权凭证

提供信息后，Smile 会根据所提供的 ID 和您在请求中包含的数据检查所有可靠的数据源，让您能够快速判断最终用户所提供数据的真实性。通过将快速验证与 Snap Verification API 相结合，并在所提供的数据不充分时使用 Wink SDK，您可以高效获得服务客户所需的信息。

_Smile Snap Verification API 目前处于 alpha 阶段。_

### 如何发送验证请求

1. **准备验证请求的详细信息。**

   您需要发送以下信息：

   * 用户的姓名（全名或名+姓）
   * 用户的标识符（以下支持的标识符之一，或者您也可以提供电子邮件地址）
   * 用户的授权凭证
   
2. **使用我们的 [Request Verification](https://docs.getsmileapi.com/reference/create-verification) 端点发送验证请求。**

   > 📘 注意
   >
   > 用户授权和数据隐私对我们非常重要。您必须在创建请求时将用户授权的凭证与其数据一起提交。请查看下面的数据对象。

3. **订阅事件通知或存储您请求的验证 ID**。

4. 通过 `TASK_FINISHED` webhook 事件或 [Get Verification](https://docs.getsmileapi.com/reference/get-verification) 端点**接收验证结果**。

### 支持的标识符和数据端点

| ID 或标识符              | 可验证的数据属性                             |
|:---------------------|:-------------------------------------|
| 纳税识别号 `tin_ph`       | 全名*、名*、中间名*、姓*、后缀*、出生日期*、性别*、电子邮件、电话 | 
| 社会保障号码 `sss_ph`      | 全名*、名、中间名、姓、后缀、出生日期、性别、电子邮件、电话       |
| 专业执照 `prclicense_ph` | 全名*、名*、中间名、姓*、许可证类型、电子邮件             |
| Pag-IBIG 成员 ID 编号    | 全名*、名、中间名、姓、电子邮件                     |
| 电子邮件                 | 全名*                                  |

更多种类的 ID 敬请期待。

## 验证对象

### 请求对象

这是您提供给我们的请求对象，也是跟踪请求细节的元对象。

| 属性  | 类型     | 详情                |
| :--------- |:-------|:------------------|
| fullName | string | 请求中提供的用户的全名     |
| firstName | string | 请求中提供的用户的名字     |
| middleName | string | 请求中提供的用户的中间名    |
| lastName | string | 请求中提供的用户的姓氏     |
| suffix | string | 请求中提供的用户的后缀     |
| additionalData | object | 请求中提供的有关用户的其他数据 |
| consent | object | 请求中提供的用户授权的凭证  |

### 附加数据（请求）对象

| 属性  | 类型     | 详情                                  |
| :--------- | :----- |:------------------------------------|
| ids | array | 包含用户身份证/号码信息的对象数组（只接受一个对象）        |
| email | string | 请求中提供的用户的电子邮件地址                   |
| phone | string | 请求中提供的用户的电话号码                     |
| dob | date | 请求中提供的用户的出生日期，格式为 `YYYY-MM-DD`    |
| gender | string | 请求中提供的用户的性别，可以是 `Male` 或 `Female` |

### 标识符（请求）对象

| 属性  | 类型     | 详情                                              |
| :--------- | :----- |:------------------------------------------------|
| idType | string | 请求中发送的用户提供的 ID 类型                             |
| idSubType | string |  ID 的子类型（如适用），即许可证类型                                                |
| idNumber | string | 请求中提供的用户的 ID 编号 |

### 授权对象

如果您选择在 Smile 中存储授权文件，您可以在提出验证请求时提供授权模板的 ID ，或者直接在请求中提供授权文件的详细信息，以及用户授权验证流程的日期和时间。

| 属性  | 类型     | 详情                                                                  |
| :--------- | :----- |:--------------------------------------------------------------------|
| type | string | 授权文件的内部文件名称，如 "Product X Terms & Conditions" 或 "App Privacy Policy" |
| version | string | 您的授权文件的内部版本，用于跟踪更新                                                  |
| consentedWith | string | 通常以复选框或表单中用户签署姓名和签名的形式出现。此字段用于显示用户授权您提供给他们的文件的字样                |
| consentedAt | date-time | 用户授权您处理其数据的时间，以 Zulu 时间格式表示                                       |
| consentTemplateId | number | 如果您选择在 Smile 中存储这些数据，这代表您的授权模板 ID                                   |

### 验证对象

| 属性  | 类型     | 详情                                               |
| :--------- | :----- |:-------------------------------------------------|
| id | string | Smile Network 上验证请求的唯一 ID                        |
| createdAt | date-time | 创建验证请求的日期/时间                                     |
| updatedAt | date-time | 验证请求最后的更新日期/时间                                   |
| status | string | 验证请求的状态。可以是  `PROCESSING`、`COMPLETED` 或  `ERROR` |
| errorMessage | string | 如适用，代表验证请求的错误信息                                  |
| requestMeta | object | 包含原始请求数据的对象。请参阅 *请求对象*。                          |
| result | object | 包含验证结果的对象                                        |

### 结果对象

| 属性  | 类型     | 详情                        |
| :--------- | :----- |:--------------------------|
| finalMatches | boolean | 如果提供的姓名与提供的标识符匹配，则返回 true |
| names | object | 包含姓名的详细匹配信息的对象            |
| additionalData | object | 包含附加属性的详细匹配信息的对象          |

### 姓名（结果）对象

| 属性  | 类型     | 详情                                         |
| :--------- | :----- |:-------------------------------------------|
| fullNameMatches | boolean | 如果提供的全名与提供的标识符匹配，则返回 true。如果未提供或不支持，则返回空值  |
| firstNameMatches | boolean | 如果提供的名字与提供的标识符匹配，则返回 true。如果未提供或不支持，则返回空值  |
| middleNameMatches | boolean | 如果提供的中间名与提供的标识符匹配，则返回 true。如果未提供或不支持，则返回空值 |
| lastNameMatches | boolean | 如果提供的姓氏与提供的标识符匹配，则返回 true。如果未提供或不支持，则返回空值  |

### 补充数据（结果）对象

| 属性  | 类型     | 详情                                                                    |
| :--------- | :----- |:----------------------------------------------------------------------|
| ids | array | 如果提供的名称与提供的标识符匹配，则包含匹配信息的对象数组。如果未提供或不支持，则返回空值                         |
| dobMatches | boolean | 如果提供的出生日期与可用记录匹配，则返回 true。如果未提供、不支持或 `finalMatches` 为 false，则返回空值     |
| genderMatches | boolean | 如果提供的性别与可用记录匹配，则返回 true。如果未提供、不支持或 `finalMatches` 为 false，则返回空值            |
| phoneMatches | object | 如果提供的电话与可用记录匹配，则包含匹配信息和其他信息的对象。如果未提供、不支持或 `finalMatches` 为 false，则返回空值     |
| emailMatches | object | 如果提供的电子邮件地址与可用记录匹配，则包含匹配信息和其他信息的对象。如果未提供、不支持或 `finalMatches` 为 false，则返回空值 |

### 标识符（结果）对象

| 属性  | 类型     | 详情                                        |
| :--------- | :----- |:------------------------------------------|
| idNumber | string | 根据请求中提供的 ID 编号进行匹配                       |
| idType | string | 根据请求中提供的 ID 类型进行匹配                        |
| idSubType | string | 根据请求中提供的 ID 子类型进行匹配                     |
| matches | boolean | 如果提供的名称与提供的标识符匹配，则返回 true。如果未提供或不支持，则返回空值 |

### 电子邮件或电话匹配对象

| 属性  | 类型     | 详情                                                                       |
| :--------- | :----- |:-------------------------------------------------------------------------|
| value | string | 请求中提供的经匹配的电子邮件地址或电话号码                                                    |
| matches | boolean | 如果提供的电子邮件或电话与可用记录匹配，则返回 true。如果未提供、不支持或 `finalMatches` 为 false，则返回空值     |
| disposable | boolean | 如果匹配的电子邮件或电话是无效的，则返回 true。如果未提供、不支持或 `finalMatches` 为 false，则返回空值        |
| deliverable | boolean | 如果匹配的电子邮件/电话号码可送达，则返回 true。如果未提供、不支持、`finalMatches`为 false 或用于电话，则返回空值   |
| active | boolean | 如果匹配的电子邮件/电话号码处于激活状态，则返回 true。如果未提供、不支持、`finalMatches`为 false，则返回空值             |
| provider | string | 返回电子邮件服务提供商或电话运营商的名称。如果未提供、不支持或 `finalMatches` 为 false，则返回空值             |
| freeProvider | boolean | 如果匹配的电子邮件或电话运营商是免费服务提供商，则返回 true。如果未提供、不支持或 `finalMatches` 为 false，则返回空值 |

## 验证结果数据样例

``` json
{
  "id": "ver-123abc456def789abc123def456abc78",
  "createdAt": "2024-01-01T08:00:00Z",
  "status": "COMPLETED",
  "updatedAt": "2024-01-01T08:01:00Z",
  "errorMessage": null,
  "requestMeta": {
    "fullName": "George Cimafranca Palomero",
    "firstName": "George",
    "middleName": "Cimafranca",
    "lastName": "Palomero",
    "suffix": "",
    "additionalData": {
      "ids" : [{
        "idType": "tin_ph",
        "idSubType": "",
        "idNumber": "123456789"
      }],
      "email": "gpalomero1234@smileapi.io",
      "phone": null,
      "dob": "1980-01-01",
      "gender": "Male",
      },
      "consent": {
        "type": "Terms & Conditions",
        "version": "1.0",
        "consentedAt": "2024-01-01T08:00:00Z",
        "consentedWith": "I consent to ABC Company processing my data",
        "consentTemplateId": null
      }
  },
  "result": {
    "finalMatches": true,
    "names": {
      "fullNameMatches": true,
      "firstNameMatches": true,
      "lastNameMatches": true,
      "middleNameMatches": true
    },
    "additionalData": {
      "ids": [{
        "idNumber": "234957978",
        "idType": "tin_ph",
        "idSubtype": "",
        "matches": true
      }],
      "dobMatches": true,
      "genderMatches": true,
      "phoneMatches": null,
      "emailMatches": {
        "value": "gpalomero1234@gmail.com",
        "matches": true,
        "disposable": false,
        "deliverable": true,
        "active": null,
        "provider": "Google LLC",
        "freeProvider": true
      }
    }
  }
}
```

## 端点

| 端点                                        | |
|:------------------------------------------| :---- |
| [获取验证数据列表](/reference/list-verifications) | `GET /verifications` |
| [请求验证数据](/reference/create-verification)  | `POST /verifications` |
| [获取一条验证数据](/reference/get-verification)   | `GET /verifications/{id}` |

