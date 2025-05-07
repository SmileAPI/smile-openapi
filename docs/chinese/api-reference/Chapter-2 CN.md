---
title: 了解 API
excerpt: ""  
category: 62ce2a159aafea009af30da7
slug: chapter-2-cn
---



<!-- focus: false -->
![Jobs](https://img.icons8.com/ios-filled/50/000000/find-matching-job.png)

## 可用资源

Smile 开放 API 中的可用资源由两种类型组成：

- Smile 网络资源
- 用户数据

### Smile 网络资源

这些是用于与 Smile 开放 API 集成并从中获取数据的数据资源。

大多数 Smile 产品和流程使用通用资源，也有一些资源是您希望实施的特定流程所特有的。

#### 通用资源

| Resource          | Process             | 描述                                                              |
|-------------------|---------------------|-----------------------------------------------------------------|
| Providers         | General             | Smile 网络中可用的就业数据提供商列表。数据提供商进一步细分为不同的子类型，如零工平台、人力资源平台等。          |
| Users             | General             | 这些是您的用户，他们已经启动了账户关联流程，并同意与您和 Smile 共享其就业数据。创建新用户时，会同时发放一个Token。 |
| Tokens            | General             | 用于访问用户账户相关数据的Token。您可以使用此资源检索现有Token，或为现有用户刷新Token。             |
| Webhooks          | General             | 当您的环境中发生事件时，Webhook 用于实时通知您的应用程序。                               |
| Consent Templates | General             | 将您的同意书存储在 Smile API 中，以便在处理用户数据时更方便地引用用户的同意。                    |
| Accounts          | Account Linking     | 您的用户已成功登录的账户，将从中检索与账户相关的数据。更多信息，请参阅下面的 “源数据”。                   |
| Invites           | Account Linking     | 您可以使用此功能邀请用户通过他们首选的通信渠道（如电子邮件）关联他们的工作账户。                        |
| Invite Templates  | Account Linking     | 如果您要通过邀请邀请用户关联他们的工作账户，请使用此功能定义和检索邀请的外观。                         |
| Archives          | Document Processing | 这是指包含用户上传的扫描或拍摄文档文件的存档。                                         |
| File Types        | Document Processing | 指接受上传的文件类型，上传后将作为存档提供。                                          | 

### 用户数据资源

用户数据可以来自关联的账户、上传的数据，也可以通过验证或信号请求获得。

为了能够检索丰富的用户数据（如收入和就业数据）并在您的应用程序中使用，您需要使用我们的账户关联、文档处理或表单处理产品，并将其集成到您的应用程序中。否则，我们的风险筛查产品仍然可以提供有价值的数据。

#### 丰富的用户数据

> 📘 注意
>
> 要了解有关 Wink Widget的更多信息，请查看 **“获取用户数据”** 部分

如果您要将客户端 SDK 嵌入到自己的应用程序中，您需要实例化该Widget，之后将在 Smile 中创建一个用户，并获得一个短期Token。实例化Widget时，您的用户首先需要同意 Smile 代表他们检索该数据。之后，我们将显示一个就业和收入数据提供商列表，供您的用户选择。然后，他们需要执行以下操作之一：

1. **使用数字数据提供商进行身份验证。** 如果我们与该数据提供商有直接连接，我们将在列表中显示该提供商，用户可以从中选择。如果他们在任何显示的提供商处有账户，他们可以选择该提供商，然后输入他们在所选数据提供商处的凭据。授予权限后，将在 Smile 网络中创建一个账户，从中检索、汇总数据并将其规范化为标准模式，并以对开发者友好的 JSON 格式发送给您。
2. **上传包含其就业或收入信息的扫描或拍摄文档。** 并非所有源就业和收入信息都是数字形式。通常，此类信息仍然以纸质文档的形式存在。用户可以扫描或拍摄这些文档并上传，然后我们可以对其进行数字化处理并从中检索相关数据，在大多数情况下，还可以将数据（通过光学字符识别或 OCR）提取为对开发者友好的 JSON 格式。如果我们无法自动提取信息，我们将始终通过 /archives 端点提供上传文件的 URL。

| Resource      | Type      | 描述                                                                                                                   |
|---------------|-----------|----------------------------------------------------------------------------------------------------------------------|
| Identity      | User Data | 从现任和前任雇主那里获得经过审核的身份信息，如姓名、联系信息、居住地址等。                                                                                |
| Transactions  | User Data | 从源数据提供商那里获得用户的详细财务交易信息。这包括源提供商记录的增加项（或信贷）和扣除项（或借贷）。                                                                  |
| Ratings       | User Data | 获取用户的工作绩效评级信息。                                                                                                       |  
| Documents     | User Data | 获取文档信息，如他们的驾驶执照、国民身份证等。                                                                                              |  
| Employments   | User Data | 获取以前的就业信息，如用户曾工作过的公司、职位、任期等。                                                                                         |  
| Incomes       | User Data | 获取以前的收入信息，如毛工资和净工资，以及构成收入的其他部分。<br> 来自 Contributions 和 Transactions 的 **Estimated Income** *（抢先体验版）* 数据也将在有限时间内免费提供。 |  
| Contributions | User Data | 获取以前的社会保障缴款信息，以了解收入水平。                                                                                               |  
| Liabilities   | User Data | 获取从与就业相关的数据源和社会保障服务获得的当前和以前的贷款信息。                                                                                    |  

<!--
| Assets | Source Data | 获取用户用于就业的资产信息，如机动车、摩托车等。|  
| Schools | Source Data | 获取以前的教育历史信息，如学校、学位、就读年份等。|  
-->

#### 可操作的用户洞察

| Resource                     | Type           | 描述                                  |
|------------------------------|----------------|-------------------------------------|
| Verification Requests        | Risk Screening | 验证可以帮助您确认用户提供的数据与预验证和/或权威来源的数据是否匹配。 | 
| Signal Requests              | Risk Screening | 仅通过电话号码或电子邮件地址获取有关用户行为的关键风险信号。      | 
| Footprints                   | Risk Screening | 获取有关用户数字足迹和在线活动的有价值见解。              | 
| Multiple Application Warning | Risk Screening | 发现用户贷款活动的早期迹象。                      |
| Blacklist                    | 确保您的用户未被列入黑名单。 |

---
<!-- focus: false -->
![Modes](https://img.icons8.com/material-rounded/50/000000/switch-on.png)

## 操作模式

API 有两种模式，可通过向不同的基础 URL 发送请求来访问。您获得的每个 API 客户端密钥只能用于单一模式。例如：授予访问SANDBOX模式的 API 客户端 ID 和密钥只能在该模式下使用。

| 模式             | 主机                             | 描述                                                                                                              |
|----------------|--------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Sandbox**    | https://sandbox.smileapi.io/v1 | 使用SANDBOX模式来构建和测试您的集成。在此模式下，您必须使用测试凭据向就业数据提供商进行身份验证。所有 API 端点将返回模拟数据，不会返回实际的用户数据。所有用户的SANDBOX模式将立即开启。           |
| **Production** | https://open.smileapi.io/v1    | PRODUCTION模式用于将您的集成上线。您的最终用户将使用他们的登录凭据向他们的就业数据提供商进行身份验证。API 端点返回真实数据，在此模式下，所有 API 调用都需要计费。访问PRODUCTION模式需要获得批准。 |

注册后，您将立即免费获得在我们的SANDBOX环境中进行测试的权限。如果您需要访问生产环境，请[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)。

### 在SANDBOX模式下进行测试

Smile 为我们的生产环境提供了SANDBOX模式，以便您可以使用示例数据测试您的集成。

要使用SANDBOX，您可以使用以下示例凭据：

| 用户名       | 全名                  | 电子邮件                      | 手机号码             | 密码     | 验证码  | 社保号码       |
|-----------|---------------------|---------------------------|------------------|--------|------|------------|
| George    | George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456 | 1234 | 3300000008 |
| Ryan      | Ryan Lestari        | ryan1234@smileapi.io      | (+62) 8119994321 | 654321 | 1234 | N/A        |
| Christina | Christina Tan       | christina4321@smileapi.io | (+65) 99996789   | YGUS1  | 1234 | N/A        |
| Anisha    | Anisha Bhatia       | anisha98765@smileapi.io   | (+91) 9511198765 | 123456 | 1234 | N/A        |

SANDBOX模式下的存档仅返回特定的工资单。要在SANDBOX模式下测试存档，您可以在开发者门户中下载示例工资单，并通过 Wink Widget或 API 上传。在SANDBOX模式下上传其他文件将返回错误。

---
<!-- focus: false -->
![Authentication](https://img.icons8.com/ios-glyphs/50/000000/key--v1.png)

## 身份验证

Smile 开放 API 使用 HTTP 基本身份验证。

基本身份验证是一种内置于 HTTP 协议中的简单身份验证方案。要使用它，请在发送 HTTP 请求时，在 Authorization 标头中包含 `Basic` 前缀，后跟一个空格和一个 base64 编码的字符串 `API Key:API Secret`。

这些凭据与您的 Smile 租户账户关联，可用于访问 Smile 网络。要检索您的凭据，只需[在我们的开发者门户上注册并在开发者门户中访问您的 API 密钥](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link)。

> 📘 示例
>
> `Authorization: Basic ZGVtbzpwQDU1dzByZA==`

要从我们的 API 检索数据，您应在 Authorization 标头中包含 `Basic` 前缀，后跟一个空格和一个 base64 编码（非加密）的字符串 `apikey:apisecret` 或 `Authorization: Basic {base64 encoded string}`。

**您可以通过登录[开发者门户](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link)，在 *API Keys* 部分找到您的 API 密钥和密钥。**

注册后，您将立即免费获得在我们的SANDBOX环境中进行测试的权限。如果您需要访问生产环境，请[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)。

![where-to-find-api-keys.png](https://files.readme.io/834b7582dbcdf49bf523958d5a7b33793990041654508b6af5fe6e29e24cfc10-where-to-find-api-keys.png)

您可以点击 API Key和Api Secret旁边的复制图标，轻松将其复制到计算机剪贴板。

---
<!-- focus: false -->
![Versions](https://img.icons8.com/ios-glyphs/50/000000/versions.png)

## 版本控制

版本包含在 URI 路径中。例如，它将如下所示：`https://open.smileapi.io/v1/`

我们使用的版本控制约定是 **1.2.3** 格式，其中 **1** 是主版本号，**2** 是次版本号，**3** 是补丁更新：

- **主版本号：** URI 中使用的版本号，表示对 API 的重大更改。虽然我们尽量保持更改向后兼容，但有时我们可能需要引入可能会改变现有行为或功能的更改。这些更改将在通过不同 URI 访问的 API 版本中实现（例如 `https://open.smileapi.io/v2/`）。您可以继续使用现有 URI 以避免破坏现有集成，但为了利用新功能，您必须更新应用程序以指向新版本和 URI。
- **次版本号和补丁版本号：** 这些对客户端是透明的，我们在内部使用它们进行向后兼容的更新。当我们发布次更新或补丁时，您无需更新集成。我们将通过变更日志和电子邮件通知传达这些信息，以便您了解所有这些更改。

---
<!-- focus: false -->
![Alert](https://img.icons8.com/ios-glyphs/50/000000/error--v1.png)

## 错误消息

| HTTP 状态码       | 状态描述                                               | Smile 代码               | 消息                                    |
|----------------|----------------------------------------------------|------------------------|---------------------------------------|
| 400 - 错误请求     | 由于语法不正确，服务器无法理解该请求。客户端在未修改请求的情况下不应重复该请求。           | INVALID_CREDENTIALS    | 您提供的凭据不正确。                            |
| 400 - 错误请求     | 由于语法不正确，服务器无法理解该请求。客户端在未修改请求的情况下不应重复该请求。           | INVALID_PARAMETERS     | 您的请求中发送了缺失或无效的参数。                     |
| 401 - 未授权      | 表示该请求需要用户身份验证信息。客户端可以使用合适的 Authorization 标头字段重复该请求 | INVALID_TOKEN          | 您提供的Token无效或已过期。                      |
| 403 - 禁止访问     | 未经授权的请求。客户端没有访问该内容的权限。与 401 不同，服务器知道客户端的身份。        | UNAUTHORIZED_ACCESS    | 您没有权限访问此资源。                           |
| 404 - 未找到      | 服务器找不到请求的资源。                                       | MISSING_RESOURCE       | 您提供的资源无法找到或不可用。                       |
| 415 - 不支持的媒体类型 | 有效负载格式未定义或为不支持的格式。                                 | UNSUPPORTED_TYPE       | 请为您的请求指定有效的内容类型。                      |
| 429 - 请求过多     | 在给定时间内发送了过多请求                                      | REQUEST_LIMIT_EXCEEDED | 您已超出此资源的速率限制。请稍后再试或联系支持人员。            |
| 500 - 内部服务器错误  | 服务器遇到意外情况，无法完成请求。                                  | SERVER_ERROR           | 我们的系统目前遇到问题。请稍后再试或联系支持人员。             |
| 501 - 未实现      | 服务器不支持该 HTTP 方法，无法处理。                              | UNSUPPORTED_METHOD     | 您使用的 HTTP 方法不支持此资源。                   |
| 503 - 服务不可用    | 服务器未准备好处理该请求。                                      | SERVER_UNAVAILABLE     | 服务器无法处理该请求。它可能已关闭或正在维护中。请稍后再试或联系支持人员。 |
| 504 - 网关超时     | 服务器无法及时给出响应。                                       | TIME_LIMIT_EXCEEDED    | 服务器在规定时间内无法给出响应。请重试或联系支持人员。           |

---
## 结果主体

所有响应均以 JSON 格式编码，并返回以下属性：

- **code**
- **message**
- **requestId**
- **data**

如果响应是单个对象，则 data 属性的值就是该对象。例如，Get Identity 端点将返回以下内容，其中 `data` 属性返回单个 Identity 对象：

```json
{
    "code": "OK",
    "message": "Success!",
    "requestId": "508a2074-9229-4d59-b716-bb6b4221e196",
    "data": {
        "nextCursor": null,
        "items": [
            {
                "id": "t-f4b8293631c84e759d30afebb7d98678",
                "date": "2021-08-06",
                "description": "Order revenue",
                "currency": "PHP",
                "amount": 222.0000,
                "referenceId": "Order ID-945485798532",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-281ad47efdc043e796e128ee5bdf50c3",
                "date": "2021-08-07",
                "description": "Order revenue",
                "currency": "PHP",
                "amount": 114.0000,
                "referenceId": "Order ID-023485780332",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-6853edd863514eae98b18abf56764fc3",
                "date": "2021-08-08",
                "description": "Platform fee",
                "currency": "PHP",
                "amount": -25.5000,
                "referenceId": "Order ID-934585780080",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-9409019eb2f141f898e73775be4c6600",
                "date": "2021-04-04",
                "description": "Order revenue",
                "currency": "PHP",
                "amount": 220.0000,
                "referenceId": "Order ID-934587514002",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-a402ac196f404ab5bf1d148c5685624f",
                "date": "2021-08-09",
                "description": "Platform fee",
                "currency": "PHP",
                "amount": -20.0000,
                "referenceId": "Order ID-156987512999",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-d318e3b6ad7845fda960a5d5add60bcb",
                "date": "2021-08-10",
                "description": "",
                "currency": "PHP",
                "amount": 59.0000,
                "referenceId": "Order ID-664426992012",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-b1b8412a02e5482da260c7dbb045f455",
                "date": "2021-08-12",
                "description": "Platform fee",
                "currency": "PHP",
                "amount": -20.0000,
                "referenceId": "Order ID-234728692099",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "itemCreatedAt": "2022-02-22T05:36:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            }
        ]
    }
}
```

---
<!-- focus: false -->
![参数](https://img.icons8.com/windows/50/000000/null-symbol.png)

## 空值

有时，您可能会在 API 响应中看到某个属性的返回值为 `null`。这种情况可能发生在以下场景：

- 数据提供商没有该属性对应的字段。例如，与身份数据相关的 “公民身份” 或 “居住国” 字段可能不存在。
- 在其他情况下，数据提供商支持该字段，但它是一个可选字段，未启用、处于隐藏状态，或者仅在用户共享信息时不满足某些条件时才会显示。例如，如果用户未在其就业平台上完成账户验证或 KYC 流程，可能无法获取他们的手机号码或地址等详细信息。

---
<!-- focus: false -->
![ISO](https://img.icons8.com/ios/50/000000/iso.png)

## 约定和标准

为了便于日志记录和故障排除，我们在向您返回数据时遵循了一些约定。

| 资源属性                                      | 前缀          | 示例                                         | 描述                                |
|-------------------------------------------|-------------|--------------------------------------------|-----------------------------------|
| User ID                                   | `tenantId-` | smile1234-a5b39dfe76174defb353d7e97a88a85e | 在我们的系统中，每个用户 ID 都有一个与其租户 ID 相关的前缀 |
| Identity ID                               | `i-`        | i-45567e7689be49d5bc052a6e4a3805e6         | 与身份相关的信息                          |
| Transaction ID                            | `t-`        | t-11de60721342404daa35f60d2875f37b         | 与交易相关的信息                          |
| Rating ID                                 | `r-`        | r-ff4723f9af5f4dc5b6a22ea27fb3c8a1         | 与评级相关的信息                          |
| Document ID                               | `d-`        | d-ff4723f9af5f4dc5b6a22ea27fb3c8a1         | 与文档相关的信息                          |
| Employment ID                             | `e-`        | e-ff4723f9af5f4dc5b6a22ea27fb3c8a1         | 与就业信息相关的信息                        |
| Income ID                                 | `inc-`      | inc-ff4723f9af5f4dc5b6a22ea27fb3c8a1       | 与收入相关的信息                          |
| Estimated Incomes ID <br>*(early access)* | `einc-`     | einc-ff4723f9af5f4dc5b6a22ea27fb3c8a1      | 与预估收入相关的信息                        |
| Contribution ID                           | `con-`      | con-ff4723f9af5f4dc5b6a22ea27fb3c8a1       | 与收入相关的信息                          |
| Archive ID                                | `u-`        | u-ff4723f9af5f4dc5b6a22ea27fb3c8a1         | 可作为存档的上传文件                        |
| Invite ID                                 | `iv-`       | iv-ff4723f9af5f4dc5b6a22ea27fb3c8a1        | 发出的邀请                             |
| Invite Template ID                        | `ivt-`      | ivt-ff4723f9af5f4dc5b6a22ea27fb3c8a1       | 创建的邀请模板                           |

为了标准化数据格式，我们使用普遍接受的标准来格式化数据，包括：

| 数据类型          | 格式                     | 示例                   | 标准            |
|---------------|------------------------|----------------------|---------------|
| date          | yyyy-MM-dd             | 2021-04-21           | ISO 8601 完整日期 | 
| date-time     | yyyy-MM-ddTHH:mm:ssZ   | 2021-04-21T08:25:05Z | ISO 8601 完整时间 |
| month         | yyyy-MM                | 2021-04              | ISO 8601 月份   |
| phone numbers | + (国家代码) (地区代码) (电话号码) | +65281234567         | E.164         |
| country codes | ISO alpha-2            | 'SG' 代表新加坡           | ISO 3166      |
| currency      | ISO alpha-3            | 'USD' 代表美元           | ISO 4217      |

---
<!-- focus: false -->
![分页](https://img.icons8.com/windows/50/000000/choose-page.png)

## 列表结果和分页

资源或 API 端点可以返回对象列表或集合。默认情况下，我们每次返回 10 条记录，最多返回 150 条。您可以通过传递 `size` 参数来限制结果数量。有关过滤或限制结果的更多信息，请参阅下面的查询参数部分。

当 Smile 返回一个集合时，我们还会返回一个名为 `nextCursor` 的值。示例如下：

```json
{
    "code": "OK",
    "message": "Success!",
    "requestId": "17bc5a84-2468-47f6-9d3c-05b5257befa5",
    "data": {
        "nextCursor": "20",
        "items": ["..."]
    }
}
```

要查看集合中的下一页，只需在查询端点时附加 `cursor` 参数，使用上一次查询返回的 `nextCursor` 值来转到集合中的下一页。有关cursor和其他查询参数的更多信息，请参阅下面的内容。

---
<!-- focus: false -->
![参数](https://img.icons8.com/ios-glyphs/50/000000/filled-filter.png)

## 查询参数

返回对象列表或集合的 API 端点可以根据不同的查询参数进行过滤或限制。以下是一些示例：

| 参数        | 描述                                           |
|-----------|----------------------------------------------|
| size      | 您希望在集合中返回的对象数量。有关默认值的更多信息，请参阅上文。             |
| cursor    | 使用上一页的nextCursor值来确定此次查询的开始。有关分页的更多信息，请参阅上文。 |
| userId    | 根据关联的用户 ID 过滤结果                              |
| sourceId  | 对于与源相关的数据，根据关联的源 ID 过滤结果                     |
| startDate | 对于具有日期属性的数据，能够按日期范围过滤结果                      |
| endDate   | 对于具有日期属性的数据，能够按日期范围过滤结果                      |

然而，某些资源有与之关联的独特查询参数。请查看每个端点的文档以了解更多信息。

---
<!-- focus: false -->
![速率限制](https://img.icons8.com/ios-filled/50/000000/traffic-light.png)

## 速率限制

Smile 对每个端点的 API 调用次数进行限制，以确保平台的稳定性和可用性。目前，我们仅允许每个 IP 地址每秒最多进行 **10 次请求**。此限制适用于所有 API 端点。连续发出过多请求的客户端将收到 HTTP 状态码 429（请求过多）的错误。

如果您需要更高的限制，请联系 access@getsmileapi.com。