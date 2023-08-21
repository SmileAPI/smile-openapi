---
title: Multiple Application Warning Service
excerpt: ""
category: 631090d0cbc5350036d31763
slug: links
---

Multiple Application Warning (MAW) offers lenders notifications when a potential borrower has applied for loans with multiple financial institutions. With MAW, lenders can make better and informed decisions when assessing risk with the information of their customer's behavior across the network.

Through the MAW service, once your user has connected an account via the Wink Widget SDK, you will receive a notification whether your user has connected with other lenders and institutions across Smile's network of participating organizations.

There are multiple benefits for activating MAW for your account:

- **Real-time Notifications.** Receive notifications when a borrower applies for multiple loans, allowing for proactive risk management and timely decision-making.
- **Enhanced Risk Assessment.** Mitigate the risk of lending to borrowers with excessive credit strain or suspect behaviors, reducing potential losses and improving loan portfolio quality.
- **Fraud Detection.** Detect potential fraudulent activities by identifying borrowers who attempt to obtain multiple loans simultaneously, minimizing the risk of lending to fraudulent applicants.
- **Network Effects.** Benefit from a growing network of participating lenders, contributing to richer and more accurate data for enhanced risk assessment and fraud prevention.

Once MAW has been activated for your account, there are two ways you can receive or retrieve data on your user's prior loan behavior on the network:

1. Via the ``GET /links`` endpoint
2. Via listening to the ``LINK_ADDED`` webhook

This allows you multiple ways of retrieving the data according to your needs.

## The Links object

| Attribute  | Type   | Description                                                                               |
| :--------- | :----- |:------------------------------------------------------------------------------------------|
| id | string | Unique ID of this link record                                                             |
| startDate | date-time | Start of when user data is analyzed for links, usually 730 days before account connection |
| endDate | date-time | End of when user data is analyzed for links, usually at time of account connection        |
| records | array of objects | Array containing link records                                                             |

### The Records object

| Attribute | Type | Description |
| :----- | :----- | :----- |
| count | number | Number of other participating organizations this user has connected an account to within the duration ``startDate`` to ``endDate`` |
| linkedAt | array of date-time | Date/time values of when the user has connected an account to other participating organizations |

## Sample User object

```json
{
    "id": "123abc456def789abc123def456abc78",
    "startDate": "2022-03-20T01:27:26Z",
    "endDate": "2022-09-20T01:27:26Z",
    "records": [
        {
          "count" : 3,
          "linkedAt" : [
            "2022-04-20T01:27:26Z",
            "2022-04-21T12:00:00Z",
            "2022-06-01T01:00:00Z"
          ]
        }
    ]
}
```

## Endpoints

| Endpoint                                      |                      |
|:----------------------------------------------| :------------------- |
| [Retrieve user links](/reference/list-links)  | `GET /links`      |
| [Retrieve one user link](/reference/get-link) | `GET /links/{id}` |

## Webhooks

### `LINK_ADDED`

Sent when a link is detected after the user has connected their account.

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "LINK_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "id": "link-ef789aabc41236abc7856df45bc123de",
    "providers": [
      "abccorp"
    ]
  }
}
```