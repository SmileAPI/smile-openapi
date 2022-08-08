---
title: Event Notifications
excerpt: ''
category: 6215975992e4610014e7b757
slug: chapter-5
---



<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks


Smile uses webhooks to notify your application in real time when an event happens in your environment. These are sent via a secure channel, using HTTPS with the data being sent in JSON format. These are sent via a static IP address, and also come with a signature for you to validate the authenticy of the payload. 

> 📘 Note
> 
> Our static IP address is **18.142.61.230**. You can whitelist this IP address in your back-end to ensure that your application receives event notifications coming from Smile.

Webhooks are particularly useful for getting notifications on asynchronous events, executing actions in your backend system when any of these events happen, or knowing when to refresh your front-end system to display any new data. Event notifications can be sent when a new user is created, an account is successfully connected, an employment document is uploaded, an invitation is sent, or when new any new type data is added such as a user's identity, income, employment, document, ratings, transaction, or contribution.


**Implementation Steps**

You can start receiving event notifications in your application using the following steps:

1. Use our documentation and available resources to identify the events you want to monitor and the event payloads to parse.
2. Create a webhook endpoint as an HTTPS endpoint (URL) on your  server or application. 
3. Test that your webhook endpoint is working properly. Make sure that your server or application is able to handle requests from Smile by parsing each event object and returning 2xx response status codes.
4. Deploy your webhook endpoint so it’s a publicly accessible HTTPS URL.
5. Register your publicly accessible webhook endpoint by making a request to the /webhooks endpoint. You will need to specify the:
   - URL: the webhook endpoint or URL.
   - Event types: the event types you want to monitor separated by commas (see below for the different event types), or simply use "ALL_EVENTS" to get notifications on all event types.
   - Active: whether you want this endpoint definition to be active or inactive (you can update this later via an update request)
   - Secret: a phrase or value that you can use to validate the authenticity of the payload by digesting the received payload body bnd y using HMAC-SHA512, with the secret as key

> 📘 Note
> 
> Below example shows a request using Shell script/cURL with the webhook receiving endpoint set as "https://webhook.clienturl.xyz"

``` curl
curl --request POST \
  --url https://sandbox.smileapi.io/v1/webhooks \
  --header 'Authorization: Basic amFuLnBhYmVsbG9uQHNtaWxlZmluYW5jaWFsLmFwcDpOZXRTdWl0ZTIwMTgh' \
  --header 'Content-Type: application/json' \
  --data '{
  "name": "Event Notification Postback",
  "url": "https://webhook.clienturl.xyz",
  "eventTypes": [
    "ACCOUNT_CONNECTED",
    "IDENTITY_ADDED"
  ],
  "active": true,
  "secret": "a little secret"
}'
```


