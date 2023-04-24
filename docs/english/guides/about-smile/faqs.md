---
title: FAQs
excerpt: ""  
category: 621596fd02cd9f004704ba75  
slug: faqs
---

## Security and Privacy

### How do you secure your API?

All data from Smile API is encrypted at RSA 4096 with SHA-256 signing for maximum security. Additionally, Smile does not store end-user credentials at any point: we pass these directly to the data source's servers via TLS to initiate the process of information sharing.

### Is your API compliant with the data privacy act?

Smile believes in the sanctity of one's privacy and that our users are the owners of their personal data, and should always be in full control when and to whom they share their data. Smile seeks to comply with all local laws around data privacy. In the Philippines, we comply with the Data Privacy Act of 2012 (RA 10173) and we help users exercise their right to Data Portability under Section 18 of the [Philippine Data Privacy Act](https://www.privacy.gov.ph/data-privacy-act/#18).

Sharing users' data with our clients is done provided on a revocation-based model: only via explicit consent of the user via our SDK. Users can, at any point, revoke access to their data through this same means, making sure they are in full control when and to whom they share their own data.

All information is deleted and irretrievable once users have revoked access. Any other data is retained for 60 days, after which all personal data is anonymized.

We also maintain a Privacy Policy so you can be sure how your data is being used.

## Managing User Data with Smile

### Do I need to store any user data on my servers?

We recommend you store the Smile user ID as part of your own user data in order to connect your user with the Smile user on the Smile system. This is typically in the format `tenantId-123abc456def789abc123def456abc78`.

After the user has been created on the Smile System, subsequent calls to load the Wink Widget should provide this user ID to maintain the data on your end.

Listening to the `ACCOUNT_DISCONNECTED` webhook will also inform you of when the user has revoked access to their data, after which you may safely remove the Smile user ID from your system.

## Using the Smile API

### What data sources are available?

We have a wide range of data sources available for users to connect to, from social security institutions as well as various salary and gig platforms.

To see our full list of data sources, you can get [free access to our developer portal](https://portal.getsmileapi.com/register) and test our platform out for yourself. You may also [book a call with us](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) to find out more.

### Do you provide a sandbox account for testing?

Yes! Feel free to [sign up for our developer portal](https://portal.getsmileapi.com/register) and play around with our available sandbox environment. Immediately, you'll gain access to the following:

- a testable sandbox widget do you can see what customers will see
- sandbox API keys for testing on your own environment
- credentials for test users so you can run tests on your environment or on the developer portal Wink Widget

To gain access to live data, [book a call with us](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) to enable it for your account.

### Can we get some sample JSON output from your API?

There are multiple ways to go about getting sample JSON output from our API:

1. **Use our free Developer Portal to load user data.**  
   Each connected user on the developer portal (even sandbox users) will have a JSON mode toggle so you can see the actual response from our server.  
   ![](https://files.readme.io/7cc555c-devportal-jsonmode.png)

2. **Our API Reference contains an API Explorer for you to test out API calls on the fly.**  
   Using your API and Secret from the Developer Portal, you can also execute calls against our API using the API Explorer feature on our API Reference.  
   ![](https://files.readme.io/5d046be-reference-explorer.png)

### How do we get access to live data?

Live data requires access to Production Mode so you may connect real accounts. While production mode connected users are chargeable to your account, [contact us](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) to enable it or obtain free credits if you're looking to test out our platform.

### How scalable is your API?

Smile limits the amount of API calls that can be made to each endpoint to ensure the stability and availability of the platform for all users. At the moment we only allow clients a maximum of up to 20 requests per second per IP address across all API endpoints. Automatic expansion mechanisms and load balancing assure that service uptime is maintained.

### How do you handle versioning of your API?

The versioning convention we use is the 1.2.3 format, where 1 is the major version (which denotes breaking changes to the API), 2 is the minor version, and 3 is the patch update. The latter two versions are transparent to API users, and will not require an implementation update when these changes are released.

The version is included in the URI Path for ease of calling. So for example, version 1 of the Smile API will look like `<https://open.smileapi.io/v1`>

### Can we get free credits to try live data on our account?

[Book a call with us](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) to find out how to gain free credits for production mode on your account.

### Does Smile charge per API request?

No, we only charge you based on the number of connected accounts. You can send multiple requests to the same API endpoints without any impact on your bill. Keep in mind, however, that we have a 20 requests per second rate limit. Talk to us if your use case requires a higher rate.

### What is the difference between Production Mode and Sandbox Mode?

Use Sandbox Mode if you need to test how the SDK works and during development. Sandbox Mode includes test accounts you can use that return you data for development and testing purposes. These do not connect to our partner data sources, so you can freely test out the system.

Production Mode, on the other hand, will return only Live data. Production Mode connects to live production environments of our data sources, and as such, requires actual accounts from actual people.