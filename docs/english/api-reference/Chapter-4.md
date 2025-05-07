---
title: Account Linking
excerpt: ""  
category: 6215975992e4610014e7b757
slug: chapter-4
---

**Smile Wink**, Smile API's Account Linking service, enables secure, user-permissioned sharing of identity, income, and employment data between individuals and third-party organizations.

Using Smile's Wink Widget, a JavaScript-based client SDK, developers can easily integrate this functionality into web or mobile applications. The widget provides a seamless and secure interface where users can authenticate with their employment data provider by entering credentials or uploading relevant documents. Once verified, Smile retrieves the data and makes it accessible via the Developer Portal or the Open API.

This unified solution abstracts the complexity of various authentication flows and data formats, streamlining both integration for developers and the user experience.

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## Integration Steps

Its easy to get started with the Smile Open API. Implementing the Smile Open API involves simple client and server-side integration, which are outlined below in four key steps:

1. **Link token:** Your application server sends a request to our REST API to generate a short-lived "Link" token.

2. **Wink Widget:** Using the Link token, your application client initializes the Client SDK to launch the Smile Wink Widget. Your end-users interact with this widget to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. **Connecting to Source Data:** Once in the widget, a user can then either connect their employment account or upload a photo or scanned copy of their employment data. This will be used as the source for any user data your application will be requesting.

4. **Requests:** Our servers execute your application's requests. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

5. **Webhooks:** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API. Find out more under Event Notifications.

---
<!-- focus: false -->
![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)

## Quickstart

To actually test the Smile API in your own environment, we have provided example code to instantiate the Wink Widget or SDK.

