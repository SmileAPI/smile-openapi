# Getting User Data 

Getting user data into your application involves two things:

 - **Embedding a Javascript SDK for your web application client**. At the moment, Smile only provides a Javascript SDK, but native verions of the SDK for mobile applications such as iOS or Android are coming soon. The Javascript SDK launches a modal window called a "Wink" web widget where users can provide permission for Smile to access their data. Users will first find their employer or employment data provider, then submit their login credentials over a secure and encrypted connection. By using the SDK, you will not have to worry about the different authentication and verification implementations of the different employment platforms, making the integration simple for your developers, and the experience smooth for your users. 

 - **Obtaining a user token from the Smile Open API**. Your back-end server should obtain a "Link" token  from the /users endpoint. This is a single use, short-lived token which is used to initialize the Wink widget. Your server should generate a new Link token each time you wish to launch the widget.

---
<!-- focus: false -->
![Code](https://img.icons8.com/ios/50/000000/code.png)

## Example Code
Below is sample HTML code which embeds the Wink Javascript SDK:

```
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
    <script src="https://web.smileapi.io/v1/smile.v1.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * The Link API URI. Note: Sandbox and Production modes are using different API URIs.
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',
            /**
             * User token passed from your backend service which is obtained from the Smile API.
             */
            userToken: '<usertoken>',
            /**
            * Use provider id to filter provider list. Example ['upwork', 'freelancer']
            */
            providers: [],

            onAccountCreated: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountConnected: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onAccountRemoved: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            onClose: () => {
                console.log('Widget closed')
            },

            onTokenExpired: updateToken => {
                console.log('Token expired');
            }
        });
        smileLinkModal.open()
    </script>
</body>

</html>

```
---
<!-- focus: false -->
![Settings](https://img.icons8.com/material-outlined/60/000000/settings-3--v1.png)

## Configuration parameters

| Parameter |Value |
|----------|---------|
| apiHost | https://link-sandbox.smileapi.io/v1 for Sandbox |
|         | https://link.smileapi.io/v1 for Production |
| userToken | The user token returned from Smile using the /users endpoint (see documentation on Users endpoint) |
| providers | Pass a list of providers using their provider id (see documentation on Providers endpoint) to pre-filter the list of providers in the Wink widget. Passing just one provider id will skip the selection list and take the user immediately to the authentication screen. |

---
<!-- focus: false -->
![Token](https://img.icons8.com/ios/50/000000/sms-token.png)

## Refreshing a User's Token
You can refresh a user's token by calling the /tokens endpoint. Simply pass the userId as a parameter in the query to give the user a new token. More information can be found in the Tokens endpoint documentation.

---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)

## Link events 
As the user moves through the Wink widget screen, any activities performed by the user are captured and are etiher used to update the messsages and presentation of the modal window, or are sent to Smile so that any account-related data can be updated. 

In the case of the latter, if the the user was able to successfully authenticate with an employment data provider, the Account status is changed to "CONNECTED". The account status of the user can be queried at any time via the /accounts endpoint. Examples of the events captured include:

| Event |Description |
|----------|---------|
| PENDING | The account was created but is pending successful authentication |
| AWAITING_MFA | The user was able to successfully authenticate however the data provider is waiting for the user to enter their verification code in a 2-factor authentication scenario. |
| ERROR | The data provider returned an error. The user may not have entered the wrong credentials or there was a problem on the side of the provider. |
| CONNECTED | The user was able to successfully authenticate with an employment data provider. |


---
<!-- focus: false -->
![Testing](https://img.icons8.com/material-outlined/50/000000/test-tube.png)

## Testing in Sandbox

Smile provides a Sandbox mode for our production environment to allow you to test your integration with sample data.

To use the Sandbox, you can use the following example credentials:

| Name | Email | Mobile Phone | Password | Verification Code |
|---|---|---|---|---|
| George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456 | 1234|
| Ryan Ng | ryan1234@smileapi.io |  (+62) 8119994321 | 654321 | 1234 |
| Christina Tan | christina4321@smileapi.io |  (+65) 99996789 | YGUS1 | 1234 |
| Anisha Bhatia | anisha98765@smileapi.io |  (+91) 9511198765 | 123456 | 1234 |
