---
title: Invite Templates
excerpt: ""
category: 66700efb7d3c7b005b21f71a
slug: invite-templates
---


您可以使用它向终端用户发送邀请以连接他们的工作账户。这些 API 可以在您的平台自动化您的用户流，而不需要访问 Smile Developer Portal 来手动操作。

一旦您为您的组织设置了一个 Invite Template，您就可以在使用 [Invites API](/reference/invites) 来向终端用户发送邮件时引用创建的 Invite Template。

## 创建 Invite Templates

使用 [Create Invite Template](/reference/create-invite-template) 端点来创建一个新模板。每个 Invite Template 包含三个部分：

1. *Email Message* - 这是发送给收件人的邮件，邀请他们连接他们的工作账户。其中包含一个登陆页面的链接，可以让他们开启账户连接过程。
2. *Landing Page* - 这是一个登陆页面，被邀请者可以在此开启账户连接过程。
3. *Success Page* - 该页面出现在被邀请者完成他们的账户连接之后。

您可以定制 Invite Template 的每个部分。

您可以发送以下信息：

| 属性          | 类型     | 详情                                  |
|:------------|:-------|:------------------------------------|
| name        | string | 模板的名称。该名称不会显示给收件人（必需）               |
| company     | object | 组织信息，如名称和标志，用来定制您的邀请邮件。详情见下文        |
| email       | object | 邮件信息，如发件人姓名等，用来定制您的邀请邮件。详情见下文       |
| landingPage | object | 登陆页面信息，如标题文本等，用来定制您的邀请邮件的登陆页面。详情见下文 |
| successPage | object | 成功页面信息，如标题文本等，用来定制您的邀请邮件的成功页面。详情见下文 |

*有些数值尚未应用于 Invite Template。*

### 公司信息

| 属性          | 类型     | 详情                                               |
| :--------- | :----- |:-------------------------------------------------|
| name | string | 将出现在邀请邮件和登陆页面上的组织名称。用于将`${companyName}`填入模板（必需）。 |
| logoUrl | string | 将显示在邀请邮件和登陆页面上的 logo 的完全合格URL。*暂不可用*。            |

### 邮件信息

![invite-template-email-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-email-sample20230321.png)

| 属性          | 类型     | 详情                                       |
| :--------- | :----- |:-----------------------------------------|
| sendEmail | boolean | 允许使用此模板发送邀请邮件（必需）。*必须为 true - 短信邀请暂不可用*。 |
| senderName | string | 应用于邀请邮件的发件人名称，即您的组织名称（必需）。               |
| replyAddress | string | 如果您的终端用户回复了邮件，将应用于邀请邮件的回复地址（必需）。         |
| subject | string | 邀请邮件的主题。您可以使用模板代码（见下文）来填充邮件的主题（必需）。      |
| body | string | 信息的正文。您可以使用模板代码（见下文）来填充正文，不允许使用HTML（必需）。 |

支持的模板代码如下：

- `${companyName}` - 您在邮件模板中提供的公司名称
- `${firstName}` - 您的受邀人名字（如果有的话），否则，将使用全名

### 登陆页面信息

![invite-template-landing-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-landing-sample20230321.png)

| 属性          | 类型     | 详情                                      |
| :--------- | :----- |:----------------------------------------|
| header | string | 登陆页面的标题文本。您可以使用模板代码（见下文）来填充页面标题（必需）。    |
| description | string | 登陆页面的主要/描述文本。您可以使用模板代码（见下文）来填充主体文本（必需）。 |
| button | string | 启动 Wink Widget /开启账户连接过程的按钮上的文本（必需）。    |

支持的模板代码如下：

- `${companyName}` - 您在邮件模板中提供的公司名称
- `${firstName}` - 您的受邀人名字（如果有的话），否则，将使用全名。

### 成功页面信息

![invite-template-success-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-success-sample20230321.png)

| 属性          | 类型     | 详情                                         |
| :--------- | :----- |:-------------------------------------------|
| header | string | 成功页面的标题文本。您可以使用模板代码（见下文）来填充成功页面的标题（必需）。    |
| description | string | 成功页面的主要/描述文本。您可以使用模板代码（见下文）来填充成功页面的正文（必需）。 |
| button | string | 结束账户连接过程的按钮上的文本（必需）。                       |

支持的模板代码如下：

