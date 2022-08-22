---
title: 了解 API 
excerpt: ""  
category: 62ce2a159aafea009af30da7
slug: chapter-3-cn
---



<!-- focus: false -->
![Authentication](https://img.icons8.com/ios-glyphs/50/000000/key--v1.png)

## 验证

Smile API 使用 HTTP 基本身份验证。一组与您的开发人员帐户相关联的被称为 API key 和 API secret 的凭据可用于访问 Smile Network 。要检索您的凭据，只需注册并访问开发者控制台的 API key 部分。

想要从我们的 API 检索数据，您应该在 Authorization header 中包含单词 ``Basic`` ，后跟一个空格和 base64-encoded （非加密）的字符串 ``apikey:apisecret`` 或 ``Authorization: Basic {base64 encoded string}`` 。

---
<!-- focus: false -->
![Modes](https://img.icons8.com/material-rounded/50/000000/switch-on.png)

## 运行模式

API 有两种模式，可以通过向不同的基本 URL 发送请求来访问。您被授予的每个 API 客户端密钥只能用于单一模式。 例如：授予访问 Sandbox 模式的 API 客户端 ID 和 secret 只能在该模式下使用。

| 模式        | 主页                                        | 详情 |
|-------------|---------------------------------------------|-------------|
| Sandbox     | https://sandbox.smileapi.io/v1     |     使用 Sandbox 模式来构建和测试您的集成。在这种模式下，您必须使用测试账号向就业数据提供商进行身份验证。 所有 API 都将返回模拟数据，并且不返回实际的用户数据。 |
| Production  | https://open.smileapi.io/v1  |      Production 模式用于与您的集成一起上线。您的最终用户将使用他们的真实账号向他们的就业数据提供商进行身份验证。 API 返回真实数据，在这种模式下，所有 API 调用都是计费的。  |

---
<!-- focus: false -->
![Versions](https://img.icons8.com/ios-glyphs/50/000000/versions.png)

## 版本控制
该版本包含在 URI 路径中。 例如：``https://open.smileapi.io/v1/``

我们使用的版本约定是 **1.2.3** 格式，其中**1** 是主要版本，**2** 是次要版本，**3**是补丁更新：

- **主要版本：** URI 中使用的版本，表示对 API 的重大更改。虽然我们试图保持更改向后兼容，但在某些情况下，我们需要引入可能会改变现有行为或功能的更改。这些更改将在不同 URI 下可访问的 API 版本中实现（例如 ``https://open.smileapi.io/v2/``）  。您可以继续使用现有 URI 以避免破坏现有集成，但为了使用新功能，您必须更新应用程序以指向新版本和 URI。
- **次要版本和补丁版本：** 这些对客户端是透明的，我们在内部使用它来进行向后兼容的更新。当我们发布次要更新或补丁时，您不需要更新您的集成。我们将通过我们的变更日志和电子邮件传达这些信息，以便您了解这些变更中的任何一项。


---
<!-- focus: false -->
![Alert](https://img.icons8.com/ios-glyphs/50/000000/error--v1.png)

## 错误信息

|HTTP 状态码|状态描述|Smile 代码|信息|
|----------------------|----------------------|----------------------|----------------------|
|400 - Bad Request         |由于语法不正确，服务器无法理解该请求。客户端不应该在没有修改的情况下重复请求。   |INVALID_CREDENTIALS   |由于参数不正确，服务器无法接受该请求。                                                    |
|400 - Bad Request         |由于语法不正确，服务器无法理解该请求。客户端不应该在没有修改的情况下重复请求。      |INVALID_PARAMETERS    |您的请求中发送了缺失或无效的参数。                           |
|401 - Unauthorized        |表示请求需要用户认证信息。客户端可以使用合适的 Authorization 头域重复请求|INVALID_TOKEN         |您提供的 token 无效或已过期。                                                                            |
|403 - Forbidden           |未经授权的请求。客户端没有内容的访问权限。与 401 不同，客户端的身份为服务器所知。        |UNAUTHORIZED_ACCESS   |您无权访问此资源。                                                           |
|404 - Not Found           |服务器找不到请求的资源。                                                                                             |MISSING_RESOURCE      |您提供的资源找不到或不可用。                                      |
|415 - Unsupported Media Type           |内容格式未定义或格式不受支持。                                                                                                 |UNSUPPORTED_TYPE      |请为您的请求指定有效的内容类型。              |
|429 - Too Many Requests   |在给定时间内发送的请求过多。                                                                                  |REQUEST_LIMIT_EXCEEDED|您已超出此资源的速率限制。请稍后再试或联系支持人员。            |
|500 - Internal Server Error |服务器遇到了一个意外情况，导致它无法完成请求。                                      |SERVER_ERROR          |我们的系统目前遇到问题。请稍后再试或联系支持人员。                                    |
|501 - Not Implemented      |服务器不支持 HTTP 方式，无法处理。                                                                       |UNSUPPORTED_METHOD    |此资源不支持您使用的 HTTP 方法。                                                                  |
|503 - Service Unavailable  |服务器尚未准备好处理请求。                                                                                          |SERVER_UNAVAILABLE    |服务器无法处理请求。它可能已关闭或正在维护中。请稍后再试或联系支持人员。|
|504 - Gateway Timeout      |服务器无法及时响应。                                                                                            |TIME_LIMIT_EXCEEDED   |服务器无法在分配的时间内给出响应。 请稍后再试或联系支持人员。 


---
<!-- focus: false -->
![JSON](https://img.icons8.com/glyph-neue/50/000000/json.png)

## 响应数据

所有响应都以 JSON 编码并返回以下属性：

- **code**
- **message**
- **requestId**
- **data**

如果响应是单个对象，则数据属性的值就是该对象。 例如，获取 Identity API 将返回以下内容，属性 ``data`` 返回单个身份对象

```json
{
    "code": "OK",
    "message": "Success!",
    "requestId": "58be58d8-fdc9-4834-a5d2-711fb7386a0c",
    "data": {
        "id": "i-94683880ab98435582773936c361defd",
        "fullName": "Ryan Joseph Peterson Chua Ng",
        "firstName": "Ryan Joseph Peterson",
        "middleName": "Chua",
        "lastName": "Ng",
        "suffix": null,
        "gender": "Male",
        "dob": "1995-06-24",
        "maritalStatus": "Single",
        "countryResidence": "PH",
        "citizenship": null,
        "photoUrl": "https://cdn.smileapi.io/image/avatar/v20211115191600/ryan.jpg",
        "referenceId": "Ryan",
        "profileUrl": null,
        "emails": [
            {
                "address": "ryan1234@gmail.com",
                "type": "Primary"
            }
        ],
        "phones": [
            {
                "number": "+63289053000",
                "type": "Fixed"
            },
            {
                "number": "+639559994321",
                "type": "Mobile"
            }
        ],
        "socialProfiles": [
            {
                "socialUrl": "https://www.twitter.com/xklxyz",
                "type": "Twitter"
            },
            {
                "socialUrl": "https://www.facebook.com/ryanpetersonng",
                "type": "Facebook"
            }
        ],
        "addresses": [
            {
                "fullAddress": "24 Eagle St, Binondo, Manila, NCR, 1008, PH",
                "line1": "24 Eagle St",
                "line2": "Binondo",
                "city": "Manila",
                "region": "NCR",
                "zip": "1008",
                "country": "PH",
                "latitude": "14.600454",
                "longitude": "120.969042",
                "type": "Primary"
            }
        ],
        "metadata": {
            "createdAt": "2022-01-06T00:21:58Z",
            "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
            "sourceType": "ACCOUNT",
            "userId": "smilejan-54a668d15cf34568b5a861ff35bb2f51",
            "providerId": "199jobs"
        }
    }
}
```

如果结果与从用户帐户检索的数据相关，则还会返回元数据对象，其中包含有关响应的更多信息，例如：

- **createdAt**
- **sourceId**
- **sourceType**
- **userId**
- **providerId**

如果响应是列表或集合，则 data 属性的值是对象数组。 例如，List Transactions API 将返回一个 Transactions 集合：

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
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-20f74540926a4e71b17a93bf9932bbe7",
                "date": "2021-08-16",
                "description": "Order revenue",
                "currency": "PHP",
                "amount": 20.0000,
                "referenceId": "Order ID-994728692055",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-e392935c34a040e181fb4b38a0b9e827",
                "date": "2021-08-19",
                "description": "Platform fee",
                "currency": "PHP",
                "amount": -19.6000,
                "referenceId": "Order ID-993128902044",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
                    "sourceId": "0e0e97100eec49e8b954e9e419d527fe",
                    "sourceType": "ACCOUNT",
                    "userId": "smilejan-329789936388493f831ad0edd1f8bc8c",
                    "providerId": "upwork"
                }
            },
            {
                "id": "t-67635c20c6164094b3f2fdaa9f0e0eb0",
                "date": "2021-08-21",
                "description": "Platform fee",
                "currency": "PHP",
                "amount": -16.9000,
                "referenceId": "Order ID-996438805066",
                "metadata": {
                    "createdAt": "2022-02-22T05:26:09Z",
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
![Parameters](https://img.icons8.com/windows/50/000000/null-symbol.png)

## 空值

有时您可能会看到 ``null`` 作为 API 响应中给定属性的返回值。这可能发生在以下情况：

- 数据提供商没有该属性的字段。例如，它没有与 Identities 数据相关的“公民身份”或“居住国”字段。
- 在其他情况下，该字段由数据提供商支持，但它是一个可选字段，未启用、隐藏或仅在用户共享信息时不存在的某些条件下显示。 例如，如果他们未在其就业平台中进行帐户验证或 KYC 流程，则可能无法获得其手机或地址等详细信息。

---
<!-- focus: false -->
![ISO](https://img.icons8.com/ios/50/000000/iso.png)

## 公约和标准

为了帮助进行日志记录和故障排除，我们在向您返回数据时应用了一些约定。

| 资源属性 | 前缀 | 样例 | 详情 |
| -------------------| ------ | ------- | ----------- |
| User ID | ``tenantId-`` | smile1234-a5b39dfe76174defb353d7e97a88a85e |在我们的系统中，每个用户 ID 都有一个与其租户 ID 相关的前缀 |
| Identity ID | ``i-`` | i-45567e7689be49d5bc052a6e4a3805e6 |身份相关信息 |
| Transaction ID | ``t-`` | t-11de60721342404daa35f60d2875f37b | 交易相关信息 |
| Ratings ID | ``r-`` | r-ff4723f9af5f4dc5b6a22ea27fb3c8a1 | 评级相关信息 |
| Documents ID | ``d-`` | d-ff4723f9af5f4dc5b6a22ea27fb3c8a1 | 文件相关信息 |
| Employments ID | ``e-`` | e-ff4723f9af5f4dc5b6a22ea27fb3c8a1 | 就业相关信息 |
| Incomes ID | ``inc-`` | inc-ff4723f9af5f4dc5b6a22ea27fb3c8a1 | 收入相关信息 |
| Contributions ID | ``con-`` | con-ff4723f9af5f4dc5b6a22ea27fb3c8a1 |缴费相关信息 |
| Archives ID | ``u-`` | u-ff4723f9af5f4dc5b6a22ea27fb3c8a1 |上传的文件可用作存档|
| Invites ID | ``iv-`` | iv-ff4723f9af5f4dc5b6a22ea27fb3c8a1 | 发出的邀请 |
| Invite Templates ID | ``ivt-`` | ivt-ff4723f9af5f4dc5b6a22ea27fb3c8a1 |已创建的邀请模板 |

为了标准化数据格式，我们使用普遍接受的标准来格式化数据，包括：

| 数据类型 | 格式 | 样例 | 标准 |
| -----| ------ | --------| -------- |
| date | yyyy-MM-dd | 2021-04-21 | ISO 8601 full date | 
| date-time | yyyy-MM-ddTHH:mm:ssZ | 2021-04-21T08:25:05Z | ISO 8601 full time |
| phone numbers | + (country code) (local area code) (phone number) | +65281234567 | E.164 |
| country codes | ISO alpha-2 | 'SG' for Singapore | ISO 3166 |
| currencies | ISO alpha-3 | 'USD' for US Dollars | ISO 4217 |

---
<!-- focus: false -->
![Pagination](https://img.icons8.com/windows/50/000000/choose-page.png)

## 列出结果和分页

资源或 API 可以返回一个列表或对象集合。 默认情况下，我们一次返回 10 个，最多返回 150 个。 您可以通过传递大小参数来限制结果。 有关过滤或限制结果的更多信息，请参阅下面的查询参数。

当 Smile 返回一个集合时，我们也会返回一个名为 ``nextCursor`` 的值。 请参阅下面的示例：
```json
{
    "code": "OK",
    "message": "Success!",
    "requestId": "17bc5a84-2468-47f6-9d3c-05b5257befa5",
    "data": {
        "nextCursor": "20",
        "items": [...]
    }
}
```

要转到集合中的下一页，只需在查询 API 时附加 ``cursor`` 参数，使用从上一个查询返回的 ``nextCursor`` 值转到集合中的下一页。 有关游标和其他查询参数的更多信息，请参见下文。

---
<!-- focus: false -->
![Parameters](https://img.icons8.com/ios-glyphs/50/000000/filled-filter.png)

## 查询参数

可以根据不同的查询参数过滤或限制返回对象列表或对象集合的 API 。下面是一些例子：

| 参数 | 详情 |
|----------------------|----------------------|
| size | 您希望在集合中返回的对象数。请参阅上面有关默认值的更多信息。|
| cursor |使用上一页的过滤器值来确定下一组项目。请参阅上面有关分页的更多信息。|
| userId |按关联的 userId 过滤结果。 |
| sourceId | 对于源相关数据，根据关联的 sourceId 过滤结果。 |
| startDate |对于具有日期属性的数据，能够按日期范围过滤结果。 |
| endDate | 对于具有日期属性的数据，能够按日期范围过滤结果。 |

然而，一些资源具有与之关联的唯一查询参数。 查看每个API中的文档以了解更多信息。

<!-- focus: false -->
![Rate Limits](https://img.icons8.com/ios-filled/50/000000/traffic-light.png)

## 速率限制

Smile 限制了对每个 API 的调用量，以确保平台的稳定性和可用性。目前，我们的客户端对**每个 IP 地址最多只允许每秒 20 个请求**。这适用于所有 API 。连续发出过多请求的客户端将收到 HTTP 状态码 429 或请求过多的错误。

如要请求更高的限制，请联系 access@getsmileapi.com 。