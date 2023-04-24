---
title: 常见问题
excerpt: ""  
category: 62ce2a159aafea009af30da6 
slug: faqs
---

## 安全和隐私

### 如何确保 API 是安全的?

为了实现最大的安全性，来自 Smile API 的所有数据都使用 SHA-256 签名在 RSA 4096 上加密。 此外，无论何时 Smile 都不会存储最终用户的凭证：我们通过 TLS 将这些凭据直接传递到数据源的服务器以启动信息共享过程。

### API 是否符合数据隐私法？?

Smile 相信个人隐私的神圣不可侵犯，我们的用户是他们个人数据的所有者，应该始终完全控制他们何时以及向谁共享数据。 Smile 力求遵守所有有关数据隐私的当地法律。 在菲律宾，我们遵守 2012 年数据隐私法 (RA 10173)，我们帮助用户根据 [菲律宾数据隐私法](https://www.privacy.gov.ph/data-privacy-act/#18) 第 18 条行使其数据可移植性权利。

与我们的客户共享用户数据基于可撤销的模式：只有通过我们的 SDK 获得用户的明确同意，才能进行共享。 用户可以随时通过同样的方式撤销对其数据的访问，确保他们完全控制何时以及向谁共享自己的数据。

一旦用户撤销访问权限，所有信息将被删除且无法恢复。 任何其他数据将保留 60 天，之后所有个人数据都将被删除。

我们还维护隐私政策，以便您可以确定您的数据是如何被使用的。

## 使用 Smile 管理用户数据

### 我需要在我的服务器上存储任何用户数据吗？

我们建议您将 Smile user ID 存储为您自己的用户数据的一部分，以便将您的用户与 Smile 系统上的用户关联起来。Smile user ID 这通常采用`tenantId-123abc456def789abc123def456abc78`格式。

在 Smile 系统上创建用户后，后续加载 Wink Widget 的调用应提供此 user ID 用于维护您的数据。

监听 `ACCOUNT_DISCONNECTED` webhook 还会通知您用户何时撤销了对其数据的访问权限，在此之后您可以安全地从系统中删除 Smile user ID。

## 使用 Smile API

### 有哪些数据源可用？

我们有众多来自社会保障机构以及各种薪资和 gig 平台的数据源可供用户连接。

如果要查看我们的完整数据源列表，您可以[免费访问我们的 developer portal ](https://portal.getsmileapi.com/register) 亲自测试我们的平台。 您也可以[联系我们](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) 来了解更多信息。

### Smile提供用于测试的 sandbox 帐户吗？

是的！ 欢迎[注册我们的 developer portal ](https://portal.getsmileapi.com/register) 并试用我们可用的 sandbox 环境。 现在，您将可以访问以下内容：

- 一个可测试的 sandbox widget，可供您模拟客户会看到什么
- 用于在您自己的环境中进行测试的 sandbox API key
- 测试用户的凭据，以便您可以在您的环境或开发人员门户 Wink Widget 上运行测试

要访问实时数据，请 [联系我们](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) 为您启用此功能。

### 我们可以从您的 API 获取一些示例 JSON 输出吗？

有多种方法可以从我们的 API 获取示例 JSON 输出：

1. **通过我们免费的 developer portal 来加载用户数据。**
   开发人员门户上的每个连接用户（甚至 sandbox 用户）都可以切换到 JSON 模式，因此您可以看到来自我们服务器的实际响应。
   ![](https://files.readme.io/7cc555c-devportal-jsonmode.png)

2. **我们的 API Reference 包含一个 API Explorer，供您即时测试 API 调用。**
   使用开发人员门户中的 API 和 Secret，您还可以使用 API 参考中的 API Explorer 功能对我们的 API 执行调用。
   ![](https://files.readme.io/5d046be-reference-explorer.png)

### 我们怎样访问实时数据？

访问实时数据需要开启生产模式(Production Mode), 这样你可以连接真实账户。您的帐户在Production Mode下连接用户需要向收费，如果您想测试我们的平台，[联系我们](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) 启用它，也可获得免费额度。

### Smile API 的可扩展性如何？

Smile 限制了对每个 API 的调用量，以确保平台的稳定性和可用性。目前，我们的客户端对每个 IP 地址最多只允许每秒 20 个请求。自动扩展机制和负载平衡可确保维持服务正常运行。

### Smile 如何处理 API 的版本控制？

我们使用的版本控制约定是 1.2.3 格式，其中 1 是主要版本（表示对 API 的重大更改），2 是次要版本，3 是补丁更新。 后两个版本对 API 用户是透明的，发布这些更改时不需要执行更新。

该版本包含在 URI 路径中，以便于调用。 因此，例如，Smile API 的版本 1 将类似于 `<https://open.smileapi.io/v1`>

### 我们可以获得免费额度来试用我们帐户中的实时数据吗？

[联系我们](https://www.getsmileapi.com/book-a-call-with-smile-api?utm_source=FAQ&utm_medium=FAQ&utm_campaign=FAQ) 了解如何在您的账户中获得 Production Mode 的免费额度。

### Smile 是否按每个 API 请求收费？

不，我们只根据已连接账户的数量收费。您可以向同一个 API 端点发送多个请求，而不会影响您的账单。但是请记住，我们有每秒 20 个请求的速率限制。如果您需要更高请求频率，请与我们联系。

### Production Mode 和 Sandbox Mode 有什么区别?

如果您需要在开发过程中测试 SDK 的工作方式，请使用 Sandbox Mode 。 Sandbox Mode 包括测试帐户，您可以使用这些帐户返回您的数据用于开发和测试目的。 这些不连接到我们的合作伙伴数据源，因此您可以自由测试系统。

另一方面，Production Mode 将仅返回实时数据。 Production Mode 连接到我们数据源的实时生产环境，因此需要来自真实人员的真实账户。