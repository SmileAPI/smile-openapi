---
title: 实施与上线
excerpt: ""  
category: 6422597473b6df0073e64c8e  
slug: credit-decisioning-implementation
---

![](https://files.readme.io/8123ce2-image.png)

为了成功地将 Smile 融入您的流程，我们建议通过以下3个步骤来实现：

- 收集需求 - 探索您的使用用例，以及您想通过 Smile 数据实现什么目标
- [Design](/docs/credit-decisioning-design) - 设计您的用户流程以及与 Smile 的集成
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
             * Link API URI。注意：Sandbox 和 Production 模式使用不同的API URI。
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * 从您的后端服务传递的 Smile API 的 User token(link token)。
             */
            userToken: '<usertoken>',

            /**
             * 通过提供商 ID 将某些提供商提升到列表的顶部。例如 ['upwork', 'freelancer']。
             */
            topProviders: [],

            /**
             * 通过使用提供商 ID，在 Wink Widget 中只显示选定的提供商。例如 ['upwork', 'freelancer'] 。
             */
            providers: [],

            /**
             * 如果您想隐藏提供商搜索栏，请将 enableSearchBar 设置为 false。
             * 默认为：true
             */
            enableSearchBar: true,

            /**
             * 如果您想隐藏提供商类型过滤器，请将 enableTypeBar 设置为 false。
             * 默认为: true
             */
            enableTypeBar: true,

            /**
             * 启用或禁用上传文件。
             */
            enableUpload: true,           

            /**
             * 如果您希望公司名称反映在同意和登录页面上，请设置为您的公司名称。
             * 默认为: 空
             */
            companyName: "",

            /**
             * 帐户创建回调。
             */
            onAccountCreated: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * 帐户登录成功回调。
             */
            onAccountConnected: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * 帐户撤销回调。
             */
            onAccountRemoved: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Token 过期回调。
             */
            onTokenExpired: () => {
                console.log('Token expired');
            },

            /**
             * Smile link SDK 关闭回调。
             */
            onClose: () => {
                console.log('Widget closed')
            },

            /**
             * 帐户连接错误回调。
               其中 errorCode 是来自 https://docs.getsmileapi.com/reference/get-account-1 中的账户连接 errorCode。
               例如：
                    ACCOUNT_DISABLED 
                    ACCOUNT_INACCESSIBLE 
                    ACCOUNT_INCOMPLETE 
                    ACCOUNT_LOCKED 
                    AUTH_REQUIRED 
                    EXPIRED_CREDENTIALS 
                    INVALID_ACCOUNT_TYPE 
                    INVALID_AUTH 
                    INVALID_CREDENTIALS 
                    INVALID_MFA MFA_TIMEOUT 
                    SERVICE_UNAVAILABLE SYSTEM_ERROR 
                    TOS_REQUIRED 
                    UNSUPPORTED_AUTH_TYPE 
                    UNSUPPORTED_MFA_METHOD
             */
            onAccountError: ({ accountId, userId, providerId, errorCode }) => {
                console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
            },

            /**
             * 上传提交回调。
             */
            onUploadsCreated: ({ uploads, userId }) => {
                console.log('Uploads: ', uploads, ' User ID:', userId);
            },
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
2. 通过调用 [`/tokens` endpoint](https://docs.getsmileapi.com/reference/tokens) ，使用 `userId` 来创建一个新的 user token。您将收到相应的 `userToken`。
3. 我们在您的 Smile Wink 初始化中提供`userToken`。请确保 user token 在服务器端被请求，您的 `client_id` 和 `client_secret` 将永远不会暴露在前端。

****老用户的链接初始化或刷新 Link token****

1. 通过调用 [`/tokens` endpoint ](https://docs.getsmileapi.com/reference/tokens) 获得一个新的 user token，其 `userId`是您之前保存的。
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
            userToken: '<usertoken>', // 在这里输入您的 user token 

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

# 第3步：检索 transaction、estimated income (eincome) 和 contribution 数据

**对于交易信息**，从 `/transactions` 端点获取以下字段：

- Amount
- Start date
- End date

向 Smile OpenAPI 发出一个`GET`请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/transactions?sourceId=<accountId>

# 在请求中输入您的用户账号。
# 这个示例使用的是 sandbox 模式。如果您想在 production 模式中测试，不要忘记切换到 production 模式。

```



下面是一个示例响应：

```json
[{
    "id": "t-123abc456def789abc123def456abc78",
    "date": "2022-08-31",
    "currency": "PHP",
    "amount": -16.9,
    "metadata": {
        "createdAt": "2022-09-02T23:36:12Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    },
    "description": "Platform fee",
    "referenceId": "Order ID-996438805066"
}, {
    "id": "t-123abc456def789abc123def456abc78",
    "date": "2022-08-29",
    "currency": "PHP",
    "amount": 550,
    "metadata": {
        "createdAt": "2022-09-02T23:36:12Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    },
    "description": "Order revenue",
    "referenceId": "Order ID-994728692055"
}, {
    "id": "t-123abc456def789abc123def456abc78",
    "date": "2022-08-28",
    "currency": "PHP",
    "amount": 250,
    "metadata": {
        "createdAt": "2022-09-02T23:36:12Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    },
    "description": "Rider incentive",
    "referenceId": "Order ID-234728692099"
}]
```



**对于预估收入（eincomes）信息**，从 `/eincomes` 端点获取以下字段：

- Amount
- Month

向 Smile OpenAPI 发出一个`GET`请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/eincomes?sourceId=<accountId>

# 在请求中输入您的用户账号。
# 这个示例使用的是 sandbox 模式。如果您想在 production 模式中测试，不要忘记切换到 production 模式。

```



下面是一个示例响应：

```json
[
   {
      "id":"einc-cd80c6779ef7423c8af5b38b57e4b1eb",
      "month":"2022-11",
      "currency":"PHP",
      "baseAmount":8500,
      "metadata":{
         "createdAt":"2022-12-07T09:33:11Z",
         "sourceId":"a-94f56ca9c3ae42b5acc0c5bd64017f4b",
         "sourceType":"ACCOUNT",
         "userId":"smilebond-7892a2010b444bbe98916db4969e1863",
         "providerId":"sss_ph",
         "accountId":"a-94f56ca9c3ae42b5acc0c5bd64017f4b"
      }
   },
   {
      "id":"einc-cefcc7e769cd48ea8c4e58d3653b3cab",
      "month":"2022-10",
      "currency":"PHP",
      "baseAmount":8500,
      "metadata":{
         "createdAt":"2022-12-07T09:33:11Z",
         "sourceId":"a-94f56ca9c3ae42b5acc0c5bd64017f4b",
         "sourceType":"ACCOUNT",
         "userId":"smilebond-7892a2010b444bbe98916db4969e1863",
         "providerId":"sss_ph",
         "accountId":"a-94f56ca9c3ae42b5acc0c5bd64017f4b"
      }
   }
]
```



**对于社保缴费信息**，从 `/contributions` 端点获取以下字段：

- Employer name
- Job title
- Start date
- End date

向 Smile OpenAPI 发出一个`GET`请求：

```curl
GET https://https://open-sandbox.smileapi.io/v1/employments?sourceId=<accountId>

# 在请求中输入您的用户账号。
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



关于其他数据字段，请参考 [Smile API reference](https://docs.getsmileapi.com/reference/chapter-1)

# 第4步：将 transaction, eincome 以及 contribution 数据输入您的信用决策引擎

您可以使用 Smile 的数据来进一步计算与您的产品相匹配的因子，然后将这些因子发送到您的信用决策引擎。通常情况下，因子可以分为以下几类：

- 累计的收入/社保缴费月数
- 最近3/6/9/12个月的收入/社保缴费数目
- 最近6/12/24个月的收入/社保缴费额度差值

# 第5步：设置 webhooks

如果想要定期收到用户的账户，identity，contribution 以及 employment 数据的更新，请订阅 [webhooks](https://docs.getsmileapi.com/reference/chapter-5) 。

![](https://files.readme.io/e9abfe9-image.png)

Webhooks 在每次发生事件时向您的系统发送通知，例如，当一个账户被连接、移除或更新时。

为了监控新的以及现有的账户，Smile 建议您订阅以下 webhooks：

| 事件                               | 事件类型            | 详情                                                                  |
|----------------------------------|---------------------|---------------------------------------------------------------------|
| 帐户连接成功   | ACCOUNT_CONNECTED   | 当用户成功连接其工作账户时发送          |
| 帐户断线成功 | ACCOUNT_DISCONNECTED | 当用户断开或撤销其工作账户的连接时发送 |
| 帐户连接失败       | ACCOUNT_FAILED      | 当账户连接失败时发送           |

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

# 第6步：上线运行并扩大规模

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