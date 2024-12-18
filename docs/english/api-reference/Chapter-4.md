---
title: Getting User Data  
excerpt: ""  
category: 6215975992e4610014e7b757
slug: chapter-4
---



You can obtain data from your users via two ways:
 - Inviting your user via the ``/invitations`` endpoint in the API or using [the invitation functionality in the Developer Portal, under the Users section](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link).
 - Embedding the Client SDK and instantiating the Wink Widget.

---
<!-- focus: false -->
![Invitations](https://img.icons8.com/ios/50/000000/email-open.png)

## Invitations

Invitations allow you to invite your users to connect their work accounts or upload copies of their employment-related documents via communication channels such as email. Using the Invitation endpoint in the API, you can send a message to a user, or send multiple invitations by looping through the contact information such as email address of several users. To make it easier for you to try it out, we provide an [example implementation of Invitations in the Developer Portal](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link). 

If you want to customize the content of the messages, you can define an Invitation Template. You can do so via the API or use the example implementation in the the Developer Portal. The template accepts dynamic variables such as the following:


|Party|Variable Name|Description|
|---|---|---|
|Sender|${companyName}|Company Name|
|Recipient|${fullName}|Full Name|


---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/open-in-popup.png)


## Client SDK

Getting user data via the Client SDK into your application involves two things:

 - **Embedding a Javascript SDK for your web application client**. At the moment, Smile only provides a Javascript SDK, but native verions of the SDK for mobile applications such as iOS or Android are coming soon. The Javascript SDK launches a modal window called a "Wink" web widget where users can provide permission for Smile to access their data. Users will first find their employer or employment data provider, then submit their login credentials over a secure and encrypted connection and/or upload some files. By using the SDK, you will not have to worry about the different authentication and verification implementations of the different employment platforms, or provide a file upload mechanism and manage data analysis or OCR. We make the process of getting data and using that data simple for your developers, and the experience smooth for your users. 

 - **Obtaining a user token from the Smile Open API**. Your back-end server should obtain a "Link" token  from the /users endpoint. This is a single use, short-lived token which is used to initialize the Wink widget. Your server should generate a new Link token each time you wish to launch the widget.


---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/code.png)

