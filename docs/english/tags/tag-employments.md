---
title: Employments
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: employments
---

The Employments data point can contain valuable information about your users' employment status. Employment data is most often retrieved from government services and institutions as well as payroll platforms connected by your user to Smile.

Smile returns employment information as-is from the platform, such as start and end dates, employer names, job titles, and other information. Access to verified data from government services and partnering this with information from payroll platforms can give you a definitive view of your user's employment status.

Employment data does not include jobs taken in gig platforms such as ride sharing apps and the like.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Employment data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Employment data is ready.

## Verifying Employment

Most platforms will contain at least a start date and employer name. If assessing employment status from social security accounts, you may match these against contributions made in order to verify the length of employment and current status.

## Fallback Methods

If the sources provided by your user are not enough, you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload payslips or company IDs.

## The Employment object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the employment information on the Smile Network |
| name | string | Work performed, if available from the provider. Null if not available |
| description | string | Description of the work performed, if available from the provider. Null if not available |
| jobTitle | string | Job title or position with the employer, if available from the provider. Null if not available |
| department | string | Department of the user with the employer, if available from the provider. Null if not available |
| employeeNumber | string | Employee number of the user with the employer, if available from the provider. Null if not available |
| employer | string | Company or business name of the employer, if available from the provider. Null if not available. Possible values: `Male`, `Female`, `Non-binary` |
| status | string | Status of the user's employment, if available from the provider. Null if not available |
| startDate | date | Start date of the user's employment with the employer, if available from the provider. Null if not available |
| endDate | date | End date of the user's employment with the employer, if available from the provider. Null if not available |
| metadata | object | Contains data about this employment data point. See object below |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the employment was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Employment data

```
{
    "id": "e-123abc456def789abc123def456abc78",
    "startDate": "2022-07-01",
    "name": "Security",
    "description": null,
    "jobTitle": "Security Guard",
    "department": null,
    "employeeNumber": "EMP-123456",
    "employer": "ABC Corporation",
    "status": "Permanent",
    "endDate": "2022-07-31",
    "metadata": {
        "createdAt": "2022-09-01T01:44:18Z",
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
| [List all employments](/reference/list-employments-1) | `GET /employments` |
| [Retrieve one employment](/reference/get-employment-1) | `GET /employments/{id}` |

## Webhooks

### `EMPLOYMENTS_ADDED`

Sent when employment data shared by a user is added from the provider.

```
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "EMPLOYMENTS_ADDED",
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

```
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
      "EMPLOYMENTS"
    ]
  }
}
```
