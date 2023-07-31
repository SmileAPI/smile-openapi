---
title: 实施与上线
excerpt: ""  
category: 6422597473b6df0073e64c8e  
slug: customer-verification-implementation
---

![](https://files.readme.io/62a894c-image.png)

为了成功地将 Smile 融入您的流程，我们建议通过以下3个步骤来实现：

- 收集需求 - 探索您的使用用例，以及您想通过 Smile 数据实现什么目标
- [设计](/docs/customer-verification-design) - 设计您的用户流程以及与 Smile 的集成
- 实施与上线（本指南）--设置和启动集成的详细步骤

***



# 第1步：实施 Smile Wink

如果想让用户在您的网站或应用程序上连接他们的就业账户，您需要集成 Smile Wink Widget。请看下面的配置示例：

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * Link API URI 。注意： Sandbox 和 Production 模式使用不同的 API URI 。
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * User Token： 从你的后端服务里面获取，你的后端服务需要调用 SmileAPI /tokens 或者 /users 接口来获取。
             */
            userToken: '<usertoken>',

            /**
             * 使用模板来控制集成在你APP或者网站上的WinkWidget的页面样式与数据
             * 你可以在 Smile 的开发者控制台创建并获取 TemplateID
             * https://developer-portal.smileapi.io/link/template
             */
            templateId: "<ID of wink template >",

            /**
             * 账号创建时的回调.
             */
            onAccountCreated: ({ accountId, userId, providerId }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * 账号登录成功时的回调.
             */
            onAccountConnected: ({ accountId, userId, providerId }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * 账号撤销链接的回调.
             */
            onAccountRemoved: ({ accountId, userId, providerId }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Token 失效时的回调
             */
            onTokenExpired: () => {
                console.log('Token expired');
            },

            /**
             * Smile 的 WinkWidget 关闭时回调。如果你想知道用户通过哪种方式关闭的 WinkWidget，你可以像下面的实例一样传递参数：
             * onClose:({reason})=>{}
             * 如果 reason == "close"， 说明用户点击了右上角的关闭图标
             * 如果 reason == "exit"， 说明用户点击了链接成功页面的 "DONE" 按钮
             */
            onClose: ({ reason }) => {
                console.log('Link closed, reason:', reason)
            },

            /**
             * 账号链接出错时的回调
             */
            onAccountError: ({ accountId, userId, providerId, errorCode }) => {
                console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
            },

            /**
             * 数据上传时的回调
             */
            onUploadsCreated: ({ uploads, userId }) => {
                console.log('Uploads: ', uploads, ' User ID:', userId);
            },

            /**
             * 撤销已上传的数据时的回调
             */
            onUploadsRemoved: ({ uploads, userId }) => {
                console.log('Uploads: ', uploads, ' User ID:', userId);
            },

            /**
             * 当页面UI发生改变时推送的事件
             * @param eventName 事件名称
             * @param eventTime 发生时间
             * @param mode 沙箱|生产环境
             * @param userId 用户ID
             * @param account Account对象
             * @param archive Archive对象
             * Uploads revoke callback.
             */
            onUIEvent: ({ eventName, eventTime, mode, userId, account, archive }) => {
                console.log('eventName:', eventName,
                    "eventTime:", eventTime,
                    "mode:", mode,
                    "userId:", userId,
                    "account:", account,
                    "archive:", archive);
            }
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```



注意，示例代码中的 `apiHost` 配置参数指向 `https://link-sandbox.smileapi.io/v1 `。这确保了插件能在 Sandbox 环境中启动（Sandbox Mode），您可以使用下面显示的 Sandbox 测试凭证来测试实现。

## User tokens (Link tokens)

User tokens 是临时的（5小时后失效）访问密钥，通过它开始您与 Smile 链接的过程。

**新用户的链接初始化：**

1. 通过调用 `/users` 端点创建一个带有源数据的新的 Smile 用户，类似于您的产品/系统中的用户标识。您将收到一个 Smile `userId`。我们建议您在系统中保存这个 Smile `userId`，以便将来参考与使用。
2. 通过调用 [`/tokens` endpoint](/reference/tokens) ，使用 `userId` 来创建一个新的 user token。您将收到相应的 `userToken`。
3. 我们在您的 Smile Wink 初始化中提供`userToken`。请确保 user token 在服务器端被请求，您的 `client_id` 和 `client_secret` 将永远不会暴露在前端。

**老用户的链接初始化或刷新 Link token**

1. 通过调用 [`/tokens` endpoint ](/reference/tokens) 获得一个新的 user token，其 `userId`是您之前保存的。
2. 我们在您的 Smile Wink 初始化中提供 `userToken`。请确保 user token 在服务器端被请求，您的 `client_id` 和 `client_secret` 永远不会暴露在前端。

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * Link API URI。注意：Sandbox 和 Production 模式使用不同的API URI。
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * 来自 Smile API 的user token 是从您的后端服务进行传递的。
             */
            userToken: '<usertoken>', // Put your user token here.

            // .....
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```




# 第2步: 连接测试账户

如果想要使用 Sandbox，您可以使用以下示例凭证：

| User Name | Full Name           | Email                     | Mobile Phone     | Password | Verification Code |
| --------- | ------------------- | ------------------------- | ---------------- | -------- | ----------------- |
| George    | George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456   | 1234              |
| Ryan      | Ryan Ng             | ryan1234@smileapi.io      | (+62) 8119994321 | 654321   | 1234              |
| Christina | Christina Tan       | christina4321@smileapi.io | (+65) 99996789   | YGUS1    | 1234              |
| Anisha    | Anisha Bhatia       | anisha98765@smileapi.io   | (+91) 9511198765 | 123456   | 1234              |

在进行下一步之前，请确保您测试过您的实施。点击提供商列表中的一个提供商，并使用其中一个 sandbox 凭证来连接所选的提供商。

# 第3步: 检索 identity, employment 以及 contribution 数据

为了验证个人信息，从 `/identities` 端点获取以下字段：

- First name
- Last name
- Primary address

向 Smile OpenAPI 发出一个 GET 请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/identities?sourceId=<accountId>

# 在请求中输入您的用户账户。
# 这个示例使用的是 sandbox 模式。如果您想在 production 模式中测试，不要忘记切换到 production 模式。

```



下面是一个示例响应：

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
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```



为了验证就业信息，从 `/employments` 端点获取以下字段：

- Employer name
- Job title
- Start date
- End date

向 Smile OpenAPI 发出一个 GET 请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/employments?sourceId=<accountId>
curl --request GET \
     --url 'https://sandbox.smileapi.io/v1/identities?size=10&sourceId=<accountId>' \
     --header 'accept: application/json' \
     --header 'authorization: Basic <authorization>'
     
# 在请求中输入您的用户账户。
# 这个示例使用的是 sandbox 模式。如果您想在 production 模式中测试，不要忘记切换到 production 模式。

```



下面是一个示例响应：

```json
[{
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
}, {
    "id": "e-123abc456def789abc123def456abc78",
    "startDate": "2022-06-01",
    "name": "Security",
    "description": null,
    "jobTitle": "Security Guard",
    "department": null,
    "employeeNumber": "CDE-98765",
    "employer": "CDE Corporation",
    "status": "Permanent",
    "endDate": "2022-06-30",
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "cdecorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```



为了验证社保缴费信息，从 `/contributions` 端点获取以下字段：

- Employer name
- Job title
- Start date
- End date

向 Smile OpenAPI 发出一个 GET 请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/employments?sourceId=<accountId>

# 在请求中输入您的用户账户。
# 这个示例使用的是 sandbox 模式。如果您想在 production 模式中测试，不要忘记切换到 production 模式。

```



下面是一个示例响应：

```json
[{
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-06-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-05-31",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-04-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```



关于其他数据字段，请参考 [Smile API reference](/reference/chapter-1-cn) 。

# 第4步：设置 webhooks

如果想要定期收到用户的账户，identity，contribution 以及 employment 数据的更新，请订阅 [webhooks](/reference/chapter-5-cn) 。

![](https://files.readme.io/79ad8de-image.png)

Webhooks 在每次发生事件时向您的系统发送通知，例如，当一个账户被连接、移除或更新时。

为了监控 identity, contribution 以及 employment  数据的变化，Smile 建议您订阅以下 webhooks 事件，然后调用 Smile OpenAPI 来检索相应的数据。

| 事件   | 事件类型            | 详情                                                              |
|------| ------------- | ------------------------------------------------------------------------------------------------------------- |
| 任务开始 | TASK_STARTED  | 当用户账户的数据同步开始时发送                                             |
| 任务结束 | TASK_FINISHED | 当用户账户的数据同步结束时发送，包含已被同步的数据端点 |

或者您可以订阅特定数据端点的相关事件

| 事件                    | 事件类型            | 详情                 |
|-----------------------| ------------------- |--------------------|
| 添加了社保缴费数据             | CONTRIBUTIONS_ADDED | 当用户提供的社保缴费数据被添加时发送 |
| 添加了预估收入数据             | EINCOMES_ADDED      | 当用户提供的预估收入数据被添加时发送 |
| 添加了交易数据 | TRANSACTIONS_ADDED  | 当用户提供的交易数据被添加时发送   |
| ...                   | ...                 | ...                |

# 第5步：上线运行并扩大规模

在 Sandbox 模式下成功实施并测试成功后，您可以切换到 Production 模式进行发布。

### 修改 apiHost

首先，将 Wink 配置中的 `apiHost` 从：

`https://link-sandbox.smileapi.io/v1`

修改为:

`https://link.smileapi.io/v1`

同样的逻辑适用于您以前使用过的任何 Open API 请求，例如，将 `/employments` 从：

`GET https://open-sandbox.smileapi.io/v1/employments?sourceId={accountId}`

修改为：

`GET https://open.smileapi.io/v1/employments?sourceId={accountId}`

### 更改 API Keys

API Key 可以在 [Developer Portal](https://portal.getsmileapi.com) 的 API Key 部分找到。在切换到 Production 模式时请使用 Production密钥。

### 循序渐进

对于您的第一个 Production 账户，您可以使用自己的账户进行测试，或者在一个自由职业者的工作平台（如 Upwork）上创建一个账户并连接。

### 上线运行并扩大规模

在您的个人账户测试成功后，您可以对真实用户进行测试。我们建议从一个小的用户子集开始，以确保一切正常。然后，将这个子集逐渐推进到您的全部用户群。
