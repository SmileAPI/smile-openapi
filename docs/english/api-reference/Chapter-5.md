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
| `onUploadsRemoved` | `uploads`, `userId` | Fired when the user has removed/revoked uploaded documents via the Wink Widget. |
| `onUIEvent` | `eventName`, `eventTime`, `mode`, `userId`, `account`, `archive` | Fired whenever a new widget screen is shown to the user. See list of screens below. |

### Example Events

#### onAccountCreated

Fired when the account linking process has been initiated by the user such as through sending their login credentials. This does not surface the user's login credentials.

``` javascript
onAccountCreated: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| accountId | string | Account Id that the user is attempting to connect to |
| userId | string | User Id of the end user on the Smile Network |
| providerId | string | Provider Id that the user is attempting to connect to |

#### onAccountConnected

Fired when the account linking process has completed successfully, and the user is shown the success connection screen.

``` javascript
onAccountConnected: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| accountId | string | Account Id that the user has connected to |
| userId | string | User Id of the end user on the Smile Network |
| providerId | string | Provider Id that the user has connected to |

#### onAccountRemoved

Fired when the account access has been revoked by the user.

``` javascript
onAccountRemoved: ({
    accountId,
    userId,
    providerId
}) => {
    console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| accountId | string | Account Id that the user has removed |
| userId | string | User Id of the end user on the Smile Network |
| providerId | string | Provider Id of the account that the user has removed |

#### onTokenExpired

Fired when the Link token has expired. You may then call the [Refresh Token API](/reference/create-token-1) to refresh the user's token.

``` javascript
onTokenExpired: () => {
    console.log('Token expired');
},
```

#### onClose

Fired when the Wink Widget has been closed by the user via the close icon or exit buttons.

``` javascript
onClose: () => {
    console.log('Widget closed')
},
```

#### onAccountError

Fired when the user account linking results in an error. The full list of errors can be seen at the [Get Account API reference](/reference/get-account-1).

``` javascript
onAccountError: ({
    accountId,
    userId,
    providerId,
    errorCode
}) => {
    console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| accountId | string | Account Id that the user is attempting to connect to |
| userId | string | User Id of the end user on the Smile Network |
| providerId | string | Provider Id that the user is attempting to connect to |
| errorCode | string | Error code for the error |

#### onUploadsCreated

Fired when the user has submitted documents to be uploaded via the Wink Widget.

``` javascript
onUploadsCreated: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| uploads | object | Contains specific information about the upload |
| userId | string | User Id of the end user on the Smile Network |

#### onUploadsRemoved

Fired when the user has removed/revoked uploaded documents via the Wink Widget.

``` javascript
onUploadsRemoved: ({ uploads, userId }) => {
    console.log('Uploads: ', uploads, ' User ID:', userId);
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| uploads | object | Contains specific information about the upload |
| userId | string | User Id of the end user on the Smile Network |

#### onUIEvent

Fired whenever a new widget screen is shown to the user.

``` javascript
onUIEvent: ({ eventName, eventTime, mode, userId, account, archive }) => {
    console.log('Event Name: ', eventName, ', Event Time: ', eventTime, ', mode: ', mode, ', User ID: ', userId, ', Account: ', account, ', Archive: ', archive);
},
```

| Property | Type | Description |
| :------- | :---- | :---- |
| eventName | string | Name of the event, i.e. `LoginPageOpened` |
| eventTime | string | Time of the event |
| mode | string | Mode of the Wink Widget currently running, i.e. `SANDBOX` or `PRODUCTION` |
| userId | string | User Id of the end user on the Smile Network |
| account | object | Contains specific account-related information relevant to the event, i.e. `providerId` or `accountId`. Note that these are Ids specific to Smile Network |
| archive | object | Contains specific archive-related information relevant to the event, i.e. `fileType` |

For the list of event names, see the table below:

| Event Name | Description | Event-specific Properties |
| :------- | :---- | :---- |
| ConsentPageOpened | The user opened the consent screen | |
| ProviderListPageOpened | The user opened the provider list screen | |
| LoginPageOpened | The user opened the login screen | providerId |
| MfaPageOpened | The user opened the Multi-Factor Authentication screen | providerId |
| ConnectSuccessPageOpened | The user opened the account connected success screen | providerId, accountId |
| AccountRevokePageOpened | The user opened the account connection status screen / revoke screen | providerId, accountId |
| LoginOptionsPageOpened | The user opened the alternative login options screen | |
| EmployerSurveyPageOpened | The user opened the employer survey screen | |
| FileTypeListPageOpened | The user opened the document type selection screen (i.e. to select what type of document they wish to upload, such as SSS records, Income Tax Records, etc.) | |
| FileTypePageOpened | The user opened the document upload screen | |
| ArchiveSuccessPageOpened | The user has successfully uploaded a file and has opened the success screen | |
| RevokeArchivePageOpened | The user opened the archive status screen / delete screen | |
