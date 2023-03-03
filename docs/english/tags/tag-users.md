---
title: Users  
excerpt: ""  
category: 6294c0fd9494580032b22740  
slug: users
---

All users who have initiated the account linking process with at least one data provider account is related to a specific tenant, identified by the API key and secret used while creating their Smile record.

A token for the user is issued at the same time, and may be renewed through the ``GET /tokens`` endpoint.

Users may have one or multiple [Accounts](/reference/accounts) connected to their user record.

We retain user records for up to 60 days. Additionally, if users revoke their consent to sharing their data any time before this period is up, their record is also removed from Smile. _This is irreversible._

## The User object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID of this user |
| externalMetadata | | |
| createdAt | string | When this user was created |
| providers | array of strings | List of providers that the user has an account with, and have shared their data through Smile |

## Sample User object

``` json
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

## Endpoints

| Endpoint                                                        |                      |
| :-------------------------------------------------------------- | :------------------- |
| [Retrieve user records](/reference/list-users-1)      | `GET /users`      |
| [Create new user record](/reference/create-user-1) | `POST /users` |
| [Retrieve one user record](/reference/get-user-1) | `GET /users/{id}` |

## Webhooks

### `USER_CREATED`

Fired when a new user has been created in the Smile Network and their link token is available.

``` json
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