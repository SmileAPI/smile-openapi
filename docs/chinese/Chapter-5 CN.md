---
title: 事件通知
excerpt: ""
category: 62ce2a159aafea009af30da7
slug: chapter-5-cn
---



<!-- focus: false -->
![Webhooks](https://img.icons8.com/ios-filled/50/000000/webhook.png)

## Webhooks


当您的环境中发生事件时，Smile 使用 webhook 实时通知您的应用程序。

这些通知将以安全的方式，使用来自静态 IP 地址的 HTTPS 协议，以 JSON 格式来发送数据。并且还带有一个签名，供您验证请求的真实性。

> 📘 Note
> 
> Smile 静态IP地址 **18.142.61.230**， 您可以加入 IP 白名单，这样确保能收到 Smile 的 webhook 的请求。

Webhook 对于获取有关异步事件的通知非常有用，当这些事件发生时，它可以在你的后台系统中执行行动，或者知道何时刷新你的前端系统以显示新数据。

当创建一个用户，成功连接一个账号，上传一个就业文件，发送一个邀请时，或者当任何新类型的数据，如用户的身份，收入，就业等被添加时，事件通知将被发送。在下面的*事件清单*中，您可查看订阅的可用事件清单。


### 实现步骤

您可以按照如下步骤使用 Webhook

1. 使用我们的文档和可用资源**识别您要监控的事件**和要解析的事件内容。
2. **在您的服务器或应用程序上创建一个 Webhook 端点**作为 HTTPS 端点 (URL)。
3. **测试您的 webhook 端点是否正常工作。** 通过解析每个事件对象并返回 “2xx” 响应状态代码，确保您的服务器或应用程序能够处理来自 Smile 的请求。
4. **部署您的 webhook 端点**，使其成为可公开访问的 HTTPS URL。
5. **通过向 ``/webhooks`` 端点发出请求来注册您的可公开访问的 webhook 端点**。您将需要指定以下内容：
   - **URL**：webhook 端点或 URL。
   - **事件类型**：您要监控的事件类型，用逗号分隔（不同的事件类型见下文），或者简单地使用 ``ALL_EVENTS`` 来获取所有事件类型的通知。
   - **活动**：您希望此端点定义处于活动状态还是非活动状态（您可以稍后通过更新请求进行更新）
   - **Secret**：一个短语或值，可用于通过使用 HMAC-SHA512 消化接收到的内容正文来验证其真实性，其中 Secret 作为密钥。 请参阅下面的*验证内容*。

> 📘 Note
> 
> 下面的示例显示了一个使用 Shell 脚本/cURL 的请求，其中 webhook 接收端点设置为``https://webhook.clienturl.xyz``
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

### Webhook 重试

为了确保您能收到通知，Smile 保证提供"至少一次“的投递。

当我们发送 webhook 时，Smile 将会从您的端点检查 http status 在200到299之间的 HTTP 响应。如果我们收到的响应不在200-299之间，Smile 将尝试最多两次重新发送 webhook ，每次重试之间有几十秒的时间。

这意味着您可能会不止一次地收到同一个 webhook 事件。请确保您可以在您的端点或应用程序中处理这些可能重复的通知。您可以通过比较``id``值和以前的事件来检测重复的 webhook 事件（见下面的*示例内容*）。 


<!-- focus: false -->
![Events](https://img.icons8.com/dotty/50/000000/notification-center.png)


## 事件列表
以下是您可以通过 webhook 订阅的事件:

| 事件                                         | 事件类型                       | 详情                                             |
|--------------------------------------------|----------------------------|------------------------------------------------|
| User Creation Successful                   | USER_CREATED               | 当创建新用户和链接 token 时发送                            |
| Account Connection Successful              | ACCOUNT_CONNECTED          | 当用户成功连接其工作账户时发送。                               |
| Account Disconnection Successful           | ACCOUNT_DISCONNECTED       | 当用户断开或撤销与其账户的链接时发送。                            |
| Account Connection Failed                  | ACCOUNT_FAILED             | 当账户关联过程失败时发送。                                  |
| Task Started                               | TASK_STARTED  | 当账户关联过程中开始获取数据或者上传文件开始解析时发送。                   |
| Task Finished                              | TASK_FINISHED | 当账户关联过程获取数据任务结束或者上传文件开始解析完成时发送。                |
| Archive Creation Successful                | ARCHIVE_STARTED            | 当用户成功上传一个或多个文件时发送，这些文件将作为 Smile 中的 “archive” 。 |
| Archive Analysis Successful                | ACCOUNT_ANALYZED           | 当 archive 已通过 OCR 自动分析并转换为 JSON 数据时发送。         |
| Archive Revocation Successful              | ARCHIVE_REVOKED            | 当用户删除访问或使用 archive 的权限时发送。                     |
| Archive Creation or Analysis Failed        | ARCHIVE_FAILED             | 当 archive 创建或分析过程失败时发送。                        |
| Invitation Sending Successful              | INVITE_INVITED             | 当邀请成功发送给用户时发送。                                 |
| Account Link by Invitation Successful      | INVITE_LINKED              | 当已收到邀请的用户能够成功关联其账户时发送。                         |
| Identity Data Added                        | IDENTITY_ADDED             | 当添加有关用户的身份数据时发送。                               |
| Rating Data Added                          | RATING_ADDED               | 当添加有关用户的评级数据时发送。                               |
| Transactions Data Added                    | TRANSACTIONS_ADDED         | 当添加用户共享的交易数据时发送。                               |
| Documents Data Added                       | DOCUMENTS_ADDED            | 当添加用户共享的文档数据时发送。                               |
| Employments Data Added                     | EMPLOYMENTS_ADDED          | 当添加用户共享的就业数据时发送。                               |
| Incomes Data Added                         | INCOMES_ADDED              | 当添加用户共享的收入数据时发送。                               |
| Estimated Incomes Data Added <br>*(抢先试用版)* | EINCOMES_ADDED             | 当添加用户共享的估计收入数据时发送。                             |
| Contributions Data Added                   | CONTRIBUTIONS_ADDED        | 当添加用户共享的社会保障缴款数据时发送。                           |
| Liabilities Data Added                     | LIABILITIES_ADDED          | 添加用户共享的负债数据时发送。                                |



<!-- focus: false -->
![Payload](https://img.icons8.com/ios/50/000000/json-download.png)

## 事件内容

### Users

#### 创建 User 成功
创建新用户和链接 token 时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "USER_CREATED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78"
  }
}
```

### Accounts

#### Account 连接成功
用户成功连接其账户时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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
#### Account Revoke 连接
用户断开或撤销与其账户的链接时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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
#### Account 连接失败
账户关联过程失败时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ACCOUNT_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "loginName": "userLoginName",
    "errorCode": "500",
    "errorMessage": "Error message",
    "providers": [
      "abccorp"
    ]
  }
}
```

#### 任务开始
任务开始时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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
#### 任务结束
任务结束时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

### Archives

#### Archive 上传成功
用户上传一个或多个文件时，事件发送格式如下，这些文件在 Smile 中作为 “archive” ：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_STARTED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "u-123abc456def789abc123def456abc78"
  }
}
```

#### Archive 分析成功
archive 被分析并通过 OCR 自动转换为 JSON 数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_ANALYZED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "u-123abc456def789abc123def456abc78"
  }
}
```


