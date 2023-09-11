---
title: Liabilities
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: liabilities
---


The Liabilities data point allows you to retrieve provider-specific loans in seconds, giving you access to important data for decisions and underwriting. Currently these are from government institutions that provide this service to their citizens.

In the Philippines, Liabilities support is provided for SSS. Pag-IBIG and other sources are part of the roadmap and will be added at a later date.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Liabilities data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Liabilities data is ready.

## Fallback Methods

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload relevant documentation.

## The Liabilities object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the liability information on the Smile Network |
| type | string | Liability type, provider-dependent |
| referenceId | string | Unique reference ID of the liability on the Provider's network |
| startDate | date | Start date of the liability |
| endDate | date | End date of the liability. Null if not available or still ongoing |
| firstAmortizationDate | date | Date of the first amortization payment |
| amortizationFrequency | string | Frequency of the amortization payments. Possible values: `Hourly`, `Daily`, `Weekly`, `Semimonthly`, `Monthly`, `Bimonthly`, `Quarterly`, `Annually`, `Variable`, `Unspecified` |
| currency | string | Currency of the liability in 3 character alpha ISO 4217 |
| loanAmount | float | Amount of the liability |
| amortizationAmount | float | Amount of the amortization to be paid according to `amortizationFrequency` value |
| outstandingBalance | float | Amount of the liability still outstanding |
| nextPaymentAmount | float | Amount due for the next amortization payment. May include overdue amounts |
| overduePaymentAmount | float | Amount of the liability that is overdue. Does not include expected payment that is not yet past its due |
| metadata | object | Contains data about this liabilities data point. See object below |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the liability record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Liabilities data

```json
[{
    "id": "lia-123abc456def789abc123def456abc78",
    "type": "Salary Loan",
    "startDate": "2022-10-06",
    "amortizationFrequency": "Monthly",
    "currency": "PHP",
    "loanAmount": 16000,
    "referenceId": "SL201601011234567",
    "endDate": "2023-10-06",
    "firstAmortizationDate": "2022-11-06",
    "amortizationAmount": 738.32,
    "outstandingBalance": 14599.76,
    "nextPaymentAmount": 732.38,
    "overduePaymentAmount": 0,
    "metadata": {
        "createdAt": "2022-11-01T01:01:01Z",
        "itemCreatedAt": "2022-11-01T01:11:01Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "xyzservice",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all liabilities](/reference/list-liabilities) | `GET /liabilities` |
| [Retrieve one liability](/reference/get-liabilities) | `GET /liabilities/{id}` |

## Webhooks

### `LIABILITIES_ADDED`

Sent when liabilities data about a user is added from the provider.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LIABILITIES_ADDED",
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
      "LIABILITIES"
    ]
  }
}
```
