---
title: Signals(Beta)
category:
  uri: '/branches/1.0-Chinese/categories/reference/用户数据'
slug: signals-beta
content:
  excerpt: ''
---

在当今快节奏的金融环境中，准确及时的风险评估对于做出明智的决策至关重要。Smile API 的 Signals API 通过使用个人的手机号码或电子邮件地址，从各种活动和事件中提供实时风险信号，从而提供了一个强大的解决方案。

Smile API 提供对数百个风险信号的访问，让您可以挑选对您的使用案例和细分市场有意义的信号。我们还预选了 30 种最常见的风险信号，以便您可以立即开始使用，但我们强烈建议您联系我们，根据我们的风险信号目录测试您的数据。

_Signals 目前处于 Beta 阶段。_

## Signals 对象

| 属性            | 类型        | 描述                                                                                    |
|:--------------|:----------|:--------------------------------------------------------------------------------------|
| id            | string    | Signal 请求的唯一 ID                                                                       |
| createdAt     | date-time | 发出 signal 请求的日期和时间                                                                    |
| status        | string    | signal 请求的当前状态，可以是以下状态之一：  `PROCESSING`, `ERROR`, `COMPLETED`                         |
| resultCode    | string    | signal 请求的最终结果，可能是以下结果之一： `SUCCESS`, `NO_DATA`, `SYSTEM_ERROR`, `SERVICE_UNAVAILABLE` |
| resultMessage | string    | 对 signal 请求最终结果更详细的描述                                                                 |
| requestMeta   | object    | 与 signal 请求一起提供的数据                                                                    |
| items         | array     | signal 请求的结果集                                                                         |

**`requestMeta`对象**

`requestMeta` 对象包含您在 signal 请求中提供的值。

| 属性         | 类型     | 描述                                           |
|:-----------|:-------|:---------------------------------------------|
| phone      | string | 通话对象的手机号码                                    |
| templateId | string | 模板ID，不同的模板ID返回的子集不一样。您可以联系客户支持获取SMILE所有的模版ID |
| consent    | object | 当事人的授权凭证详情                                   |

**`consent`对象** 

如果您选择在 Smile 存储授权模板，您可以在提出验证请求时提供授权凭证模板 ID。或者，您也可以直接在通话中提供授权凭证文件的详细信息，以及当事人授权凭证验证流程的日期和时间。

| 属性  | 类型   | 描述                                                                  |
| :--------- | :----- |:--------------------------------------------------------------------|
| type | string | 授权凭证的内部文件名称，如 "Product X Terms & Conditions" 或 "App Privacy Policy" |
| version | string | 您的授权凭证的内部版本，用于跟踪                                                    |
| consentedWith | string | 通常以复选框或表单中用户签署姓名和签名的形式出现。该字段用于显示用户同意您提供给他们的文件的字样                    |
| consentedAt | date-time | 当事人同意您处理其数据的时间，以 Zulu 时间格式表示                                        |
| consentTemplateId | number | 如果您选择在 Smile 中存储这些数据，这代表您的授权凭证模板 ID                                   |

**`result`对象**

`result` 对象包含请求处理成功后的结果值。可能是不同的结果子集，具体取决于您的账户设置。请联系Smile 支持获取详细信息。

