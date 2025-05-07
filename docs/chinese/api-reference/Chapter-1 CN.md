---
title: 快速入门  
excerpt: ""  
category: 62ce2a159aafea009af30da7 
slug: chapter-1-cn
---

<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)

## 关于 Smile
您好，欢迎来到 Smile！

Smile 通过单一的 API 提供跨平台、跨雇主和跨文档的身份、收入和就业数据。银行、金融科技公司、招聘机构和其他服务提供商可以通过单一的 API 获取并分析就业和收入数据来提高采用率和转化率、降低成本和风险。

数据访问权限由用户自己提供，这是我们所提供 API 的一部分。我们提供了一种机制，通过该机制，您的用户可以同意将其个人数据收集起来，并代表他们将其传输给您或他们信任的任何一方。所有这些操作都以简单、安全和无缝的方式完成。

根据您可用的输入和预期的输出，**Smile API 的产品可以帮助您更好地了解您的客户。**

![Smile API 产品线](https://files.readme.io/a7db7799e61dadb3822eb2dab65dd38480ea0d26625aa48f6200a6c72b111ca7-smile-api-inputs-outputs.png)

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)

## 我们的 API
Smile API 基于 RESTFUL 原则构建。所有请求和响应的有效负载均采用 JSON 格式编码。出于安全考虑，所有请求必须通过 HTTPS 发送。要访问该 API，您需要[注册我们的开发者门户](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)。

要了解更多关于我们 API 的信息，请参阅[第 2 章，了解 API](/reference/chapter-2-cn?utm_source=docs&utm_medium=internal_link)。

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## 使用开发者控制台
要开始使用，只需在[开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)上注册。注册后，您将被要求验证您的电子邮件，验证通过后即可登录。

默认情况下，当您注册并登录时，您将处于“SANDBOX”模式，该模式仅返回测试数据。您可以通过预约电话或[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)，并提交上线所需的必要信息来访问“PRODUCTION”模式。

> 📘 注意
>
> 要了解更多关于不同模式的信息，请查看下一节**“了解 API”**

在开发者控制台内，您将看到以下内容：

1. **[账户使用情况](https://portal.getsmileapi.com/usage?utm_source=docs&utm_medium=internal_link)：** 您可以在此查看您的账户使用情况，例如您的租户中已连接的账户和用户数量。
2. **[Wink Widget](https://portal.getsmileapi.com/link/emulator?utm_source=docs&utm_medium=internal_link)：** 使用此功能可预览 Wink Widget的工作方式。Widget的行为会根据您所处的模式而变化。在SANDBOX模式下，您可以使用页面上提供的测试账户来模拟登录不同数据提供商（如零工平台或工资系统）的过程。在PRODUCTION模式下，您将能够实际连接一个真实账户或上传一份实际文件。
3. **Snap 查询：** 您可以在这里测试各种 Smile Snap 服务，如[验证](https://portal.getsmileapi.com/snap/verification?utm_source=docs&utm_medium=internal_link)、[智能文档处理](https://portal.getsmileapi.com/snap/scanned?utm_source=docs&utm_medium=internal_link)和[信号](https://portal.getsmileapi.com/snap/signals?utm_source=docs&utm_medium=internal_link)。
4. **[用户数据](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link)：** 在账户连接过程中或用户上传文件后，查看在后台创建的用户以及从该用户获取的数据。在此部分中，您还可以预览从 Smile 返回的每个资源（如就业和收入）的数据。
5. **[数据源](https://portal.getsmileapi.com/providers?utm_source=docs&utm_medium=internal_link)：** 在数据源部分，您可以找到所有的数据提供商以及可上传的文件类型。数据提供商包括不同类型，如不同雇主的名称、零工平台、政府服务或人力资源和工资系统。而文件类型则是用户可以上传的文件，如工资单副本、税务文件等。
6. **[API Key](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link)：** 注册后，您将获得一个SANDBOX API 密钥对。API 密钥对必须妥善保管，并且只能在您的应用程序服务器和 Smile API 服务器之间的交换中使用。根据您的请求，您还可以获得在生产环境中使用 Smile API 的 API 密钥对。这也将允许您将开发者控制台切换到“PRODUCTION”模式进行实时测试。
7. **[Webhook](https://portal.getsmileapi.com/webhooks?utm_source=docs&utm_medium=internal_link)：** 您可以在此创建和管理 Webhook 以与您的应用程序进行通信。
8. **[设置](https://portal.getsmileapi.com/account/organization?utm_source=docs&utm_medium=internal_link)：** 您可以在这里输入有关您的组织和团队的详细信息。您还可以邀请组织中的其他成员加入控制台，共享一个共同的租户或工作区。
9. **文档：** 这是您正在阅读的 API 文档的链接！

## 使用本参考文档
要充分探索 Smile API，我们鼓励您在参考页面的右侧输入您的 API 密钥对，以充分利用本参考网站。

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
> 您可以通过登录[开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)，在[**API Key**部分](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link)找到您的 API 密钥和密钥秘密。注册后，您将可以立即免费在我们的SANDBOX环境中进行测试。如果您需要访问生产环境，请[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)。
>
>![](https://files.readme.io/70f1152-where-to-find-api-keys.png)
>
> 您可以点击您的 API Key和API Secret旁边的复制图标，轻松将其复制到您的计算机剪贴板。

---
<!-- focus: false -->
![API](https://img.icons8.com/ios/50/000000/api-settings.png)

## 额外资源
我们在下面提供了一些**开源**资源，帮助您立即开始使用 Smile API！

### API 规范

> 📘 注意
>
> 您可以在 [Github](https://github.com/SmileAPI) 上下载 Smile API 的[规范](https://github.com/SmileAPI/smile-openapi/blob/main/openapi-v1.yaml)副本。如果您安装了 git，您可以克隆该仓库或运行以下命令：

```bash
git clone https://github.com/SmileAPI/smile-openapi
```

规范文档采用 **YAML 格式**，遵循 [Open API Specification version 3.0.0](https://swagger.io/specification/)。您还可以在 /docs 子目录下以 **markdown 格式** 下载我们的开发者文档的离线副本。

### Postman 集合

> 📘 注意
>
> 在 [Github](https://github.com/SmileAPI) 上下载 Smile API 的 [Postman 集合](https://github.com/SmileAPI/smile-openapi/blob/main/postman-collection-v1.json)。如果您安装了 git，您可以克隆该仓库或运行以下命令：

```bash
git clone https://github.com/SmileAPI/smile-openapi
```

您可以通过以 **JSON 格式** 下载我们的 Postman 集合并将其导入 Postman 来轻松开始审查和测试我们的 API。

#### 使用 Postman 集合

1. 从我们的 [Github 仓库](https://github.com/SmileAPI/smile-openapi) 下载 “postman-collection-(v#).json” 文档。
2. 如果您还没有这样做，请访问 [Postman](https://www.postman.com/) 并创建一个账户，或下载他们的免费桌面客户端。
3. 打开 Postman 并选择一个工作区。
4. 导入 Postman 集合。
5. 确保您能够通过输入您的 API Key和 API Secret进行身份验证。
6. 就是这样！您现在可以开始测试 Smile 的 API 了！