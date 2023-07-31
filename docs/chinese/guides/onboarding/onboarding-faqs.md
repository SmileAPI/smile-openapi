---
title: 引导常见问题解答
excerpt: ""  
category: 642259a1f9ba81005d805d98
slug: onboarding-faqs
---

# 要求

## 在需求收集过程中我需要考虑的典型问题是什么？ 

1. **您想用 Smile 数据解决的主要问题是什么?** 通常，有两个用例
    1. [客户验证](/docs/customer-verification-design) - 使用最新的就业数据自动化您的eKYC流程.
    2. [信用决策](/docs/credit-decisioning-design) - 使用最新的就业和收入数据自动化承保流程.
2. **您的用户群是什么样的，您想从中获得什么样的数据？** 您可以跨不同细分市场对用户群进行分类，例如：
    1. 就业状况-他们有工作吗？他们就业还是失业？
    2. 就业类型-他们是 gig 工人还是承包商？他们是全职工作，兼职还是企业所有者？
    3. 识别和分类您的用户群可以帮助您缩小所需的数据属性，例如家庭住址，雇主姓名，就业期限，收入稳定性等。
3. **您是否有任何使用Smile数据实现的业务目标/收益?** 这些通常可以
    1. 减少不良贷款
    2. （进一步）自动化注册/信用决策过程
    3. 其他

# 设计

## Smile Wink SDK支持哪些移动操作系统和运行环境?

我们支持以下内容：

- IOS Native
- Android Native
- Flutter
- ReactNative

我们的Wink Widget位于您的本机应用程序的网络视图实例中，您或用户可以随时关闭用以返回您的应用程序。 我们建议您使用 iframes 封装 Wink SDK. 您可以查看我们的 [快速入门](https://github.com/SmileAPI/quickstart) 示例代码库。

## 我们如何断开/撤销用户的链接帐户？

断开链接帐户有两种方法：

1. 让用户通过 Wink SDK 自行完成，如 [解决方案](https://docs.getsmileapi.com/docs/customer-verification-design#how-can-a-user-disconnect-their-account)
2. 客户可以调用 Smile [OpenAPI](https://docs.getsmileapi.com/reference/delete-account) 主动撤销账户：

```curl curl
DELETE https://open.smileapi.io/v1/accounts/{id}
```



# 实施与上线

## 用户（Link）token 的有效期是多少？

用户token用于初始化 Smile Wink Widget，有效期为 5 小时（300 分钟），到期前。 您可以随时调用 [刷新 Token 端点](https://docs.getsmileapi.com/reference/create-token-1) 获取新的用户token以获取新的token。

## Invite Link 的有效期是多久？

Invite Link 有效期为 14 天。 到期前，收件人可以随时访问邀请链接，已连接的数据提供商将被显示，收件人可以撤销连接。

## 用户数据在 Smile 服务器中存储多长时间？

一旦用户撤销访问权限，所有数据将被删除且无法恢复。

## 邀请链接的有效期是多久？

邀请链接有效期为 14 天。 用户可以在到期前随时打开链接，以允许他们查看之前连接的账户、撤销之前连接的账户或添加更多连接账户。

## 用户账号关联后，Smile 多久会返回用户数据？

帐户连接和数据可用的连接时间取决于数据提供者的性能。 这通常需要几秒到几分钟不等。 Smile服务级别协议为 5 分钟，这意味着您可以在 5 分钟内通过 [API](https://docs.getsmileapi.com/reference/) 获取用户数据。
你也可以监听我们可用的 [Webhooks](https://docs.getsmileapi.com/reference/webhooks) ，一旦数据可用您就可以立即检索数据。

## Smile 用户如何关联您的用户？

您的用户应以一对一的方式映射到 Smile 用户（user ID），并且最终应保持映射关系，因此对于任何返回的用户，您始终可以获得其相应的 Smile 用户名，请参考此 [链接](https://docs.getsmileapi.com/docs/credit-decisioning-design#step-2-make-a-loan-decision) 用于Smile数据映射
