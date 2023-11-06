---
title: Webhooks
excerpt: ""
category: 6294c0fd9494580032b22740
slug: webhooks
---

## Webhooks

Smile uses webhooks to notify your application in real time when an event happens in our servers that is related to your environment.

Event notifications can be sent when a new user is created, an account is successfully connected, an employment document is uploaded, an invitation is sent, or when new any new type data is added such as a user's identity, income, employment, and others. Check out the list of available events that you can subscribe to in *List of Events*, below. 

These webhooks are sent via a secure channel, using HTTPS from a static IP address, with the data being sent in JSON format. These also come with a signature for you to validate the authenticity of the payload. 

> 📘 Note
> 
> Our static IP address is **18.142.61.230**. You can whitelist this IP address in your back-end to ensure that your application receives event notifications coming from Smile.

Webhooks are particularly useful for getting notifications about asynchronous events, and either executing actions in your backend system when any of these events happen, or knowing when to refresh your front-end system to display any new data.


### Implementation Steps

You can start receiving event notifications in your application using the following steps:

1. Use our documentation and available resources to **identify the events you want to monitor** and the event payloads to parse.
2. **Create a webhook endpoint** as an HTTPS endpoint (URL) on your  server or application. 
3. **Test that your webhook endpoint is working properly.** Make sure that your server or application is able to handle requests from Smile by parsing each event object and returning ``2xx`` response status codes.
4. **Deploy your webhook endpoint** so it's a publicly accessible HTTPS URL.
5. **Register your publicly accessible webhook endpoint** by [making a POST request to the ``/webhooks`` endpoint](/reference/create-webhook). You will need to specify the following:
   - **URL**: the webhook endpoint or URL.
   - **Event types**: the event types you want to monitor, separated by commas (see below for the different event types), or simply use ``ALL_EVENTS`` to get notifications on all event types.
   - **Active**: whether you want this endpoint definition to be active or inactive (you can update this later via an update request)
   - **Secret**: a phrase or value that you can use to validate the authenticity of the payload by digesting the received payload body using HMAC-SHA512, with the secret as the key. See *Validating Payloads*, below.

> 📘 Note
> 
> Below example shows a request using Shell script/cURL with the webhook receiving endpoint set as ``https://webhook.clienturl.xyz``
> 
> ``` curl
> curl --request POST \
>   --url https://sandbox.smileapi.io/v1/webhooks \
>   --header 'Authorization: Basic amFuLnBhYmVsbG9uQHNtaWxlZmluYW5jaWFsLmFwcDpOZXRTdWl0ZTIwMTgh' \
>   --header 'Content-Type: application/json' \
>   --data '{
>   "name": "Event Notification Postback",
>   "url": "https://webhook.clienturl.xyz",
>   "eventTypes": [
>     "ACCOUNT_CONNECTED",
>     "IDENTITY_ADDED"
>   ],
>   "active": true,
>   "secret": "a little secret"
> }'
> ```

### Webhook Retries

To ensure you receive the notification, Smile operates on an "at least once" delivery guarantee.

Smile checks for an HTTP response with status code between 200 and 299 from your endpoint when we send the webhook. In the event that we receive a response outside of 200 - 299, Smile will attempt to resend the webhook up to two times with a few dozen seconds between each retry.

This means that you may receive the same webhook event more than once. Please ensure you process these possible duplicate notifications in your endpoint or application. You can detect duplicate webhook events by comparing the ``id`` value to previous events (see *Example Payloads*, below).


