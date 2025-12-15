---
title: Archives
category:
  uri: '/branches/1.0-Chinese/categories/reference/Smile Network'
slug: archives
content:
  excerpt: ''
---

Smile API 还可以存储和处理照片及其他文件，以帮助验证用户的记录。启用后用户可以上传照片、扫描件或 PDF 文件，作为供您记录和验证使用的备份或额外的数据点。支持以下文件类别：

它们可以是以下任何一种：

| Archive 类型                                     | Wink Widget 上传 | API 上传 | 数据提取 | API 文件类型 | 文件子类型 | 
|:-----------------------------------------------| :----------------- | :--------- | :-------------- | :------------ | :------------ |
| Income Tax Document                            | ✅ | ✅ | ✅ | `TAX_DOCUMENT` | `TAX_PAYMENT` |
| Payslip                                        | ✅ | ✅ | ✅ | `PAYSLIP` | `PAYSLIP` |
| Company ID                                     | ✅ | ✅ | ❌ | `COMPANY_ID` | `COMPANY_ID_FRONT`, `COMPANY_ID_BACK` |
| NBI Clearance Document                         | ❌ | ✅ | ✅ | `CLEARANCE_NBI` | N/A |
| ID (Front)                                     | ❌ | ✅ | ❌ | `ID_FRONT` | N/A |
| ID (Back)                                      | ❌ | ✅ | ❌ | `ID_BACK` | N/A |
| Bank Statement                                 | ❌ | ✅ | ❌ | `BACK_STATEMENT` | N/A |
| Utility Bills                                  | ❌ | ✅ | ❌ | `UTILITY_BILLS` | N/A |
| Police Clearance                               | ❌ | ✅ | ❌ | `CLEARANCE_POLICE` | N/A |
| Barangay Clearance                             | ❌ | ✅ | ❌ | `CLEARANCE_BARANGAY` | N/A |
| Others                                         | ❌ | ✅ | ❌ | `OTHERS` | N/A |

对支持的文件类型进行额外分析，从上传的文件中检索就业和收入等基本信息。这样，您可以迅速地从文件中获取信息，而无需手动转录数据。

对 社保记录、所得税文件和工资单进行额外分析，以便从上传的文件中检索基本信息，如就业和收入信息。这样，您就可以直接从文件中获取信息，而无需手动转录数据。

这些用户上传的文件可以通过 Archives 端点进行检索，以便在您需要时下载或进行人工验证。

我们接受最大为 15MB 的文件，可以是以下格式：

- Portable Network Graphic files (`.png`)
- Portable Document Format files (`.pdf`)
- Joint Photographic Experts Group files (`.jpg` or `.jpeg`)
- Tag Image File Format files (`.tiff`)

文件将一直保存到用户通过 SDK 删除或通过 API 撤销为止，最长保存 60 天。

从可验证来源自动检索的文件和档案，如经许可访问薪资系统，也可在 [Documents endpoint](/reference/documents) 下找到。从文件中获取的数据也可在相应的数据类型下找到，如 [Employments](/reference/employments) 或 [Incomes](/reference/incomes) 。

> 🚧 注意
>
> Sandbox 模式下的 Archive 只支持测试特定的工资单。要在 Sandbox 模式下测试 Archive，您可以在 Developer Portal 下载工资单样例，然后通过 Wink Widget 或 API 上传。在 Sandbox 模式下上传其他文件将返回错误。

## Archive 对象

| 属性         | 类型               | 详情                                                                      |
|:-----------|:-----------------|:------------------------------------------------------------------------|
| id         | string           | Archive/文件的唯一ID                                                         |
| createdAt  | date-time        | 用户上传文件的时间                                                               |
| providerId | string           | 总是设置为 `"user-provided"`，因为是用户自己上传的文件                                    |
| userId     | string           | 上传文件的人的用户ID                                                             |
| type       | string           | 上传文件的类型，可以是以下之一：`PAYSLIP`，`TAX_DOCUMENT`，`COMPANY_ID`，`SOCIAL_SECURITY` |
| state      | object           | 该文件的当前处理状态，见下文                                                          |
| rawFiles   | array of objects | 关于原始文件的其他细节                                                             |
| classification | object | 根据对文件内容的人工智能分析，确定上传文件的文件类型                                              |
| analysis | object | 根据对文件内容的人工智能分析提取数据                                                      |

