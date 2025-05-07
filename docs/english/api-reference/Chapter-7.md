---
title: Form Processing
excerpt: ''
category: 6215975992e4610014e7b757
slug: chapter-7
---

**Smile Flip** is a powerful, flexible, no-code user journey builder designed to help you quickly transform your old manual paper-based forms into a digital form your users can access anywhere to share their data securely with your organization.

Using the intuitive UI within the Developer Portal, you can easily design your user journey from scratch by adding screens or pages for each step of the journey. This enables you to accept data directly from your users for ingestion along with any other shared information via the Wink Widget. A powerful routing feature allows you to direct users to specific screens based on their inputs and the form state, allowing you control over the user journey.

*Smile Flip is currently in Alpha.*

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)
## Integration Steps

While Smile's Form Processing service allows you to design your user journey and publish it without any coding required, it is flexible enough to also allow you to easily drop it into existing systems and retrieve the data for seamless inclusion into your own network with a few technical steps.

### No-Code Solution

These are the following steps to get started quickly with Smile Flip without any coding required:

1. **Create a Flip Site within the Smile Developer Portal**

    > Log into your Smile Developer Portal account and create your Flip Site. Each newly-created Flip Site has an initial screen already available that you can modify or delete as you require. You may do the following:
    > 1. Add, edit, or delete screens for each step in your user journey:
    >     - Form Screens allow you to add any number of form fields to obtain data directly from your user.
    >     - Wink Screens allow you to embed any number of Wink widgets directly within the user journey.
    > 2. Add. edit, or delete form fields within the Form Screen.
    > 3. Direct users to different screens based on their inputs.
    > 4. Specify what happens after the user finishes all the screens in the Flip Site.

2. **Save and publish your Flip Site and provide access to your users**

    > After you have finished configuring the Flip Site, you may click on the Copy URL button to copy the Flip Site URL to your keyboard. You can use this URL directly and share it to users for them to start submitting their applications or information to you.
    >
    > Popular next steps to share this information without any coding required is to use a QR code to direct the users to the Flip Site on demand.

3. **Retrieve the user data**

    > Once users have accomplished the Flip Site form, you may access their data easily via the Developer Portal within 60 days. You may view online or download their responses for offline storage.

### Systems Integration

Smile's User Journey and Form Processing tool also allows you more freedom in embedding the user journey and retrieving the data depending on your organization's technical capabilities.

- **Embed the Flip Site** - You can embed the Flip Site into your app or your website to provide a seamless journey for your app or website users. Show the Flip Site in an embedded frame on a click of a button or link, and return to your website or app seamlessly after the last screen submission.
- **Retrieve the User Data via API** - You can retrieve the User Data directly from the Smile Open API using the ``/forms`` endpoint.
- **Attach a unique ID to your User Data** - Each accomplished form is attached to a unique Smile User ID that you can store in your system so you can go back to retrieve their form data anytime. You can also pass in your own system's Unique ID through pass-through variables to easily connect it to your user at a later date.

<!-- focus: false -->
<!-- ![Quickstart](https://img.icons8.com/ios/50/000000/speed.png) -->
<!-- ## Quickstart / How to Set Up -->

<!-- focus: false -->
<!-- ![User Data](https://img.icons8.com/?size=50&id=FD1d9t9lMoS2&format=png&color=000000) -->
<!-- ## Getting User Data -->

<!-- focus: false -->
<!-- ![Settings](https://img.icons8.com/material-outlined/50/000000/settings-3--v1.png) -->
<!-- ## Configuration -->

<!-- focus: false -->
<!-- ![Event](https://img.icons8.com/ios/50/000000/important-event.png) -->
<!-- ## Event Notifications -->

---
<!-- focus: false -->
![Storage](https://img.icons8.com/?size=50&id=1476&format=png&color=000000)
## Maintaining User Data

User data is stored by Smile API only until one of the following occur:

1. The user revokes access to their data via the Wink Widget
2. The access is revoked via the Revoke API (i.e. if initiated by the developer)
3. 60 days have passed from document upload

To ensure continued access to the data past the 60-day maximum timeframe, ensure you retrieve and store the user's data in your own servers. You may instruct Smile to delete the data as soon as you have retrieved it from the Smile servers using the Revoke API. You will also receive an event notification from Smile to notify you when the user has manually revoked the sharing of their data.

---
<!-- focus: false -->
![Versioning](https://img.icons8.com/?size=50&id=21889&format=png&color=000000)
## Versioning

**Flip Site's current version in Alpha cotains many user experience and functionality improvements and is the recommended version**.

The initial version of the renamed Flip Site is the Wink Site, the last maintained version of which is Version 2 and allows customization of a landing and result page before and after the Wink widget is displayed to the user.

Wink Site v2 is still maintained and security monitoring, updates, and patches will continue to be done.
