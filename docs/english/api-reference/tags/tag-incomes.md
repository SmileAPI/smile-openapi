---
title: Incomes
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: incomes
---

The Incomes data point allows you to retrieve users' available income records depending on the available data from the provider. Income data can primarily be obtained from:

- Payroll accounts
- Select government service accounts
- Select gig platforms

Verifiable income from platforms such as payroll and service accounts are valuable data points in assessing a person's credit worthiness.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Incomes data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Incomes data is ready.

In the event that raw Income data is not available from the provider, Smile also provides [Estimated Income](/reference/estimated-incomes) as additional User Insights.

## Fallback Methods

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload their own pay slips or tax records.

Also check out [Estimated Income](/reference/estimated-incomes) from Smile's User Insights products for derived income from available data sources.

## The Income object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the income information on the Smile Network |
| workItem | string | Work performed (i.e. for freelance jobs) |
| employer | string | Name of the employer |
| startDate | date | Start date of the income period |
| endDate | date | End date of the income period |
| currency | string | Currency of the transaction in 3 character alpha ISO 4217 |
| frequency | string | Frequency or pay period of the income record. Possible values: `Hourly`, `Daily`, `Weekly`, `Semimonthly`, `Monthly`, `Bimonthly`, `Quarterly`, `Annually`, `Variable`, `Unspecified` |
| baseAmount | float | Base amount of the income paid |
| grossAmount | float | Gross amount of the income paid |
| netAmount | float | Net amount of the income paid |
| metadata | object | Contains data about this incomes data point. See object below |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the income record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Income data

```json
[{
    "id": "inc-123abc456def789abc123def456abc78",
    "startDate": "2022-07-01",
    "endDate": "2022-07-31",
    "workItem": "Regular employment",
    "employer": "ABC Corporation",
    "frequency": "Monthly",
    "currency": "PHP",
    "baseAmount": 8500,
    "grossAmount": 10000,
    "netAmount": 7820.25,
    "metadata": {
        "createdAt": "2022-09-01T01:44:22Z",
        "itemCreatedAt": "2022-09-01T01:54:22Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}, {
    "id": "inc-123abc456def789abc123def456abc78",
    "startDate": "2022-06-01",
    "endDate": "2022-06-30",
    "workItem": "Regular employment",
    "employer": "ABC Corporation",
    "frequency": "Monthly",
    "currency": "PHP",
    "baseAmount": 8500,
    "grossAmount": 10000,
    "netAmount": 7820.25,
    "metadata": {
        "createdAt": "2022-09-01T01:44:22Z",
        "itemCreatedAt": "2022-09-01T01:54:22Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "abccorp",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}]
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all income records](/reference/list-incomes-1) | `GET /incomes` |
| [Retrieve one income record](/reference/get-income-1) | `GET /incomes/{id}` |

## Webhooks

### `INCOMES_ADDED`

Sent when income data about a user is added from the provider.

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INCOMES_ADDED",
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
      "INCOMES"
    ]
  }
}
```