| 名称                                                   | 值类型    | 描述                      |
|:-----------------------------------------------------|:-------|:------------------------|
| events_marketing_day30_institution_count             | NUMBER | 最近 30 天内举办过营销推广活动的机构数量  |
| events_application_reception_day30                   | NUMBER | 最近 30 天内的申请接待活动次数       |
| events_application_reception_day30_institution_count | NUMBER | 最近 30 天内举办过申请接待活动的机构数量  |
| events_application_approval_day30                    | NUMBER | 最近 30 天内申请批准的数量         |
| events_loan_disbursement_day30                       | NUMBER | 最近 30 天内发放贷款的次数         |
| events_loan_disbursement_day30_institution_count     | NUMBER | 最近 30 天内发放过贷款的机构数量      |
| events_repayment_reminder_day30                      | NUMBER | 最近 30 天内的还款提醒次数         |
| events_repayment_reminder_day30_institution_count    | NUMBER | 最近 30 天内提醒过还款的机构数量      |
| events_successful_repayment_day30                    | NUMBER | 最近 30 天内成功还款的次数         |
| events_successful_repayment_day30_institution_count  | NUMBER | 最近 30 天内成功还款的机构数量       |
| events_overdue_day30                                 | NUMBER | 最近 30 天内发生逾期的数量         |
| events_overdue_day30_institution_count               | NUMBER | 最近 30 天内有逾期事件的机构数量      |
| events_overdue_day30_amount                          | NUMBER | 最近 30 天内发生逾期的金额         |
| events_debt_day30_amount                             | NUMBER | 最近 30 天的债务金额            |
| events_overdue_day30_days                            | NUMBER | 最近 30 天内发生逾期的天数         |
| events_marketing_day90_institution_count             | NUMBER | 过去 90 天内举办过营销推广活动的机构数量  |
| events_application_reception_day90                   | NUMBER | 最近 90 天内的申请接待活动次数       |
| events_loan_disbursement_day90                       | NUMBER | 最近 90 天内的贷款发放次数         |
| events_loan_disbursement_day90_institution_count     | NUMBER | 最近 90 天内发放过贷款的机构数量      |
| events_overdue_day90                                 | NUMBER | 最近 90 天内发生逾期的数量         |
| events_overdue_day90_institution_count               | NUMBER | 最近 90 天内有逾期事件的机构数量      |
| events_overdue_day90_amount                          | NUMBER | 最近 90 天内发生逾期的金额         |
| events_debt_day90_amount                             | NUMBER | 最近 90 天内的债务金额           |
| events_overdue_day90_days                            | NUMBER | 最近 90 天内的逾期天数           |
| events_marketing_day180_institution_count            | NUMBER | 最近 180 天内举办过营销推广活动的机构数量 |
| events_application_reception_day180                  | NUMBER | 最近 180 天内的申请接待活动次数      |
| events_loan_disbursement_day180                      | NUMBER | 最近 180 天内的贷款发放次数        |
| events_loan_disbursement_day180_institution_count    | NUMBER | 最近 180 天内发放过贷款的机构数量     |
| events_overdue_day180                                | NUMBER | 最近 180 天内发生逾期的数量        |
| events_overdue_day180_institution_count              | NUMBER | 最近 180 天内有逾期事件的机构数量     |
| events_overdue_day180_amount                         | NUMBER | 最近 180 天的逾期金额           |
| events_overdue_day180_days                           | NUMBER | 最近 180 天内逾期事件的天数        |
| events_loan_disbursement_days_since_last             | NUMBER | 自上次发放贷款以来的天数            |
| events_successful_repayment_days_since_last          | NUMBER | 自上次成功还款后的天数             |
| events_overdue_days_since_last                       | NUMBER | 自上次逾期以来的天数              |

## Signal 数据样例

``` json
{
  "code": "OK",
  "message": "Success!",
  "requestId": "123abc456def789abc123def456abc78",
  "data": {
    "id": "signal-123abc456def789abc123def456abc78",
    "createdAt": "2024-08-09T12:55:51Z",
    "status": "COMPLETED",
    "resultCode": "SUCCESS",
    "resultMessage": "query success",
    "requestMeta": {
      "phone": "+639171234567",
      "consent": {
        "type": "[Motor Loans] Terms & Conditions",
        "version": "Loan Terms & Conditions",
        "consentedAt": "2024-08-08T16:06:00Z",
        "consentedWith": "I agree to ABC Company's Terms & Conditions",
        "consentTemplateId": "ct-fa84d4ec5a064c898b62b46b7affbcd5"
      }
    },
    "items": [
      {
        "name": "events_arbitrary_day30",
        "value": 0,
        "valueType": "NUMBER"
      },
      {
        "name": "events_preloan_day30",
        "value": 0,
        "valueType": "NUMBER"
      },
      {
        "name": "events_debt_day90_amount",
        "value": "A0",
        "valueType": "STRING"
      }
    ]
  }
}
```

## 端点

| 端点                                            |                          |
|:----------------------------------------------|:-------------------------|
| [请求 Signals](/reference/create-beta-signal)   | `POST /beta/signals`     |
| [获取 Signals 列表](/reference/list-beta-signals) | `GET /beta/signals`      |
| [获取一条 Signal 数据](/reference/get-beta-signal)  | `GET /beta/signals/{id}` |


## Risk Signals

以下是 Smile API 网络中所有可用 risk signal 的总清单。我们将为您预选多达 35 个 signal ，您可以根据自己的需要更换不同的 signal。联系我们了解更多信息。

图例:

