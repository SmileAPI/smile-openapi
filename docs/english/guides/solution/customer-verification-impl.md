---
title: Implementation & Go-Live  
excerpt: ""  
category: 638fff38b56c92003c1a1e55  
slug: customer-verification-implementation
---

![](https://files.readme.io/62a894c-image.png)

To successfully integrate Smile into your process, we suggest doing so through 3 steps:

- Requirements gathering - explore your use case and what do you want to achieve with Smile data
- [Design](/docs/customer-verification-design) - design your user journey and integration with Smile.
- Implementation & Go-Live (this guide) - detailed steps to set up and get the integration launched

***



# Step 1: Implement Smile Wink

If you want the users to connect their employment accounts while they are on your website or app, you need to integrate the Smile Wink Widget. See below an example configuration to start:

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * The Link API URI. Note: Sandbox and Production modes use different API URIs.
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * User token(link token) passed from your backend service which is obtained from the Smile API.
             */
            userToken: '<usertoken>',

            /**
             * Use provider id to promote certain providers to the top of the list. Example ['upwork', 'freelancer']
             */
            topProviders: [],

            /**
             * Use provider id to show only select providers in the widget. Example ['upwork', 'freelancer']
             */
            providers: [],

            /**
             * Set enableSearchBar to false if you wish to hide the providers search bar.
             * Default: true
             */
            enableSearchBar: true,

            /**
             * Set enableTypeBar to false if you wish to hide the provider types filter.
             * Default: true
             */
            enableTypeBar: true,

            /**
             * Enable or disable file uploads.
             */
            enableUpload: true,           

            /**
             * Set to your company name if you wish your company name to be reflected on the Consent and Login screens.
             * Default: empty
             */
            companyName: "",

            /**
             * Account login callback.
             */
            onAccountCreated: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account created: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Account login success callback.
             */
            onAccountConnected: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account connected: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Account revoke callback.
             */
            onAccountRemoved: ({
                accountId,
                userId,
                providerId
            }) => {
                console.log('Account removed: ', accountId, ' User ID:', userId, ' Provider ID:', providerId)
            },

            /**
             * Token expired callback.
             */
            onTokenExpired: () => {
                console.log('Token expired');
            },

            /**
             * Smile link SDK close callback.
             */
            onClose: () => {
                console.log('Widget closed')
            },

            /**
             * Account connection error callback.
               Where errorCode is from the account connection errorCode in https://docs.getsmileapi.com/reference/get-account-1.
               Example.
                    ACCOUNT_DISABLED 
                    ACCOUNT_INACCESSIBLE 
                    ACCOUNT_INCOMPLETE 
                    ACCOUNT_LOCKED 
                    AUTH_REQUIRED 
                    EXPIRED_CREDENTIALS 
                    INVALID_ACCOUNT_TYPE 
                    INVALID_AUTH 
                    INVALID_CREDENTIALS 
                    INVALID_MFA MFA_TIMEOUT 
                    SERVICE_UNAVAILABLE SYSTEM_ERROR 
                    TOS_REQUIRED 
                    UNSUPPORTED_AUTH_TYPE 
                    UNSUPPORTED_MFA_METHOD
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
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```



Notice that the `apiHost` configuration parameter in the example code points to `https://link-sandbox.smileapi.io/v1`. This ensures that the plugin starts in a sandbox environment (the Sandbox Mode) where you can use the sandbox test credentials shown below to test the implementation.

## User tokens (Link tokens)

User tokens are temporary (expires in 5 hours) access keys that allow you to start the Smile Linking process.

**Link initialization for new user :**

1. Create a new Smile user by calling the `/users` endpoint with metadata, such as your user identifier in your product/system. You will receive a Smile `userId`. We recommend storing this Smile `userId` in your system for future reference and use
2. Create a new user token by calling the [`/tokens` endpoint](https://docs.getsmileapi.com/reference/tokens) with their `userId`. You will receive their `userToken`
3. Provide the `userToken` in your Smile Wink initialization. Make sure the user tokens are requested server-side and your `client_id` and `client_secret` are never exposed on the front-end.

**Link initialization for a returning user or for refreshing the Link token**

1. Obtain a new user token by calling the [`/tokens` endpoint ](https://docs.getsmileapi.com/reference/tokens)with their `userId` that you have previously stored.
2. Provide the `userToken` in your Smile Wink initialization. Make sure user tokens are requested server-side and your `client_id` and `client_secret` are never exposed on the front-end.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="icon" href="smileicon32.webp" sizes="32x32">
    <link rel="icon" href="smileicon192.webp" sizes="192x192">
    <title>Smile Wink</title>
</head>

<body>
    <script src="https://web.smileapi.io/v2/smile.v2.js"></script>
    <script type="text/javascript">
        const smileLinkModal = new SmileLinkModal({
            /**
             * The Link API URI. Note: Sandbox and Production modes use different API URIs.
             */
            apiHost: 'https://link-sandbox.smileapi.io/v1',

            /**
             * User token passed from your backend service which is obtained from the Smile API.
             */
            userToken: '<usertoken>', // Put your user token here.

            // .....
        });
        smileLinkModal.open()
    </script>
