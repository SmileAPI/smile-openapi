---
title: Contributions
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: contributions
---

The Contributions data point allows you to identify the user's social security contributions activity. This data, depending on the source, can allow you to:

- make calculations on the user's income range
- determine regularity of formal employment

While not an exact source of income information, the raw contributions data from government services can be used as a factor in assessing a person's credit worthiness.

In the Philippines, Contributions data is available for social security services, the national health insurance agency, and the national housing provident fund platforms.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Contributions data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Contributions data is ready.

You may also check out the [Estimated Income](/reference/estimated-incomes) User Insight product Smile provides as a quick way to determine income without the need to compare against yearly contribution tables.

## Fallback Methods

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload their own pay slips or tax records.

Also check out [Estimated Income](/reference/estimated-incomes) from Smile's User Insights products for derived income from contributions.

## The Contributions object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the contribution information on the Smile Network |
| date | string | Date the contribution was made. When exact dates are not available, defaults to the end of the month |
| currency | string | Currency of the contribution in 3 character alpha ISO 4217 |
| amount | float | Amount of the contribution remitted |
| referenceId | string | Provider-specific reference ID for the contribution transaction |
| metadata | object | Contains data about this contributions data point. See object below |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the contribution record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Contributions data

```json
{
    "id": "con-123abc456def789abc123def456abc78",
    "date": "2022-06-30",
    "currency": "PHP",
    "amount": 2250,
    "referenceId": null,
    "metadata": {
        "createdAt": "2022-08-24T05:14:37Z",
        "itemCreatedAt": "2022-08-24T05:24:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "sss_ph",
        "accountId": "a-123abc456def789abc123def456abc78"
    }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all contributions](/reference/list-contributions) | `GET /contributions` |
| [Retrieve one contribution](/reference/get-contribution) | `GET /contributions/{id}` |

## Webhooks

### `CONTRIBUTIONS_ADDED`

Sent when contributions data about a user is added from the provider.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "CONTRIBUTIONS_ADDED",
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
      "CONTRIBUTIONS"
    ]
  }
}
```
