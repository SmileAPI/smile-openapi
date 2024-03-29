---
title: Transactions
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: transactions
---

The Transactions data point is available for many gig platform providers, and may contain both income and expense transactions as well as e-wallet deposits or withdrawals.

In certain cases, Smile also derives monthly income information from transactions through its [Estimated Income](/reference/estimated-incomes) user insight product.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Transactions data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Transaction data is ready.

## Fallback Methods

If the sources your user provided are not enough, you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload their payslip document.

## The Transaction object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the transaction item on the Smile Network |
| date | date | Date of the transaction |
| description | string | Description of the transaction |
| currency | string | Currency of the transaction in 3 character alpha ISO 4217 |
| amount | float | Amount of the transaction |
| referenceId | string | Reference ID of the transaction from the provider |
| metadata | object | Contains data about this transaction data point. See object below |

### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the transaction record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |

## Sample Transaction data

```json
{
  "id": "t-123abc456def789abc123def456abc78",
  "date": "2023-08-17",
  "description": "xxx",
  "currency": "PHP",
  "amount": 8510.50,
  "referenceId": "1234567890",
  "metadata": {
    "createdAt": "2022-09-01T01:44:18Z",
    "itemCreatedAt": "2022-08-24T05:24:37Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp",
    "accountId": "a-123abc456def789abc123def456abc78"
  }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all transactions](/reference/list-transactions-1) | `GET /transactions` |
| [Retrieve one transaction](/reference/get-transaction-1) | `GET /transactions/{id}` |

## Webhooks

### `TRANSACTIONS_ADDED`

Sent when transaction data from a user is added from the provider.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TRANSACTIONS_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 625,
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
  "id": "et-123abc456def789abc123def456abc78",
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
      "TRANSACTIONS"
    ]
  }
}
```
