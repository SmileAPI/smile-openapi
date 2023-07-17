---
title: Accounts
excerpt: ""
category: 62ce2a159aafea009af30daa
slug: accounts
---

Smile Network 中的账户数据是客户与终端用户共享数据的基本信息。每个用户可以在 Smile 支持的[ Providers ]( /reference/providers )中连接多个账户，这样可以更清楚地了解他们的历史信息。

在得到来自最终用户的同意和直接访问权限后，Smile 从账户中检索可用数据，并在该特定时间点提供每个数据端点下的规范化数据。如果您的账户启用了 *Continuous Data Sync* ，Smile 也会定期检查提供商更新的数据，并在账户连接期间（即没有被用户撤销）持续更新您的用户信息。

每个提供商支持的可用数据端点可能有所不同，您可以使用 [the Data Sources section of the Developer Portal](https://developer-portal.smileapi.io/providers) 实时检查。您也可以使用 [Webhook event notifications](/reference/chapter-5) 跟踪数据的可用性。

默认情况下，List Accounts API 将返回您的 `tenantId` 下所有符合查询参数的账户。请确保通过`userId`、`startDate`或`endDate`来过滤结果，以缩小查询范围。

当用户通过 SDK，或客户通过启动 [Revoke Account API](/reference/delete-account) 撤销了连接的账户时，用户的数据将被删除，不能再被访问。

## 持续数据同步

当这些用户同意并通过 Wink Widget 连接了他们的账户后，Smile API 的 *Continuous Data Sync*（CDS）功能可以持续更新用户已连接账户的数据。

如果您需要更新后的信息，CDS 可以在后台向您持续提供最新数据，而不需要用户重新连接他们的账户。通过同意 CDS，用户可以授权 Smile 在多个月内为您同步数据，直到他们撤销对其账户的访问。

当一个账户被更新时，我们会触发一个 webhook 事件`ACCOUNT_SYNC_TASK_FINISHED`（见下文），所以您可以收到关于更新的信息。

您的企业必须启用 CDS 才能享受这些功能，但启用后，并不需要改变您与 Smile API 的整合。

### 支持的提供商和数据端点

| 提供商                  | 可用数据端点| 更新频率                                |
|:---------------------| :----- |:------------------------------------|
| My.SSS               | Identities, Employments, Documents, Contributions, Liabilities, Estimated Incomes* | 每月一次，在首次连接当日                        |
| eGSIS MO             | Identities, Employments, Documents, Incomes, Estimated Incomes* | 每月一次，在首次连接当日 |
| My PhilHealth Portal | Identities, Employments, Documents, Contributions, Estimated Incomes* | 每月一次，在首次连接当日 |
| Virtual Pag-IBIG     | Identities, Employments, Documents, Contributions, Liabilities, Estimated Incomes* | 每月一次，在首次连接当日 |

## 帐户对象

| 属性         | 类型          | 详情                                          |
|:-----------|:------------|:--------------------------------------------|
| id         | string-time | Smile Network 上账户的唯一 ID                     |
| createdAt  | date-time   | 创建账户的时间                                     |
| providerId | string      | 用户账户所连接的数据提供商 ID                            |
| userId     | string      | Smile Network 上用户的 ID                       |
| connectionStatus | string | 账户连接状态，请参见下文*账户状态*部分                        |
| connection | object      | 包含账户连接信息的对象                                 |
| monitorStatus | string | 账户的监控/同步状态，参见下面的*账户状态*部分。 |
| monitor | object | 包含账户监控信息的对象 |

## 账户状态

### 连接状态

| 事件           | 详情                                     |
|--------------|----------------------------------------|
| PENDING      | 帐户已创建，正在等待成功验证                         |
| AWAITING_MFA | 用户成功通过身份验证，数据提供商正在等待用户在双因素身份验证场景中输入验证码 |
| ERROR        | 数据提供商返回错误。可能是用户输入了错误的凭据，或数据提供商出现了问题    |
| CONNECTED    | 用户能够成功通过就业数据提供商的身份验证                   |
| DISCONNECTED | 用户断开了与就业数据提供商的链接                       |

### 监控状态

| 事件                   | 详情                                              |
|----------------------|-------------------------------------------------|
| UNSUPPORTED          | 账户未启用数据同步功能                                     |
| ACTIVE               | 账户已启用数据同步功能，并且当前处于激活状态                          |
| USER_ACTION_REQUIRED | 账户已启用数据同步功能，但用户需要重新授权访问。这可能是由于密码更改或其他原因导致账户更新失败 |
| CUSTOMER_DISABLED    | 账户同步功能已被禁用                                      |

## 账户数据样例

``` json
{
    "id": "a-123abc456def789abc123def456abc78",
    "createdAt": "2022-10-01T00:00:00Z",
    "providerId": "abccorp",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "connectionStatus": "CONNECTED",
    "connection": {
        "status": "CONNECTED",
        "errorCode": null,
        "errorMessage": null,
        "updatedAt": "2022-10-01T00:00:00Z"
    },
    "monitorStatus": "UNSUPPORTED",
    "monitor": {
        "status" : "UNSUPPORTED",
        "updatedAt" : null
    }
}
```

## 端点

| 端点                                             | |
|:-----------------------------------------------| :---- |
| [获取账户列表](/reference/list-accounts-1)           | `GET /accounts` |
| [获取一条账户记录](/reference/get-account-1)           | `GET /accounts/{id}` |
| [撤销账户访问权](/reference/delete-account)           | `DELETE /accounts` |
| [关闭账户监控功能](/reference/disable-account-monitor) | `POST /accounts/{id}/disableMonitor` |

## Webhooks

### `ACCOUNT_CREATED`

当用户启动账户链接过程时，就会发布此事件。即使对于不需要登录的提供商，也会启动这个 webhook。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_CREATED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `ACCOUNT_CONNECTED`

当用户成功地将一个账户连接到 Smile Network 时，就会发布此事件。只有在数据提供商需要登录时才会触发。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_CONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "loginName": "userLoginName"
    "providers": [
      "abccorp"
    ]
  }
}
```

### `ACCOUNT_DISCONNECTED`

当用户成功断开或撤销他们在 Smile Network 中账户的连接，就会发布此事件。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_DISCONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78"
    "providers": [
      "abccorp"
    ]
  }
}
```

