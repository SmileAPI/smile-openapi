---
title: 简介  
excerpt: ""  
category: 62ce2a159aafea009af30da7 
slug: chapter-1-cn
---

# 简介

<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)


##  关于 Smile
您好，欢迎来到 Smile !

Smile 通过简单的 API 提供跨平台的就业和雇佣数据。银行、金融科技公司、招聘机构和其他服务提供商可以利用就业和收入数据，通过简单的API来提高采用率和转化率、降低成本和风险。

对数据的访问权限由用户自己提供，这也是我们提供的 API 的一部分。通过我们提供的授权机制，您的用户可以允许 Smile 将这些个人数据收集起来，并将其以简单、安全和无缝的方式传输给您或他们信任的任何一方。 

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)
 

##  我们的 API
Smile API 建立在 RESTful 原则之上。所有请求和响应的内容都以 JSON 格式编码。 出于安全考虑，所有请求都必须通过 HTTPS 发送。 要访问 API，您需要[注册我们的开发者控制台](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link)。

<!-- focus: false -->
![Jobs](https://img.icons8.com/ios-filled/50/000000/find-matching-job.png)

## 现有资源
Smile API 中的现有资源由两种类型组成。
- Smile Network Resources - Smile 资源数据
- User Data - 用户数据

### Smile Network
这些是用于与 Smile API 集成和获取数据的数据资源。 他们包括：

| 资源 | 类型    | 详情 |
|----------|---------|-------------|
| Providers | Smile Network | Smile Network 中可用的就业数据提供商列表。数据提供商进一步细分为不同的子类型，如 Gig 平台、人力资源平台和其他。 |
| Users | Smile Network | 这些是您的用户，他们已经启动了账户链接程序，并同意与您和 Smile 分享他们的就业数据。当一个新的用户被创建时，一个 token 也同时被发出。 |
| Tokens | Smile Network |通过使用 token 来访问用户账户的相关数据。您可以使用这个资源来检索现有的 token ，或为现有用户刷新一个 token 。 |
| Accounts | Smile Network |您的用户已经成功登录的账户，以及与账户相关的数据将被检索出来。更多信息请参见下面的 "源数据"。 |
| Archives | Smile Network | 这是指包含用户上传的扫描或拍照文件。 |
| File Types | Smile Network | 这是指接受上传的文件类型，上传后可作为存档使用。 | 
| Invites | Smile Network | 您可以使用它来邀请用户通过他们首选的通信渠道（例如电子邮件）链接他们的工作帐户。 |
| Invite Templates | Smile Network |如果您将邀请用户通过 Invite 链接他们的工作帐户，请使用它来定义和检索 Invite 的外观。  |
| Webhooks | Smile Network | Webhook 用于在您的环境中发生事件时实时通知您的应用程序。  |



### User Data
User Data 可以来自关联的帐户，也可以来自上传的数据。为了能够检索就业和收入数据并将其用于您的应用程序，您需要使用我们的用户邀请功能或使用我们的客户端 SDK 并将我们的 Wink Widget 嵌入到您的应用程序中。
> 📘 注意事项
> 
> 要了解有关 Wink Widget 的更多信息，请查看 **"获取用户数据"部分** 

如果您想将客户端 SDK 嵌入到您自己的应用程序中，您将需要实例化 Wink Widget ，之后将在 Smile Network 中创建一个用户，并得到一个短期 token 。当 Wink Widget 被实例化时，首先需要您的用户同意 Smile 代表他们检索该数据。之后，我们将为用户显示可以选择的就业和收入数据提供商列表。然后，他们将需要：

1. **通过数字化数据提供商进行身份验证。** 如果我们与该数据提供商有直接链接，我们会将其显示在用户可以从中选择的列表中。如果他们有任何显示的提供商的帐号，他们可以选择该提供商，然后登陆他们的账号。授予权限后，将会在 Smile Network 中创建一个帐户，从中检索、汇总数据并将其规范化为标准形式，并以对开发人员友好的 JSON 格式发送给您。
2. **上传包含其就业或收入信息的扫描或照片文件。** 并非所有来源的就业和收入信息都是数字形式。通常，此类信息仍以纸质文件的形式出现。用户可以扫描或拍摄这些文档，上传，然后我们可以数字化并从中检索相关数据，在大多数情况下，还可以将数据（通过光学字符识别即 OCR）提取为开发人员友好的 JSON 格式。如果我们无法自动提取信息，我们将始终通过 /archives API 提供上传文件的 URL 。


| 资源 | 类型    | 详情                                                                                                                 |
|----------|---------|--------------------------------------------------------------------------------------------------------------------|
| Identity | User Data | 从现任和前任雇主那里获得经过审核的身份信息，如姓名、联系信息、居住地址等。                                                                              |
| Transactions |User Data | 从源数据提供商那里获得用户的详细交易数据。这包括在源提供商那里记录的增加项（或信贷）和扣除项（或借贷）。                                                               |
| Ratings | User Data | 获取用户的工作业绩评级信息。                                                                                                     |  
| Documents | User Data | 获取文件信息，如他们的驾驶执照、国民身份证，以及其他。                                                                                        |  
| Employments | User Data | 获得以前的就业信息，如用户曾工作过的公司、工作职位、任期和其他。                                                                                   |  
| Incomes | User Data | 获得以前的收入信息，如毛收入和净收入，以及构成收入的其他部分。<br> 来自 Contributions 和 Transactions 的 **Estimated Income** *（抢先试用版）* 数据也可在期限内免费获得。 |  
| Contributions | User Data | 获取以前的社会保障缴款信息，以了解收入水平。                                                                                             |  
| Liabilities | User Data | 获取从与就业相关的数据源和社会保障服务得到的当前和以前的贷款信息。                                                                                  |  

<!--
| Assets | Source Data | Get information on assets owned or used for their employment such as motor vehicles, motorcycles and others.|  
| Schools | Source Data | Get previous educational history such as school, degree, years attended and so on.|  
-->