</body>

</html>
```



# Step 2: Connect test accounts

To use the Sandbox, you can use the following example credentials:

| User Name | Full Name           | Email                     | Mobile Phone     | Password | Verification Code |
| --------- | ------------------- | ------------------------- | ---------------- | -------- | ----------------- |
| George    | George Palomero Jr. | gpalomero1234@smileapi.io | (+63) 9559991234 | 123456   | 1234              |
| Ryan      | Ryan Ng             | ryan1234@smileapi.io      | (+62) 8119994321 | 654321   | 1234              |
| Christina | Christina Tan       | christina4321@smileapi.io | (+65) 99996789   | YGUS1    | 1234              |
| Anisha    | Anisha Bhatia       | anisha98765@smileapi.io   | (+91) 9511198765 | 123456   | 1234              |

Before proceeding to the next step, make sure to test your implementation. Click on one of the providers on the provider list, and use one of the sandbox credentials to connect the selected provider.

# Step 3: Retrieve identity, employment and contribution data

For personal information verification, fetch the following fields from the `/identities` endpoint:

- First name
- Last name
- Primary address

Issue a GET request to Smile OpenAPI:

```curl
GET https://https://open-sandbox.smileapi.io/v1/identities?sourceId=<accountId>

# insert your user's accountId in the request.
# this example uses the sandbox mode. Don't forget to switch to the production mode if you are testing in production.

