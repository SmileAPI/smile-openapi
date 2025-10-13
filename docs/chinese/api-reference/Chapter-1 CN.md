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

Smile 通过单一的 API 提供跨平台、跨雇主和跨文档的身份、收入和就业数据。银行、金融科技公司、招聘机构以及其他服务提供商可以利用就业与收入数据来提升用户采用与转化、降低成本并降低风险，而这一切都可通过单一的 API 实现。

数据访问由用户本人授权，这是我们所提供 API 的一部分。我们提供了一种机制，您的用户可以通过该机制同意收集其个人数据，并将其安全地传输给您或其信任的任何第三方。整个过程简单、安全且无缝。

根据您可用的输入与预期的输出，**Smile API 的产品可以帮助您更好地了解您的客户（KYC）。**

![Smile API 产品线](https://files.readme.io/a7db7799e61dadb3822eb2dab65dd38480ea0d26625aa48f6200a6c72b111ca7-smile-api-inputs-outputs.png)

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)

## 我们的 API
Smile API 基于 RESTful 原则构建。所有请求与响应载荷均采用 JSON 格式。出于安全考虑，所有请求必须通过 HTTPS 发送。要获取 API 访问权限，您需要先[注册我们的开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)。

要进一步了解我们的 API，请参阅[第 2 章《了解 API》](/reference/chapter-2-cn?utm_source=docs&utm_medium=internal_link)。

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## 使用开发者控制台
要开始使用，只需在[开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)上注册。注册后，系统会提示您验证邮箱，通过验证后即可登录。

默认情况下，注册并登录后，您将处于“Sandbox（沙盒）”模式，返回的仅为测试数据。您可以通过预约电话或[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)，并提交上线所需信息以获取“Production（生产）”模式的访问权限。

> 📘 注意
>
> 想了解不同模式的详细信息，请查看下一节 **“了解 API”**。

在开发者控制台中，您将看到以下内容：

