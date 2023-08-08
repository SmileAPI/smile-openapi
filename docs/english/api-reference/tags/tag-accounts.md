---
title: Accounts
excerpt: ""
category: 6294c0fd9494580032b22740
slug: accounts
---

Accounts in the Smile Network form the basis of the data shared by the user to our clients. Each user may connect multiple accounts among the data [Providers](/reference/providers) that Smile supports, which provides a clearer picture of their history and information.

Upon providing consent and access directly from the end user, Smile retrieves available data from the account and provides normalized data under each user data endpoint at that particular point in time. If your account has *Continuous Data Sync* enabled, Smile will also periodically check with the provider for updated data, and keep your user's information updated for as long as the account is connected (i.e., not revoked by the user).

Available data points for each provider may vary, which you can review real-time using [the Data Sources section of the Developer Portal](https://portal.getsmileapi.com/providers). You can track availability of the data using [Webhook event notifications](/reference/chapter-5).

By default, the List Accounts API will return all accounts under your `tenantId` that match your query parameters. Make sure to filter the results by `userId` or `startDate` and `endDate` to narrow down your query.

Once users revoke their accounts (via the SDK, or tenants may initiate this process through the [Revoke Account API](/reference/delete-account)), their data will be removed and will no longer be accessible.

## Continuous Data Sync

Smile API's *Continuous Data Sync* (CDS) feature provides you access to the most up-to-date and recent data from your users, once these users have consented and connected their account through the Wink Widget.

Instead of requiring the user to reconnect their account if you need updated information, CDS provides you with permissioned access to updated data. By consenting to CDS, users can authorize Smile to sync data for you across multiple months, until they revoke access to their account.

We fire a webhook event `ACCOUNT_SYNC_TASK_FINISHED` (see below) when an Account has been newly refreshed, so you can receive information about the update.

CDS must be enabled for your business to enjoy these features, but once enabled, there is no change needed to your integration with Smile API.

### Supported Providers and Data Points

| Provider | Data Points Available | Update Frequency |
| :--------- | :----- | :-------- |
| My.SSS | Identities, Employments, Documents, Contributions, Liabilities, Estimated Incomes* | Monthly, on the day of initial connection |
| eGSIS MO | Identities, Employments, Documents, Incomes, Estimated Incomes* | Monthly, on the day of initial connection |
| My PhilHealth Portal | Identities, Employments, Documents, Contributions, Estimated Incomes* | Monthly, on the day of initial connection |
| Virtual Pag-IBIG | Identities, Employments, Documents, Contributions, Liabilities, Estimated Incomes* | Monthly, on the day of initial connection |

## The Account object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string-time | Unique ID of the account on the Smile Network |
| createdAt | date-time | Date/time when the account was created |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |
| connectionStatus | string | Status of the account's connection state, see *Account Statuses* section below |
| connection | object | Object containing connection information for the account |
| monitorStatus | string | Status of the account's monitoring/sync state, see *Account Statuses* section below |
| monitor | object | Object containing monitoring information for the account |

## Account Statuses

### Connection Status

| Event | Description |
|----------|---------|
| PENDING | The account was created but is pending successful authentication. |
| AWAITING_MFA | The user was able to successfully authenticate, however the data provider is waiting for the user to enter their verification code in a 2-factor authentication scenario. |
| ERROR | The data provider returned an error. The user may have entered the wrong credentials, or there was a problem on the side of the provider. |
| CONNECTED | The user was able to successfully authenticate with an employment data provider. |
| DISCONNECTED | The user disconnected the link with the employment data provider. |

### Monitoring Status

| Event | Description |
|----------|---------|
| UNSUPPORTED | The account does not have data syncing enabled |
| ACTIVE | The account has data syncing enabled and is currently active |
| USER_ACTION_REQUIRED | The account has data syncing enabled but the user needs to re-authorize access. This may be due to a change of password or other reason where the account connection has failed. |
| CUSTOMER_DISABLED | The account syncing has been disabled |

## Sample Account data

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

## Endpoints

| Endpoint | |
| :------- | :---- |
| [Retrieve all accounts](/reference/list-accounts-1) | `GET /accounts` |
| [Retrieve one account](/reference/get-account-1) | `GET /accounts/{id}` |
| [Revoke account access](/reference/delete-account) | `DELETE /accounts` |
| [Disable account monitoring](/reference/disable-account-monitor) | `POST /accounts/{id}/disableMonitor` |

## Webhooks

### `ACCOUNT_CREATED`

Fired when the account linking process has been initiated by the user. This webhook will be fired even for providers who do not require logins.

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

Fired when a user has successfully connected an account to the Smile Network. This will only be fired if the data provider requires a login.

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

Fired when a user has successfully disconnected or revoked the link to their account from the Smile Network.

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

Fired when the account linking process initiated by the user is unsuccessful.

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
    "errorCode": "INVALID_CREDENTIALS",
    "errorMessage": "Invalid username or password!",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `ACCOUNT_SYNC_TASK_FINISHED`

Fired when the account syncing task has been completed in the backend.

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