<!-- focus: false -->
![Events](https://img.icons8.com/dotty/50/000000/notification-center.png)


## Example Events 
Below are the example events you can subscribe to via webhooks:

|Event|Event Type|Description|
|---|---|---|
|User Creation Successful|USER_CREATED|Sent when a new user and link token is created.|
|Account Connection Successful|ACCOUNT_CONNECTED|Sent when a user successfully connects his/her work account.|
|Account Disconnection Successful|ACCOUNT_DISCONNECTED|Sent when a user disconnects or revokes the link to his/her work account.|
|Account Connection Failed|ACCOUNT_FAILED|Sent when the account linking process is is unsuccessful.|
|Archive Creation Successful|ARCHIVE_STARTED|Sent when a user has uploaded one or several files which becomes an "archive" in Smile.|
|Archive Analysis Successful|ACCOUNT_ANALYZED|Sent when an archive has been analyzed and converted into JSON data automatically via OCR.|
|Archive Revocation Successful|ARCHIVE_REVOKED|Sent when user removes permission to access or use an archive.|
|Archive Creation or Analysis Failed|ARCHIVE_FAILED|Sent when the the archive creation or analysis process is unsuccessful.|
|Invitation Sending Successful|INVITE_INVITED|Sent when an invitation is sent out to a user successfully.|
|Account Link by Invitation Successful|INVITE_LINKED|Sent when the a user that has been sent an invitation is able to link his or her work account successfully.|
|Identity Data Added|IDENTITY_ADDED|Sent when identity data about a user is added.|
|Rating Data Added|RATING_ADDED|Sent when rating data about a user is added.|
|Transactions Data Added|TRANSACTIONS_ADDED|Sent when transactions data shared by a user are added.|
|Documents Data Added|DOCUMENTS_ADDED|Sent when documents data shared by a user are added.|
|Employments Data Added|EMPLOYMENTS_ADDED|Sent when employment data shared by a user are added.|
|Incomes Data Added|INCOMES_ADDED|Sent when income data shared by a user are added.|
|Contributions Data Added|CONTRIBUTIONS_ADDED|Sent when social security contributions data shared by a user are added.|


<!-- focus: false -->
![Payload](https://img.icons8.com/ios/50/000000/json-download.png)

## Example Payloads

### Users

#### User Created
Payload when a new user and link token is created
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "USER_CREATED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string"
  }
}
```

### Accounts

#### Account Connected
Payload when a user successfully connects his/her work account.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ACCOUNT_CONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "loginName": "string"
  }
}
```
#### Account Disconnected
Payload when a user disconnects or revokes the link to his/her work account.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ACCOUNT_DISCONNECTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string"
  }
}
```
#### Account Failed
Payload when the account linking process is unsuccessful.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ACCOUNT_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "loginName": "string",
    "errorCode": "string",
    "errorMessage": "string",
    "providers": [
      "string"
    ]
  }
}
```

### Archives

#### Archive Started
Payload when a user has uploaded one or several files which becomes an "archive" in Smile.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ARCHIVE_STARTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "archiveId": "string"
  }
}
```

#### Archive Analyzed
Payload when an archive has been analyzed and converted into JSON data automatically via OCR.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ARCHIVE_ANALYZED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "archiveId": "string"
  }
}
```


#### Archive Revoked
Payload when user removes permission to access or use an archive.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ARCHIVE_REVOKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "archiveId": "string"
  }
}
```

#### Archive Failed
Payload when the the archive creation or analysis process is unsuccessful.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "ARCHIVE_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "archiveId": "string",
    "errorCode": "string",
    "errorMessage": "string"
  }
}
```

### Invitations

#### Invitations Sent
Payload when an invitation is sent out to a user successfully.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "INVITE_INVITED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "inviteId": "string"
  }
}
```

#### Account Linked by Invitation
Payload when the a user that has been sent an invitation is able to link his or her work account successfully.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "INVITE_LINKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "inviteId": "string"
  }
}
```

### User Data

#### Identity Added
Payload when identity data about a user is added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "IDENTITY_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "identityId": "string"
  }
}
```

#### Rating Added
Payload when rating data about a user is added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "RATING_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "ratingId": "string"
  }
}
```

#### Transactions Added
Payload when transactions data shared by a user are added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "TRANSACTIONS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```

#### Documents Added
Payload when documents data shared by a user are added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "DOCUMENTS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```

#### Employments Added
Payload when employment data shared by a user are added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "EMPLOYMENTS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```

#### Incomes Added
Payload when income data shared by a user are added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "INCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```

#### Contributions Added
Payload when contributions data shared by a user are added.
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "CONTRIBUTIONS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```



<!-- focus: false -->
![Signatures](https://img.icons8.com/ios/50/000000/signature.png)


## Validating Payloads
When events are sent from Smile, you might want to validate the authenticity of the webhook payload, to make sure it came from Smile. You can do that by using the signature, which is included in the headers of each payload. 

> 📘 Note
> 
> To validate the authenticy of the payload, you need to get the entirety of the payload body and digest it using HMAC-SHA512, with the "secret" you defined when you registered your endpoint as the key.

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

    public static String getRequestBody(HttpServletRequest request) throws IOException {
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

    public static String generateSignature(String secret, String requestBody) {
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