- ✅ 默认可用
- 🟨 可用

### Risk Signals - Phone

| Signal                                  | 值   | 30 天 | 90 天 | 180 天 | 详情                 |
|:----------------------------------------|:----|:-----|:-----|:------|:-------------------|
| Application approval                    | N/A | ✅    | 🟨   | 🟨    | 贷款期限内申请批准的数量       |
| Application approval institution count  | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内申请批准的机构数量     |
| Application approval days since last    | 🟨  | N/A  | N/A  | N/A   | 自上次申请批准以来的天数       |
| Application reception                   | N/A | ✅    | ✅    | ✅     | 贷款期限内申请接待活动的次数     |
| Application reception institution count | N/A | ✅    | 🟨   | 🟨    | 贷款期限内举办申请接待活动的机构数量 |
| Application reception days since last   | 🟨  | N/A  | N/A  | N/A   | 自上次申请接待活动以来的天数     |
| Application rejection                   | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内申请被拒绝的次数      |
| Application rejection institution count | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内申请被拒的机构数量     |
| Application rejection days since last   | 🟨  | N/A  | N/A  | N/A   | 自上次申请被拒后的天数        |
| Arbitrary                               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内任意事件的数量       |
| Arbitrary institution count             | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内发生任意事件的机构数量   |
| Captcha                                 | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内发送验证码的数量      |
| Captcha institution count               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内发送验证码的机构数量    |
| Captcha days since last                 | 🟨  | N/A  | N/A  | N/A   | 距离上次发送验证码的天数       |
| Debt amount                             | N/A | ✅    | ✅    | 🟨    | 贷款期限内债务的金额         |
| Lending                                 | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内的借贷次数         |
| Lending institution count               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内有贷款活动的机构数量    |
| Loan disbursement                       | N/A | ✅    | ✅    | ✅     | 贷款期限内的贷款发放次数       |
| Loan disbursement amount                | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内贷款发放的金额       |
| Loan disbursement institution count     | N/A | ✅    | ✅    | ✅     | 贷款期限内发放贷款的机构数量     |
| Loan disbursement days since last       | ✅   | N/A  | N/A  | N/A   | 自上次发放贷款后的天数        |
| Marketing                               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内营销推广活动的数量     |
| Marketing institution count             | N/A | ✅    | ✅    | ✅     | 贷款期限内举办营销推广活动的机构数量 |
| Marketing days since last               | 🟨  | N/A  | N/A  | N/A   | 自上次营销推广活动以来的天数     |
| Other                                   | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内的其他活动次数       |
| Other institution count                 | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内举办其他活动的机构数量   |
| Overdue                                 | N/A | ✅    | ✅    | ✅     | 贷款期限内的逾期次数         |
| Overdue amount                          | N/A | ✅    | ✅    | ✅     | 贷款期限内逾期的金额         |
| Overdue autorepayment days              | N/A | 🟨   | 🟨   | 🟨    | 自动付款在贷款期限内的逾期天数    |
| Overdue institution count               | N/A | ✅    | ✅    | ✅     | 贷款期限内有逾期事件的机构数量    |
| Overdue days                            | N/A | ✅    | ✅    | ✅     | 贷款期限内逾期的天数         |
| Overdue days since last                 | ✅   | N/A  | N/A  | N/A   | 自上次逾期以来的天数         |
| Preloan                                 | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内的贷前活动次数       |
| Preloan institution count               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内开展贷前活动的机构数量   |
| Repayment reminder                      | N/A | ✅    | 🟨   | 🟨    | 贷款期限内提醒还款的次数       |
| Repayment reminder amount               | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内提醒还款的金额       |
| Repayment reminder institution count    | N/A | ✅    | 🟨   | 🟨    | 贷款期限内提醒还款的机构数量     |
| Repayment reminder days since last      | 🟨  | N/A  | N/A  | N/A   | 自上次提醒还款后的天数        |
| Successful repayment                    | N/A | ✅    | 🟨   | 🟨    | 贷款期限内成功还款的次数       |
| Successful repayment amount             | N/A | 🟨   | 🟨   | 🟨    | 贷款期限内成功还金额         |
| Successful repayment institution count  | N/A | ✅    | 🟨   | 🟨    | 贷款期限内成功还款的机构数量     |
| Successful repayment days since last    | ✅   | N/A  | N/A  | N/A   | 自上次成功还款后的天数        |

### Risk Signals - Email

_即将上线。_
