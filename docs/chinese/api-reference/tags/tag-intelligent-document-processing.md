---
title: Intelligent Document Processing
excerpt: ""  
category: 64c78531461848004b92b92f
slug: intelligent-document-processing
---

Smile Snap 的智能文档处理 (IDP) 服务结合了光学字符识别 (OCR) 的效率和人工智能的优势。IDP 能准确捕捉、理解文档内容并将其与上下文联系起来。

支持的文档可通过我们的Open API 发送至 Smile，或通过 Wink SDK（如果启用）发送。Smile 接受各种格式的文档，如照片、扫描件或 PDF 文件。

获取这些数据可作为一种备用方法，或作为您记录和验证使用的额外数据点。从文件中收集的数据随后将作为 Smile 用户数据内容的一部分。

这些文档在 Smile Network 中被称为 [Archives](/reference/archives)。

## 使用服务

在您的流程中实施 Smile API 的 IDP 服务只需以下几个步骤：

1. **向 Smile API 提供文件**

    > 有两种方法可以将文档或文件提供给 Smile API 进行处理：
    1. 使用 [Wink Widget SDK](/reference/chapter-4#client-sdk) 快速实现用户流程。
    2. 使用 [Archives API](/reference/archives) 对用户流程进行更精细的控制。

2. **检索分析数据**

    > 数据上传后，我们的 IDP 引擎会根据预期文件类型自动检查并分类成支持的文件类型。
    >
    > 一旦完成分类，我们的引擎就会开始解析文件，从文件中提取数据并进行标记。每种文件类型都有不同的数据集，并将反映在分析结果中。
    >
    > 分析完成后，Archives 数据内容将通过 webhook 发送给您，您也可以直接调用 Archives API。更多信息请参阅 API 文档。

3. **对提取的数据进行验证**

   > 我们目前正在努力将这些调用集成到 API 中，但您可以使用从 *步骤 2* 获取的数据调用我们的[Verification API](/reference/verification)，以验证主体的信息（如姓名和身份证号码）。这将为您提供另一层保证，以来确保文件有效。

## 测试服务

要测试服务，您可以在 Sandbox 模式下调用 API ，也可以使用 [Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) 下的 [Snap Lookup > Scanned Documents 部分](https://portal.getsmileapi.com/snap/scanned?utm_source=docs&utm_medium=internal_link) 直接试用服务。

> 🚧 注意
>
> 由于 Sandbox 模式下的 Archives 只返回特定的工资单。所以，您需要在 Developer Portal 内下载工资单样本文件，然后通过 Wink Widget 或 API 上传。在 Sandbox 模式下上传的其他文件都将返回错误。