---
title: 快速入门  
excerpt: ""  
category: 62ce2a159aafea009af30da7
slug: chapter-2-cn
---



<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## 集成步骤
SmileAPI 很容易上手！ 使用 SmileAPI 涉及简单的客户端和服务器端集成，下面分四个关键步骤进行概述：

1. **Link token:** 您的应用服务器向我们的 REST API 发送一个请求，以生成一个短暂的 "Link " token 。

2. **Wink Widget:** 使用 Link token ，您的应用程序客户端将初始化客户端 SDK 以启动 Smile Wink Widget 。您的终端用户将与 Wink Widget 互动以登陆他们的账号，以便通过安全和加密的连接向他们的就业数据提供商进行身份验证。

3. **连接到源数据:** 一旦进入 Wink Widget ，用户就可以链接他们的就业账号或上传他们就业数据的照片或扫描文件。这将被用作您的应用程序所请求的用户数据的来源。

4. **请求:** 我们的服务器执行您的应用程序的请求。我们从用户的就业数据提供商那里读取、转换和临时存储数据，以便将其发送到客户端应用程序。

<!--
5. **Webhooks (coming soon):** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API.
-->

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## 使用开发者控制台
要想开始只需注册[开发者控制台](https://portal.getsmileapi.com)。注册后，我们将要求验证您的电子邮件，然后您就可以登录了。

默认情况下，当您注册和登录时，您将处于 "Sandbox" 模式。您可以通过预约电话或发送电子邮件到 access@getsmileapi.com 并提交上线所需的信息来访问 “Production” 模式。

> 📘 注意事项
> 
> 要了解有关不同模式的更多信息，请查看下一节“了解 API”

在开发者控制台内，您将会看到以下内容。

1. **Wink Widget:** 使用它来预览 Wink Widget 的工作原理。 Wink Widget 的行为取决于您所处的模式。在 Sandbox 模式下，您可以使用页面上提供的测试帐户来模拟登录到不同数据提供商（例如 Gig 平台或工资系统）的过程。在 Production 模式下，您将能够实际链接到真实账户或上传实际文件。

2. **Users:** 在帐户链接过程中或用户上传文件后，查看在后端创建的用户以及从该用户捕获的数据。在本部分中，您还可以预览从 Smile 返回的数据,包括每个资源（例如就业和收入）的格式。

3. **Data Source:** 数据源部分是您可以找到所有数据提供商以及可以上传的文件类型的地方。数据提供商包括不同的类型，例如不同雇主的名称、Gig 平台、政府服务或人力资源和工资系统。另一方面，文件类型是用户可以上传的文件类型，例如工资单、税务文件和其他文件的副本。

4. **API Keys:** 注册后，您将获得一个 Sandbox API key 和一个 API secret 。API secret 必须保持安全，并且仅用于您的应用程序服务器和 Smile API 的服务器之间的交换。 根据要求，您还可以获得 Production API key 和 API secret ，以便在Production模式中使用 Smile API 。 这也将允许您将开发者控制台切换到 “Production” 模式以进行实时测试。

5. **Organizations:** 您可以在此处输入有关您的组织的详细信息。

6. **Team:** 您可以在此处邀请组织中的其他成员加入门户并共享公共租户或工作区。

7. **Documentation:** 这是您正在阅读的 API 文档的链接！

## 如何使用本参考文档

如要充分探索 Smile API，我们鼓励您通过在参考页面右侧输入 API Key 和 Secret来充分利用本参考文档。

[block:image]
{
"images": [
{
"image": [
"https://files.readme.io/b7d08d8-how-to-use-reference-sidebar.png",
null,
""
],
"align": "center"
}
]
}
[/block]

> 📘 注意
>
> 您可以登录 [Developer Portal](https://portal.getsmileapi.com/) ，在 **API Keys** 部分找到 API Key 和 Secret。注册后，您可以免费访问我们的 Sandbox mode 进行测试。如果您需要 Production mode 的访问权限，请 [联系我们](https://www.getsmileapi.com/contact-us) 。
>
>![](https://files.readme.io/70f1152-where-to-find-api-keys.png)
> 
> 您可以通过点击 API Key 和 Secret 旁边的复制图标，轻松将其复制到电脑剪贴板。
---
<!-- focus: false -->
![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)

## Quickstart 

为了在您自己的环境中实际测试 Smile API ，我们提供了示例代码来实例化 Wink Widget 或 SDK 。
> 📘 注意事项
> 
> 我们在[Github](https://github.com/SmileAPI)中提供了[ Quickstart 示例代码](https://github.com/SmileAPI/quickstart)，您可以根据自己的需求进行下载和修改。
>
>示例代码安装了一个运行在 Node.js 上的后端服务，该服务自动从我们的 API 检索 token，因此您可以在自己的本地机器上实例化 Wink Widget 。

>
示例实现由两部分组成：
* 在 ``/frontend`` 下，您将找到已经嵌入 Wink Javascript SDK 的 HTML 示例代码。
* 在 ``/node`` 下，您将找到服务器端的 Javascript 代码来获取 Token 。 您需要下载并运行 Node.js 才能运行代码。

**实施步骤**

以下步骤也包含在 Quickstart [仓库](https://github.com/SmileAPI/quickstart)中的 README.md 文档中。

1. **将 Quickstart 文件下载到您的计算机上。**

   > 📘 注意事项
   >
   > 如果您有 git，则可以克隆仓库或运行以下命令：
   > 
   > ```bash
   > git clone https://github.com/SmileAPI/quickstart
   > ```

2. **转到 Quickstart 的 ``/node`` 目录。**
 
3. **在该目录中创建一个名为``.env``的新文件，其内容如下：**
 
   ```bash
   # 您希望示例服务器监听的端口
   APP_PORT=<portnumber>
    
   # Smile Link API 密钥（您可以通过向 access@getsmileapi.com 请求访问来获取此密钥）
   API_KEY=<apikey>
   API_SECRET=<apisecret>
    
   # API Host (决定这将在Sandbox还是Production模式下运行)
   OPEN_API_HOST=<openapihost>
   ```

   您可以使用 Quickstart 仓库中包含的 ``.env.example`` 文件作为参考。

   > 🚧 注意事项
   > 
   > **.env 文件通常被您的系统隐藏。** 您可能需要在系统首选项中启用隐藏文件的显示以便能够看到它。
   >
   > 此外，在 Windows 机器上，Windows 不允许您直接从 Windows 资源管理器创建 ``.env`` 文件，因为它不允许文件名以 ``.`` 开头。 要解决此问题，您可以执行以下步骤：
   > 
   > 1. 打开记事本并写入文件的内容（见下文）。
   > 2. 转到记事本中的文件->另存为窗口。
   > 3. 在选择窗口中选择“所有文件”类型。
   > 4. 将文件另存为 ``.env``

   您可能需要确保您的计算机具有适当的权限才能创建文件。

   > 📘 注意事项
   >  
   > 在 Mac 或 Linux 机器上，您可以打开 Terminal 并以 Super User 身份输入以下命令：
   >
   > ```bash
   > sudo touch .env
   > ```

4. **保存并关闭您的文件。**
 
5. 如果您的计算机中没有安装 Node.js，**请安装 Node.js。**

   > 📘 注意事项
   >
   > **对于 Mac ,** 您可以打开 Terminal 并运行:
   > ```bash
   > curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
   > ```
   >
   > **对于 Windows ,** 您可以 [下载安装程序](https://nodejs.org/en/#home-downloadhead).
   >
   > **对于其他操作系统,** [您可以在 Node.js 网站上找到说明](https://nodejs.org/en/download/package-manager/#macos) from the Node.js website.

6. 使用 Node.js 附带的 [ npm 包管理器](https://www.npmjs.com/) 来**运行 Yarn**，然后输入以下命令：
   ```bash
   npm install --global yarn
   yarn install
   ```
   
   > 📘 注意事项
   >
   > 在 Mac 或 Linux 中，您需要打开 Terminal 。如果您使用的是 Windows ，则可以转到命令行。 确保您仍在您刚刚下载到计算机上的 Quickstart 文件的 ``/node`` 目录中。
   > 
   > 如果您没有足够的权限，您可能需要以 Super User 身份运行。 在 Mac 或 Linux 机器上，您可以使用 ``sudo`` 以 Super User 身份运行命令。 在 Windows 上，您可以使用管理员信任级别运行命令，或者右键单击 UI 中的程序并选择“以管理员身份运行”。

8. **运行服务器:**
   ```bash
   node index.js
   ```

   > 🚧 注意事项
   >
   > 如果您在运行 Node 服务器时遇到问题，您可能需要在环境中安装 dotenv 。 要安装 dotenv ，只需运行以下命令：
   > 
   > ```bash
   > npm install dotenv
   > ```
   > 
9. **打开浏览器并打开 Wink Widget 示例。** 例如，如果您在``.env``配置文件中指定端口 ``:8000``，请在 Web 浏览器中打开 http://127.0.0.1:8000。
 
10.使用提供的 [ Sandbox 帐户](/reference/chapter-4-cn) 来**测试 Wink Widget**。
 
> 👍 做得好！
>
> 坐下来，放松一下，您完成了一项出色的工作！