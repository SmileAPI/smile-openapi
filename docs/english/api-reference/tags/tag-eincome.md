---
title: Estimated Incomes
excerpt: ""  
category: 631090d0cbc5350036d31763
slug: estimated-incomes
---

Where there is limited income information available, Smile can also provide additional derived income information from secondary data types such as:

- social security contributions
- annual salary calculations
- computed earnings from transactions

Based on available historical data from the data provider, we calculate an estimated monthly income for the user and surface that information via our API, saving you additional computational overhead.

_Estimated Incomes is currently in alpha._

## The Estimated Income object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id         | string | Unique ID of this estimated income object                                                  |
| month      | string | The month where this estimated income is for, in 'YYYY-MM' format                          |
| currency   | string | Currency of the estimated income in standard three-letter ISO code                         |
| amount | number | Income amount                                                                              |
| metadata   | object | Additional information about the resource such as created date, data source, user id, etc. |

### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the estimated income record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |

## Sample Estimated Income data

Estimated income is always returned as a monthly amount.

```json
{  
    "id": "einc-123abc456def789abc123def456abc78",  
    "month": "2022-07",  
    "currency": "PHP",  
    "amount": 8500,  
    "metadata": {  
        "createdAt": "2022-09-01T01:44:18Z",
        "itemCreatedAt": "2022-08-24T05:24:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",  
        "sourceType": "ACCOUNT",  
        "userId": "tenantId-123abc456def789abc123def456abc78",  
        "providerId": "abccorp",  
        "accountId": "a-123abc456def789abc123def456abc78"  
    }  
}, {  
    "id": "einc-123abc456def789abc123def456abc78",  
    "month": "2022-06",  
    "currency": "PHP",  
    "amount": 8500,  
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

| Endpoint                                                        |                      |
| :-------------------------------------------------------------- | :------------------- |
| [Retrieve all estimated incomes](/reference/list-eincomes)      | `GET /eincomes`      |
| [Retrieve one estimated income record](/reference/get-eincomes) | `GET /eincomes/{id}` |

## Webhooks

### `EINCOMES_ADDED`

Fired when estimated income data has been derived from data shared by a user, either from transactions, contributions, or other data from the provider.

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "EINCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0
  }
}
```
