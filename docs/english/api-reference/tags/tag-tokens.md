---
title: Tokens 
excerpt: ""
category: 6294c0fd9494580032b22740
slug: tokens
---

To provide authorized access for your user, your application should obtain a user token (the **Link token**) from the /users endpoint. This is a single use, short-lived token which is used to initialize our **Wink Widget**.

Time of expiry is included when a token is generated. You may also listen for events from the SDK when the token has expired (see below).

Your server or application should generate a new Link token for the user each time you wish to launch the widget.

## Refreshing a User's Token

You can refresh a user's token by calling the `/tokens` endpoint. Simply pass the `userId` of the user as a parameter in the query to give the user a new token.

## The Token object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| expiresAt | date-time | Date and time when the issued token will expire |
| mode | string | Valid mode for the Link token, either `SANDBOX` or `PRODUCTION` |
| accessToken | string | Short-lived token to initiate link flow |

## Sample Token data

```json
{
    "expiresAt": "2022-11-01T09:00:00Z",
    "mode": "SANDBOX",
    "accessToken": "abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFEDCBA.0987654321abcdefghijklmnopqrstuvwxyz.ABCDEFGHIJKLMNOPQRSTUVWXYZ-0123456789zyxwvutsrqponmlkjihgfedcbaZYXWVUTSRQPPONMLKJIHGFED"
}
```


## Endpoints

| Endpoint | |
| :------- | :---- |
| [Refresh token](/reference/create-token-1) | `POST /tokens` |

## Webhooks

### `USER_CREATED`

Fired when a new user has been created in the Smile Network and their link token is available.

```json
{
    "id": "et-123abc456def789abc123def456abc78",
    "version": 1,
    "type": "USER_CREATED",
    "createdAt": "2021-04-14T09:30:24Z",
    "data": {
        "userId": "tenantId-123abc456def789abc123def456abc78"
    }
}
```

## Event Listeners

The SDK also emits events that can be caught by your native application to allow the application to react and perform functions as needed.

| Callback | Data | Description |
| :------- | :---- | :---- |
| `onTokenExpired` | - | Fired when the Link token has expired |
