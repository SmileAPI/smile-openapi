---
title: 事件通知
excerpt: ''
category: 62ce2a159aafea009af30da7
slug: chapter-5-cn
---

<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks

当我们的服务器中发生与您的环境相关的事件时，Smile 使用 webhooks 实时通知您的应用程序。

当创建一个用户，成功连接一个账号，上传一个就业文件，发送一个邀请时，或者当任何新类型的数据，如用户的身份，收入，就业等被添加时，事件通知将被发送。在我们的[Webhooks reference page](/reference/webhooks)中查看您可以订阅的可用事件列表。

这些 webhooks 通过安全通道发送，使用来自静态 IP 地址的 HTTPS，数据以 JSON 格式发送。并带有一个签名，供您验证内容的真实性。

> 📘 Note
>
> 我们的静态 IP 地址是 **18.142.61.230**。您可以在后端将此 IP 地址列入白名单，以确保您的应用程序收到来自 Smile 的事件通知。

Webhook 对于获取有关异步事件的通知非常有用，当这些事件发生时，它可以在您的后台系统中执行行动，或者知道何时刷新您的前端系统以显示新数据。

关于详细的实施步骤，请访问我们的[Webhooks reference page](/reference/webhooks)了解更多信息。

## 回调

Smile还使用回调来实时通知您的应用程序在您的环境中发生的与前端有关的事件。

通过回调，一旦用户使用 Wink Widget 执行了被支持的动作，您就可以做出反应或执行其他动作。监听诸如账户连接、token 到期或关闭 Wink Widget 等事件，可以帮助您的本地应用程序管理并对用户的行为做出反应。

### 回调列表

| 回调                   | 数据                                               | 详情                                                                             |
|:---------------------|:-------------------------------------------------|:-------------------------------------------------------------------------------|
| `onAccountCreated`   | `accountId`, `userId`, `providerId`              | 当启动账户连接过程时触发                                                                   |
| `onAccountConnected` | `accountId`, `userId`, `providerId`              | 当账户连接过程成功完成时触发                                                                 |
| `onAccountRemoved`   | `accountId`, `userId`, `providerId`              | 当账户访问权被用户撤销时触发                                                                 |
| `onTokenExpired`     | -                                                | 当链接 token 过期时触发                                                                |
| `onClose`            | -                                                | 当 Wink Widget 被用户关闭时触发                                                         |
| `onAccountError`     | `accountId`, `userId`, `providerId`, `errorCode` | 当用户账户链接出现错误时触发                                                                 |
| `onUploadsCreated`   | `uploads`, `userId`                              | 当用户通过 Wink Widget 提交要上传的文件时触发|

### 事件示例

#### onAccountCreated

当账户连接过程由用户启动时触发，例如通过发送他们的登录凭证。这不会显示用户的登录凭证。

```
onAccountCreated: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onAccountConnected

当账户连接过程成功完成，并向用户显示成功连接屏幕时触发。

```
onAccountConnected: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onAccountRemoved

当账户访问权被用户撤销时触发。

```
onAccountRemoved: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onTokenExpired

当链接令牌已过期时触发。您可以通过调用[Refresh Token API](/reference/creat-token-1)来更新用户的 token 。

```
onTokenExpired: () => {
    console.log('Token expired');
},
```

#### onClose

当 Wink Widget 被用户通过关闭图标或退出按钮关闭时触发。

```
onClose: () => {
    console.log('Widget closed')
},
```

#### onAccountError

当用户账户链接出现错误时触发。完整的错误列表可以在[Get Account API reference](/reference/get-account-1)中看到。

```
onAccountError: ({
    accountId,
    userId,
    providerId,
    errorCode
}) => {
    console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
},
```

#### onUploadsCreated

当用户通过 Wink Widget 提交要上传的文件时触发。

```
onUploadsCreated: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
},
```