- `${companyName}` - 您在邮件模板中提供的公司名称
- `${firstName}` - 您的受邀人名字（如果有的话），否则，将使用全名。

## 补充数据方法

如果您不能使用 Invites API 来创建自动发送给终端用户的邮件，您也可以通过访问 [Smile Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) 来手动发送邀请给部分用户。请注意，您必须在 Production Mode 下才能使用此功能。

## 邀请模板对象

您可以检索到现有的邀请模板。

| 属性          | 类型     | 详情                                                                                                                |
| :--------- | :----- |:------------------------------------------------------------------------------------------------------------------|
| id | string | Smile Network 上 Invite Template 的唯一 ID                                                                            |
| name | string | 模板的名称                                                                                                             |
| company | object | 组织信息，如名称和 logo，用来定制 Invite Template。详见下文                                                                          |
| email | object | 邮件信息，如发件人姓名等，用来定制 Invite Template。详见下文                                                                            |
| landingPage | object | 登陆页面信息，如标题文本等，用来定制 Invite Template 的登陆页面。详见下文                                                                                                                  |
| successPage | object | 成功页面信息，如标题文本等，用来 Invite Template 的成功页面。详见下文 |

### 公司对象

| 属性          | 类型     | 详情                                                                                                                |
| :--------- | :----- | :------- |
| name | string | 组织名称，将出现在邀请邮件和登陆页面中。用于将`${companyName}`填充到模板中。 |
| logoUrl | string | 在邀请邮件和登陆页面中显示的 logo 完全合格 URL。*暂不可用。* |

### 邮件对象

| 属性          | 类型     | 详情                        |
| :--------- | :----- |:--------------------------|
| sendEmail | boolean | 允许使用此模板发送邀请邮件。*短信邀请暂不可用*。 |
| senderName | string | 应用于邀请邮件的发件人姓名，即您的组织名称。    |
| replyAddress | string | 应用于邀请邮件的回复地址              |
| subject | string | 邀请邮件的主题                   |
| body | string | 信息的正文                     |

### 登陆页面对象

| 属性          | 类型     | 详情                        |
| :--------- | :----- | :------- |
| header | string | 登陆页面的标题文本 |
| description | string | 登陆页面的主要/描述文本 |
| button | string | 启动 Wink Widget /开启账户连接过程的按钮上的文本 |

### 成功页面对象

| 属性          | 类型     | 详情                        |
| :--------- | :----- | :------- |
| header | string | 成功页面的标题文本 |
| description | string | 成功页面的主要/描述文本 |
| button | string | 结束账户连接过程的按钮上的文本 |


## Invite Template 数据样例

```
{
    "id": "tpl-123abc456def789abc123def456abc78",
    "name": "Email Template v1",
    "company": {
        "name": "ABC Corporation",
        "logoUrl": "https://xyzbank.co/logo.png"
    },
    "email": {
        "sendEmail": true,
        "senderName": "ABC Corporation",
        "replyAddress": "loans@abccorporation.com",
        "subject": "Please connect your work account to verify your previous employment",
        "body": "Hello ${firstName}! We are working with our partner, Smile API, so you can easily share your employment and income data to us as a requirement for employment. It will be a quick process and should take no more than a few seconds of your time."
    },
    "landingPage": {
        "header": "Please connect your work account to verify your previous employment at ${companyName}",
        "description": "We are working with our partner, Smile API, so you can easily share your employment and income data to us as a requirement for giving you service. It will be a quick process and should take no more than a few seconds of your time.",
        "button": "START SHARING NOW"
    },
    "successPage": {
        "header": "The process was successful! Please wait for us to get in touch!",
        "description": "Thank you for sharing your employment and income data with us at ${companyName}.",
        "button": "Connect another account"
    }
}
```

## 端点

| 端点                                                        | |
|:----------------------------------------------------------| :---- |
| [获取 Invite Template 列表](/reference/list-invite-templates) | `GET /inviteTemplates` |
| [创建 Invite Template](/reference/create-invite-template)   | `POST /inviteTemplates` |
| [获取一条 Invite Template 记录](/reference/get-invite-template) | `GET /inviteTemplates/{id}` |
| [更新 Invite Template](/reference/get-invite)               | `PUT /inviteTemplates/{id}` |
| [删除 Invite Template](/reference/get-invite)               | `DELETE /inviteTemplates/{id}` |

## Webhooks

没有可用于 Invite Template 管理的 Webhooks。
