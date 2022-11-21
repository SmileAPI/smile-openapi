---
title: Users  
excerpt: ""  
category: 62ce2a159aafea009af30daa  
slug: users
---

所有的用户都与一个特定的租户关联，由创建用户时使用的 API key 和 secret 来识别。

同时为用户发放一个 token ，并可通过 ``GET /tokens`` 端点更新。

用户可以有一个或多个[Accounts](/reference/accounts)连接到他们的用户记录。

我们保留长达 60 天的用户记录。此外，如果用户或者租户在这段时间内的任何时候撤销共享数据，他们的记录也将被从 Smile 中删除。_这个行为是不可逆的。_

## 用户对象

| 属性  | 类型               | 详情                          |
| :--------- |:-----------------|:----------------------------|
| id | string           | 该用户唯一的ID                    |
| externalMetadata |                  |                             |
| createdAt | string           | 该用户被创建的时间                   |
| providers | array of strings | 用户拥有账号并通过 Smile 分享其数据的提供商名单 |

## 用户对象样例

```
[{
    "id": "tenantid-f482de95b2154985b65551c85095f886",
    "externalMetadata": null,
    "createdAt": "2022-09-20T01:27:26Z",
    "providers": [
        "abccorp",
        "abcplatform",
        "xyzemployer"
    ]
}]
```

## 端点

| 端点                                 |                      |
|:-----------------------------------| :------------------- |
| [获取用户列表](/reference/list-users-1)  | `GET /users`      |
| [创建新的用户](/reference/create-user-1) | `POST /users` |
| [获取一条用户记录](/reference/get-user-1)  | `GET /users/{id}` |

## Webhooks

### `USER_CREATED`

当一个新的用户在 Smile Network 中被创建，并且他们的链接 token 是可用的，就会发布此事件。

```
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