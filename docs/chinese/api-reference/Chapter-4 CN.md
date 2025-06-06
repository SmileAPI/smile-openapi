---
title: 连接账户 
excerpt: ""  
category: 62ce2a159aafea009af30da7
slug: chapter-4-cn
---


**Smile Wink** 是 Smile API 的账户关联服务，它支持个人与第三方组织之间在用户授权的前提下，安全地共享身份、收入和就业数据。

开发者可以使用基于 JavaScript 的客户端 SDK（即 Smile 的 Wink Widget），轻松地将此功能集成到 Web 或移动应用程序中。该 Widget 提供了一个无缝且安全的界面，用户可以通过输入凭证或上传相关文件，与他们的就业数据提供商进行身份验证。验证通过后，Smile 会获取数据，并可通过开发者门户或开放 API 访问这些数据。

这个统一的解决方案简化了各种认证流程和数据格式的复杂性，既简化了开发者的集成工作，也优化了用户体验。

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## 集成步骤

开始使用 Smile 开放 API 非常简单。实现 Smile 开放 API 涉及简单的客户端和服务器端集成，下面概述了四个关键步骤：

1. **Link token**：您的应用服务器向我们的 REST API 发送请求，以生成一个短期的“token”。
2. **Wink Widget**：您的应用客户端使用token初始化客户端 SDK，以启动 Smile Wink Widget。您的最终用户将与该 Widget 进行交互，通过安全加密连接提交登录凭证，以向其就业数据提供商进行身份验证。
3. **连接到源数据**：进入 Widget 后，用户可以连接他们的就业账户，或者上传其就业数据的照片或扫描件。这将作为您的应用程序请求的任何用户数据的来源。
4. **请求**：我们的服务器执行您的应用程序的请求。我们从用户的就业数据提供商处读取、转换并临时存储数据，以便将其发送到客户端应用程序。
5. **Webhook**：在数据需要异步处理的情况下，Webhook 也可以发送到您的服务器。每当数据可用或更新时，都会通过 Webhook 发送消息。然后，您的服务器可以从我们的 REST API 获取数据。在事件通知部分了解更多信息。

---
<!-- focus: false -->
![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)

## 快速入门

为了在您自己的环境中实际测试 Smile API，我们提供了用于实例化 Wink Widget 或 SDK 的示例代码。

