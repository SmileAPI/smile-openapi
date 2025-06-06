---
title: 事件通知
excerpt: ""  
category: 62ce2a159aafea009af30da7
slug: chapter-3-cn
---

<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhook（网络钩子）

当我们服务器中发生与您的环境相关的事件时，Smile 会使用 Webhook 实时通知您的应用程序。

当创建新用户、成功连接账户、上传就业文件、发送邀请，或者添加任何新类型的数据（如用户身份、收入、就业等）时，都会发送事件通知。您可以在我们的 [Webhook 参考页面](/reference/webhooks) 查看可订阅的可用事件列表。

这些通知通过安全通道发送，使用来自静态 IP 地址的 HTTPS，数据以 JSON 格式传输。同时还会附带一个签名，供您验证负载的真实性。

> 📘 注意
>
> 我们的静态 IP 地址是 **18.142.61.230**。您可以在后端将此 IP 地址列入白名单，以确保您的应用程序能收到来自 Smile 的事件通知。

Webhook 对于获取异步事件的通知特别有用，您可以在这些事件发生时在后端系统中执行操作，或者知道何时刷新前端系统以显示新数据。

有关详细的实施步骤，请访问我们的 [Webhook 参考页面](/reference/webhooks) 了解更多信息。

## 回调

Smile 还使用回调来实时通知您的应用程序在您的环境中发生的与前端相关的事件。

通过回调，一旦您的用户使用 Wink Widget 执行了受支持的操作，您就可以做出反应或执行其他操作。监听账户连接、Token过期或关闭 Widget 等事件，可以帮助您的原生应用程序管理并响应用户的操作。

### 回调列表

| 回调                   | 参数                                                               | 描述                              |
|:---------------------|:-----------------------------------------------------------------|:--------------------------------|
| `onAccountCreated`   | `accountId`, `userId`, `providerId`                              | 账户链接过程启动时触发                     |
| `onAccountConnected` | `accountId`, `userId`, `providerId`                              | 账户链接过程成功完成时触发                   |
| `onAccountRemoved`   | `accountId`, `userId`, `providerId`                              | 用户撤销账户访问权限时触发                   |
| `onTokenExpired`     | -                                                                | 链接Token过期时触发                    |
| `onClose`            | `reason`                                                         | 用户关闭 Wink Widget 时触发            |
| `onAccountError`     | `accountId`, `userId`, `providerId`, `errorCode`                 | 用户账户链接出现错误时触发                   |
| `onUploadsCreated`   | `uploads`, `userId`                                              | 用户通过 Wink Widget 提交要上传的文件时触发    |
| `onUploadsRemoved`   | `uploads`, `userId`                                              | 用户通过 Wink Widget 删除/撤销已上传的文件时触发 |
| `onUIEvent`          | `eventName`, `eventTime`, `mode`, `userId`, `account`, `archive` | 向用户显示新的 Widget 页面时触发。见下面的页面列表   |

### 事件示例

#### onAccountCreated

当用户通过发送登录凭证等方式启动账户链接过程时触发。此操作不会显示用户的登录凭证。

```javascript
onAccountCreated: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

| Property   | Type   | 描述                    |
|:-----------|:-------|:----------------------|
| accountId  | string | 用户试图连接的账户 ID          |
| userId     | string | 终端用户在 Smile 网络上的用户 ID |
| providerId | string | 用户试图连接的提供商 ID         |

#### onAccountConnected

当账户链接过程成功完成，并且向用户显示连接成功屏幕时触发。

```javascript
onAccountConnected: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

| Property   | Type   | 描述                    |
|:-----------|:-------|:----------------------|
| accountId  | string | 用户已连接的账户 ID           |
| userId     | string | 终端用户在 Smile 网络上的用户 ID |
| providerId | string | 用户已连接的提供商 ID          |

#### onAccountRemoved

当用户撤销账户访问权限时触发。

```javascript
onAccountRemoved: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
}
```

| Property   | Type   | 描述                    |
|:-----------|:-------|:----------------------|
| accountId  | string | 用户已移除的账户 ID           |
| userId     | string | 终端用户在 Smile 网络上的用户 ID |
| providerId | string | 用户已移除账户的提供商 ID        |

#### onTokenExpired

当链接Token过期时触发。您可以调用 [刷新Token API](/reference/create-token-1) 来刷新用户的Token。

