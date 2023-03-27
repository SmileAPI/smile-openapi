---
title: Tokens
excerpt: ""
category: 62ce2a159aafea009af30daa
slug: tokens
---

为了给用户提供授权访问，您的应用程序应该从 /users 端点获得一个用户 token（ **链接 token** ）。这是一个一次性的、短暂的 token ，用于初始化我们的 **Wink Widget** 。

过期时间在 token 生成时就被包含在内。您还可以在 token 过期时监听 SDK 的事件（见下文）。

您的服务器或应用程序应该在每次启动 Wink Widget 时为用户生成一个新的链接 token 。

## 刷新一个用户的 token

可以通过调用 `/tokens` 端点来刷新用户的 token 。只需在查询中将用户的 `userId` 作为参数，您就可以给用户一个新的 token 。

## Token 对象

| 属性          | 类型        | 详情                                            |
|:------------|:----------|:----------------------------------------------|
| expiresAt   | date-time | token 将要过期的时间                                 |
| mode        | string    | 链接 token 的有效模式，可以是 `SANDBOX` 或 `PRODUCTION` 。 |
| accessToken | string    | 启动链接流的短暂标志                                    |

## Token 数据样本

```json
{
    "expiresAt": "2022-11-01T09:00:00Z",
    "mode": "SANDBOX",
    "accessToken": "abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFED"
}
```


## 端点

| 端点                                    | |
|:--------------------------------------| :---- |
| [刷新 token](/reference/create-token-1) | `POST /tokens` |

## Webhooks

### `USER_CREATED`

当一个新的用户在 Smile Network 中被创建，并且他们的链接 token 可用时，此 Webhook 事件会被触发。

```json
{
    "id": "123abc456def789abc123def456abc78",
    "version": 1,
    "type": "USER_CREATED",
    "createdAt": "2021-04-14T09:30:24Z",
    "data": {
        "userId": "tenantId-123abc456def789abc123def456abc78"
    }
}
```

## 事件监听器

SDK 还可以发出特定的事件，该事件可被您的本地应用程序捕获，以便应用程序根据需要作出反应和执行功能。

| 回调 | 数据  | 详情                |
| :------- |:----|:------------------|
| `onTokenExpired` | -   | 当链接 Token 过期时被触发。 |