> 📘 注意
>
> 我们在 [Github](https://github.com/SmileAPI) 上提供了 [快速入门示例代码](https://github.com/SmileAPI/quickstart)，您可以根据自己的需求下载和修改。

示例代码安装了一个运行在 Node.js 上的小型服务器，该服务器会自动从我们的 API 获取Token，因此您可以在自己的本地机器上实例化 Wink Widget。

示例实现由两部分组成：
- 在 ``/frontend`` 目录下，您会找到已经嵌入 Wink JavaScript SDK 的 HTML 示例代码。
- 在 ``/node`` 目录下，您会找到用于获取Token的服务器端 JavaScript 代码。您需要下载并运行 Node.js 才能运行此代码。

**实施步骤**

以下步骤也包含在快速入门 [仓库](https://github.com/SmileAPI/quickstart) 的 README.md 文件中。

1. **将快速入门文件下载到您的机器上**

   > 📘 注意
   >
   > 如果您安装了 git，您可以克隆该仓库或运行以下命令：
   >
   > ```bash
   > git clone https://github.com/SmileAPI/quickstart
   > ```

2. **进入您下载的快速入门文件的 ``/node`` 目录**

3. **在该目录中创建一个名为 ``.env`` 的新文件**，内容如下：

   ```bash
   # 您希望示例服务器监听的端口
   APP_PORT=<portnumber>
   
   # Smile 链接 API 密钥（您可以通过向 access@getsmileapi.com 请求访问来获取此密钥）
   API_KEY=<apikey>
   API_SECRET=<apisecret>
   
   # API 主机（决定这将在SANDBOX环境还是生产环境中运行）
   OPEN_API_HOST=<openapihost>
   ```

   您可以参考快速入门仓库中包含的 ``.env.example`` 文件。

   > 🚧 警告
   >
   > **.env 文件通常会被系统隐藏**。您可能需要在系统偏好设置中启用隐藏文件的显示才能看到它。
   >
   > 此外，在 Windows 机器上，Windows 不允许您直接从 Windows 资源管理器创建以 ``.`` 开头的文件名。要解决这个问题，您可以执行以下步骤：
   >
   > 1. 打开记事本并写入文件内容（见下文）。
   > 2. 在记事本中转到“文件” -> “另存为”窗口。
   > 3. 在选择窗口中选择“所有文件”类型。
   > 4. 将文件保存为 ``.env``

   您可能需要确保您的机器具有创建该文件的适当权限。

   > 📘 注意
   >
   > 在 Mac 或 Linux 机器上，您可以打开终端并以超级用户身份输入以下命令：
   >
   > ```bash
   > sudo touch .env
   > ```

4. **保存并关闭文件**

5. 如果您的机器上没有安装 Node.js，请**安装 Node.js**

   > 📘 注意
   >
   > **对于 Mac**，您可以打开终端并运行：
   > ```bash
   > curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
   > ```
   >
   > **对于 Windows**，您可以[下载安装程序](https://nodejs.org/en/#home-downloadhead)。
   >
   > **对于其他操作系统**，您可以从 [Node.js 网站](https://nodejs.org/en/download/package-manager/#macos) 找到安装说明。

6. **使用 [npm 包管理器](https://www.npmjs.com/) 运行 Yarn**，该管理器包含在 Node.js 中，并输入以下命令：
   ```bash
   npm install --global yarn
   yarn install
   ```

   > 📘 注意
   >
   > 在 Mac 或 Linux 系统中，您需要打开终端。如果使用 Windows 系统，您可以打开命令行。确保您仍处于刚刚下载到机器上的快速入门文件的 ``/node`` 目录中。
   >
   > 如果您没有足够的权限，可能需要以超级用户身份运行。在 Mac 或 Linux 机器上，您可以使用 ``sudo`` 以超级用户身份运行命令。在 Windows 上，您可以使用管理员信任级别运行命令，或者右键单击 UI 中的程序并选择“以管理员身份运行”。

7. **运行服务器**
   ```bash
   node index.js
   ```

   > 🚧 警告
   >
   > 如果您在运行 Node 服务器时遇到问题，可能需要在环境中安装 dotenv。要安装 dotenv，只需运行以下命令：
   >
   > ```bash
   > npm install dotenv
   > ```

8. **打开浏览器并打开示例 Wink Widget**。例如，如果您在 ``.env`` 配置文件中指定端口为 ``:8000``，则在 Web 浏览器中打开 http://127.0.0.1:8000。

9. **使用提供的 [SANDBOX账户](ref:getting-user-data#testing-in-sandbox) 测试 Widget**

> 👍 做得好！
>
> 坐下来，放松一下，为自己出色的工作鼓掌吧！


---
<!-- focus: false -->
![User Data](https://img.icons8.com/?size=50&id=FD1d9t9lMoS2&format=png&color=000000)
## 获取用户数据

您可以通过三种方式从用户那里获取数据：

1. 通过 API 中的 ``/invitations`` 端点邀请您的用户，或使用 [开发者门户中用户部分的邀请功能](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link)。
2. 嵌入客户端 SDK 并实例化 Wink Widget，让您的用户直接从您的应用或网站分享他们的信息。
3. 发布一个嵌入了 Wink Widget 的 Flip 站点，并引导您的用户完成表单（请参阅表单处理）。

### 邀请

邀请功能允许您通过电子邮件等通信渠道邀请用户连接他们的工作账户或上传与就业相关的文件副本。使用 API 中的邀请端点，您可以向单个用户发送消息，或者通过遍历多个用户的联系信息（如电子邮件地址）发送多个邀请。为了方便您进行尝试，我们在 [开发者门户中提供了邀请的示例实现](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link)。

如果您想自定义消息内容，可以定义一个邀请模板。您可以通过 API 来完成此操作，也可以使用开发者门户中的示例实现。该模板接受以下动态变量：

| 参与方 | 变量名            | 描述   |
|-----|----------------|------|
| 发送方 | ${companyName} | 公司名称 |
| 接收方 | ${fullName}    | 全名   |

### 客户端 SDK

通过客户端 SDK 将用户数据获取到您的应用程序中涉及两件事：

- **为您的 Web 应用程序客户端嵌入 JavaScript SDK**。目前，Smile 仅提供 JavaScript SDK，但适用于 iOS 或 Android 等移动应用程序的原生 SDK 版本即将推出。JavaScript SDK 会启动一个名为“Wink”的模态窗口Widget，用户可以在其中授权 Smile 访问他们的数据。用户首先需要找到他们的雇主或就业数据提供商，然后通过安全加密连接提交登录凭证和/或上传一些文件。使用 SDK 时，您无需担心不同就业平台的不同认证和验证实现，也无需提供文件上传机制和管理数据分析或 OCR。我们为您的开发人员简化了获取和使用数据的过程，也为您的用户提供了流畅的体验。
- **从 Smile 开放 API 获取用户Token**。您的后端服务器应从 /users 端点获取“链接”Token。这是一个一次性使用的短期Token，用于初始化 Wink Widget。每次您希望启动该 Widget 时，您的服务器都应生成一个新的token。

---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/code.png)

#### 示例代码
以下是嵌入 Wink JavaScript SDK 的 HTML 示例代码。

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink 快速入门 - SANDBOX模式</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * 从您的后端服务传递的用户Token（token），该Token从 Smile API 获取。
             */
            userToken: '<usertoken>',

            /**
             * 使用模板 ID 来确定您的Widget嵌入到应用或网站中的外观。
             * 您可以在 Smile 开发者门户中找到并创建模板 ID。
             * https://developer-portal.smileapi.io/link/template
             */
            templateId: "<wink 模板的 ID>",

            /**
             * 账户登录回调。
             */
            onAccountCreated: ({ accountId, userId, providerId }) => {
                console.log('账户已创建: ', accountId, ' 用户 ID:', userId, ' 提供商 ID:', providerId)
            },

            /**
             * 账户登录成功回调。
             */
            onAccountConnected: ({ accountId, userId, providerId }) => {
                console.log('账户已连接: ', accountId, ' 用户 ID:', userId, ' 提供商 ID:', providerId)
            },

            /**
             * 账户撤销回调。
             */
            onAccountRemoved: ({ accountId, userId, providerId }) => {
                console.log('账户已移除: ', accountId, ' 用户 ID:', userId, ' 提供商 ID:', providerId)
            },

            /**
             * Token过期回调。
             */
            onTokenExpired: () => {
                console.log('Token已过期');
            },

            /**
             * Smile 链接 SDK 关闭回调。如果您想知道用户点击了哪个按钮来触发关闭事件，您可以像这样传递参数。
             * onClose:({reason})=>{}
             * 如果 reason 的值等于 "close"，则表示用户点击了页面右上角的关闭图标来关闭 SDK
             * 如果 reason 的值等于 "exit"，则表示用户点击了连接页面上的“完成”按钮来关闭 SDK
             */
            onClose: ({ reason }) => {
                console.log('链接已关闭，原因:', reason)
            },

            /**
             * 账户连接错误回调。
             */
            onAccountError: ({ accountId, userId, providerId, errorCode }) => {
                console.log('账户错误: ', accountId, ' 用户 ID:', userId, ' 提供商 ID:', providerId, '错误代码:', errorCode)
            },

            /**
             * 上传提交回调。
             */
            onUploadsCreated: ({ uploads, userId }) => {
                console.log('上传内容: ', uploads, ' 用户 ID:', userId);
            },

            /**
             * 上传撤销回调。
             */
            onUploadsRemoved: ({ uploads, userId }) => {
                console.log('上传内容: ', uploads, ' 用户 ID:', userId);
            },

            /**
             * 用户事件回调用于捕获 Smile Wink SDK 中的所有用户活动
             */
            onUIEvent: ({ eventName, eventTime, mode, userId, account, archive }) => {
                console.log('事件名称:', eventName,
                    "事件时间:", eventTime,
                    "模式:", mode,
                    "用户 ID:", userId,
                    "账户:", account,
                    "存档:", archive);
            }
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```
> 📘 注意
>
> 目前有两个版本的 SDK 可供使用。上面显示的是版本 2（最新版本）的代码。版本 1 已经不维护，所以请使用版本 2。要在版本 1 和版本 2 之间切换，只需将 SDK 源代码切换到版本 1 即可，无需进行其他更改。

---
<!-- focus: false -->
![Settings](https://img.icons8.com/material-outlined/50/000000/settings-3--v1.png)

## 配置

Wink Widget 使用 Wink 模板来管理嵌入到您应用中的每个 Widget 的实例化设置。Wink Widget 模板允许对您的 Widget 进行丰富的自定义，包括主要颜色和为该实例选择的数据源。

| 参数         | 值                                                     |
|------------|-------------------------------------------------------|
| templateId | 正在使用的 Wink 模板的 ID                                     |
| userToken  | 使用 /users 端点从 Smile 返回的用户Token（请参阅用户端点的文档）            |
| callbacks  | 所有回调都是可选的，但建议监听 onClose() 回调，以便从 Smile SDK 返回您的应用程序页面 |

---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)
## 事件通知

当用户在 Wink Widget 屏幕中操作时，用户执行的任何活动都会被捕获，这些活动要么用于更新模态窗口的消息和显示，要么发送到 Smile 以便检索任何与源相关的数据。

### 关联账户

如果用户能够成功地通过数字就业数据提供商进行身份验证，则链接状态将更改为“已连接”。可以随时通过 /accounts 端点查询用户的账户状态。捕获的事件示例包括：

| 事件           | 描述                                         |
|--------------|--------------------------------------------|
| PENDING      | 账户已创建，但等待成功的身份验证                           |
| AWAITING_MFA | 用户能够成功进行身份验证，但数据提供商正在等待用户在双因素身份验证场景中输入验证码。 |
| ERROR        | 数据提供商返回错误。用户可能输入了错误的凭证，或者提供商方面存在问题。        |
| CONNECTED    | 用户能够成功地通过就业数据提供商进行身份验证。                    |
| DISCONNECTED | 用户断开了与就业数据提供商的链接。                          |

您也可以允许用户使用 /accounts 端点撤销对其账户数据的访问权限。与被撤销账户相关的所有数据将从系统中删除。

---
<!-- focus: false -->
![Storage](https://img.icons8.com/?size=50&id=1476&format=png&color=000000)
## 维护用户数据

Smile API 仅在以下情况之一发生之前存储用户数据：

1. 用户撤销对其数据的访问权限
2. 通过撤销 API 撤销访问权限（即由开发者发起）
3. 自账户连接之日起已过去 60 天

为确保在最长 60 天的时间范围之后仍能持续访问数据，请确保您在自己的服务器上检索并存储用户数据。一旦您从 Smile 服务器检索到数据，您可以使用撤销 API 指示 Smile 撤销该数据。当用户手动撤销其数据共享时，您还将收到 Smile 发出的事件通知。

### 连续数据同步

一旦用户同意并通过 Wink Widget连接他们的账户，Smile API 的*连续数据同步*（CDS）功能可让您访问用户的最新数据。通过同意 CDS，用户可以授权 Smile 为您跨多个月同步数据，直到他们撤销对其账户的访问权限。

在[账户部分](/reference/accounts)了解更多关于 CDS 以及如何启用 CDS 的信息。

### 刷新用户Token

您可以通过调用 `/tokens` 端点来刷新用户的Token。只需在查询中传递 `userId` 作为参数，即可为用户提供一个新的Token。更多信息可在Token端点文档中找到。

---
<!-- focus: false -->
![Versioning](https://img.icons8.com/?size=50&id=21889&format=png&color=000000)
## 版本管理

**Wink Widget版本 2 包含许多用户体验和功能改进，是推荐使用的版本**。

版本 1 仍会得到维护，并且会继续进行安全监控、更新和打补丁。

| 版本                 | SDK JavaScript 嵌入代码                                              |
|--------------------|------------------------------------------------------------------|
| version 2 **(推荐)** | `<script src="https://web.smileapi.io/v2/smile.v2.js"></script>` |
| version 1          | `<script src="https://web.smileapi.io/v1/smile.v1.js"></script>` |