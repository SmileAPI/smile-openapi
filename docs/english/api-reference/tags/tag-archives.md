---
title: Archives
excerpt: ""
category: 66611ec162e8c700572c4be3
slug: archives
---

Smile API can also store and process photos and other files to aid in verifying users' records. If enabled, users may upload photos, scans, or PDF files as a fallback method or as an additional data point for your records and verification use.

These can be any of the following:

| Archive Type | Wink Widget Upload | API Upload | Data Extraction | API File Type | File Subtypes |
| :----------- | :----------------- | :--------- | :-------------- | :------------ | :------------ |
| Income Tax Document | ✅ | ✅ | ✅ | `TAX_DOCUMENT` | `TAX_PAYMENT` |
| Payslip | ✅ | ✅ | ✅ | `PAYSLIP` | `PAYSLIP` |
| SSS Record Screenshot (Deprecated) | ❌ | ❌ | ❌ | `SOCIAL_SECURITY` | `PERSONAL_INFORMATION`, `EMPLOYMENT_INFORMATION` |
| Company ID | ✅ | ✅ | ❌ | `COMPANY_ID` | `COMPANY_ID_FRONT`, `COMPANY_ID_BACK` |
| NBI Clearance Document | ❌ | ✅ | ✅ | `CLEARANCE_NBI` | N/A |
| ID (Front) | ❌ | ✅ | ❌ | `ID_FRONT` | N/A |
| ID (Back) | ❌ | ✅ | ❌ | `ID_BACK` | N/A |
| Bank Statement | ❌ | ✅ | ❌ | `BACK_STATEMENT` | N/A |
| Utility Bills | ❌ | ✅ | ❌ | `UTILITY_BILLS` | N/A |
| Police Clearance | ❌ | ✅ | ❌ | `CLEARANCE_POLICE` | N/A |
| Barangay Clearance | ❌ | ✅ | ❌ | `CLEARANCE_BARANGAY` | N/A |
| Others | ❌ | ✅ | ❌ | `OTHERS` | N/A |

Additional analysis is done on supported document types to retrieve basic information from the uploaded file such as employment and income information. This allows you to immediately ingest the information from the document without needing to manually transcribe the data.

These user-uploaded files can be retrieved via the Archives endpoint, to allow for download or manual verification if you require.

Files up to a maximum of 15MB are accepted, and can be of the following formats:

- Portable Network Graphic files (`.png`)
- Portable Document Format files (`.pdf`)
- Joint Photographic Experts Group files (`.jpg` or `.jpeg`)
- Tag Image File Format files (`.tiff`)

Files are stored until removed by the user via the SDK, or revoked via the API, or for a maximum of 60 days.

Documents and files that are automatically retrieved from verifiable sources such as permissioned access to payroll systems will also be found under the [Documents endpoint](/reference/documents). The data retrieved from the document will also be found under the respective data type, such as [Employments](/reference/employments) or [Incomes](/reference/incomes).

> 🚧 Warning
> 
> Archives in Sandbox Mode return only specific payslips. To test Archives while in Sandbox Mode, you may download the sample payslips within the Developer Portal and upload it through the Wink Widget or through the API. Other files uploaded during Sandbox mode will return errors.

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
| classification | object | File type of the uploaded file based on AI analysis of the file contents |
| analysis | object | Extracted data based on AI analysis of the file contents |

### The State object

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| status | string | Current status of the analysis of the file, can be one of the following: `STARTED`, `ANALYZED`, `UNSUPPORTED`, `ERROR`, `REVOKED` |
| errorCode | string | Any errors found during analysis, can be one of the following: `MISSING_MANDATORY_FIELD`, `INVALID_FIELD_FORMAT`, `SYSTEM_ERROR` |
| errorMessage | string | Human-readable error message for the `errorCode` above |
| updatedAt | date-time | Date and time when the file was last updated/analyzed |

### The Raw Files object

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID of the raw file |
| createdAt | date-time | Date and time when the file was uploaded by the user |
| name | string | Filename of the file as uploaded by the user |
| subType | string | Type of file updated based on the parent file type |
| size | integer | File size in kilobytes |
| format | string | File format of the file, can be one of the following: `PDF`, `PNG`, `TIFF`, `JPEG` |
| url | string | Accessible URL to the file |

