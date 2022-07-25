---
title: 事件通知
excerpt: ""
category: 62ce2a159aafea009af30da7
---



<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks


当有有事件发生时，Smile 使用 webhook 实时通知您的系统。使用HTTPS协议，数据以 JSON 格式发送。这些请求是通过静态 IP 地址发出来的，并且还带有一个签名，供您验证请求的真实性。

> 📘 Note
> 
> Smile 静态IP地址 **18.142.61.230**， 你可以加入IP白名单，这样确保能收到Smile的webhook的请求。

Webhook 被用来做异步通知是非常有用的，当有特定事件发生的时候，你的系统会被通知到这些事件，然后可以对相应的事件做对应的处理，无论是拉取最新的用户数据，还是更新前端App

**实现步骤**

你可以按照如下步骤使用Webhook

1. 确定你需要监听的事件。
2. 创建一个 Webhook HTTPS Endpoint(URL)。
3. 测试您的 Webhook Endpoint是否正常工作。能解析每个事件对象并返回 2xx 状态码。
4. 部署您的 Webhook Endpoint，使其成为可公开访问的 HTTPS URL。
5. 通过调用/webhook 接口，来注册Webhook Endpoint.
   - URL: Webhook endpoint or URL.
   - Event types: 需要监听的事件类型，或者ALL_EVENTS来监听所有事件。
   - Active: 是否激活这个webhook, 只有激活的webhook才能收到回调通知。
   - Secret: 密钥，用HMAC-SHA512来加密整个回调请求。

> 📘 Note
> 
> 下面是一个用curl 来展示以 "https://webhook.clienturl.xyz" 作为Webhook Endpoint的例子

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

|事件|事件类型|事件触发条件|
|---|---|---|
|创建User成功|USER_CREATED|一个新用户创建成功。|
|Account连接成功|ACCOUNT_CONNECTED|用户成功连接一个Provider。|
|Account Revoke连接|ACCOUNT_DISCONNECTED|用户revoke了一个account连接。|
|Account连接失败|ACCOUNT_FAILED|用户连接一个Provider失败了。|
|Archive上传成功|ARCHIVE_STARTED|用户成功上传了Archive|
|Archive分析成功|ACCOUNT_ANALYZED|Archive 被OCR引擎成功识别出来。|
|Archive Revoke|ARCHIVE_REVOKED|用户revoke了Archive。|
|Archive上传或者分析失败|ARCHIVE_FAILED|用户上传失败，或者OCR引擎分析失败。|
|邀请发送成功|INVITE_INVITED|邀请成功发出。|
|邀请的用户账号连接成功|INVITE_LINKED|被邀用户连接了一个账号。|
|新加Identity 数据|IDENTITY_ADDED|新的Identity 数据添加了。|
|新加Rating 数据|RATING_ADDED|新的Ratings 数据添加了。|
|新加Transactions 数据|TRANSACTIONS_ADDED|新的Transactions 数据添加了。|
|新加Documents 数据|DOCUMENTS_ADDED|新的Documents 数据添加了。|
|新加Employments 数据|EMPLOYMENTS_ADDED|新的Employments 数据添加了。|
|新加Incomes 数据|INCOMES_ADDED|新的Incomes 数据添加了。|
|新加Contributions 数据|CONTRIBUTIONS_ADDED|新的Contributions 数据添加了。|


<!-- focus: false -->
![Payload](https://img.icons8.com/ios/50/000000/json-download.png)

## 事件payload

### Users

#### 创建User成功
一个新用户创建成功.
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

#### Account连接成功
用户成功连接一个Provider
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
#### Account Revoke连接
用户revoke了一个account连接
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
#### Account连接失败
用户连接一个Provider失败了
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

#### Archive上传成功
用户成功上传了Archive
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

#### Archive分析成功
Archive 被OCR引擎成功识别出来
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


#### Archive删除成功
用户revoke了Archive
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

#### Archive上传或者分析失败
用户上传失败，或者OCR引擎分析失败
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
邀请成功发出
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
被邀用户连接了一个账号
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

#### 新加Identity
新的Identity 数据添加了
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

#### 新加Rating 数据
新的Ratings 数据添加了
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

#### 新加Transactions 数据
新的Transactions 数据添加了
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

#### 新加Documents 数据
新的Documents 数据添加了
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

#### 新加Employments
新的Employments 数据添加了
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

#### 新加Incomes 数据
新的Incomes 数据添加了
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

#### 新加Contributions
新的Contributions 数据添加了
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
当收到请求后，可以对请求进行校验，来验证是否来自Smile。

> 📘 Note
> 
> 需要对整个请求的payload进行签名，然后把签名和Smile请求Header里面Smile-Signature进行对比，来确定回调请求是否合法。

下面的例子展示如何通过HMAC-SHA512计算签名：
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


> 🚧 注意
> 
>在验证签名的时候，请把原始的、未经过转换的整个的请求的request body作为加密的对象。

