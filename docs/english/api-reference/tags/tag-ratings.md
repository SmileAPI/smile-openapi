---
title: Ratings
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: ratings
---

The Ratings data point provides information on the user's ratings as available in the [Provider](/reference/providers) platform. If the platform selected has this data on the user, Smile retrieves this data for your records and also calculates a percentage rating based on the user's current rating and the maximum rating allowed on the platform.

Where available, Smile also retrieves other ratings-related information such as reviews and likes received, and jobs completed, as an additional data point for decision making.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Ratings data (if available). You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Identity data is ready.

## The Rating object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the rating information on the Smile Network |
| currentRating | number | The current rating score of the user from the provider. Null if not available |
| maxRating | number | The maximum possible rating from the provider. Null if no rating score is available |
| calculatedPercentage | number | Current rating expressed as percentage. Calculated by `currentRating / maxRating x 100`. Null if no rating score is available |
| reviewsReceived | number | Number of reviews received, if available from the provider. Null if not available |
| likesReceived | number | Number of recommendations, likes, or kudos received, if available from the provider. Null if not available |
| jobsCompleted | number | Number of jobs completed on the platform, if available from the provider. Null if not available |
| metadata | object | Contains data about this rating data point. See object below |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the rating record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Rating data

```json
{
    "id": "r-123abc456def789abc123def456abc78",
    "currentRating": 4,
    "maxRating": 5,
    "calculatedPercentage": 80,
    "reviewsReceived": 27,
    "likesReceived": 82,
    "jobsCompleted": 125,
    "metadata": {
        "createdAt": "2022-09-02T23:36:12Z",
        "itemCreatedAt": "2022-08-24T05:24:37Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "xyzgigcompany"
    }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all ratings](/reference/list-ratings-1) | `GET /ratings` |
| [Retrieve one rating](/reference/get-rating-1) | `GET /ratings/{id}` |

## Webhooks

### `RATING_ADDED`

Sent when ratings data about a user is added from the provider.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "RATING_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "ratingId": "r-123abc456def789abc123def456abc78",
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
      "RATINGS"
    ]
  }
}
```
