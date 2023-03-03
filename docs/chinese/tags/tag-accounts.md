---
title: Accounts
excerpt: ""
category: 62ce2a159aafea009af30daa
slug: accounts
---

Smile Network 中的账户数据是客户与终端用户共享数据的基本信息。每个用户可以在 Smile 支持的[ Providers ]( /reference/providers )中连接多个账户，这样可以更清楚地了解他们的历史信息。
 
我们不在[ User ]( /reference/users )中存储登录凭证。在用户授权访问时，Smile 从用户所在的 Provider 账户中获取可用的数据，并将数据规范化后存入 Accounts 的每个数据端点下。每个提供商的可用数据端点可能有所不同。您可以使用[ Webhook event notifications ]( /reference/chapter-5 )来跟踪数据的可用性。

默认情况下，List Accounts API 将返回您的 `tenantId` 下所有符合查询参数的账户。请确保通过`userId`、`startDate`或`endDate`来过滤结果，以缩小查询范围。

用户连接后的数据将被保存60天，除非他们经由 SDK 或其他方式通过[ Revoke Account API ]( /reference/delete-account )撤销访问。

## 帐户对象

| 属性         | 类型          | 详情                      |
|:-----------|:------------|:------------------------|
| id         | string-time | Smile Network 上账户的唯一 ID |
| createdAt  | date-time   | 创建账户的时间                 |
| providerId | string      | 用户账户所连接的数据提供商 ID        |
| userId     | string      | Smile Network 上用户的 ID   |
| connection | object      | 包含账户连接信息的对象             |

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
    }
}
```

## 端点

| 端点                                                 | |
|:---------------------------------------------------| :---- |
| [获取账户列表](/reference/list-accounts-1)               | `GET /accounts` |
| [获取一条账户记录](/reference/get-account-1)               | `GET /accounts/{id}` |
| [撤销账户访问权](/reference/delete-account) | `DELETE /accounts` |

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
| ACCOUNT_DISABLED       | 根据数据源提供商，该账户已被禁用                                                                     
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