## Example Code
Below is sample HTML code which embeds the Wink Javascript SDK.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink Quickstart - Sandbox Mode</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * User token(link token) passed from your backend service which is obtained from the Smile API.
             */
            userToken: '<usertoken>',

            /**
             * Use the template ID to determine how your widget looks like embedded in your app or website.
             * You can find and create the template ID in the Smile developer-portal.
             * https://developer-portal.smileapi.io/link/template
             */
            templateId: "<ID of wink template >",

            /**
             * Account login callback.
             */
            onAccountCreated: ({ accountId, userId, providerId }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Account login success callback.
             */
            onAccountConnected: ({ accountId, userId, providerId }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Account revoke callback.
             */
            onAccountRemoved: ({ accountId, userId, providerId }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Token expired callback.
             */
            onTokenExpired: () => {
                console.log('Token expired');
            },

            /**
             * Smile link SDK close callback.If you want to know which button the user clicked to trigger the close event, you can pass parameters like this.
             * onClose:({reason})=>{}
             * If the value of reason is equal to "close", it means that the user clicked the close icon in the upper right corner of the page to close the SDK
             * If the value of reason is equal to "exit", it means that the user clicked the DONE button on the connection page to close the SDK
             */
            onClose: ({ reason }) => {
                console.log('Link closed, reason:', reason)
            },

            /**
             * Account connect error callback.
             */
            onAccountError: ({ accountId, userId, providerId, errorCode }) => {
                console.log('Account error: ', accountId, ' User ID:', userId, ' Provider ID:', providerId, 'Error Code:', errorCode)
            },

            /**
             * Uploads submit callback.
             */
            onUploadsCreated: ({ uploads, userId }) => {
                console.log('Uploads: ', uploads, ' User ID:', userId);
            },

            /**
             * Uploads revoke callback.
             */
            onUploadsRemoved: ({ uploads, userId }) => {
                console.log('Uploads: ', uploads, ' User ID:', userId);
            },

            /**
             * User event callback is used to capture all the user activities from Smile Wink SDK
             */
            onUIEvent: ({ eventName, eventTime, mode, userId, account, archive }) => {
                console.log('eventName:', eventName,
                    "eventTime:", eventTime,
                    "mode:", mode,
                    "userId:", userId,
                    "account:", account,
                    "archive:", archive);
            }
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```

> 📘 Note
> 
> There are currently two versions of the SDK available. Code for Version 2 (the latest version) is shown above. To switch from version 1 and version 2, simply switch the SDK source code to Version 1. No other changes are needed.

## Wink Widget Versioning

**Wink Widget Version 2 contains many user experience and functionality improvements and is the recommended version**.

Version 1 is still maintained and security monitoring, updates, and patches will continue to be done.

| Version | SDK JavaScript Embed |
| --- | --- |
| Version 2 **(recommended)** | `<script src="https://web.smileapi.io/v2/smile.v2.js"></script>` |
| Version 1 | `<script src="https://web.smileapi.io/v1/smile.v1.js"></script>` |

---


<!-- focus: false -->
![Settings](https://img.icons8.com/material-outlined/60/000000/settings-3--v1.png)

## Configuration parameters

| Parameter  |Value |
|------------|---------|
| userToken  | The user token returned from Smile using the /users endpoint (see documentation on Users endpoint) |
| callbacks  | All the callbacks are optional, but suggest listening to onClose() callback, so you can return from Smile SDK to your application page                                                                                   |
| templateId | ID of wink template                                                                                   |


> 🚧 Warning
> 
> Archives in Sandbox Mode return only specific payslips. To test Archives while in Sandbox Mode, you may download the sample payslips within the Developer Portal and upload it through the Wink Widget or through the API. Other files uploaded during Sandbox mode will return errors.

---
<!-- focus: false -->
![Token](https://img.icons8.com/ios/50/000000/sms-token.png)

## Refreshing a User's Token
You can refresh a user's token by calling the /tokens endpoint. Simply pass the userId as a parameter in the query to give the user a new token. More information can be found in the Tokens endpoint documentation.

---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)

## Link events 
As the user moves through the Wink widget screen, any activities performed by the user are captured and are either used to update the messsages and presentation of the modal window, or are sent to Smile so that any source-related data can be retrieved. 

### Linked Accounts
If the the user was able to successfully authenticate with a digital employment data provider, the Link status is changed to "CONNECTED". The account status of the user can be queried at any time via the /accounts endpoint. Examples of the events captured include:

| Event |Description |
|----------|---------|
| PENDING | The account was created but is pending successful authentication |
| AWAITING_MFA | The user was able to successfully authenticate however the data provider is waiting for the user to enter their verification code in a 2-factor authentication scenario. |
| ERROR | The data provider returned an error. The user may not have entered the wrong credentials or there was a problem on the side of the provider. |
| CONNECTED | The user was able to successfully authenticate with an employment data provider. |
| DISCONNECTED | The user disconnected the link with the employment data provider. |

You can allow the user to revoke access to their account data using the /accounts endpoint as well. All data related to the revoked account will be removed from the system.

### Successful Uploads
If the the user was able to successfully upload employment and income data via scanned or photographed documents, the Link status is changed to "STARTED". The upload status of the user can be queried at any time via the /archives endpoint. Examples of the events captured include:

| Event |Description |
|----------|---------|
| STARTED | The upload was successful, and analysis on whether data can be extracted has started. |
| ANALYZED | The analysis has completed and data was successfully extracted (via OCR) and converted to JSON format. |
| UNSUPPORTED | The type of file uploaded cannot be analyzed. Data cannot be automatically extracted. |
| ERROR | Something went wrong with the analysis of the uploaded file. |
| REVOKED | The user revoked permission to share data from the uploaded files. |

## Maintaining User Data

Smile API's *Continuous Data Sync* (CDS) feature provides you access to the most up-to-date and recent data from your users, once these users have consented and connected their account through the Wink Widget. By consenting to CDS, users can authorize Smile to sync data for you across multiple months, until they revoke access to their account.

Find out more about CDS and enabling CDS in the [Accounts section](/reference/accounts).

---
<!-- focus: false -->
![Testing](https://img.icons8.com/material-outlined/50/000000/test-tube.png)

## Testing in Sandbox

Smile provides a Sandbox mode for our production environment to allow you to test your integration with sample data.

To use the Sandbox, you can use the following example credentials:

| User Name | Full Name | Email | Mobile Phone | Password | Verification Code | SS Number |
|---|---|---|---|---|---|---|
| George | George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456 | 1234 | 3300000008 |
| Ryan | Ryan Lestari | ryan1234@smileapi.io |  (+62) 8119994321 | 654321 | 1234 | N/A |
| Christina | Christina Tan | christina4321@smileapi.io |  (+65) 99996789 | YGUS1 | 1234 | N/A |
| Anisha | Anisha Bhatia | anisha98765@smileapi.io |  (+91) 9511198765 | 123456 | 1234 | N/A |

Archives in Sandbox Mode return only specific payslips. To test Archives while in Sandbox Mode, you may download the sample payslips within the Developer Portal and upload it through the Wink Widget or through the API. Other files uploaded during Sandbox mode will return errors.