#### Archive 删除成功
用户删除访问或使用 archive 的权限时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_REVOKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "u-123abc456def789abc123def456abc78"
  }
}
```

#### Archive 上传或者分析失败
archive 创建或分析过程不成功时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "ARCHIVE_FAILED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "archiveId": "u-123abc456def789abc123def456abc78",
    "errorCode": "500",
    "errorMessage": "Error Message"
  }
}
```

### Invitations

#### 邀请发送成功
成功向用户发送邀请时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_INVITED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```

#### 邀请的用户账号连接成功
已被邀请的用户成功链接其账户时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Identity 
添加有关用户的身份数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Rating 
添加有关用户的评级数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Transactions 
添加用户共享的交易数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Documents 
添加用户共享的文档数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Employments
添加用户共享的就业数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Incomes 
添加用户共享的收入数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Contributions
添加用户共享的社会保障缴款数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

#### 新加 Liabilities 
添加用户共享的负债数据时，事件发送格式如下：
``` json
{
  "id": "123abc456def789abc123def456abc78",
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

### 用户洞察数据

#### 新加 Estimated Incomes (抢先试用版)

添加用户共享的预估收入数据时，事件发送格式如下：
``` json
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


<!-- focus: false -->
![Signatures](https://img.icons8.com/ios/50/000000/signature.png)


## 验证内容

当事件从 Smile 发送时，您可能想要验证 webhook 内容的真实性，以确保它来自 Smile。您可以通过使用签名来做到这一点，该签名包含在每个内容的标头中。

> 📘 注意
> 
> 要验证内容的真实性，您需要获取整个内容主体并使用 HMAC-SHA512 对其进行分析，并使用您在注册端点时定义的 “Secret” 作为密钥。

下面是使用 HMAC-SHA512 检查内容有效性的示例：

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

如果您的摘要与您在标头中作为内容签名收到的摘要匹配，则该内容是有效且真实的。

> 🚧 注意
> 
> 验证内容时，请确保验证整个内容。不要在它之前或之后包含额外的空格。在进行验证检查之前不要预先解析或重新格式化它。
