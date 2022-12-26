---
title: Event Notifications
excerpt: ''
category: 6215975992e4610014e7b757
slug: chapter-5
---

<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks

Smile uses webhooks to notify your application in real time when an event happens in our servers that is related to your environment.

Event notifications can be sent when a new user is created, an account is successfully connected, an employment document is uploaded, an invitation is sent, or when new any new type data is added such as a user's identity, income, employment, and others. Check out the list of available events that you can subscribe to in our [Webhooks reference page](/reference/webhooks). 

These are sent via a secure channel, using HTTPS from a static IP address, with the data being sent in JSON format. These also come with a signature for you to validate the authenticity of the payload. 

> 📘 Note
> 
> Our static IP address is **18.142.61.230**. You can whitelist this IP address in your back-end to ensure that your application receives event notifications coming from Smile.

Webhooks are particularly useful for getting notifications about asynchronous events, and either executing actions in your backend system when any of these events happen, or knowing when to refresh your front-end system to display any new data.

For detailed implementation steps, visit our [Webhooks reference page](/reference/webhooks) for more information.

## Callbacks

Smile also uses callbacks to notify your application in real time of frontend-related events that happen in your environment.

Via callbacks, you can react or perform other actions once your user performs a supported action using the Wink Widget. Listening to events such as account connection, token expiry, or closing of the widget can help your native application manage and react to your user's actions.

### List of Callbacks

| Callback | Data | Description |
| :------- | :---- | :---- |
| `onAccountCreated` | `accountId`, `userId`, `providerId` | Fired when the account linking process has been initiated |
| `onAccountConnected` | `accountId`, `userId`, `providerId` | Fired when the account linking process has completed successfully |
| `onAccountRemoved` | `accountId`, `userId`, `providerId` | Fired when the account access has been revoked by the user |
| `onTokenExpired` | - | Fired when the Link token has expired |
| `onClose` | - | Fired when the Wink Widget has been closed by the user |
| `onAccountError` | `accountId`, `userId`, `providerId`, `errorCode` | Fired when the user account linking results in an error. |
| `onUploadsCreated` | `uploads`, `userId` | Fired when the user has submitted documents to be uploaded via the Wink Widget. |

### Example Events

#### onAccountCreated

Fired when the account linking process has been initiated by the user such as through sending their login credentials. This does not surface the user's login credentials.

```
onAccountCreated: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onAccountConnected

Fired when the account linking process has completed successfully, and the user is shown the success connection screen.

```
onAccountConnected: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onAccountRemoved

Fired when the account access has been revoked by the user.

```
onAccountRemoved: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

#### onTokenExpired

Fired when the Link token has expired. You may then call the [Refresh Token API](/reference/create-token-1) to refresh the user's token.

```
onTokenExpired: () => {
    console.log('Token expired');
},
```

#### onClose

Fired when the Wink Widget has been closed by the user via the close icon or exit buttons.

```
onClose: () => {
    console.log('Widget closed')
},
```

#### onAccountError

Fired when the user account linking results in an error. The full list of errors can be seen at the [Get Account API reference](/reference/get-account-1).

```
onAccountError: ({
    accountId,
    userId,
    providerId,
    errorCode
}) => {
    console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
},
```

#### onUploadsCreated

Fired when the user has submitted documents to be uploaded via the Wink Widget.

```
onUploadsCreated: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
},
```