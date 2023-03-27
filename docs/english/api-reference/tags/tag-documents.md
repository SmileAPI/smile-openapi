---
title: Documents
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: documents
---


The Documents data point contain valuable official-document-related information that is available from the provider, such as:

- Verified government ID numbers such as Social Security et al.
- Clearance document information for criminal checks
- Certificate and license information
- Pay slip document information

While some Documents may have file attachments related to them, these should not be confused with user-uploaded [Archives](/reference/archives).

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves any available document data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Document data is ready (if applicable).

## Fallback Methods

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload their own documents. This can be a drivers' license, passport, or even banking or payroll documents.

## The Document object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the document information on the Smile Network |
| name | string | Name of the document, such as *NBI Clearance document*, *SSS Number*, etc. |
| docId | string | Unique identifier of the document |
| status | string | Document status if available, currently only in use by the NBI Clearance document. Null if not available. Possible values: `VALID`, `HIT`, `EXPIRED` |
| documentType | string | Type of document. Possible values: `IDENTIFICATION`, `PAYSLIP`, `CLEARANCE`, `CERTIFICATE` |
| issueDate | date | Date of document issuance. Null if not available. |
| expiryDate | date | Date of document expiry. Null if not available. |
| fileUrl | string | Fully-formed URL reference file for the document. Null if not available. |
| metadata | object | Contains data about this documents data point. See object below |

### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the document record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Document data

```json
{
  "id": "d-123abc456def789abc123def456abc78",
  "name": "NBI Clearance",
  "docId": "A123BCDE45-AA123456",
  "status": "VALID",
  "documentType": "CLEARANCE",
  "issueDate": "2022-06-06",
  "expiryDate": "2023-06-06",
  "fileUrl": null,
  "metadata": {
    "createdAt": "2022-08-19T07:29:08Z",
    "itemCreatedAt": "2022-08-24T05:24:37Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all documents](/reference/list-documents-1) | `GET /documents` |
| [Retrieve one document](/reference/get-document-1) | `GET /documents/{id}` |

## Webhooks

### `DOCUMENTS_ADDED`

Sent when document data about a user is added from the provider.

```json
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

### `TASK_FINISHED`

Sent when the full data sync task process for a user's account is finished.

```json
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
      "DOCUMENTS"
    ]
  }
}
```
