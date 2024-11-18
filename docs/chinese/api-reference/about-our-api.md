---
title: 关于我们的 API 
excerpt: ""  
category: 62ce2a159aafea009af30da8
slug: about-our-api
---




# 模式

> 👍 注意
>
> **Sandbox:** <https://sandbox.smileapi.io/v1>  
> **Production:** <https://open.smileapi.io/v1>

# 认证

基本身份验证是内置于 HTTP 协议中的一种简单身份验证方案。如要使用它，请在发送 HTTP 请求时，在 Authorization 标头中包含 `Basic` 一词，后面跟一个空格和一个 base64 编码的字符串 `API Key:API Secret`。

> 📘 样例
>
> `Authorization: Basic ZGVtbzpwQDU1dzByZA==`

**您可以登录 [Developer Portal](https://portal.getsmileapi.com/?utm_source=docs&utm_medium=internal_link) ，在 *API Keys* 部分找到您的 API Key 和Secret**

注册后，您可以免费访问我们的 Sandbox mode 进行测试。如果您需要 Production mode 的访问权限，请 [联系我们](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link) 。

![where-to-find-api-keys.png](../../../assets/images/where-to-find-api-keys.png)

您可以通过点击 API Key 和 Secret 旁边的复制图标，轻松将其复制到电脑剪贴板。