<!-- focus: false -->
![Events](https://img.icons8.com/dotty/50/000000/notification-center.png)


## List of Events 

Below are the events you can subscribe to via webhooks.

| Event                                             | Event Type           | Description                                                                                        |
|---------------------------------------------------|----------------------|----------------------------------------------------------------------------------------------------|
| User Creation Successful                          | USER_CREATED         | Sent when a new user and link token is created.                                                    |
| Account Creation Initiated                        | ACCOUNT_CREATED      | Sent when the account linking process has been initiated by the user.                              |
| Account Connection Successful                     | ACCOUNT_CONNECTED    | Sent when a user successfully connects their work account.                                         |
| Account Disconnection Successful                  | ACCOUNT_DISCONNECTED | Sent when a user disconnects or revokes the link to their work account.                            |
| Account Connection Failed                         | ACCOUNT_FAILED       | Sent when the account linking process is unsuccessful.                                          |
| Task Started                                      | TASK_STARTED         | Sent when the data sync process for a user's account is started.                                 |
| Task Finished                                     | TASK_FINISHED        | Sent when the data sync task process for a user's account is finished.                             |
| Account Sync Task Finished                         | ACCOUNT_SYNC_TASK_FINISHED | Sent when the account syncing process is finished.                                          |
| Archive Creation Successful                       | ARCHIVE_STARTED      | Sent when a user has uploaded one or several files which becomes an "archive" in Smile.            |
| Archive Analysis Successful                       | ARCHIVE_ANALYZED     | Sent when an archive has been analyzed and converted into JSON data automatically via OCR.         |
| Archive Revocation Successful                     | ARCHIVE_REVOKED      | Sent when a user removes permission to access or use an archive.                                   |
| Archive Creation or Analysis Failed               | ARCHIVE_FAILED       | Sent when the the archive creation or analysis process is unsuccessful.                            |
| Invitation Sending Successful                     | INVITE_INVITED       | Sent when an invitation is sent out to a user successfully.                                        |
| Account Link by Invitation Successful             | INVITE_LINKED        | Sent when a user that has been sent an invitation is able to link their work account successfully. |
| Identity Data Added                               | IDENTITY_ADDED       | Sent when identity data about a user is added.                                                     |
| Rating Data Added                                 | RATING_ADDED         | Sent when ratings data about a user is added.                                                      |
| Transactions Data Added                           | TRANSACTIONS_ADDED   | Sent when transactions data shared by a user is added.                                             |
| Documents Data Added                              | DOCUMENTS_ADDED      | Sent when documents data shared by a user is added.                                                |
| Employments Data Added                            | EMPLOYMENTS_ADDED    | Sent when employment data shared by a user is added.                                               |
| Incomes Data Added                                | INCOMES_ADDED        | Sent when income data shared by a user is added.                                                   |
| Estimated Incomes Data Added <br>*(early access)* | EINCOMES_ADDED       | Payload when estimated income data has been derived from data shared by a user.                    |
| Contributions Data Added                          | CONTRIBUTIONS_ADDED  | Sent when social security contributions data shared by a user is added.                            |
| Liabilities Data Added                            | LIABILITIES_ADDED    | Sent when liabilities data shared by a user is added.                                              |
| Insight Data Added                            | INSIGHT_ADDED    | Sent when insights data calculated from shared user data is added. |
| Link Data Added                                   | LINK_ADDED           | Sent when a link is detected after the user has connected their account. |

> 📘 Note
> 
> The following Continuous Data Sync related events are deprecated, please use `ACCOUNT_SYNC_TASK_FINISHED` to track the following events:
> 
> - CONTRIBUTIONS_UPDATED
> - INCOMES_UPDATED
> - DOCUMENTS_UPDATED
> - EMPLOYMENTS_UPDATED
> - EINCOMES_UPDATED
> - LIABILITIES_UPDATED

<!-- focus: false -->
![Payload](https://img.icons8.com/ios/50/000000/json-download.png)

## Example Payloads

### Users

#### User Created
Payload when a new user and link token is created
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

### Accounts

#### Account Created

Payload when the account linking process has been initiated by the user. This webhook will be fired even for providers who do not require logins.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_CREATED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Account Connected
Payload when a user successfully connects his/her work account.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_CONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "loginName": "userLoginName",
    "providers": [
      "abccorp"
    ]
  }
}
```
#### Account Disconnected
Payload when a user disconnects or revokes the link to his/her work account.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_DISCONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```
#### Account Failed
Payload when the account linking process is unsuccessful.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "loginName": "userLoginName",
    "errorCode": "INVALID_CREDENTIALS",
    "errorMessage": "Invalid username or password!",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Task Started
Sent when the data sync process for a user's account is started.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TASK_STARTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ]
  }
}
```
#### Task Finished
Sent when the data sync task process for a user's account is finished.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TASK_FINISHED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ],
    "datapoints": [
      "IDENTITIES",
      "INCOMES"
    ]
  }
}
```

#### Account Sync Task Finished
Sent when the account syncing process is finished.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_SYNC_TASK_FINISHED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ],
    "status": "SUCCEEDED",
    "monitorStatus": "ACTIVE",
    "dataPoints": [
      "IDENTITIES",
      "EMPLOYMENTS",
      "INCOMES"
    ]
  }
}
```

### Archives

#### Archive Started
Payload when a user has uploaded one or several files which becomes an "archive" in Smile.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_STARTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "archive-123abc456def789abc123def456abc78"
  }
}
```

#### Archive Analyzed
Payload when an archive has been analyzed and converted into JSON data automatically via OCR.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_ANALYZED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "archive-123abc456def789abc123def456abc78"
  }
}
```


#### Archive Revoked
Payload when user removes permission to access or use an archive.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_REVOKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "archive-123abc456def789abc123def456abc78"
  }
}
```

#### Archive Failed
Payload when the the archive creation or analysis process is unsuccessful.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "archive-123abc456def789abc123def456abc78",
    "errorCode": "FILE_UNABLE_TO_RECOGNIZE",
    "errorMessage": "Invalid file!"
  }
}
```

### Invitations

#### Invitations Sent
Payload when an invitation is sent out to a user successfully.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_INVITED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```