### `ACCOUNT_FAILED`

当用户发起的账户连接过程失败，就会发布此事件。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "loginName": "userLoginName",
    "errorCode": "500",
    "errorMessage": "Error message",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `ACCOUNT_SYNC_TASK_FINISHED`

当账户同步任务在后台完成时，就会发布此事件。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_SYNC_TASK_FINISHED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ],
    "status": "SUCCEEDED",
    "monitorStatus": "ACTIVE",
    "dataPoints": [
      "IDENTITIES",
      "EMPLOYMENTS",
      "INCOMES"
    ]
  }
}
```

## 事件监听器

SDK 还可以发出特定的事件，该事件可被您的本地应用程序捕获，以便应用程序根据需要作出反应和执行功能。

| 回调                   | 数据                                  | 详情                      |
|:---------------------|:------------------------------------|:------------------------|
| `onAccountCreated`   | `accountId`, `userId`, `providerId` | 当账户连接过程开始时触发            |
| `onAccountConnected` | `accountId`, `userId`, `providerId` | 当账户连接过程完成时触发            |
| `onAccountRemoved`   | `accountId`, `userId`, `providerId` | 当账户访问权被用户撤销时触发          |
| `onAccountError` | `accountId`, `userId`, `providerId`, `errorCode` | 当账户连接错误时触发，可能出现的错误列表见下文 |

## 错误代码

当用户连接账户时，他们可能会遇到下面列出的各种错误。

| 错误代码                   | 详情                                                                                   |
|:-----------------------|:-------------------------------------------------------------------------------------|
| ACCOUNT_DISABLED       | 根据数据源提供商，该账户已被禁用                                                                     |
| ACCOUNT_INACCESSIBLE   | 根据数据源提供商，该账户无法访问                                                                     |
| ACCOUNT_INCOMPLETE     | 根据数据源提供商，该账户被标记为不完整                                                                  |
| ACCOUNT_LOCKED         | 根据数据源提供商，该账户已被锁定                                                                     |
| AUTH_REQUIRED          | 没有向数据源提供商发送凭证                                                                        |
| EXPIRED_CREDENTIALS    | 根据数据源提供商，用户的凭证已经过期                                                                   |
| INVALID_ACCOUNT_TYPE   | 根据数据源提供商，该账户不是有效账户                                                                   |
| INVALID_AUTH           | 帐户认证过程失败，请联系 Smile API 寻求帮助                                                          |
| INVALID_CREDENTIALS    | 根据数据源提供商，用户的凭证错误                                                                     |
| INVALID_MFA            | 用户提交的多因素认证凭证无效                                                                       |
| MFA_TIMEOUT            | 多因素认证已超时                                                                             |
| SERVICE_UNAVAILABLE    | 数据源提供商目前不可用                                                                          |
| SYSTEM_ERROR           | Smile Network 存在系统错误，请联系 Smile API 寻求帮助                                              | 
| TOS_REQUIRED           | 用户没有同意数据源提供商的服务条款                                                                    |
| UNSUPPORTED_AUTH_TYPE  | 认证类型不被支持，请联系 Smile API 寻求帮助               |
| UNSUPPORTED_MFA_METHOD | 多因素认证方法不被支持，请联系 Smile API 寻求帮助 |
