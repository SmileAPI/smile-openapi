---
title: Invites
excerpt: ""
category: 62ce2a159aafea009af30daa
slug: invites
---

无需手动访问 Smile Developer Portal，Invites API 就可以让您直接通过您的网站或应用程序来管理以及发送邀请给终端用户。这有利于为终端用户提供一个自动化的过程和体验。

该 API 还使用了预定义的 [Invite Templates](/reference/invite-templates)，您可以用它来定制发送给用户的邀请邮件的内容。

## 发送邀请

您需要以下信息来通过 API 发送邀请：

| 属性             | 类型     | 详情                                                                        |
|:---------------|:-------|:--------------------------------------------------------------------------|
| fullName       | string | 受邀人的全名（必填）                                                                |
| firstName      | string | 受邀人的名字                                                                    |
| lastName       | string | 受邀人的姓氏                                                                    |
| email          | string | 邀请应发送至的邮件地址（必填）                                                           |
| templateId     | string | 要使用的 Invite Template ID，通常格式为`tpl-123abc456def789abc123def456abc78`（必需）   |
| winkTemplateId | string | 要使用的 Wink Widget Template ID，通常格式为`wtpl-123abc456def789abc123def456abc78` |

您可以通过 [Invite Templates](/reference/invite-templates) API 来管理邮件邀请模板。

请参阅 [Create Invite](/reference/create-invite) 端点，了解更多关于通过 API 创建和发送邀请的信息。

## 补充数据方式

如果无法使用 Invite API 来创建自动发送给终端用户的邮件，您还可以通过访问 [Smile Developer Portal](https://portal.getsmileapi.com/) 的 Users 页面手动发送邀请。

## 邀请对象

| 属性             | 类型     | 详情                                                                     |
| :--------- | :----- |:-----------------------------------------------------------------------|
| id | string |                                                                        |
| createdAt | datetime | 邀请创建的日期和时间                                                             |
| fullName | string | 受邀人的全名（必填）                                                             |
| firstName | string | 受邀人的名字                                                                 |
| lastName | string | 受邀人的姓氏                                                                 |
| email | string | 邀请应发送到的邮件地址（必填）                                                        |
| templateId | string | 要使用的 Wink Template ID，通常格式为 `tpl-123abc456def789abc123def456abc78`（必填） |
| winkTemplateId | string | 要使用的 Wink Template ID，通常格式为 `wtpl-123abc456def789abc123def456abc78`    |
| userId | string | 邀请人唯一的用户 ID，当发送邀请时创建                                                   |
| status | string | 邀请的状态。可能的值：`INVITED`、`LINKED`                                          |
| updatedAt | datetime | 上次更新邀请的日期和时间                                                           |
| invitedAt | datetime | 邀请发送的日期和时间                                                             |
| linkedAt | datetime | 受邀用户连接帐户的日期和时间                                                         |
| inviteLandingPageUrl | string | 供受邀用户连接其账户登陆页面的唯一 URL                                                  |

## 邀请数据样例

```
{
    "id": "iv-123abc456def789abc123def456abc78",
    "createdAt": "2023-02-02T02:35:01Z",
    "fullName": "George Palomero Jr",
    "firstName": "George",
    "lastName": "Palomero",
    "email": "gpalomero123@email.com",
    "templateId": "tpl-123abc456def789abc123def456abc78",
    "winkTemplateId": "wtpl-123abc456def789abc123def456abc78",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "status": "INVITED",
    "updatedAt": "2023-02-02T02:35:01Z",
    "invitedAt": "2023-02-02T02:35:01Z",
    "linkedAt": null
}
```

## 端点

| 端点                                       | |
|:-----------------------------------------| :---- |
| [获取 Invite 列表](/reference/list-invites)  | `GET /invites` |
| [创建并发送 Invite](/reference/create-invite) | `POST /invites` |
| [获取一条 Invite 记录](/reference/get-invite)  | `GET /invites/{id}` |

## Webhooks

### `INVITE_INVITED`

邀请成功发送给用户时，事件发送格式如下：

```
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_INVITED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```

### `INVITE_LINKED`

当受邀用户成功连接他们的工作账户时，事件发送格式如下：

```
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_LINKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```
