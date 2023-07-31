---
title: Archives
excerpt: ""
category: 6294c0fd9494580032b22740
slug: archives
---

Smile API can also store and process photos and other files to aid in verifying users' records. If enabled, users may upload photos, scans, or PDF files as a fallback method or as an additional data point for your records and verification use. These can be any of the following:

- SSS records
- Income tax documents
- Payslips
- Company IDs

Additional analysis is done on SSS records and income tax documents to retrieve basic information from the uploaded file.

These user-uploaded files can be retrieved via the Archives endpoint, to allow for download or manual verification if you require.

Files up to a maximum of 15MB are accepted, and can be of the following formats:

- Portable Network Graphic files (`.png`)
- Portable Document Format files (`.pdf`)
- Joint Photographic Experts Group files (`.jpg` or `.jpeg`)
- Tag Image File Format files (`.tiff`)

Files are stored until removed by the user via the SDK.

Documents and files that are automatically retrieved from verifiable sources such as payroll systems will be found under the Documents endpoint.

## The Archive object

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID for the archive/file |
| createdAt | date-time | Date and time when the file was uploaded by the user |
| providerId | string | Always set to `"user-provided"` as the user has uploaded the file themselves |
| userId | string | User's ID of the person who uploaded the file |
| type | string | Type of file uploaded, can be one of the following: `PAYSLIP`, `TAX_DOCUMENT`, `COMPANY_ID`, `SOCIAL_SECURITY` |
| state | object | Current state of the processing for this file, see below |
| rawFiles | array of objects | Additional details about the raw file |

**The State object**

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| status | string | Current status of the analysis of the file, can be one of the following: `STARTED`, `ANALYZED`, `UNSUPPORTED`, `ERROR`, `REVOKED` |
| errorCode | string | Any errors found during analysis, can be one of the following: `MISSING_MANDATORY_FIELD`, `INVALID_FIELD_FORMAT`, `SYSTEM_ERROR` |
| errorMessage | string | Human-readable error message for the `errorCode` above |
| updatedAt | date-time | Date and time when the file was last updated/analyzed |

**The rawFiles object**

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID of the raw file |
| createdAt | date-time | Date and time when the file was uploaded by the user |
| name | string | Filename of the file as uploaded by the user |
| subType | string | Type of file updated |
| size | integer | File size in kilobytes |
| format | string | File format of the file, can be one of the following: `PDF`, `PNG`, `TIFF`, `JPEG` |
| url | string | Accessible URL to the file |

## Sample Archive data


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


## Endpoints

| Endpoint | |
| :------- | :---- |
| [List archives](/reference/list-archives) | `GET /archives` |
| [Get archive](/reference/get-archive) | `GET /archives/{id}` |

## Webhooks

### `ARCHIVE_STARTED`

Fired when a user has uploaded one or several files ("archive") to Smile.

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

Fired when an archive has been analyzed and converted into JSON data automatically via OCR.

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

Fired when a user removes permission to access or use an archive.

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

Fired when the archive creation or analysis process is unsuccessful.

``` json
{
   "id": "123abc456def789abc123def456abc78",
   "version": 1,
   "type": "ARCHIVE_FAILED",
   "createdAt": "2021-04-14T09:30:24Z",
   "data": {
      "userId": "tenantId-123abc456def789abc123def456abc78",
      "archiveId": "u-123abc456def789abc123def456abc78",
      "errorCode": "FILE_UNABLE_TO_RECOGNIZE",
      "errorMessage": "Invalid file!"
   }
}
```

## Event Listeners

The SDK also emits events that can be caught by your native application to allow the application to react and perform functions as needed.

| Callback | Data | Description |
| :------- | :---- | :---- |
| `onUploadsCreated` | `uploads`, `userid` | Fired when the user uploads files via the SDK. Contains upload array and user's userId |