#### Account Linked by Invitation
Payload when the a user that has been sent an invitation is able to link his or her work account successfully.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_LINKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```

### User Data

#### Identity Added
Payload when identity data about a user is added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "IDENTITY_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "identityId": "i-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Rating Added
Payload when ratings data about a user is added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "RATING_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "ratingId": "r-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Transactions Added
Payload when transactions data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TRANSACTIONS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Documents Added
Payload when documents data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "DOCUMENTS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Employments Added
Payload when employments data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "EMPLOYMENTS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Incomes Added
Payload when income data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Contributions Added
Payload when contributions data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "CONTRIBUTIONS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Liabilities Added
Payload when liabilities data shared by a user are added.
```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LIABILITIES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

### User Insights Data

#### Estimated Incomes Added (early access)

Payload when estimated income data has been derived from data shared by a user.
```json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "EINCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0,
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Insight Added

Payload when insight data has been derived from data shared by a user.
```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INSIGHT_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "id": "insight-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### Link Added

Payload when link data has been derived from data shared by a user.
```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LINK_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "id": "link-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

<!-- focus: false -->
![Signatures](https://img.icons8.com/ios/50/000000/signature.png)


## Validating Payloads

When events are sent from Smile, you might want to validate the authenticity of the webhook payload, to make sure it came from Smile. You can do that by using the signature, which is included in the headers of each payload. 

> 📘 Note
> 
> To validate the authenticity of the payload, you need to get the entirety of the payload body and digest it using HMAC-SHA512, with the "secret" you defined when you registered your endpoint as the key.

Below is example to check the validity of a payload using HMAC-SHA512:

- NodeJs
    ``` javascript
    const http = require('http');
    const crypto = require('crypto');
    const serverPort = 80
    const requestListener = function (req, res) {
      // the client secret is being configured when a webhook is created
      const client_secret = 'a little secret';
      var requestBody = '';
      req.on('readable', () => {
        var read = req.read()
        if(read != null) {
        requestBody += read;
        }
      });
      req.on('end', () => {
        jsonBody = JSON.stringify(requestBody);
        // do whatever you need with jsonBody, however use requestBody in the signature payload
        signature = crypto.createHmac('sha512',client_secret).update(requestBody).digest('hex');
      console.log('Signature:' + signature);
      res.writeHead(200);
      res.end(signature);
      })
    }
    const server = http.createServer(requestListener);
    server.listen(serverPort);
    ```
- JAVA
    ``` Java
    package com.smile.webhook;
    
    import java.io.BufferedReader;
    import java.io.IOException;
    import java.util.Objects;
    import javax.crypto.Mac;
    import javax.crypto.SecretKey;
    import javax.crypto.spec.SecretKeySpec;
    import javax.servlet.http.HttpServletRequest;
    import org.apache.commons.codec.binary.Hex;
    
    public class VerifySignatureUtil {
    
        public static boolean verifySignature(HttpServletRequest request) throws IOException {
            String data = getRequestBody(request);
            String secret = "<your secret>";
            String signature = request.getHeader("Smile-Signature");
            boolean result = Objects.equals(signature, generateSignature(secret, data));
            System.out.println("verify result:" + result);
            return result;
        }
    
        private static String getRequestBody(HttpServletRequest request) throws IOException {
            if (request.getMethod().equals("POST")) {
                StringBuilder sb = new StringBuilder();
    
                try (BufferedReader bufferedReader = request.getReader()) {
                    char[] charBuffer = new char[128];
                    int bytesRead;
                    while ((bytesRead = bufferedReader.read(charBuffer)) != -1) {
                        sb.append(charBuffer, 0, bytesRead);
                    }
                }
    
                return sb.toString();
            }
            return "";
        }
    
        private static String generateSignature(String secret, String requestBody) {
            byte[] key= secret.getBytes();
            byte[] content= requestBody.getBytes();
            String signature = null;
            try {
                SecretKey secretKey = new SecretKeySpec(key, "HmacSHA512");
                Mac mac = Mac.getInstance("HmacSHA512");
                mac.init(secretKey);
                byte[] bytes = mac.doFinal(content);
                signature = Hex.encodeHexString(bytes);
            } catch (Exception var6) {
                throw new RuntimeException(var6);
            }
            System.out.println("signature=" + signature);
            return signature;
        }
    
    }
    ```

If your digest matches the one that you received as the payload signature in the headers, then the payload is valid and authentic.

> 🚧 Warning
> 
> When you validate the payload, make sure you digest the entire payload. Do not include extra spaces before or after it. Do not pre-parse or reformat it before doing the validation check.