### The Classification object

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| fileType | string | File type of the uploaded file based on AI analysis of the file contents, can be one of the following: `PAYSLIP`, `TAX_DOCUMENT`, `EMPLOYMENT_CERTIFICATE`, `OTHERS` |

### The Analysis object

The Analysis object will return extracted data based on the file type of the uploaded file. Other fields that are not found on the file will return null.

| Attribute  | Type | Supported File Type | Description |
| :--------- | :--- | :------------------ | :---------- |
| startDate | date | `PAYSLIP`, `TAX_DOCUMENT` | Start date of the payslip period, in YYYY-MM-DD format. Null if not available. |
| endDate | date | `PAYSLIP`, `TAX_DOCUMENT` | End date of the payslip period, in YYYY-MM-DD format. Null if not available. |
| payDate | date | `PAYSLIP` | Payment date of the payslip, in YYYY-MM-DD format. Null if not available. |
| currency | date | `PAYSLIP` | Currency of the payslip in 3 character alpha ISO 4217 format. Null if not available. |
| baseAmount | float | `PAYSLIP`, `TAX_DOCUMENT` | Base salary amount. Null if not available. |
| grossAmount | float | `PAYSLIP`, `TAX_DOCUMENT` | Gross salary payment amount. Null if not available. |
| netAmount | float | `PAYSLIP` | Net salary payment amount. Null if not available. |
| employerName | string | `PAYSLIP`, `TAX_DOCUMENT` | Employer name from the payslip. Null if not available. |
| employeeName | string | `PAYSLIP`, `TAX_DOCUMENT` | Employee name from the payslip. Null if not available. |
| ssNumber | string | `PAYSLIP` | Social Security Number from the payslip. Null if not available. |
| philHealthNumber | string | `PAYSLIP` | PhilHealth Identification Number from the payslip. Null if not available. |
| taxNumber | string | `PAYSLIP`, `TAX_DOCUMENT` | Tax Identification Number from the payslip. Null if not available. |
| pagIbigNumber | string | `PAYSLIP` | Pag-IBIG Member ID Number from the payslip. Null if not available. |
| expireDate | date | `CLEARANCE_NBI` | Expiry date of the clearance document, in YYYY-MM-DD format. Null if not available. |
| dateOfBirth | date | `CLEARANCE_NBI` | Date of birth, in YYYY-MM-DD format. Null if not available. |
| firstName | string | `CLEARANCE_NBI` | First name from the document. Null if not available. |
| lastName | string | `CLEARANCE_NBI` | Last name from the document. Null if not available. |
| middleName | string | `CLEARANCE_NBI` | Middle name from the document. Null if not available. |
| nbiIdNumber | string | `CLEARANCE_NBI` | NBI Clearance Document Number from the document. Null if not available. |
| address | string | `CLEARANCE_NBI` | Address from the document. Null if not available. |
| maritalStatus | string | `CLEARANCE_NBI` | Marital status from the document. Null if not available. |
| gender | string | `CLEARANCE_NBI` | Gender from the document. Null if not available. |
| citizenship | string | `CLEARANCE_NBI` | Citizenship from the document. Null if not available. |
| remark | string | `CLEARANCE_NBI` | Remarks from the document. Null if not available. |

## Sample Archive data

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
        "philHealthNumber": "123456789012",
        "taxNumber": null,
        "pagIbigNumber": "123456789012",
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


## Endpoints

| Endpoint | |
| :------- | :---- |
| [List archives](/reference/list-archives) | `GET /archives` |
| [Create archive](/reference/create-archive) | `POST /archives` |
| [Get archive](/reference/get-archive) | `GET /archives/{id}` |
| [Classify archive](/reference/create-and-classify-archive) | `POST /archives/classify` |


## Webhooks

### `ARCHIVE_STARTED`

Fired when a user has uploaded one or several files ("archive") to Smile.

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

Fired when an archive has been analyzed and converted into JSON data automatically via OCR.

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

Fired when a user removes permission to access or use an archive.

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

Fired when the archive creation or analysis process is unsuccessful.

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

## Event Listeners

The SDK also emits events that can be caught by your native application to allow the application to react and perform functions as needed.

| Callback | Data | Description |
| :------- | :---- | :---- |
| `onUploadsCreated` | `uploads`, `userid` | Fired when the user uploads files via the SDK. Contains upload array and user's userId |