```



Here is an example response:

```json
{
  "id": "i-123abc456def789abc123def456abc78",
  "fullName": "George Cimafranca Palomero, Jr",
  "firstName": "George",
  "middleName": "Cimafranca",
  "lastName": "Palomero",
  "suffix": "Jr",
  "gender": "Male",
  "dob": "1970-08-24",
  "maritalStatus": "Married",
  "countryResidence": "PH",
  "citizenship": "Citizen",
  "photoUrl": "https://cdn.smileapi.io/image/avatar/v20211115191600/george.jpg",
  "referenceId": null,
  "profileUrl": null,
  "emails": [
    {
      "address": "gpalomero1234@smileapi.io",
      "type": "Primary"
    }
  ],
  "phones": [
    {
      "number": "+639559991234",
      "type": "Mobile"
    }
  ],
  "socialProfiles": [
    {
      "socialUrl": "https://www.facebook.com/gpalomero1234",
      "type": "Facebook"
    }
  ],
  "addresses": [
    {
      "fullAddress": "12 Maybunga St, Barangay Paraiso, Pasig City, NCR, 1600, PH",
      "line1": "12 Maybunga St",
      "line2": "Barangay Paraiso",
      "city": "Pasig City",
      "region": "NCR",
      "zip": "1600",
      "country": "PH",
      "latitude": "14.573454",
      "longitude": "121.085042",
      "type": "Primary"
    }
  ],
  "metadata": {
    "createdAt": "2022-08-19T07:29:08Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```



For employment information verification, fetch the following fields from the `/employments` endpoint:

- Employer name
- Job title
- Start date
- End date

Issue a GET request to Smile OpenAPI:

```curl
GET https://https://open-sandbox.smileapi.io/v1/employments?sourceId=<accountId>
curl --request GET \
     --url 'https://sandbox.smileapi.io/v1/identities?size=10&sourceId=<accountId>' \
     --header 'accept: application/json' \
     --header 'authorization: Basic <authorization>'
# insert your user's accountId in the request.
# this example uses the sandbox mode. Don't forget to switch to the production mode if you are testing in production.

```



Here is an example response:

```json
[{
    "id": "e-123abc456def789abc123def456abc78",
    "startDate": "2022-07-01",
    "name": "Security",
    "description": null,
    "jobTitle": "Security Guard",
    "department": null,
    "employeeNumber": "EMP-123456",
    "employer": "ABC Corporation",
    "status": "Permanent",
    "endDate": "2022-07-31",
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "e-123abc456def789abc123def456abc78",
    "startDate": "2022-06-01",
    "name": "Security",
    "description": null,
    "jobTitle": "Security Guard",
    "department": null,
    "employeeNumber": "CDE-98765",
    "employer": "CDE Corporation",
    "status": "Permanent",
    "endDate": "2022-06-30",
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "cdecorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```



For contribution information verification, fetch the following fields from the `/contributions` endpoint:

- Employer name
- Job title
- Start date
- End date

Issue a GET request to Smile OpenAPI:

```curl
GET https://https://open-sandbox.smileapi.io/v1/employments?sourceId=<accountId>

# insert your user's accountId in the request.
# this example uses the sandbox mode. Don't forget to switch to the production mode if you are testing in production.

```



Here is an example response:

```json
[{
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-06-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-05-31",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-04-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```



For additional data fields, please refer to the [Smile API reference](https://docs.getsmileapi.com/reference/chapter-1).

# Step 4: Setup webhooks

To receive regular updates on a user's accounts, identity, contribution and employment data, subscribe to [webhooks](https://docs.getsmileapi.com/reference/chapter-5).

![](https://files.readme.io/79ad8de-image.png)

Webhooks send notifications to your system every time something occurs, i.e., when an account is connected, removed, or updated.

To monitor changes to identity, contribution and employment data, Smile recommends subscribing to the following webhook events, then call the Smile OpenAPI to retrieve data accordingly.

| Event         | Event Type    | Description                                                                                                       |
| ------------- | ------------- | ----------------------------------------------------------------------------------------------------------------- |
| Task Started  | TASK_STARTED  | Sent when the data sync process for a user's account is started.                                                  |
| Task Finished | TASK_FINISHED | Sent when the data sync task process for a user's account is finished, contains which datapoints have been synced |

Or you can subscribe to dedicated datapoint related events

| Event                        | Event Type          | Description                                                                     |
| ---------------------------- | ------------------- | ------------------------------------------------------------------------------- |
| Contributions Data Added     | CONTRIBUTIONS_ADDED | Sent when social security contributions data shared by a user is added.         |
| Estimated Incomes Data Added | EINCOMES_ADDED      | Payload when estimated income data has been derived from data shared by a user. |
| Transactions Data Added      | TRANSACTIONS_ADDED  | Sent when transactions data shared by a user is added.                          |
| ...                          | ...                 | ...                                                                             |

# Step 5: Go live and scale

After a successful implementation and multiple successful tests in Sandbox Mode, you can switch to the Production mode for your launch.

### Change the apiHost

Firstly, change the `apiHost` in your Wink configuration from:

`https://link-sandbox.smileapi.io/v1`

to:

`https://link.smileapi.io/v1`

The same logic applies to any Open API requests that you have previously used, so `/employments` for example:

`GET https://open-sandbox.smileapi.io/v1/employments?sourceId={accountId}`

change to:

`GET https://open.smileapi.io/v1/employments?sourceId={accountId}`

## Change the API Key pair

The API Key pair can be found in the API Keys section of the [Developer Portal](https://portal.getsmileapi.com) . Use a production key when switching to Production Mode.

## Start slow

For your first Production accounts, you can test on yourself with your own accounts, or create an account with a freelance gig platform (i.e. Upwork) and connect that account.

## Launch and scale

After testing with your personal accounts, you can test with your real users. We recommend starting with a small subset of your users to make sure that everything is working as expected. Then, advance the subset gradually to your full user base.