> 📘 Note
> 
> We provide [Quickstart sample code](https://github.com/SmileAPI/quickstart) in [Github](https://github.com/SmileAPI) which you can download and modify according to your own requirements. 

The example code installs a small server running on Node.js that automatically retrieves a token from our API, so you can instantiate the Wink widget in your own local machine.

The example implementation is composed of two parts:
* Under ``/frontend``, you will find example code in HTML that already has the Wink Javascript SDK embedded.
* Under ``/node``, you will find server-side Javascript code that will retrieve the token. You will need to download and run Node.js to run the code.

**Implementation Steps**

Below steps are also included in the README.md document found in the the Quickstart [repository](https://github.com/SmileAPI/quickstart).

1. **Download the Quickstart files onto your machine.**
   
   > 📘 Note
   >
   > If you have git, you can clone the repository or run the following command:
   > 
   > ```bash
   > git clone https://github.com/SmileAPI/quickstart
   > ```

2. **Go to the ``/node`` directory of your Quickstart download.**

3. **Create a new file called ``.env`` in this directory** with the following contents:
   
   ```bash
   # The port you want the example server to listen to
   APP_PORT=<portnumber>
   
   # Smile Link API keys (you can get this by requesting access from access@getsmileapi.com)
   API_KEY=<apikey>
   API_SECRET=<apisecret>
   
   # API Host (whether this will run in Sandbox or Production)
   OPEN_API_HOST=<openapihost>
   ```

   You can use the ``.env.example`` file, included in the Quickstart repository, as a reference.

   > 🚧 Warning
   > 
   > **The .env file is normally hidden by your system.** You may want to enable display of hidden files in your system preferences to be able to see it.
   >
   > Additionally, on Windows machines, Windows will not allow you to create a ``.env`` file directly from Windows Explorer since it will not allow file names starting with a ``.``. To get around this, you can do the following steps:
   > 
   > 1. Open Notepad and write the contents of the file (see below).
   > 2. Go to FILE -> SAVE AS window in Notepad.
   > 3. Select the "All files" type in the selection window.
   > 4. Save the file as ``.env``

   You may need to ensure that you have proper permissions in your machine to create the file.

   > 📘 Note
   >  
   > In Mac or Linux machines, you can open up Terminal and enter the following commands as a Super User:
   >
   > ```bash
   > sudo touch .env
   > ```
   
4. **Save and close your file.**

5. If you don't have Node.js installed in your machine, **install Node.js.**
   
   > 📘 Note
   >
   > **For Mac,** you can open up the Terminal and run:
   > ```bash
   > curl "https://nodejs.org/dist/latest/node-${VERSION:-$(wget -qO- https://nodejs.org/dist/latest/ | sed -nE 's|.*>node-(.*)\.pkg</a>.*|\1|p')}.pkg" > "$HOME/Downloads/node-latest.pkg" && sudo installer -store -pkg "$HOME/Downloads/node-latest.pkg" -target "/"
   > ```
   >
   > **For Windows,** you can [download the installer](https://nodejs.org/en/#home-downloadhead).
   >
   > **For other operating systems,** [you can find the instructions](https://nodejs.org/en/download/package-manager/#macos) from the Node.js website.

8. **Run Yarn** with [npm package manager](https://www.npmjs.com/) which is included with Node.js and enter the following commands:
   ```bash
   npm install --global yarn
   yarn install
   ```
   
   > 📘 Note
   >
   > In Mac or Linux, you will need to open up the Terminal. If you are using Windows, you can go to the command line. Make sure you are still in the ``/node`` directory of the Quickstart files you just downloaded onto your machine.
   > 
   > You may need to run as a Super User if you don't have enough permissions. On a Mac or Linux machine, you can run the commands as a superuser by using ``sudo``. On Windows, you can run the command with an administrator trust-level, or by right-clicking the program in the UI and choosing "run as administrator."

8. **Run the server:**
   ```bash
   node index.js
   ```

   > 🚧 Warning
   >
   > You may need to install dotenv in your environment if you run into issues running the Node server. To install dotenv, simply run the following:
   > 
   > ```bash
   > npm install dotenv
   > ```

9. **Open up the your browser and open up the example Wink Widget.** For example, if you specified port ``:8000`` in your ``.env`` configuration file, open up http://127.0.0.1:8000 in your web browser.

10. **Test the Widget** using the [Sandbox accounts](ref:getting-user-data#testing-in-sandbox) provided.

> 👍 Good job!
>
> Sit back, relax, and pat yourself on the back for a job well done!


---
<!-- focus: false -->
![User Data](https://img.icons8.com/?size=50&id=FD1d9t9lMoS2&format=png&color=000000)
## Getting User Data

You can obtain data from your users via three ways:

1. Inviting your user via the ``/invitations`` endpoint in the API or using [the invitation functionality in the Developer Portal, under the Users section](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link).
2.  Embedding the Client SDK and instantiating the Wink Widget to allow your users to share their information directly from your app or website.
3.  Publishing a Flip Site with an embedded Wink Widget and directing your users to accomplish the form (see Form Processing).


### Invitations

Invitations allow you to invite your users to connect their work accounts or upload copies of their employment-related documents via communication channels such as email. Using the Invitation endpoint in the API, you can send a message to a user, or send multiple invitations by looping through the contact information such as email address of several users. To make it easier for you to try it out, we provide an [example implementation of Invitations in the Developer Portal](https://portal.getsmileapi.com/users/invite?utm_source=docs&utm_medium=internal_link). 

If you want to customize the content of the messages, you can define an Invitation Template. You can do so via the API or use the example implementation in the the Developer Portal. The template accepts dynamic variables such as the following:

|Party|Variable Name|Description|
|---|---|---|
|Sender|${companyName}|Company Name|
|Recipient|${fullName}|Full Name|



### Client SDK

Getting user data via the Client SDK into your application involves two things:

 - **Embedding a Javascript SDK for your web application client**. At the moment, Smile only provides a Javascript SDK, but native verions of the SDK for mobile applications such as iOS or Android are coming soon. The Javascript SDK launches a modal window called a "Wink" web widget where users can provide permission for Smile to access their data. Users will first find their employer or employment data provider, then submit their login credentials over a secure and encrypted connection and/or upload some files. By using the SDK, you will not have to worry about the different authentication and verification implementations of the different employment platforms, or provide a file upload mechanism and manage data analysis or OCR. We make the process of getting data and using that data simple for your developers, and the experience smooth for your users. 

 - **Obtaining a user token from the Smile Open API**. Your back-end server should obtain a "Link" token  from the /users endpoint. This is a single use, short-lived token which is used to initialize the Wink widget. Your server should generate a new Link token each time you wish to launch the widget.


---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/code.png)

#### Example Code
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
> 


---
<!-- focus: false -->
![Settings](https://img.icons8.com/material-outlined/50/000000/settings-3--v1.png)

## Configuration

The Wink Widget uses Wink Templates to manage instantiated settings for each Widget embedded in your app. The Wink Widget Templates allow for rich customization of your Widget including primary colors and the data sources selected for the instance.

| Parameter  |Value |
|------------|---------|
| templateId | ID of the Wink Template in use |
| userToken  | The user token returned from Smile using the /users endpoint (see documentation on Users endpoint) |
| callbacks  | All the callbacks are optional, but suggest listening to onClose() callback, so you can return from Smile SDK to your application page                                                                                   |




---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)
## Event Notifications

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


---
<!-- focus: false -->
![Storage](https://img.icons8.com/?size=50&id=1476&format=png&color=000000)
## Maintaining User Data

User data is stored by Smile API only until one of the following occur:

1. The user revokes access to their data
2. The access is revoked via the Revoke API (i.e. if initiated by the developer)
3. 60 days have passed from account connection

To ensure continued access to the data past the 60-day maximum timeframe, ensure you retrieve and store the user's data in your own servers. You may instruct Smile to revoke the data as soon as you have retrieved it from the Smile servers using the Revoke API. You will also receive an event notification from Smile to notify you when the user has manually revoked the sharing of their data.

### Continuous Data Sync

Smile API's *Continuous Data Sync* (CDS) feature provides you access to the most up-to-date and recent data from your users, once these users have consented and connected their account through the Wink Widget. By consenting to CDS, users can authorize Smile to sync data for you across multiple months, until they revoke access to their account.

Find out more about CDS and enabling CDS in the [Accounts section](/reference/accounts).

### Refreshing a User's Token

You can refresh a user's token by calling the ``/tokens`` endpoint. Simply pass the ``userId`` as a parameter in the query to give the user a new token. More information can be found in the Tokens endpoint documentation.



---
<!-- focus: false -->
![Versioning](https://img.icons8.com/?size=50&id=21889&format=png&color=000000)
## Versioning

**Wink Widget Version 2 contains many user experience and functionality improvements and is the recommended version**.

Version 1 is still maintained and security monitoring, updates, and patches will continue to be done.

| Version | SDK JavaScript Embed |
| --- | --- |
| Version 2 **(recommended)** | `<script src="https://web.smileapi.io/v2/smile.v2.js"></script>` |
| Version 1 | `<script src="https://web.smileapi.io/v1/smile.v1.js"></script>` |
