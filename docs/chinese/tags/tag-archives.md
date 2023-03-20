---
title: Archives
excerpt: ""
category: 62ce2a159aafea009af30daa
slug: archives
---

Smile API 还可以存储和处理照片及其他文件，以帮助验证用户的记录。启用后用户可以上传照片、扫描件或 PDF 文件，作为供您记录和验证使用的备份或额外的数据点。支持以下文件类别：

- SSS records
- Income tax documents
- Payslips
- Company IDs

对 SSS 记录和所得税文件进行额外分析，以便从上传的文件中检索出基本信息。

这些用户上传的文件可以通过 Archives 端点进行检索，以便在您需要时下载或进行人工验证。

我们接受最大为 15MB 的文件，可以是以下格式：

- Portable Network Graphic files (`.png`)
- Portable Document Format files (`.pdf`)
- Joint Photographic Experts Group files (`.jpg` or `.jpeg`)
- Tag Image File Format files (`.tiff`)

除非被用户删除，所有文件从上传之日起保存 60 天。

从可核实的来源（如工资系统）自动检索的文件和档案将在 Documents 端点下找到。

## Archive 对象

| 属性         | 类型               | 详情                                                                           |
|:-----------|:-----------------|:-----------------------------------------------------------------------------|
| id         | string           | Archive/文件的唯一ID                                                              |
| createdAt  | date-time        | 用户上传文件的时间                                                                    |
| providerId | string           | 总是设置为 `"user-provided"`，因为是用户自己上传的文件                                         |
| userId     | string           | 上传文件的人的用户ID                                                                  |
| type       | string           | 上传文件的类型，可以是以下之一：`PAYSLIP`，`TAX_DOCUMENT`，`COMPANY_ID`，`SOCIAL_SECURITY`      |
| state      | object           | 该文件的当前处理状态，见下文                                                               |
| rawFiles   | array of objects | 关于原始文件的其他细节                                                                  |

**状态对象**

| 属性           | 类型        | 详情                                                                                      |
|:-------------|:----------|:----------------------------------------------------------------------------------------|
| status       | string    | 文件当前的分析状态，可以是下列之一：`STARTED`，`ANALYZED`，`UNSUPPORTED`，`ERROR`，`REVOKED`                  |
| errorCode    | string    | 在分析过程中发现的任何错误，可以是下列之一：`MISSING_MANDATORY_FIELD`, `INVALID_FIELD_FORMAT`, `SYSTEM_ERROR` |
| errorMessage | string    | 上述 "errorCode" 的可读错误信息                                                                  |
| updatedAt    | date-time | 文件最后一次更新/分析的时间                                                                          |

**原始文件对象**

| 属性        | 类型        | 详情                                                                               |
|:----------|:----------|:---------------------------------------------------------------------------------|
| id        | string    | 原始文件的唯一ID                                                                        |
| createdAt | date-time | 用户上传文件的时间                                                                        |
| name      | string    | 用户上传文件的文件名                                                                       |
| subType   | string    | 更新的文件类型                                                                          |
| size      | integer   | 文件大小，以千字节为单位                                                                     |
| format    | string    | 文件的格式，可以是以下之一：`pdf`，`png`，`tiff`，`jpeg`                                          |
| url       | string    | 文件的可访问URL                                                                        |

## Archive 数据样本


``` json
{
   "id": "u-123abc456def789abc123def456abc78",
   "createdAt": "2022-11-01T10:00:00Z",
   "providerId": "user-provided",
   "userId": "tenandId-123abc456def789abc123def456abc78",
   "type": "TAX_DOCUMENT",
   "state": {
     "status": "ANALYZED",
     "errorCode": null,
     "errorMessage": null,
     "updatedAt": "2022-11-17T02:04:21Z"
   },
   "rawFiles": [
      {
         "id": "f-123abc456def789abc123def456abc78",
         "createdAt": "2022-11-01T10:00:00Z",
         "name": "ITR-2020-2021.png",
         "subType": "TAX_PAYMENT",
         "size": 300,
         "format": "PNG",
         "url": "https://url-to-file.png"
      }
      ]
   },
   {
      "id": "u-123abc456def789abc123def456abc78",
      "createdAt": "2022-11-01T10:00:00Z",
      "providerId": "user-provided",
      "userId": "tenantId-123abc456def789abc123def456abc78",
      "type": "PAYSLIP",
      "state": {
         "status": "UNSUPPORTED",
         "errorCode": null,
         "errorMessage": null,
         "updatedAt": "2022-11-17T02:04:21Z"
      },
      "rawFiles": [
      {
         "id": "f-123abc456def789abc123def456abc78",
         "createdAt": "2022-11-01T10:00:00Z",
         "name": "payslip-november-2022.jpeg",
         "subType": "PAYSLIP",
         "size": 100,
         "format": "JPEG",
         "url": "https://url-to-file.jpeg"
      }
      ]
   }
}
```


## 端点

| 端点                                         | |
|:-------------------------------------------| :---- |
| [获取 Archives 列表](/reference/list-archives) | `GET /archives` |
| [获取一条 Archive 记录](/reference/get-archive)  | `GET /archives/{id}` |

## Webhooks

### `ARCHIVE_STARTED`

当用户上传一个或几个文件（"Archive"）到 Smile 时，此 Webhook 事件会被触发。

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

### `ARCHIVE_ANALYZED`

当 Archive 已通过 OCR 解析为 JSON 数据时，此 Webhook 事件会被触发。

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

### `ARCHIVE_REVOKED`

当用户取消访问 Archive 的权限时，此 Webhook 事件会被触发。

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

### `ARCHIVE_FAILED`

当 Archive 创建或分析过程失败时，此 Webhook 事件会被触发。

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

## 事件监听器

SDK 还可以发出特定的事件，该事件可被您的本地应用程序捕获，以便应用程序根据需要作出反应和执行功能。

| 回调 | 数据                  | 详情                                  |
| :------- |:--------------------|:------------------------------------|
| `onUploadsCreated` | `uploads`, `userid` | 当用户通过 SDK 上传文件时触发，包含上传队列和用户的 userID |