### State 对象

| 属性           | 类型        | 详情                                                                                      |
|:-------------|:----------|:----------------------------------------------------------------------------------------|
| status       | string    | 文件当前的分析状态，可以是下列之一：`STARTED`，`ANALYZED`，`UNSUPPORTED`，`ERROR`，`REVOKED`                  |
| errorCode    | string    | 在分析过程中发现的任何错误，可以是下列之一：`MISSING_MANDATORY_FIELD`, `INVALID_FIELD_FORMAT`, `SYSTEM_ERROR` |
| errorMessage | string    | 上述 "errorCode" 的可读错误信息                                                                  |
| updatedAt    | date-time | 文件最后一次更新/分析的时间                                                                          |

### Raw Files 对象

| 属性        | 类型        | 详情                                      |
|:----------|:----------|:----------------------------------------|
| id        | string    | 原始文件的唯一ID                               |
| createdAt | date-time | 用户上传文件的时间                               |
| name      | string    | 用户上传文件的文件名                              |
| subType | string | 根据上级文件类型更新的文件类型                         |
| size      | integer   | 文件大小，以千字节为单位                            |
| format    | string    | 文件的格式，可以是以下之一：`pdf`，`png`，`tiff`，`jpeg` |
| url       | string    | 文件的可访问URL                               |

### Classification 对象

| 属性        | 类型        | 详情                                      |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| fileType | string | 根据 AI 对文件内容的分析，上传文件的文件类型可以是以下类型之一：`PAYSLIP`, `TAX_DOCUMENT`, `EMPLOYMENT_CERTIFICATE`, `OTHERS` |

### Analysis 对象

Analysis 对象将根据上传文件的文件类型返回提取的数据。文件中找不到的其他字段将返回空值。

| 属性               | 类型     | 支持文件类型                    | 详情                                                                          |
|:-----------------|:-------|:--------------------------|:----------------------------------------------------------------------------|
| startDate        | date   | `PAYSLIP`, `TAX_DOCUMENT` | 工资单的开始日期，格式为 YYYY-MM-DD。如果没有，则为空。                                           |
| endDate          | date   | `PAYSLIP`, `TAX_DOCUMENT` | 工资单的结束日期，格式为 YYYY-MM-DD。如果没有，则为空。                                           |
| payDate          | date   | `PAYSLIP`                 | 工资单的支付日期，格式为 YYYY-MM-DD。如果没有，则为空。                                           |
| currency         | date   | `PAYSLIP`                 | 以 3 个字符的 alpha ISO 4217  格式表示的工资单货币。如果没有，则为空。                               |
| baseAmount       | float  | `PAYSLIP`, `TAX_DOCUMENT` | 基薪金额。如果没有，则为空。                                                              |
| grossAmount      | float  | `PAYSLIP`, `TAX_DOCUMENT` | 工资支付毛额。如果没有，则为空。                                                            |
| netAmount        | float  | `PAYSLIP`                 | 净工资支付额。如果没有，则为空。                                                            |
| employerName     | string | `PAYSLIP`, `TAX_DOCUMENT` | 工资单上的雇主姓名。如果没有，则为空。                                                         |
| employeeName     | string | `PAYSLIP`, `TAX_DOCUMENT` | 工资单上的员工姓名。如果没有，则为空。                                                         |
| ssNumber         | string | `PAYSLIP`                 | 工资单上的社保号。如果没有，则为空。                                                          |
| taxNumber        | string | `PAYSLIP`, `TAX_DOCUMENT` | 工资单上的纳税识别号。如果没有，则为空。                                                        |
| expireDate       | date   | `CLEARANCE_NBI`           | 文件的有效期，格式为 YYYY-MM-DD。如果没有，则为空。                                             |
| dateOfBirth      | date   | `CLEARANCE_NBI`           | 出生日期，格式为 YYYY-MM-DD。如果没有，则为空。                                               |
| firstName        | string | `CLEARANCE_NBI`           | 文件中的名字。如果没有，则为空。                                                            |
| lastName         | string | `CLEARANCE_NBI`           | 文件中的姓氏。如果没有，则为空。                                                            |
| middleName       | string | `CLEARANCE_NBI`           | 文件中的中间名。如果没有，则为空。                                                           |
| nbiIdNumber      | string | `CLEARANCE_NBI`           | 文件中的 NBI 审核文件编号。如果没有，则为空。                                                   |
| address          | string | `CLEARANCE_NBI`           | 文件中的地址。如果没有，则为空。                                                            |
| maritalStatus    | string | `CLEARANCE_NBI`           | 文件中的婚姻状况。如果没有，则为空。                                                          |
| gender           | string | `CLEARANCE_NBI`           | 文件中的性别。如果没有，则为空。                                                            |
| citizenship      | string | `CLEARANCE_NBI`           | 文件中的公民身份。如果没有，则为空。                                                          |
| remark           | string | `CLEARANCE_NBI`           | 文件中的备注。如果没有，则为空。                                                            |