1. **[账户使用情况](https://portal.getsmileapi.com/usage?utm_source=docs&utm_medium=internal_link)：** 查看账户使用情况，例如组织内已连接的账户数与用户数。
2. **[Wink Widget](https://portal.getsmileapi.com/link/emulator?utm_source=docs&utm_medium=internal_link)：** 包含使用 Smile 账户连接 SDK（Wink Widget）所需的一切。**Emulator（模拟器）** 允许您体验 Wink Widget 的工作方式。在 Sandbox 模式下，您可以使用页面提供的测试账号来模拟登录不同的数据提供方（如零工平台或薪资系统）。在 Production 模式下，您可以实际连接真实账号或上传真实文件。您还可以在该部分管理您的 [Wink 模板](https://portal.getsmileapi.com/link/template?utm_source=docs&utm_medium=internal_link)与 [Wink 站点](https://portal.getsmileapi.com/link/winkSite?utm_source=docs&utm_medium=internal_link)。

    ![devportal-emulator.png](https://files.readme.io/ded43f52b13308bb62cce9ee74fa8345855371e8ec3789c51ecb258276c8af0a-devportal-emulator.png)

3. **[Snap 文档](https://portal.getsmileapi.com/snap?utm_source=docs&utm_medium=internal_link)：** 您可以在此试用或使用 Smile Snap，Sandbox 模式可上传示例文件，Production 模式可上传真实文件。每个文件的处理状态与输出都可在该页面直接查看。
4. **[Signal 请求](https://portal.getsmileapi.com/signal/signals?utm_source=docs&utm_medium=internal_link)：** 在此可测试多种 Smile Signals 服务，例如 [Signals](https://portal.getsmileapi.com/signal/signals?utm_source=docs&utm_medium=internal_link)、[Verifications](https://portal.getsmileapi.com/signal/verification?utm_source=docs&utm_medium=internal_link)、[Blacklists](https://portal.getsmileapi.com/signal/blacklists?utm_source=docs&utm_medium=internal_link)、[Digital Footprint](https://portal.getsmileapi.com/signal/footprints?utm_source=docs&utm_medium=internal_link) 与 [Multiple Application Warning](https://portal.getsmileapi.com/signal/maws?utm_source=docs&utm_medium=internal_link)。
5. **[用户数据](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link)：** 查看后端创建的用户以及在账户连接或文件上传过程中采集到的数据。您还可以预览 Smile 返回的各资源（如就业与收入）的数据结构与示例。
6. **[集成](https://portal.getsmileapi.com/developer/providers?utm_source=docs&utm_medium=internal_link)：** 包含帮助您接入 Smile Network 的各类工具：了解不同的[数据源](https://portal.getsmileapi.com/providers?utm_source=docs&utm_medium=internal_link)、生成与管理[API Keys](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link) 与 [Webhooks](https://portal.getsmileapi.com/webhooks?utm_source=docs&utm_medium=internal_link)，以及配置[授权（Consent）模板](https://portal.getsmileapi.com/developer/consent-templates?utm_source=docs&utm_medium=internal_link)。

在页面右上方的顶栏导航中，您还可以管理[组织与账户设置](https://portal.getsmileapi.com/account/organization?utm_source=docs&utm_medium=internal_link)、[服务状态与可用性](https://status.getsmileapi.com/?utm_source=docs&utm_medium=internal_link)，以及当前正在阅读的 API 文档。

## 使用本参考文档
为了完整体验 Smile API，我们建议您在参考文档页面右侧输入您的 API Key 与 Secret，以充分利用本参考站点的交互功能。

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
> 您可以登录[开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)，在[**API Keys** 部分](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link)找到您的 API Key 与 Secret。注册后，您将立即免费获得 Sandbox 环境的测试权限；如需 Production 环境访问，请[联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link)。
>
>![](https://files.readme.io/8032442ec83f0f739d2025e2016ca00296c110088fc1d1dce2b2e1af2e7ba09e-image.png)
>
> 您可点击 API Key 与 API Secret 旁的复制图标，快速复制到剪贴板。

---
<!-- focus: false -->
![API](https://img.icons8.com/ios/50/000000/api-settings.png)

## 额外资源
我们在下方提供一些**开源**资源，帮助您立即开始使用 Smile API！

### API 规范

> 📘 注意
>
> 您可以在 [Github](https://github.com/SmileAPI) 上下载 Smile API 的[规范](https://github.com/SmileAPI/smile-openapi/blob/main/openapi-v1.yaml)副本。如果您安装了 git，您可以克隆该仓库或运行以下命令：

``` bash
git clone https://github.com/SmileAPI/smile-openapi
```

规范文档为 **YAML 格式**，遵循 [OpenAPI Specification 3.0.0](https://swagger.io/specification/)。您也可在 /docs 子目录下下载本开发者文档的 **Markdown** 离线副本。

### Postman 集合

> 📘 注意
>
> 在 [Github](https://github.com/SmileAPI) 上下载 Smile API 的 [Postman 集合](https://github.com/SmileAPI/smile-openapi/blob/main/postman-collection-v1.json)。如果您安装了 git，您可以克隆该仓库或运行以下命令：

``` bash
git clone https://github.com/SmileAPI/smile-openapi
```

您可以下载 **JSON 格式** 的 Postman 集合并导入 Postman，轻松开始审阅与测试我们的 API。

#### 使用 Postman 集合

1. 从我们的 [Github 仓库](https://github.com/SmileAPI/smile-openapi) 下载 “postman-collection-(v#).json” 文档。
2. 如果您还没有这样做，请访问 [Postman](https://www.postman.com/) 并创建一个账户，或下载他们的免费桌面客户端。
3. 打开 Postman 并选择一个工作区。
4. 导入 Postman 集合。
5. 确保您能通过输入 API Key 与 API Secret 完成认证。
6. 就是这样！您现在可以开始测试 Smile 的 API 了！