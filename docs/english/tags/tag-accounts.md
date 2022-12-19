---
title: Accounts
excerpt: ""
category: 6294c0fd9494580032b22740
slug: accounts
---

Accounts in the Smile Network form the basis of the data shared by the user to our clients. Each user may connect multiple accounts among the data [Providers](/reference/providers) that Smile supports, which provides a clearer picture of their history and information.

No login credentials are stored with [User](/reference/users) accounts. Upon providing access, Smile retrieves available data from the account and provides normalized data under each user data endpoint. Available data points for each provider may vary. You can track availability of the data using [Webhook event notifications](/reference/chapter-5).

By default, the List Accounts API will return all accounts under your `tenantId` that match your query parameters. Make sure to filter the results by `userId` or `startDate` and `endDate` to narrow down your query.

Once connected by the user, their data is kept for 60 days unless they revoke access via the SDK or otherwise through the [Revoke Account API](/reference/delete-account).

## The Account object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string-time | Unique ID of the account on the Smile Network |
| createdAt | date-time | Date/time when the account was created |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |
| connection | object | Object containing connection information for the account |

## Sample Account data

```
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

## Endpoints

| Endpoint | |
| :------- | :---- |
| [Retrieve all accounts](/reference/list-accounts-1) | `GET /accounts` |
| [Retrieve one account](/reference/get-account-1) | `GET /accounts/{id}` |
| [Revoke account access](/reference/delete-account) | `DELETE /accounts` |

## Webhooks

### `ACCOUNT_CONNECTED`

Fired when a user has successfully connected an account to the Smile Network.

```
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

Fired when a user has successfully disconnected or revoked the link to their account from the Smile Network.

```
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

Fired when the account linking process initiated by the user is unsuccessful.

```
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

## Event Listeners

The SDK also emits events that can be caught by your native application to allow the application to react and perform functions as needed.

| Callback | Data | Description |
| :------- | :---- | :---- |
| `onAccountCreated` | `accountId`, `userId`, `providerId` | Fired when the account linking process has been initiated |
| `onAccountConnected` | `accountId`, `userId`, `providerId` | Fired when the account linking process has completed successfully |
| `onAccountRemoved` | `accountId`, `userId`, `providerId` | Fired when the account access has been revoked by the user |
| `onAccountError` | `accountId`, `userId`, `providerId`, `errorCode` | Fired when the user account linking results in an error. See below for list of possible errors. |

## Error Codes

As users connect their accounts, your users may come across various errors listed below.

| Error Code | Description |
| :---- | :---- |
| ACCOUNT_DISABLED | Account is disabled according to the data source provider. |
| ACCOUNT_INACCESSIBLE | Account is inaccessible according to the data source provider. |
| ACCOUNT_INCOMPLETE | Account is marked as incomplete according to the data source provider. |
| ACCOUNT_LOCKED | Account is locked according to the data source provider. |
| AUTH_REQUIRED | Credentials were not sent to the data source provider. |
| EXPIRED_CREDENTIALS | User's credentials have expired according to the data source provider. |
| INVALID_ACCOUNT_TYPE | The account is not a valid account according to the data source provider. |
| INVALID_AUTH | Account authentication process failed, contact Smile API for assistance. |
| INVALID_CREDENTIALS | User's credentials is incorrect according to the data source provider. |
| INVALID_MFA | User-submitted Multi-factor Authentication Credential is invalid. |
| MFA_TIMEOUT | Multi-factor Authentication has timed out. |
| SERVICE_UNAVAILABLE | Data source provider is currently unavailable. |
| SYSTEM_ERROR | There is a system error on the Smile Network, contact Smile API for assistance. | 
| TOS_REQUIRED | Account has not consented to the data source provider's terms of service. |
| UNSUPPORTED_AUTH_TYPE | Authentication type is unsupported, contact Smile API for assistance. |
| UNSUPPORTED_MFA_METHOD | Multi-factor Authentication method is unsupported, contact Smile API for assistance. |
