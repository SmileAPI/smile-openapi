---
title: 设计  
excerpt: ""  
category: 6422597473b6df0073e64c8e  
slug: customer-verification-design
---

# 规划并设计您的用户验证集成

***



![](https://files.readme.io/04916ed-image.png)

客户验证通常是在用户注册过程中进行的。为了成功地将 Smile 集成到您的流程中，我们建议通过以下3个步骤来完成：

- 需求收集 - 探讨您的使用情况以及您想通过 Smile 的数据实现什么目标
- 设计（本指南）--设计您的用户流程和与 Smile 的集成。
- [实施与上线](/docs/customer-verification-implementation) - 设置和启动 Smile 的步骤

***



# 第1步：设计您的用户流程

![](https://files.readme.io/1ae27c5-image.png)

在考虑用户流程的时候，有以下四个方面需要考虑：

1. 在这个过程中，您想在哪个阶段使用 Smile？
2. 您想通过哪些数据提供商来引导用户？
3. 您想让用户怎样进入和离开 Smile？
4. 用户怎样取消他们的账户连接？

***



## 在这个过程中，您想在哪个阶段使用 Smile？

![](https://files.readme.io/e02a73b-image.png)

- **在资格预审或早期申请期间** - 在整个申请中自动填写个人信息
- **核保期间** - 对申请人进行决策
- **验证期间** - 核实就业证明、账单证明等

***



## 您想通过哪些数据提供商来引导用户？

在 Smile Developer Portal 里，您可以找到每个数据提供商所支持的数据端点，以及每个数据端点所支持的数据属性。

[block:image]
{
"images": [
{
"image": [
"https://files.readme.io/d541b14-image.png",
null,
""
],
"align": "center",
"border": true
}
]
}
[/block]



1. 导航到 Smile [Developer Portal](https://portal.getsmileapi.com) 上的 Data Sources 页面
2. 查看所选数据提供商所支持的数据端点
3. 查看所选数据端点所支持的数据属性

选择提供商主要考虑的因素有：

- 您的用户群正在使用哪些数据提供商？
- 数据提供商对您的用户群的覆盖率是多少？
- 您需要哪些由提供商支持的数据端点和属性？

基于您筛选出的提供商，我们提供两种设计用户流的方式：

![](https://files.readme.io/bf68868-image.png)

- 特定的提供商（推荐）
- 多个提供商

### 特定的提供商

这个选项要求您确定哪个数据提供商适用于您的用户群。用户将被直接带到特定提供商的登录页（不需要显示同意页以及提供商列表页）

![](https://files.readme.io/635420f-image.png)

### 多个提供商

该选项为用户展示 SDK 的提供商列表，他们可以从所有提供商或您筛选出的提供商中进行选择，然后连接他们的账户：

![](https://files.readme.io/918f517-image.png)

对于 Smile 没有覆盖到的用户，他们会看到一个 **Can't find your employer?** 按钮。然后，有两种可能的情况：

- 如果档案上传被启用，点击这个按钮将直接使用
- 如果启用了上传 archive，点击这个按钮将引导用户手动上传他们的文件，如工资单、所得税记录等：

![](https://files.readme.io/a568785-image.png)

- 否则，点击这个按钮将关闭 Smile Wink SDK 并启动一个回调，让您把用户送回您的应用程序。

![](https://files.readme.io/86704bc-image.png)

我们建议让所有用户都使用 Smile，因为这种方式提供了最好的用户体验和最高的转换率。

***



## 用户怎样开始在 Smile 的流程？

现在您已经确定了 1）Smile 在您的流程中的位置，以及 2）您想把Smile 展现给哪些用户，现在重要的是为用户介绍他们将经历的流程。最佳的实施方案包含两部分：

1. **激励措施** - 用户需要清楚地了解为什么要核对他们的收入和就业数据，以及核对这些将带给他们的好处。激励措施将使他们更快地完成申请并获得最佳费率，清晰地说明这些是十分理想的做法。
2. **背景** - 为用户提供他们将经历的过程的背景。用户应该了解他们需要 1）搜索提供商，和 2）连接就业或工资账户。

下面提供了一个介绍页的例子：

![](https://files.readme.io/cdb6390-image.png)

***



## 用户怎样结束在 Smile 的流程？

在用户连接完他们的账户并被送回您的应用程序后，现在应该让用户知道接下来会发生什么。这取决于您的整体流程和目标，下面是一些例子：

![](https://files.readme.io/d32ed9c-image.png)

***



## 用户怎样取消他们的账户连接？

默认情况下，Smile 会让用户持续授权访问他们的就业账户。您应该为用户提供一个调用 Smile Wink SDK 的选项（例如，从账户设置页面），以便他们可以撤销访问权限。

![](https://files.readme.io/e6ac81e-image.png)

# 第2步：设计所需的数据

![](https://files.readme.io/3cbc3a5-image.png)

![](https://files.readme.io/683da66-image.png)

Smile 可以获取140多个就业记录数据端点。对于就业数据的核实，您最有可能想检索：

Identity:

- First name
- Last name
- Primary address

Employment:

- Employer name
- Job title
- Start date
- End date

Contribution:

- Amount
- Start date
- End date
