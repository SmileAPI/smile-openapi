---
title: 事件通知
excerpt: ""
category: 62ce2a159aafea009af30da7
slug: chapter-5-cn
---



<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks


当有有事件发生时，Smile 使用 webhook 实时通知您的系统。使用 HTTPS 协议，数据以 JSON 格式发送。这些请求是通过静态 IP 地址发出来的，并且还带有一个签名，供您验证请求的真实性。

> 📘 Note
> 
> Smile 静态IP地址 **18.142.61.230**， 您可以加入 IP 白名单，这样确保能收到 Smile 的 webhook 的请求。

Webhook 被用来做异步通知是非常有用的，当有特定事件发生的时候，这些事件会被通知到您的系统，然后可以对相应的事件做对应的处理，无论是拉取最新的用户数据，还是更新前端 App 。

**实现步骤**

您可以按照如下步骤使用 Webhook

1. 确定您需要监听的事件。
2. 创建一个 Webhook HTTPS Endpoint(URL)。
3. 测试您的 Webhook Endpoint 是否正常工作。能解析每个事件对象并返回 2xx 状态码。
4. 部署您的 Webhook Endpoint，使其成为可公开访问的 HTTPS URL 。
5. 通过调用/webhook 接口，来注册Webhook Endpoint 。
   - URL: Webhook endpoint or URL.
   - Event types: 需要监听的事件类型，或者 ALL_EVENTS 来监听所有事件。
   - Active: 是否激活这个 webhook , 只有激活的 webhook 才能收到回调通知。
   - Secret: 密钥，用 HMAC-SHA512 来加密整个回调请求。

> 📘 Note
> 
> 下面是一个用 curl 来展示以 "https://webhook.clienturl.xyz" 作为 Webhook Endpoint 的例子

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


## 事件类型 
下面是支持的事件类型:

|事件|事件类型|详情|
|---|---|---|
|User Creation Successful|USER_CREATED|当创建新用户和链接 token 时发送|
|Account Connection Successful|ACCOUNT_CONNECTED|当用户成功连接其工作帐户时发送。|
|Account Disconnection Successful|ACCOUNT_DISCONNECTED|当用户断开或撤销与其帐户的链接时发送。|
|Account Connection Failed|ACCOUNT_FAILED|当帐户关联过程失败时发送。|
|Archive Creation Successful|ARCHIVE_STARTED|当用户成功上传一个或多个文件时发送，这些文件将作为 Smile 中的 “archive” 。 |
|Archive Analysis Successful|ACCOUNT_ANALYZED|当 archive 已通过 OCR 自动分析并转换为 JSON 数据时发送。|
|Archive Revocation Successful|ARCHIVE_REVOKED|当用户删除访问或使用 archive 的权限时发送。|
|Archive Creation or Analysis Failed|ARCHIVE_FAILED|当 archive 创建或分析过程失败时发送。|
|Invitation Sending Successful|INVITE_INVITED|当邀请成功发送给用户时发送。|
|Account Link by Invitation Successful|INVITE_LINKED|当已收到邀请的用户能够成功关联其帐户时发送。|
|Identity Data Added|IDENTITY_ADDED|当添加有关用户的身份数据时发送。|
|Rating Data Added|RATING_ADDED|当添加有关用户的评级数据时发送。|
|Transactions Data Added|TRANSACTIONS_ADDED|当添加用户共享的交易数据时发送。|
|Documents Data Added|DOCUMENTS_ADDED|当添加用户共享的文档数据时发送。|
|Employments Data Added|EMPLOYMENTS_ADDED|当添加用户共享的就业数据时发送。|
|Incomes Data Added|INCOMES_ADDED|当添加用户共享的收入数据时发送。|
|Estimated Incomes Data Added <br>*(抢先试用版)*|EINCOMES_ADDED|当添加用户共享的估计收入数据时发送。|
|Contributions Data Added|CONTRIBUTIONS_ADDED|当添加用户共享的社会保障缴款数据时发送。|


<!-- focus: false -->
![Payload](https://img.icons8.com/ios/50/000000/json-download.png)

## 事件内容

### Users

#### 创建 User 成功
创建新用户和链接 token 时，事件发送格式如下：
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

#### Account 连接成功
用户成功连接其帐户时，事件发送格式如下：
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
#### Account Revoke 连接
用户断开或撤销与其帐户的链接时，事件发送格式如下：
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
#### Account 连接失败
帐户关联过程失败时，事件发送格式如下：
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

#### Archive 上传成功
用户上传一个或多个文件时，事件发送格式如下，这些文件在 Smile 中作为 “archive” ：
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

#### Archive 分析成功
archive 被分析并通过 OCR 自动转换为 JSON 数据时，事件发送格式如下：
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


#### Archive 删除成功
用户删除访问或使用 archive 的权限时，事件发送格式如下：
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

#### Archive 上传或者分析失败
archive 创建或分析过程不成功时，事件发送格式如下：
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

#### 邀请发送成功
成功向用户发送邀请时，事件发送格式如下：
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

#### 邀请的用户账号连接成功
已被邀请的用户成功链接其帐户时，事件发送格式如下：
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

#### 新加 Identity 
添加有关用户的身份数据时，事件发送格式如下：
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

#### 新加 Rating 
添加有关用户的评级数据时，事件发送格式如下：
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

#### 新加 Transactions 
添加用户共享的交易数据时，事件发送格式如下：
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

#### 新加 Documents 
添加用户共享的文档数据时，事件发送格式如下：
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

#### 新加 Employments
添加用户共享的就业数据时，事件发送格式如下：
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

#### 新加 Incomes 
添加用户共享的收入数据时，事件发送格式如下：
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

#### 新加 Estimated Incomes (抢先试用版)
添加用户共享的预估收入数据时，事件发送格式如下：
``` json
{
  "id": "17bbf36498de4d68a0d4f86c7b62f69f",
  "version": 1,
  "type": "EINCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "string",
    "accountId": "string",
    "count": 0
  }
}
```

#### 新加 Contributions
添加用户共享的社会保障缴款数据时，事件发送格式如下：
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


## 校验签名
当收到请求后，可以对请求进行校验，来验证是否来自 Smile 。

> 📘 Note
> 
> 需要对整个请求的 payload 进行签名，然后把签名和 Smile 请求 Header 里面 Smile-Signature 进行对比，来确定回调请求是否合法。

下面的例子展示如何通过 HMAC-SHA512 计算签名：
- Nodejs
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


> 🚧 注意
> 
>在验证签名的时候，请把原始的、未经过转换的整个的请求的 request body 作为加密的对象。

