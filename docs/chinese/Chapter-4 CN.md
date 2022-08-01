---
title: 获取用户数据  
excerpt: ""  
category: 62ce2a159aafea009af30da7
---


您可以通过两种方式从用户那里获取数据：
- 通过 API 中的 /invitations API邀请您的用户，或使用Developer Portal中“Users”部分下的邀请功能。
- 嵌入客户端 SDK 并实例化 Wink Widget。

---
<!-- focus：false-->
![邀请函](https://img.icons8.com/ios/50/000000/email-open.png)

## 邀请

Invite允许您邀请您的用户通过电子邮件等通信渠道连接他们的工作帐户或上传与就业相关的文件的副本。使用 API 中的 Invitation API，您可以向一个用户发送消息，或者通过循环访问多个用户的电子邮件地址等联系信息来发送多个邀请。为了让您更容易尝试，我们在 Developer Portal 中提供了邀请的示例实现。

如果您想自定义消息的内容，您可以定义一个邀请模板。您可以通过 API 执行此操作，也可以使用 Developer Portal 中的示例实现。该模板接受如下动态变量：


| Party | Variable Name | Description |
|---|---|---|
| Sender | ${companyName} | Company Name |
| Recipient | ${fullName} | Full Name |


---
<!-- focus：false-->
![代码](https://img.icons8.com/ios/50/000000/open-in-popup.png)


## 客户端 SDK

通过客户端 SDK 将用户数据获取到您的应用程序中涉及两件事：

- **为您的 Web 应用程序客户端嵌入 Javascript SDK**。目前，Smile 仅提供 Javascript SDK，但即将推出适用于 iOS 或 Android 等移动应用程序的原生 SDK 版本。Javascript SDK 会启动一个名为“Wink Widget"，用户可以在其中为 Smile 提供访问其数据的权限。用户将首先找到他们的雇主或就业数据提供者，然后通过安全和加密的连接提交他们的登录凭据和/或上传一些文件。使用SDK时，您无需担心不同就业平台的不同认证和验证实现，或提供文件上传机制和管理数据分析或OCR。我们为您的开发人员简化了获取数据和使用该数据的过程。

- **从 Smile Open API 获取用户令牌**。您的后端服务器应该从 /users API获取“链接”令牌。这是一个一次性使用的短期令牌，用于初始化 Wink Widget。每次您希望启动Widget时，您的服务器都应生成一个新的链接令牌。


---
<!-- focus: false -->
![代码](https://img.icons8.com/ios/50/000000/code.png)

## 示例代码
下面是嵌入 Wink Javascript SDK 的示例 HTML 代码：

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink Quickstart - Sandbox Mode</title>
</head>

<body>
    <script src="https://web.smileapi.io/v1/smile.v1.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * 链接API URI。注意：Sandbox和Production模式使用不同的API URI。
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * User Token： 从你的后端服务里面获取，你的后端服务需要调用SmileAPI /tokens或者/users接口来获取。
             */
            userToken: '<usertoken>',

            /**
             * 用来置顶部分provider，在Wink Widget的Provider List页面里面会显示在顶部， 比如： ['upwork', 'freelancer']
             */
            topProviders: [],

            /**
             * 用来控制只显示部分Provider。比如： ['upwork', 'freelancer']。
             */
            providers: [],

            /**
             * 启用或禁用文件上传。
             */
            enableUpload: true,           

            onAccountCreated: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountConnected: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountRemoved: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onClose: () => {
                console.log('Widget closed')
            },

            onTokenExpired: updateToken => {
                console.log('Token expired');
            }
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```

---


<!-- focus：false-->
![设置](https://img.icons8.com/material-outlined/60/000000/settings-3--v1.png)

## 配置参数

| 参数 |值 |
|---------|---------|
| apiHost | https://link-sandbox.smileapi.io/v1 用于 Sandbox 模式 |
| | https://link.smileapi.io/v1 用于 Production 模式 |
| userToken | 使用 /users API 从 Smile 返回的用户令牌（请参阅有关User API的文档）|
| topProviders | 使用Provider ID 传递提供者列表（请参阅Provider API上的文档），以使它们出现在 Wink Widget中提供者列表的顶部。使用此参数突出显示某些Provider，并确保在首次加载列表时用户可以轻松看到它们。|
| providers| 使用Provider ID 传递提供者列表（请参阅Provider API上的文档）以预过滤 Wink Widget中的提供者列表。只传递一个Provider ID 将跳过选择列表并立即将用户带到身份验证界面。|
| enableUpload | 启用或禁用在提供者列表中显示Upload选项（true 或 false）。默认情况下，如果未设置，我们会禁用Upload。禁用Upload还会隐藏无法直接连接帐户或链接的数据源。|

> 🚧 警告
>
> **上传在Sandbox模式下被禁用。**如果您需要预览上传的工作方式，您将需要访问Production模式。请通过 access@getsmileapi.com 联系我们或通过开发者控制台预订电话以获取访问权限。

---
<!-- focus：false-->
![令牌](https://img.icons8.com/ios/50/000000/sms-token.png)

## 刷新用户令牌
您可以通过调用 /tokens API 来刷新用户的令牌。只需在查询中将 userId 作为参数传递给用户一个新的令牌。更多信息可以在 Tokens API文档中找到。

---
<!-- focus：false-->
![事件](https://img.icons8.com/ios/50/000000/important-event.png)

## 链接事件
当用户在 Wink Widget 界面上移动时，用户执行的任何活动都会被捕获并用于更新消息和模式窗口的呈现，或者发送到 Smile 以便可以检索任何与源相关的数据。

### 关联账户
如果用户能够成功地通过数字就业数据提供者进行身份验证，则链接状态将更改为“CONNECTED”。可以通过 /accounts API 随时查询用户的账户状态。捕获的事件示例包括：

| 活动 |描述 |
|---------|---------|
| PENDING | 帐户已创建，但正在等待成功的身份验证 |
| AWAITING_MFA| 用户能够成功进行身份验证，但是数据提供者正在等待用户在 2 因素身份验证场景中输入他们的验证码。|
| ERROR | 数据提供者返回错误。用户可能没有输入错误的凭据，或者提供商方面存在问题。|
| CONNECTED | 用户能够成功地通过就业数据提供者进行身份验证。|
| DISCONNECTED | 用户断开了与就业数据提供者的链接。|

您也可以允许用户使用 /accounts API 撤销对其帐户数据的访问权限。与被撤销帐户相关的所有数据将从系统中删除。

### 成功上传
如果用户能够通过扫描或拍照文件成功上传就业和收入数据，则链接状态将更改为“STARTED”。可以随时通过 /archives API 查询用户的上传状态。捕获的事件示例包括：

| 活动 |描述 |
|---------|---------|
| STARTED | 上传成功，开始分析能否提取数据。|
| ANALYZED | 分析已完成，数据已成功提取（通过 OCR）并转换为 JSON 格式。|
| UNSUPPORTED | 无法分析上传的文件类型。无法自动提取数据。|
| ERROR | 上传文件的分析出现问题。|
| REVOKED | 用户撤销了从上传的文件中共享数据的权限。|


---
<!-- 焦点：假-->
![测试](https://img.icons8.com/material-outlined/50/000000/test-tube.png)

## 沙盒测试

Smile 为我们的生产环境提供了Sandbox模式，让您可以测试与示例数据的集成。

您可以使用以下示例账号来使用Sandbox：

| 姓名 | 电子邮件 | 手机 | 密码 | 验证码 |
|---|---|---|---|---|
| George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456 | 1234|
| Ryan Ng | ryan1234@smileapi.io | (+62) 8119994321 | 654321 | 1234 |
| Christina Tan | christina4321@smileapi.io | (+65) 99996789 | YGUS1 | 1234|
| Anisha Bhatia | anisha98765@smileapi.io | (+91) 9511198765 | 123456 | 1234|