```javascript
onTokenExpired: () => {
    console.log('Token expired');
}
```

#### onClose

当用户通过关闭图标或退出按钮关闭 Wink Widget 时触发。

`reason` 参数可以是以下任意值：

- `close` - 用户点击页面右上角的关闭图标关闭 SDK
- `exit` - 用户点击成功连接屏幕上的 “完成” 按钮关闭 SDK
- `error` - 用户点击错误页面上的退出按钮关闭 SDK

```javascript
onClose: ( reason ) => {
    console.log('Widget closed. Reason: ', reason )
}
```

#### onAccountError

当用户账户链接出现错误时触发。完整的错误列表可以在 [获取账户 API 参考](/reference/get-account-1) 中查看。

```javascript
onAccountError: ({
    accountId,
    userId,
    providerId,
    errorCode
}) => {
    console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
}
```

| Property   | Type   | 描述                    |
|:-----------|:-------|:----------------------|
| accountId  | string | 用户试图连接的账户 ID          |
| userId     | string | 终端用户在 Smile 网络上的用户 ID |
| providerId | string | 用户试图连接的提供商 ID         |
| errorCode  | string | 错误的错误代码               |

#### onUploadsCreated

当用户通过 Wink Widget 提交要上传的文件时触发。

```javascript
onUploadsCreated: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
}
```

| Property | Type   | 描述                    |
|:---------|:-------|:----------------------|
| uploads  | object | 包含有关上传的具体信息           |
| userId   | string | 终端用户在 Smile 网络上的用户 ID |

#### onUploadsRemoved

当用户通过 Wink Widget 删除/撤销已上传的文件时触发。

```javascript
onUploadsRemoved: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
}
```

| Property | Type | 描述 |
| :------- | :---- | :---- |
| uploads | object | 包含有关上传的具体信息 |
| userId | string | 终端用户在 Smile 网络上的用户 ID |

#### onUIEvent

每当向用户显示新的 Widget 页面时触发。

```javascript
onUIEvent: ({ eventName, eventTime, mode, userId, account, archive }) => {
    console.log('Event Name: ', eventName, ', Event Time: ', eventTime, ', mode: ', mode, ', User ID: ', userId, ', Account: ', account, ', Archive: ', archive);
}
```

| Property  | Type   | 描述                                                                  |
|:----------|:-------|:--------------------------------------------------------------------|
| eventName | string | 事件名称，例如 `LoginPageOpened`                                           |
| eventTime | string | 事件发生的时间                                                             |
| mode      | string | 当前运行的 Wink Widget 模式，例如 `SANDBOX` 或 `PRODUCTION`                    |
| userId    | string | 终端用户在 Smile 网络上的用户 ID                                               |
| account   | object | 包含与事件相关的特定账户信息，例如 `providerId` 或 `accountId`。请注意，这些是 Smile 网络特定的 ID |
| archive   | object | 包含与事件相关的特定存档信息，例如 `fileType`                                        |

事件名称列表如下：

| Event Name               | 描述                                          | 事件特定属性                |
|:-------------------------|:--------------------------------------------|:----------------------|
| ConsentPageOpened        | 用户打开同意页面                                    |                       |
| ProviderListPageOpened   | 用户打开提供商列表页面                                 |                       |
| LoginPageOpened          | 用户打开登录页面                                    | providerId            |
| MfaPageOpened            | 用户打开多因素身份验证页面                               | providerId            |
| ConnectSuccessPageOpened | 用户打开账户连接成功页面                                | providerId, accountId |
| AccountRevokePageOpened  | 用户打开账户连接状态页面/撤销页面                           | providerId, accountId |
| LoginOptionsPageOpened   | 用户打开替代登录选项页面                                |                       |
| EmployerSurveyPageOpened | 用户打开雇主调查问卷页面                                |                       |
| FileTypeListPageOpened   | 用户打开文档类型选择页面（例如，选择他们希望上传的文档类型，如社保记录、所得税记录等） |                       |
| FileTypePageOpened       | 用户打开文档上传页面                                  |                       |
| ArchiveSuccessPageOpened | 用户成功上传文件并打开成功页面                             |                       |
| RevokeArchivePageOpened  | 用户打开存档状态页面/删除页面                             |                       |