## Archive 数据样本


``` json
{
    "id": "archive-123abc456def789abc123def456abc78",
    "createdAt": "2024-01-01T12:34:56Z",
    "providerId": "tenant-provided",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "type": null,
    "state": {
        "status": "ANALYZED",
        "errorCode": null,
        "errorMessage": null,
        "updatedAt": "2024-01-01T12:34:56Z"
    },
    "rawFiles": [
        {
            "id": "f-123abc456def789abc123def456abc78",
            "createdAt": "2024-01-01T12:34:56Z",
            "name": "default.pdf",
            "subType": null,
            "size": 123,
            "format": "PDF",
            "url": "https://url-to-file.pdf"
        }
    ],
    "classification": {
        "fileType": "PAYSLIP"
    },
    "analysis": {
        "startDate": "2024-01-01",
        "endDate": "2024-01-15",
        "payDate": null,
        "currency": null,
        "grossAmount": 20000.0,
        "netAmount": 18000.0,
        "employerName": "ABC Corporation",
        "employeeName": "George Palomero",
        "ssNumber": "1234567890",
        "taxNumber": null,
        "baseAmount": null,
        "expireDate": null,
        "dateOfBirth": null,
        "firstName": null,
        "lastName": null,
        "middleName": null,
        "nbiIdNumber": null,
        "address": null,
        "maritalStatus": null,
        "gender": null,
        "citizenship": null,
        "remark": null
    }
}
```


## 端点

| 端点                                                      | |
|:--------------------------------------------------------| :---- |
| [获取 Archives 列表](/v1.0-Chinese/reference/list-archives) | `GET /archives` |
| [创建 archive 文件](/reference/create-archive)              | `POST /archives` |
| [获取一条 Archive 记录](/v1.0-Chinese/reference/get-archive)  | `GET /archives/{id}` |
| [识别 archive 文件](/reference/create-and-classify-archive) | `POST /archives/classify` |


## Webhooks

### `ARCHIVE_STARTED`

当用户上传一个或几个文件（"Archive"）到 Smile 时，此 Webhook 事件会被触发。

``` json
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

### `ARCHIVE_ANALYZED`

当 Archive 已通过 OCR 解析为 JSON 数据时，此 Webhook 事件会被触发。

``` json
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

### `ARCHIVE_REVOKED`

当用户取消访问 Archive 的权限时，此 Webhook 事件会被触发。

``` json
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

### `ARCHIVE_FAILED`

当 Archive 创建或分析过程失败时，此 Webhook 事件会被触发。

``` json
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

## 事件监听器

SDK 还可以发出特定的事件，该事件可被您的本地应用程序捕获，以便应用程序根据需要作出反应和执行功能。

| 回调 | 数据                  | 详情                                  |
| :------- |:--------------------|:------------------------------------|
| `onUploadsCreated` | `uploads`, `userid` | 当用户通过 SDK 上传文件时触发，包含上传队列和用户的 userID |
