# Getting Started

<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)

## Integration Steps
Its easy to get started with the Smile API! Implementing the Smile API involves simple client and server-side integration, which are outlined below in five key steps:

1. **Link token:** Your application server sends a request to our REST API to generate a short-lived "Link" token.

2. **Wink Widget:** Using the Link token, your application client initializes the client SDK to launch the Smile "Wink" widget. Your end-users interact with this widget to submit their login credentials to authenticate with their employment data provider over a secure and encrypted connection.

3. **User Creation:** Once the user successfully authenticates via the Smile Wink widget, a user account is created representing the user's authorized access to a specific employment data provider.

4. **Actions:** Our servers execute your application's requests. We read, transform, and temporarily store data from the user's employment data provider so that it can be sent to the client application.

<!--
5. **Webhooks (coming soon):** Webhooks can also be delivered to your server in cases where data will be processed asynchrounously. Messages via webhook will be sent whenever data becomes available or is updated. Your server can then fetch the data from our REST API.
-->

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## Signing up for a Developer Account
To get started, register your application with us by emailing access@getsmileapi.com.

After registration, your application will be assigned an API key and an API secret. The API secret must be kept safe and used only in exchanges between your application's server and Smile API's server.